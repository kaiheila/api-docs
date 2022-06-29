通过 Webhook 进行消息订阅可以让你的应用或机器人能够及时响应用户的消息，在用户量较多的情况下，可以提供更好的并发性能控制。你需要的只是告诉我们该向哪里（URL）发送消息。当消息发生时，KOOK 开放平台会以 HTTP POST 请求的方式将消息内容推送到你设置的回调地址。

**注意：** Webhook 模式与 Websocket 模式是互斥的，如果选择了 Webhook 模式，将不能再使用 Websocket 接收用户消息。同理，设置了 Websocket 后，平台将不会再向回调地址推送消息。

## 如何配置 Webhook

1. 在开发者后台，点击进入机器人详情页面，选择 Webhook。
2. 按照下面的说明，配置好接口。
3. 将接口的地址填入回调地址中，系统会 check 地址是否符合协议规范。如果符合，我们就能收到回调事件了。

## 配置回调地址

为了能够接收推送消息，首先你必须在开发者后台配置回调地址。当收到相应的触发消息时，开放平台会向该回调地址发送相应的 `HTTP POST` 请求。

每个应用/机器人只能配置一个请求网址，该应用/机器人在所有服务器的消息都会发送到这个地址。

点击编辑标示，在文本框内填写你要配置的请求网址。完成请求网址编辑后，点击保存按钮时，开放平台会向你配置的网址推送一个 `application/json` 格式的 POST 请求, 该请求用于验证你配置的网址的合法性。请求如下：

```javascript
{
    "s": 0, // 信令类型
    "d": {
        "type": 255,
        "channel_type": "WEBHOOK_CHALLENGE", //表示这是一个验证请求
        "challenge" : "bkes654x09XY" , //客户端需要原样返回
        "verify_token": "xxxxxx",   //机器人的token
    }
}

// 设置了Encrypt Key时
{
    "encrypt": "adfw232sdssdfadfas98XX" // 加密字符串，解密方法请看下方的消息解密模块
}
```

当你收到开放平台 POST 验证请求时，你需要解析出 challenge 值(如果应用设置了 Encrypt Key，需要做解密，解密方法[参考这里](#消息解密))，并在 1s 内原样返回该 challenge 值作为响应。响应示例如下：

```javascript
{
    "challenge": "bkes654x09XY" // 应用需要原样返回的值
}
```

## 接收并响应事件

当有消息发生时，开放平台将会通过 HTTP POST 请求发送 Json compress 格式的事件数据到你预先提供的回调地址。

你可能需要注意如下情况：

1. 为了避免同一个事件处理了多次，你可能需要使用 `sn` 对事件的唯一性进行检查。
2. 在正常配置好后，系统会给回调地址推送消息，你需要在 1s 内返回 http 200 响应。如果失败或超时，系统会按 2s, 4s, 8s, 16s, 32, 64s 的大致间隔，给你回调，直到 5 次都失败。
3. 默认配置为 Webhook 机器人且设置好回调地址后，系统会认为机器人自动上线。如果一段时间内，用户的失败次数达到警告阀值，系统会发送站内消息给相应开发者。如果失败次数过多，平台会认为机器人出现故障，平台会给开发者发送站内消息，并下线该机器人。机器人下线后，平台会停止向该机器人发送任何消息。用户在排除故障后，可以在开发者后台，重新点击上线，恢复该机器人。在恢复时，系统会再次重复之前的验证 Url 流程，来确保该 Url 依然属于您。
4. 在消息中，我们会带上 verify_token, 你可以检查 `verify_token` 是否与开发者后台的 `verify_token` 是否 相同以确保这个事件的来源确实是 KOOK 开放平台，而不是恶意的第三方伪造的事件。
5. 如果你需要更安全的事件回调机制，建议填写 `EncryptKey`，在进行业务逻辑处理前请先参考[这里](#消息解密)进行解密。
6. 默认情况下，我们的数据会进行 zlib 压缩 (**deflate**)，相应的数据你可能需要先进行 zlib 解压缩，再进行处理。如果不需要压缩，可以在传入的 callbackUrl 中加上 `compress=0`。

## 消息解密

如果你对消息有较高的安全需求，可以通过 Encrypt Key 来加密数据, 采用了 aes-256-cbc 来加密数据。主要解密逻辑如下：

1. 将密文用 base64 解码
2. 截取前 16 位得到 iv, 截取 16 位之后的数据为新的密文
3. 用 base64 解码新的密文, 得到待解密数据
4. 在 encrpytKey 后面补\0 至长度等于 32 位，得到 key
5. 利用上面的 iv, key, 待解密数据，采用 aes-256-cbc 解密数据。

### python 代码示例

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

### php 代码示例

```php
$encryptKey = "testKey";
$data = "kookapp's bot is awesome";
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

## 消息格式及说明

在配置完上述回调地址之后，我们就可以接收并处理事件了，事件的详情参见[事件格式说明](https://developer.kookapp.cn/doc/event)
