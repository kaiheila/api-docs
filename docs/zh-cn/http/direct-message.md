# 用户私聊消息接口列表
本文档主要列出私聊消息相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kaiheila.cn/doc/reference)。


|接口|接口说明|维护状态|
|--|--|--|
|[/api/v3/direct-message/list](#获取私信聊天消息列表)|获取私信聊天消息列表|正常|
|[/api/v3/direct-message/create](#发送私信聊天消息)|发送私信聊天消息|正常|
|[/api/v3/direct-message/update](#更新私信聊天消息)|更新私信聊天消息|正常|
|[/api/v3/direct-message/delete](#删除私信聊天消息)|删除私信聊天消息|正常|
|[/api/v3/direct-message/reaction-list](#获取频道消息某回应的用户列表)|获取频道消息某个回应的用户列表|正常|
|[/api/v3/direct-message/add-reaction](#给某个消息添加回应)|给某个消息添加回应|正常|
|[/api/v3/direct-message/delete-reaction](#删除消息的某个回应)|删除消息的某个回应|正常|

## 消息详情参数说明

| 参数名        | 类型    | 说明               |
| ------------- | ------- | ------------------ |
| id            | string  | 消息ID          |
| type          | int     | 消息类型           |
| author_id       | string | 作者的用户ID             |
| content       | string  | 消息内容           |
| embeds        | array   | 超链接解析数据 |
| attachments | array   | 附加的多媒体数据 |
| reactions | array   | 回应数据 |
| quote    | map | 引用数据 |
| read_status    | boolean | 是否已读 |

## 获取私信聊天消息列表

### 接口说明

|地址|请求方式|说明|
|--|--|--|
|`/api/v3/direct-message/list`|GET| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| chat_code | string  | 是    | GET | 私信会话 Code                             |
| msg_id | string  | 否    | GET | 参考消息 id，不传则默认为最新的消息 id                                        |
| flag    | string  | 否   | GET | 查询模式，有三种模式可以选择。不传则默认查询最新的消息 |


### 查询模式说明

| 查询模式 |                  详细说明                  |
| :------: | :----------------------------------------: |
|  before  |  查询参考消息之前的消息，不包括参考消息。  |
|  around  | 查询以参考消息为中心，前后一定数量的消息。 |
|  after   |  查询参考消息之后的消息，不包括参考消息。  |


### 返回参数说明

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |
| items | array   | 消息列表                                 |

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "items": [
            {
                "id": "3dcca4b3-ae4e-474264e0b676",
                "type": 1,
                "content": "Hello",
                "embeds": [],
                "attachments": false,
                "create_at": 1612677356950,
                "updated_at": 0,
                "reactions": [],
                "author_id": "8444",
                "image_name": "",
                "read_status": false,
                "quote": null,
                "mention_info": null
            }
        ]
    }
}
```

## 发送私信聊天消息

### 接口说明

|地址|请求方式|说明|
|--|--|--|
|`/api/v3/direct-message/create`|POST| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| type | int  | 否    | POST | 消息类型, 见[type], 不传默认为 `1`, 代表文本类型。`2` 图片消息，`3` 视频消息，`4` 文件消息，`9` 代表 [kmarkdown](https://developer.kaiheila.cn/doc/kmarkdown) 消息, `10` 代表[卡片消息](https://developer.kaiheila.cn/doc/cardmessage)。|
| chat_code | string  | 是    | POST | 目标会话 id                                    |
| content    | string  | 是   | POST | 消息内容                                          |
| quote    | string  | 否   | POST | 回复某条消息的 `msgId`                                          |
| nonce      | string  | 否    | POST | nonce, 服务端不做处理, 原样返回                   |

### 返回参数说明

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |
| msg_id | string       | 服务端生成的消息 id                                       |
| msg_timestamp | int          | 消息发送时间(服务器时间戳)                                          |
| nonce | string |随机字符串，见参数列表 |

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "msg_id": "50974c-364c983fa6cb",
        "msg_timestamp": 1607072537177,
        "nonce": "xxxx"
    }
}
```

## 更新私信聊天消息

### 接口说明

目前只支持消息 `type `为 `1` 的修改。

|地址|请求方式|说明|
|--|--|--|
|`/api/v3/direct-message/update`|POST| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| msg_id | string | 是   | POST | 消息 id |
| content    | string  | 是   | POST | 消息内容                                          |
| quote    | string  | 否   | POST | 回复某条消息的 `msgId`。如果为空，则代表删除回复，不传则无影响。                  |

### 返回参数说明

无返回参数

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": []
}
```

## 删除私信聊天消息

### 接口说明

只能删除自己的消息。

| 地址                            | 请求方式 | 说明 |
| ------------------------------- | -------- | ---- |
| `/api/v3/direct-message/delete` | POST     |      |

### 参数列表

| 参数名  | 类型   | 必传 | 参数区域 | 说明                                                         |
| ------- | ------ | ---- | -------- | ------------------------------------------------------------ |
| msg_id  | string | 是   | POST     | 消息 id                                                      |

### 返回参数说明

无返回参数

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": []
}
```

## 获取频道消息某回应的用户列表 

### 接口说明
|地址|请求方式|说明|
|--|--|--|
|`/api/v3/direct-message/reaction-list`|GET| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| msg_id | string  | 是    | GET |频道消息的id|
| emoji |string|是|GET| emoji的id, 可以为GuilEmoji或者Emoji, 注意：在get中，应该进行urlencode|

### 返回参数说明

返回的是用户的列表，参数如下：

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |
| id | string       |   用户的id                                    |
|username | string          | 用户的名称                                         |
|nickname | string          | 用户在服务器内的呢称                               |
|identify_num | string |用户名的认证数字，用户名正常为：user_name#identify_num |
|online| boolean| 当前是否在线|
|status|int|用户的状态, 0代表正常，10代表被封禁|
|avatar|string|用户的头像的url地址|
|bot|boolean|用户是否为机器人|
|reaction_time|intval|用户点击reaction的毫秒时间戳|

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        {
            "id": "xxxx",
            "username": "test",
            "identify_num": "xxx",
            "online": false,
            "status": 0,
            "avatar": "xxxx",
            "bot": true,
            "nickname": "xxxx",
            "reaction_time": 1612323994414
        } 
    }
}
```

## 给某个消息添加回应 

### 接口说明
|地址|请求方式|说明|
|--|--|--|
|`/api/v3/direct-message/add-reaction`|POST| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| msg_id | string  | 是    | POST |频道消息的id|
| emoji |string|是|POST| emoji的id, 可以为GuilEmoji或者Emoji|

### 返回参数说明

无返回参数

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": []
}
```

## 删除消息的某个回应

### 接口说明
|地址|请求方式|说明|
|--|--|--|
|`/api/v3/direct-message/delete-reaction`|POST| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| msg_id | string  | 是    | POST |频道消息的id|
| emoji |string|是|POST| emoji的id, 可以为GuilEmoji或者Emoji|

### 返回参数说明

无返回参数

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": []
}
```
