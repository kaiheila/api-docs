# 消息模板&管道

## 引言
很多时候，用户希望做一些常规的消息订阅功能（比如，从`github`或者`jira`等转发至`KOOK`），在传统的方式下，大体的流程如下：

![常规处理流程](https://img.kookapp.cn/assets/2024-11/07/tHmsRQJ69B0ed08t.png)

要实现这样的功能需要做如下的事情：
- 通常有一些第三方网站会支持webhook, 允许向外部发送一些通知消息/事件。
- 开发者需要有一个网站，来接收这个第三方网站的消息/事件。
- 在接收到消息/事件后，开发者需要进行代码的转换和处理，转换成KOOK支持的格式，然后发送到`KOOK`的接口

对于非技术人员而言，这样的流程下几乎无法实现这样一个简单的功能。为此，我们设计了消息管道 + 模板系统，来帮助非技术人员能够通过简单的方式来实现消息的订阅及转发。同时，消息模板也能为开发者提供便利，因此，本文主要分为两部分来讲述：消息模板系统 和 消息管道。大体的流程如下所示：

![新](https://img.kookapp.cn/assets/2024-11/07/mfFcPc6S5t0g0070.png)

## 示例
为了帮助大家很好的理解这个过程，我们来看下示例，这个示例无需服务器和代码，卡片格式可以自行定义：
- [gitlab事件转发KOOK](https://developer.kookapp.cn/doc/example/gitlab)。



## 消息管道
消息管道可以简单的理解为我们会在服务器内允许插入新的两种管道，来方便外部与服务器内进行消息交互：
- 入管道。可以通过简单的方式，向服务器的频道内发送消息。
- 出管道。当前未开放。

入管道相当于我们提供了一个有限权限的access_token来给某个服务器内来发消息，它不像bot的token的安全等级那么高，但是也需要大家谨慎使用和保管。通过该 access_token, 第三方就可以直接通过如下的方式给KOOK发消息：
```bash
curl https://www.kookapp.cn/api/v3/message/send-pipemsg?access_token=xxx  -H "Content-type: application/json" -d '{"content":"hello world"}'
```

**注意:** 消息管道只是给机器人提供了一个便捷的入口，机器人依旧需要有发消息的权限，才能通过简单发送消息。

## 消息模板

在机器人正常的消息发送中，我们会发现会遇见如下问题：
- 在常规情况下，机器人的消息量比较大，会比较容易受到rate-limit的限制
- 机器人有些时候会有一些固定的方案或者消息给用户回复，但是依旧容易受到系统的拦截
因此消息模板会帮助开发者来解决这一问题。

### 模板的基本使用
在开发者后台我们可以创建模板并更新模板。模板本质上可以如下理解：
    `input` + 环境变量  + 模板 = `kmd`/`cardmsg`
其中，`input`是开发者的输入，也就是之前调用消息发送时的，content部分。



### 模板语法
由于人力和资源的问题，目前我们仅支持了`twig`(`php`原生支持), 未来可能会支持`jinja`。

`Twig`是一款灵活、快速、安全的PHP模板引擎。用户不需要了解`php`的语法，即可以使用。我们可以在模板中，进行逻辑，循环控制等，能帮助我们很好的实现我们的想要的需求，详情参见: [twig语法](https://www.kancloud.cn/yunye/twig-cn/159454)

考虑到大家可能对`twig`比较陌生，我们在后台也提供了很多示例，大家可以多多参考示例。

鉴于`json`格式的卡片消息在书写起来有诸多不便，我们也在模板系统中支持了`xml`和`yaml`， 如果你厌烦了各种嵌套的花括号，不妨试试`yaml`/`xml`。不要有太多的心理负担，它不会对你之前的使用产生什么影响，我们只是会在生成模板的最后将`yaml`/`xml`转换为之前的`cardmsg`的`json`格式。

**模板自定义变量及函数**

在模板中，我们可以通过访问data来获取开发者传入的参数。示例`{{data.roles}}`。

除了官方提供的函数外，KOOK也提供了一些自定义的函数来供大家使用：

|函数|位置|说明|
|--|--|--|
|json_escape|filter|对文本做过滤，防止文本中出现json语法的内容，而导致模板消息发送失败。示例：`{{username|json_escape}}`|
|yaml_escape|filter|对文本做过滤，防止文本中出现yaml语法的内容，而导致模板消息发送失败, 可以接受传参，0代表双引号字符串转义，1代表单引号字符串转义，默认为0。示例：`{{xxx|yaml_escape}}`|
|kmd_escape|filter|对文本做过滤，防止文本中出现kmd语法的内容，而导致模板消息失败。先把函数名占住，目前没有做任何事|

另外，KOOK为了方便大家的使用，还提供了全局的函数，需要通过`KOOK.method（）`来访问，示例：`服务器名：{{KOOK.getGuild().name}}`。如下为目前支持的函数列表：

|函数|参数|说明|
|--|--|--|
|KOOK.getGuild(guild_id)|guild_id: string, 服务器id。可不填，不填则为当前消息发送的服务器.如果填了，只能获取自己加入的服务器的信息|服务器信息，格式参见 [服务器](https://developer.kookapp.cn/doc/objects#%E6%9C%8D%E5%8A%A1%E5%99%A8%20Guild)|
|KOOK.getChannel()|无|发送消息的频道， 格式参见 [频道](https://developer.kookapp.cn/doc/objects#%E9%A2%91%E9%81%93%20Channel)|
|KOOK.getSender()|无|获取当前消息发送者的信息, 格式参见[用户](https://developer.kookapp.cn/doc/objects#%E7%94%A8%E6%88%B7%20User)|
|KOOK.getTargetUser()|无| 目标用户信息。在频道内时，临时消息时有用户。在私聊时，为对方用户。格式参见[用户](https://developer.kookapp.cn/doc/objects#%E7%94%A8%E6%88%B7%20User)|
|KOOK.getQuote()|无| 引用的消息，格式参见 [引用消息](https://developer.kookapp.cn/doc/objects#%E5%BC%95%E7%94%A8%E6%B6%88%E6%81%AF%20Quote)|
|KOOK.image(url, defaultUrl)|url: string图片地址 ， defaultUrl: string失败时的图片地址,只能为站内地址，如果不传为KOOK默认失败图片|图片地址，示例：`{{KOOK.image(url1, url2)}}`|

注：如果需要添加额外的函数处理，请进入开发者中心找管理员提。


### 模板审核(待开发)
除非模板涉及风险被封禁，无论模板是否提交审核，该模板都可以进行消息的发送。模板审核通过之后会有如下的好处：
- 审核通过的消息，可能会减少被拦截的可能性。
- 在审核时，我们会评估该模板的内容，分配不同的消耗值。消耗值越低，意味着单位时间内可以发送更多的消息。未审核的模板跟普通消息的消息值是一样的，审核模板的消耗值 <= 普通消息的消耗值。
- 模板消息在提交审核期间，是可以正常使用模板消息进行发送的。但是不允许修改。
- 在模板审核通过后，如果更改消息，会重新进入待审核状态，需要重新提交审核。
- 模板删除后，会导致使用该模板的消息无法发送，请谨慎删除

# 模板接口
通过相关的接口，可以让机器人通过api接口来管理模板，主要的接口如下所示：  


| 接口                                                                                      | 接口说明             | 维护状态 |
| ----------------------------------------------------------------------------------------- | -------------------- | -------- |
| /api/v3/template/list| 获取模板列表     | 正常  |
| /api/v3/template/create                                                    | 创建模板        | 正常     |
| /api/v3/template/update                                                   | 更新模板         | 正常     |
| /api/v3/template/delete                                                    | 删除模板         | 正常     |


在如下的接口中，模板的字段如下所示：

|字段|类型|说明|
|--|--|--|
|id|string| 模板的id,最长16|
|title| string| 模型的标题，最长64|
|type| int| 目前固定为0，代表模型使用twig渲染|
|msgtype|int|1代表kmd消息，2代表通过json发卡片消息，3代表通过yaml发卡片消息|
|status|int|0代表未审核，1代表审核中，2代表审核通过，3代表审核拒绝，当前没有开发审核，都为0|
|test_data| string| 测试数据， 主要用于界面上的便利测试|
|test_channel| string| 测试的频道，最长64。 主要用于界面上的便利测试|
|content| string|模板内容|

## 获取模板列表

### 接口说明

| 地址                   | 请求方式 | 说明 |
| ---------------------- | -------- | ---- |
| `/api/v3/template/list` | GET      | 符合接口规范，参见 [接口规范](https://developer.kookapp.cn/doc/reference)  |

### 参数列表
无

### 返回参数说明

返回模板列表，参见模板字段说明。

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "items": [
	{
               "id": "84766989",
                "title": "github模板",
                "type": 0,
                "status": 0,
                "test_channel": "",
                "msgtype": 2,
                "content": "[\r\n  {\r\n    \"type\": \"card\",\r\n    \"theme\": \"info\",\r\n    \"size\": \"lg\",\r\n    \"modules\": [\r\n      {\r\n        \"type\": \"header\",\r\n        \"text\": {\r\n          \"type\": \"plain-text\",\r\n          \"content\": \"New Push Event from Github\"\r\n        }\r\n      },\r\n      {\r\n        \"type\": \"divider\"\r\n      },\r\n      {\r\n        \"type\": \"section\",\r\n        \"text\": {\r\n          \"type\": \"kmarkdown\",\r\n          \"content\": \"[{{ data.sender.login }}]({{ data.sender.url }}}) pushed {{ data.commits|length }} commits to\\n[{{ data.repository.full_name }}]({{ data.repository.html_url }})\"\r\n        },\r\n        \"mode\": \"left\",\r\n        \"accessory\": {\r\n          \"type\": \"image\",\r\n          \"circle\": true,\r\n          \"src\": \"{{ data.sender.avatar_url }}\",\r\n          \"size\": \"lg\"\r\n        }\r\n      },\r\n      {\r\n        \"type\": \"divider\"\r\n      },\r\n      {\r\n        \"type\": \"context\",\r\n        \"elements\": [\r\n          {\r\n            \"type\": \"plain-text\",\r\n            \"content\": \"{{ data.before|slice(0, 6) }} → {{ data.after|slice(0, 6) }}\"\r\n          }\r\n        ]\r\n      }\r\n      {% for item in data.commits %}\r\n        ,\r\n      {\r\n        \"type\": \"section\",\r\n        \"text\": {\r\n          \"type\": \"kmarkdown\",\r\n          \"content\": \"[{{ item.id|slice(0,6) }}]({{ item.url }}) By {{ item.author.name }}: {{ item.message|json_escape() }}\"\r\n        }\r\n      }\r\n      {% endfor %}\r\n    ]\r\n  }\r\n]",
                "test_data": "{}"
	}
    ],
    "meta": {
      "page": 1,
      "page_total": 1,
      "page_size": 50,
      "total": 2
    },
    "sort": []
  }
}
```

## 创建模板

### 接口说明

| 地址                   | 请求方式 | 说明 |
| ---------------------- | -------- | ---- |
| `/api/v3/template/create` | POST|  |

### 参数列表
参见template模板格式， 支持传参：title（必传）, content（必传）, test_data, msgtype, type, test_channel

### 返回参数说明

返回model的模板，参见模板字段说明。

### 返回示例

```json
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "model": {
            "id": "64291017",
            "content": "hello world",
            "type": 0,
            "status": 0,
            "test_data": "{\n}",
            "test_channel": "",
            "title": "测试前台Licensed Fresh Shoes",
            "msgtype": 1
        }
    }
}
```


## 更新模板

### 接口说明

| 地址                   | 请求方式 | 说明 |
| ---------------------- | -------- | ---- |
| `/api/v3/template/update` | POST|  |

### 参数列表
参见template模板格式，必须在post中传入id字段(模板id), 支持更改的参数：title, content, test_data, msgtype, type, test_channel

### 返回参数说明

返回model的模板，参见模板字段说明。

### 返回示例

```json
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "model": {
            "id": "64291017",
            "content": "hello world",
            "type": 0,
            "status": 0,
            "test_data": "{\n}",
            "test_channel": "",
            "title": "测试前台Licensed Fresh Shoes",
            "msgtype": 1
        }
    }
}
```

## 删除模板

### 接口说明

| 地址                   | 请求方式 | 说明 |
| ---------------------- | -------- | ---- |
| `/api/v3/template/delete` | POST|  |

### 参数列表
参见template模板格式，必须在post中传入id字段(模板id)

### 返回参数说明

无

### 返回示例

```json
{
    "code": 0,
    "message": "操作成功",
    "data": {}
}
```

