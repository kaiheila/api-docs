# Webhook
通过 Webhook 进行消息订阅可以让你的应用或机器人能够及时响应用户的消息，在用户量较多的情况下，可以提供更好的并发性能控制。你需要的只是告诉我们该向哪里（URL）发送消息。当消息发生时，KOOK 开放平台会以 HTTP POST 请求的方式将消息内容推送到你设置的回调地址。

> **注意:** Webhook、Websocket 模式不能同时使用  
> 如果选择了 Webhook 模式，将不能再使用 Websocket 接收用户消息。同理，设置了 Websocket 后，平台将不会再向回调地址推送消息。

## 配置 Webhook
### 配置 WebHook 回调地址
为了能够接收推送消息，首先你必须在开发者后台配置回调地址。当收到相应的触发消息时，开放平台会向该回调地址发送相应的 `HTTP POST` 请求。  
> **注意:** 每个应用/机器人只能配置一个请求网址，该应用/机器人在所有服务器的消息都会发送到这个地址。
1. 在开发者后台，点击任意机器人进入机器人详情页面
2. 进入`设置 > 机器人`
3. 在 `机器人连接模式` 中选择 `WebHook`
4. 填写 `Callback Url`

### 处理 Challenge 请求
点击 '重试' 按钮或上线机器人时，开放平台将会向你配置的网址推送一个 `application/json` 格式的 POST 请求进行 Challenge 验证。
> **注意:** 开放平台向机器人推送的消息将会使用 `zlib (deflate)` 压缩，请先使用先使用 `zlib` 解压或在传入的 callbackUrl 中加上 `compress=0` 停用压缩  
 
