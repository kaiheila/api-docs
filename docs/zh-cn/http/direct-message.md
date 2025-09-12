# 用户私聊消息接口列表

本文档主要列出私聊消息相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kookapp.cn/doc/reference)。

| 接口                                                                  | 接口说明                       | 维护状态 |
| --------------------------------------------------------------------- | ------------------------------ | -------- |
| [/api/v3/direct-message/list](#获取私信聊天消息列表)                  | 获取私信聊天消息列表           | 正常     |
| [/api/v3/direct-message/view](#获取私信聊天消息详情)                  | 获取私信聊天消息详情           | 正常     |
| [/api/v3/direct-message/create](#发送私信聊天消息)                    | 发送私信聊天消息               | 正常     |
| [/api/v3/direct-message/update](#更新私信聊天消息)                    | 更新私信聊天消息               | 正常     |
| [/api/v3/direct-message/delete](#删除私信聊天消息)                    | 删除私信聊天消息               | 正常     |
| [/api/v3/direct-message/reaction-list](#获取频道消息某回应的用户列表) | 获取频道消息某个回应的用户列表 | 正常     |
| [/api/v3/direct-message/add-reaction](#给某个消息添加回应)            | 给某个消息添加回应             | 正常     |
| [/api/v3/direct-message/delete-reaction](#删除消息的某个回应)         | 删除消息的某个回应             | 正常     |

## 消息详情参数说明

| 参数名      | 类型    | 说明             |
| ----------- | ------- | ---------------- |
| id          | string  | 消息 ID          |
| type        | int     | 消息类型         |
| author_id   | string  | 作者的用户 ID    |
| content     | string  | 消息内容         |
| embeds      | array   | 超链接解析数据   |
| attachments | array   | 附加的多媒体数据 |
| reactions   | array   | 回应数据         |
| quote       | map     | 引用数据         |
| read_status | boolean | 是否已读         |

## 消息配额说明
平台将基于开发者账号维度实施消息发送总量管控，每位开发者账号下所有机器人单日消息发送总量上限为 10,000 条。每日配额的重置时间为北京时间 (UTC+8) 的中午 12:00。

目前所有通过以下接口由机器人主动发出的消息，都会被计入每日配额。为了公平起见，请求失败的消息将不会被计入当日配额。

```
/api/v3/message/create
/api/v3/message/update
/api/v3/direct-message/create
/api/v3/direct-message/update
/api/v3/thread/create
/api/v3/thread/reply
```

临时消息主要用于对用户操作的临时性、交互式回复。考虑到它们的传播范围和滥用风险都非常有限，我们将它们排除在配额计算之外，以保障机器人核心互动功能的流畅。

同时如果创建和更新消息是对之前5分钟内用户发送给当前机器人的消息的第一次回复，也会在计算发送量时给于大幅折扣。

我们计划在未来增加模板消息。这类消息主要用于格式固定的通知场景，它将不会占用你的消息配额，为开发者在特定场景下提供更多的消息缓冲空间。

如有疑问，请在开发者中心社区服务器中 联系 不鲲#0001


## 获取私信聊天消息列表

### 接口说明

| 地址                          | 请求方式 | 说明                                                   |
| ----------------------------- | -------- | ------------------------------------------------------ |
| `/api/v3/direct-message/list` | GET      | 此接口非标准分页，需要根据参考消息来查询相邻分页的消息 |

### 参数列表

| 参数名    | 位置  | 类型    | 必需  | 说明                                                               |
| --------- | ----- | ------- | ----- | ------------------------------------------------------------------ |
| chat_code | query | string  | false | 私信会话 Code。`chat_code`与`target_id`必须传一个                  |
| target_id | query | string  | false | 目标用户 id，后端会自动创建会话。有此参数之后可不传`chat_code`参数 |
| msg_id    | query | string  | false | 参考消息 id，不传则查询最新消息                                    |
| flag      | query | string  | false | 查询模式，有三种模式可以选择。不传则默认查询最新的消息。           |
| page      | query | integer | false | 目标页数                                                           |
| page_size | query | integer | false | 当前分页消息数量, 默认 50                                          |

### 查询模式说明

**flag**: 查询模式，有三种模式可以选择。不传则默认查询最新的消息。  
before: 查询参考消息之前的消息，不包括参考消息  
around: 查询以参考消息为中心，前后一定数量的消息  
after: 查询参考消息之后的消息，不包括参考消息

### 返回参数说明

| 参数名 | 类型  | 说明     |
| ------ | ----- | -------- |
| items  | array | 消息列表 |

### 返回示例

```json
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
        "attachments": [],
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

## 获取私信聊天消息详情

### 接口说明

| 地址                          | 请求方式 | 说明                                                   |
| ----------------------------- | -------- | ------------------------------------------------------ |
| `/api/v3/direct-message/view` | GET      |  |

### 参数列表

| 参数名    | 位置  | 类型    | 必需  | 说明                                                               |
| --------- | ----- | ------- | ----- | ------------------------------------------------------------------ |
| chat_code | query | string  | true | 私信会话 Code。                                                  |
| msg_id    | query | string  | true | 私聊消息 id                                    |

### 返回参数说明

参考 [消息详情参数说明](#消息详情参数说明)

### 返回示例

```json
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "id": "0623c444-ca46-41ed-b17a-2870b69488e6",
        "type": 9,
        "content": "ncoixhskbhjcnjhsk",
        "embeds": [],
        "attachments": false,
        "create_at": 1684840220824,
        "updated_at": 0,
        "reactions": [
            {
                "emoji": {
                    "id": "1015054289/2/H20B7O7s8c08c08c",
                    "name": "--"
                },
                "count": 1,
                "me": true
            }
        ],
        "author_id": "3264360465",
        "image_name": "",
        "mention_info": {
            "mention_part": [],
            "channel_part": [],
            "item_part": []
        },
        "from_type": 0,
        "msg_icon": "",
        "quote": null
    }
}
```

## 发送私信聊天消息

### 接口说明

| 地址                            | 请求方式 | 说明 |
| ------------------------------- | -------- | ---- |
| `/api/v3/direct-message/create` | POST     |      |

### 参数列表

| 参数名    | 类型   | 必传 | 参数区域 | 说明                                                                                                                                                                                                                                     |
| --------- | ------ | ---- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type      | int    | 否   | POST     | 消息类型, 见[type], 不传默认为 `1`, 代表文本类型。`9` 代表 [kmarkdown](https://developer.kookapp.cn/doc/kmarkdown) 消息, `10` 代表[卡片消息](https://developer.kookapp.cn/doc/cardmessage)。 |
| target_id | string | 否   | POST     | 目标用户 id，后端会自动创建会话。有此参数之后可不传 `chat_code `参数                                                                                                                                                                     |
| chat_code | string | 否   | POST     | 目标会话 Code，`chat_code` 与 `target_id` 必须传一个                                                                                                                                                                                     |
| content   | string | 是   | POST     | 消息内容                                                                                                                                                                                                                                 |
| quote     | string | 否   | POST     | 回复某条消息的 `msgId`                                                                                                                                                                                                                   |
| nonce     | string | 否   | POST     | nonce, 服务端不做处理, 原样返回                                                                                                                                                                                                          |
| template_id| string| 否| POST|模板消息id, 如果使用了，content会作为模板消息的input，参见[模板消息](https://developer.kookapp.cn/doc/http/template)|
|reply_msg_id|string| 否| POST | 当前消息回复的用户5分钟内发送给当前机器人消息的msg_id，如果是当前开发者的第一次回复，扣减当日发送量按n分之一条计算|

### 返回参数说明

| 参数名        | 类型   | 说明                       |
| ------------- | ------ | -------------------------- |
| msg_id        | string | 服务端生成的消息 id        |
| msg_timestamp | int    | 消息发送时间(服务器时间戳) |
| nonce         | string | 随机字符串，见参数列表     |

### 返回示例

```json
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

目前支持消息 `type `为 `9、10` 的修改，即 KMarkdown 和 CardMessage

| 地址                            | 请求方式 | 说明 |
| ------------------------------- | -------- | ---- |
| `/api/v3/direct-message/update` | POST     |      |

### 参数列表

| 参数名  | 位置 | 类型   | 必需  | 说明                                                            |
| ------- | ---- | ------ | ----- | --------------------------------------------------------------- |
| msg_id  | body | string | false | 消息 id                                                         |
| content | body | string | true  | 消息内容                                                        |
| quote   | body | string | false | 回复某条消息的`msgId`。如果为空，则代表删除回复，不传则无影响。 |
| template_id| body| string | false|模板消息id, 如果使用了，content会作为模板消息的input，参见[模板消息](https://developer.kookapp.cn/doc/http/template)|
|reply_msg_id|body| string| false | 当前消息回复的用户5分钟内发送给当前机器人消息的msg_id，如果是当前开发者的第一次回复，扣减当日发送量按n分之一条计算 |

### 返回参数说明

无返回参数

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {}
}
```

## 删除私信聊天消息

### 接口说明

只能删除自己的消息。

| 地址                            | 请求方式 | 说明 |
| ------------------------------- | -------- | ---- |
| `/api/v3/direct-message/delete` | POST     |      |

### 参数列表

| 参数名 | 位置 | 类型   | 必需  | 说明    |
| ------ | ---- | ------ | ----- | ------- |
| msg_id | body | string | false | 消息 id |

### 返回参数说明

无返回参数

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {}
}
```

## 获取频道消息某回应的用户列表

### 接口说明

| 地址                                   | 请求方式 | 说明 |
| -------------------------------------- | -------- | ---- |
| `/api/v3/direct-message/reaction-list` | GET      |      |

### 参数列表

| 参数名 | 位置  | 类型   | 必需  | 说明                                                                           |
| ------ | ----- | ------ | ----- | ------------------------------------------------------------------------------ |
| msg_id | query | string | true  | 消息的 id                                                                      |
| emoji  | query | string | false | emoji 的 id, 可以为 GuildEmoji 或者 Emoji, 注意：在 get 中，应该进行 urlencode |

### 返回参数说明

返回的是用户的列表，参数如下：

| 参数名        | 类型    | 说明                                                   |
| ------------- | ------- | ------------------------------------------------------ |
| id            | string  | 用户的 id                                              |
| username      | string  | 用户的名称                                             |
| nickname      | string  | 用户在服务器内的呢称                                   |
| identify_num  | string  | 用户名的认证数字，用户名正常为：user_name#identify_num |
| online        | boolean | 当前是否在线                                           |
| status        | int     | 用户的状态,0 和 1 代表正常，10 代表被封禁              |
| avatar        | string  | 用户的头像的 url 地址                                  |
| bot           | boolean | 用户是否为机器人                                       |
| reaction_time | intval  | 用户点击 reaction 的毫秒时间戳                         |

### 返回示例

```json
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
            "avatar": "https://img.kaiheila.cn/avatars/2020-02/xxxx.jpg/icon",
            "vip_avatar": "https://img.kaiheila.cn/avatars/2020-02/xxxx.jpg/icon",
            "bot": false,
            "nickname": "xxxx",
            "reaction_time": 1612323994414
        }
    }
}
```

## 给某个消息添加回应

### 接口说明

| 地址                                  | 请求方式 | 说明 |
| ------------------------------------- | -------- | ---- |
| `/api/v3/direct-message/add-reaction` | POST     |      |

### 参数列表

| 参数名 | 位置 | 类型   | 必需 | 说明                                     |
| ------ | ---- | ------ | ---- | ---------------------------------------- |
| msg_id | body | string | true | 消息 id                                  |
| emoji  | body | string | true | emoji 的 id, 可以为 GuilEmoji 或者 Emoji |

### 返回参数说明

无返回参数

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {}
}
```

## 删除消息的某个回应

### 接口说明

| 地址                                     | 请求方式 | 说明 |
| ---------------------------------------- | -------- | ---- |
| `/api/v3/direct-message/delete-reaction` | POST     |      |

### 参数列表

| 参数名  | 位置 | 类型   | 必需  | 说明                                                                           |
| ------- | ---- | ------ | ----- | ------------------------------------------------------------------------------ |
| msg_id  | body | string | true  | 消息 id                                                                        |
| emoji   | body | string | true  | 表情的 ID                                                                      |
| user_id | body | string | false | 用户的 id, 如果不填则为自己的 id。删除别人的 reaction 需要有管理频道消息的权限 |

### 返回参数说明

无返回参数

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {}
}
```
