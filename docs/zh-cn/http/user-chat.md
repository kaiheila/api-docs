# 用户私信接口列表
本文档主要列出私信相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kaiheila.cn/doc/reference)。


|接口|接口说明|维护状态|
|--|--|--|
|[/api/v3/user-chat/index](#获取私信聊天会话列表)|获取私信聊天会话列表|正常|
|[/api/v3/user-chat/create](#创建私信聊天会话)|创建私信聊天会话|正常|
|[/api/v3/user-chat/update](#更新私信聊天会话)|更新私信聊天会话|正常|
|[/api/v3/user-chat/delete](#删除私信聊天会话)|删除私信聊天会话|正常|
|[/api/v3/user-chat/msg-list](#获取私信聊天消息列表)|获取私信聊天消息列表|正常|
|[/api/v3/user-chat/create-msg](#发送私信聊天消息)|发送私信聊天消息|正常|
|[/api/v3/user-chat/update-msg](#更新私信聊天消息)|更新私信聊天消息|正常|
|[/api/v3/user-chat/delete-msg](#删除私信聊天消息)|删除私信聊天消息|正常|

## 获取私信聊天会话列表

### 接口说明

|地址|请求方式|说明|
|--|--|--|
|`/api/v3/user-chat/index`|GET| |

### 参数列表

无请求参数

### 返回参数说明

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |
| code | string | 私信会话 Code                        |
| last_read_time | int | 上次阅读消息的时间 |
| latest_msg_time | int | 最新消息时间 |
| unread_count | int | 未读消息数 |
| target_info | object (User) | 目标用户信息 |
| ↳ id | string        | 目标用户 ID |
| ↳ username | string        | 目标用户名 |
| ↳ online | boolean  | 是否在线 |
| ↳ avatar | string        | 头像图片链接 |


### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": [
        {
            "code": "sderwrw**",
            "last_read_time": 1612696873000,
            "latest_msg_time": 1612696873000,
            "unread_count": 0,
            "target_info": {
                "id": "415212",
                "username": "工具",
                "online": false,
                "avatar": "https://***.jpg"
            },
        }
    ]
}
```

## 获取私信会话详情

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/user-chat/view` | GET      |      |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| chat_code | string  | 是    | GET | 私聊会话 Code                          |

### 返回参数说明

| 参数名       | 类型          | 说明          |
| ------------ | ------------- | ------------- |
| code         | string        | 私信会话 Code |
| last_read_time | int | 上次阅读消息的时间 |
| latest_msg_time | int | 最新消息时间 |
| unread_count | int           | 未读消息数    |
| is_friend | boolean   | 是否是好友                                     |
| is_blocked | boolean |是否已屏蔽对方 |
| is_target_blocked | boolean    | 是否已被对方屏蔽                                  |
| target_info | object (User) | 目标用户信息 |
| ↳ id | string        | 目标用户 ID |
| ↳ username | string        | 目标用户名 |
| ↳ avatar | string        | 头像图片链接 |

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "code": "5c7ec6d021216c136c9198285c15ed47",
        "last_read_time": 1612175653000,
        "latest_msg_time": 1612160693000,
        "unread_count": 0,
        "is_friend": false,
        "is_blocked": false,
        "is_target_blocked": false,
        "target_info": {
            "id": "3903536527",
            "username": "夏天1",
            "avatar": "https://chuanyuapp.oss-cn-qingdao.aliyuncs.com/assets/avatar_10.jpg/icon",
        }
    }
}
```

## 创建私信聊天会话

### 接口说明

|地址|请求方式|说明|
|--|--|--|
|`/api/v3/user-chat/create`|POST| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| target_id | string  | 是    | POST | 目标用户 id                                  |

### 返回参数说明

具体参数参考列表与详情

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "code": "3547b7*****2476dd9d7777f32a",
        "last_read_time": 1612697864000,
        "latest_msg_time": 1612168629000,
        "unread_count": 0,
        "is_friend": false,
        "is_blocked": false,
        "is_target_blocked": false,
        "target_info": {
            "id": "325***0",
            "username": "工具",
            "online": false,
            "avatar": "https://**.jpg"
        }
    }
}
```

## 删除私信聊天会话

### 接口说明

只能删除自己的消息。

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/message/delete` | POST     |      |

### 参数列表

| 参数名    | 类型   | 必传 | 参数区域 | 说明          |
| --------- | ------ | ---- | -------- | ------------- |
| chat_code | string | 是   | POST     | 私信会话 Code |

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
| quote    | object | 引用数据 |
| read_status    | boolean | 是否已读 |

## 获取私信聊天消息列表

### 接口说明

|地址|请求方式|说明|
|--|--|--|
|`/api/v3/user-chat/msg-list`|GET| |

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
|`/api/v3/user-chat/create-msg`|POST| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| type | int  | 否    | POST | 消息类型, 见[objectName], 不传默认为 `1`, 代表文本类型。`2` 图片消息，`3` 视频消息，`4` 文件消息，`9` 代表 [kmarkdown](https://developer.kaiheila.cn/doc/kmarkdown) 消息, `10` 代表[卡片消息](https://developer.kaiheila.cn/doc/cardmessage)。|
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

目前只支持消息 `type `为 `1` 的修改。

|地址|请求方式|说明|
|--|--|--|
|`/api/v3/user-chat/update-msg`|POST| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| msg_id | string | 是   | POST | 消息 id |
| content    | string  | 是   | POST | 消息内容                                          |
| quote    | string  | 否   | POST | 回复某条消息的 `msgId`。如果为空，则代表删除回复，不传则无影响。                  |

### 返回参数说明

无返回参数

### 返回示例

```json
{
    "code": 0,
    "message": "操作成功",
    "data": []
}
```

## 删除私信聊天消息

### 接口说明

只能删除自己的消息。

| 地址                         | 请求方式 | 说明 |
| ---------------------------- | -------- | ---- |
| `/api/v3/message/delete-msg` | POST     |      |

### 参数列表

| 参数名  | 类型   | 必传 | 参数区域 | 说明                                                         |
| ------- | ------ | ---- | -------- | ------------------------------------------------------------ |
| msg_id  | string | 是   | POST     | 消息 id                                                      |

### 返回参数说明

无返回参数

### 返回示例

```json
{
    "code": 0,
    "message": "操作成功",
    "data": []
}
```