> **注意:** 当配置消息加密时，请先参考[解密消息](#解密消息)解密消息。  

```json
{
    "s": 0, // 信令类型
    "d": {
        "type": 255,
        "channel_type": "WEBHOOK_CHALLENGE", //表示这是一个验证请求 
        "challenge" : "bkes654x09XY" , //客户端需要原样返回
        "verify_token": "xxxxxx",   //机器人的token
    }
}
```

> **注意:** 启用消息加密时，你收到的请求会是以下这个画风。请先参考[解密消息](#解密消息)解密消息。  

```json
{
    "encrypt": "adfw232sdssdfadfas98XX......" // 加密字符串，解密方法请看下方的消息解密模块
}
```
当你收到开放平台 POST 验证请求时，你需要解析出 `challenge` 值，并在 1s 内原样返回该 `challenge` 值作为响应。响应示例如下：
> **注意:** 无论你是否配置消息加密，你都应该返回以下响应。  

```javascript
{ 
    "challenge": "bkes654x09XY" // 应用需要原样返回的值 
}
```

## 接收并响应事件

当有消息发生时，开放平台将会通过 HTTP POST 请求发送 Json compress 格式的事件数据到你预先提供的回调地址。

### 注意事项

1. 数据会进行 `zlib (deflate)` 压缩，请先使用先使用 `zlib` 解压或在传入的 callbackUrl 中加上 `compress=0` 停用压缩 
2. 在 1s 内对推送事件请求返回 http 200 响应。如果失败或超时，系统会按 2s, 4s, 8s, 16s, 32, 64s 的大致间隔，给你回调，直到 5 次都失败。
3. 检查 `sn` 确保事件的唯一性，避免同一个事件处理了多次。
4. 检查 'verify_token' 是否与开发者后台的 `verify_token` 相同，确保这个事件的来源确实是 KOOK 开放平台，而不是恶意的第三方伪造的事件。
5. 在配置好 WebHook 后，系统会认为机器人自动上线。如果一段时间内，用户的失败次数达到警告阀值，系统会发送站内消息给相应开发者。如果失败次数过多，平台会认为机器人出现故障，平台会给开发者发送站内消息，并下线该机器人。机器人下线后，平台会停止向该机器人发送任何消息。用户在排除故障后，可以在开发者后台，重新点击上线，恢复该机器人。在恢复时，系统会再次重复之前的验证 Url 流程，来确保该 Url 依然属于您。
6. 如果需要更安全的事件回调机制，建议配置消息加密，请参考[配置消息加密](#配置消息加密)。

## 消息格式及说明
参见[事件格式说明](https://developer.kookapp.cn/doc/event)

## 配置消息加密
如果你对消息有较高的安全需求，可以通过 Encrypt Key 来加密数据。
### 配置消息加密 Encrypt Key

1. 进入 `机器人连接模式` 配置
2. 输入 `Encrypt Key` 或点击 `重新生成` 生成 `Encrypt Key`

当你配置好消息加密，你收到的请求应该是这样子的:
```json
{
    "encrypt": "adfw232sdssdfadfas98XX......" // 加密字符串，解密方法请看下方的消息解密模块
}
```

### 解密消息
事件消息采用了 aes-256-cbc 来加密数据。主要解密逻辑如下：
> **注意:** 在启用数据加密后，推送的消息依然会使用 `zlib (deflate)` 压缩，请先使用 `zlib` 解压或在传入的 callbackUrl 中加上 Url Query 参数 `compress=0` 停用压缩  

> **注意:** 解密后的内容为事件 json
1. 将密文用 `base64` 解码
2. 截取前16位得到 `iv`, 截取16位之后的数据为新的密文
3. 用 `base64` 解码新的密文, 得到待解密数据
4. 在 `encrpytKey` 后面补 `\0` 至长度等于 32 位，得到 `key`
5. 利用上面的 `iv`, `key`, 待解密数据，采用 `aes-256-cbc` 解密数据。

## 代码示例
### Python 代码示例

```python
from Crypto.Cipher import AES
import base64

class Encrypt:
    def __init__(self, key, bs=32):
        pad = lambda s: s + (bs-len(s))*"\0"
        key = pad(key)
        self.key = key.encode('utf-8')

    def aes_decrypt(self, content):
        str = base64.b64decode(content)
        iv = str[0:16]
        cipher = AES.new(self.key, AES.MODE_CBC, iv)
        return cipher.decrypt(base64.b64decode(str[16:])).decode('utf-8')
```
### PHP 代码示例

```php
$encryptKey = "testKey";
$data = "Kaiheila's bot is awesome";
$encrypt = encryptData($data, $encryptKey);
echo $encrypt. "\n";
echo decryptData($encrypt, $encryptKey);

function encryptData($data, $key)
{
    $iv = substr(md5(uniqid()), 0, 16);
    return base64_encode($iv.openssl_encrypt($data, 'aes-256-cbc', $key, 0, $iv));
}

function decryptData($eData, $key)
{
    $eData = base64_decode($eData);
    $iv = substr($eData, 0, 16);
    return openssl_decrypt(substr($eData, 16), 'aes-256-cbc', $key, 0, $iv);
}
```
### C# 代码示例
```csharp
using System.Security.Cryptography;
using System.Text;

namespace YourBot
{
    public class CryptUtil
    {
        public static string Decrypt(string data, string encryptKey)
        {
            // 在 encrypKey 右侧填充 \0 到 32 位
            encryptKey = encryptKey.PadRight(32, '\0');

            // 用 base64 解析原密文
            var originCipher = Encoding.UTF8.GetString(Convert.FromBase64String(data));
            // 取前 16 位为 iv，16 位后的文本为新密文
            var iv = originCipher.Substring(0, 16);
            var newCipher = originCipher.Substring(16);

            // 用 base64 解密新密文
            var newCipherByte = Convert.FromBase64String(newCipher);

            // 使用 aes-256-cbc 解密数据
            using (var aes = Aes.Create())
            {
                aes.Key = Encoding.UTF8.GetBytes(encryptKey);
                aes.IV = Encoding.UTF8.GetBytes(iv);

                ICryptoTransform decryptor = aes.CreateDecryptor(aes.Key, aes.IV);

                using (var memoryStream = new MemoryStream(newCipherByte))
                using (var csDecrypt = new CryptoStream(memoryStream, decryptor, CryptoStreamMode.Read))
                using (var reader = new StreamReader(csDecrypt))
                    return reader.ReadToEnd();
            }
        }
    }
}
```
### Java 代码示例
```java
import javax.crypto.Cipher;
import javax.crypto.spec.IvParameterSpec;
import javax.crypto.spec.SecretKeySpec;
import java.nio.charset.StandardCharsets;
import java.util.Base64;

public class CryptUtils {

    // data: Base64 编码的数据
    // key: encrypt-key
    public static String decrypt(String data, String key) {
        // Base64 解码
        String src = new String(Base64.getDecoder().decode(data));
        // 截取 IV
        String iv = src.substring(0, 16);
        // 待解密的密文
        byte[] newSecret = Base64.getDecoder().decode(src.substring(16));
        // Padding
        StringBuilder finalKeyBuilder = new StringBuilder(key);
        while (finalKeyBuilder.length() < 32) {
            finalKeyBuilder.append("\0");
        }
        // 最终 Key
        String finalKey = finalKeyBuilder.toString();

        try {
            Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
            cipher.init(
                    Cipher.DECRYPT_MODE,
                    new SecretKeySpec(finalKey.getBytes(), "AES"),
                    new IvParameterSpec(iv.getBytes(StandardCharsets.UTF_8))
            );
            return new String(cipher.doFinal(newSecret)); // 最终解密结果
        } catch (Exception e) {
            throw new RuntimeException(e); // 这不应该发生，如果它发生了，请检查你的 JVM 安装是否正常！
        }
    }
}
```
