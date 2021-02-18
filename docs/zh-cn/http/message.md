# 频道消息相关接口列表
本文档主要列出频道消息相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kaiheila.cn/doc/reference)。


|接口|接口说明|维护状态|
|--|--|--|
|[/api/v3/message/list](#获取频道聊天消息列表)|获取频道聊天消息列表|正常|
|[/api/v3/message/create](#发送频道聊天消息)|发送频道聊天消息|正常|
|[/api/v3/message/update](#更新频道聊天消息)|更新频道聊天消息|正常|
|[/api/v3/message/delete](#删除频道聊天消息)|删除频道聊天消息|正常|
|[/api/v3/message/reaction-list](#获取频道消息某回应的用户列表)|获取频道消息某个回应的用户列表|正常|
|[/api/v3/message/add-reaction](#给某个消息添加回应)|给某个消息添加回应|正常|
|[/api/v3/message/delete-reaction](#删除消息的某个回应)|删除消息的某个回应|正常|

## 消息详情参数说明

| 参数名        | 类型    | 说明               |
| ------------- | ------- | ------------------ |
| id            | string  | 消息 id            |
| type          | int     | 消息类型           |
| author | object | 作者的用户信息               |
| content       | string  | 消息内容           |
| mention       | array   | `@特定用户` 的用户ID数组，与 `mention_info` 中的数据对应 |
| mention_all   | boolean | 是否含有 `@全体人员` |
| mention_roles | array   | `@特定角色` 的角色ID数组，与 `mention_info` 中的数据对应 |
| mention_here  | boolean | 是否含有 `@在线人员` |
| embeds        | array   | 超链接解析数据 |
| attachments | array   | 附加的多媒体数据 |
| reactions | array   | 回应数据 |
| quote    | object (Message) | 引用消息 |
| mention_info    | object | 引用特定用户或特定角色的信息 |
| ↳ mention_part | array        | `@特定用户` 详情 |
| ↳ mention_role_part | array        | `@特定角色` 详情 |


## 获取频道聊天消息列表

### 接口说明

|地址|请求方式|说明|
|--|--|--|
|`/api/v3/message/list`|GET| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| target_id | string  | 是    | GET | 频道 id                                       |
| msg_id | string  | 否    | GET | 参考消息 id，不传则默认为最新的消息 id                                        |
| pin    | unsigned int  | 否   | GET | 只能为0或者1，是否查询置顶消息 |
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
                "id": "bac34958-2c73-45c8",
                "type": 1,
                "content": "11111111111111111111111",
                "mention": [
                    "12314**"
                ],
                "mention_all": false,
                "mention_roles": [],
                "mention_here": [],
                "embeds": [
                    {
                        "type": "bili-video",
                        "url": "https://www.bilibili.com/video/XXXXX",
                        "origin_url": "https://www.bilibili.com/video/XXXXX",
                        "av_no": "11J411E",
                        "iframe_path": "https://player.bilibili.com/player.html?xxx=xxx",
                        "duration": 97,
                        "title": "Title",
                        "pic": "https://**/lc01gi.jpg"
                    }
                ],
                "attachments": false,
                "create_at": 1612685332518,
                "updated_at": 0,
                "reactions": [
                    {
                        "emoji": {
                            "id": "[#129315;]",
                            "name": "[#129315;]"
                        },
                        "count": 1,
                        "me": true
                    }
                ],
                "author": {
                    "id": "1780328444",
                    "username": "小博",
                    "online": false,
                    "avatar": "https://***.jpg"
                },
                "image_name": "",
                "read_status": false,
                "quote": null,
                "mention_info": {
                    "mention_part": [
                        {
                            "id": "28444",
                            "username": "**",
                            "full_name": "**#49",
                            "avatar": "***.jpg"
                        }
                    ],
                    "mention_role_part": [
                        {
                            "role_id": 702,
                            "name": "管理员",
                            "color": 0,
                            "position": 1,
                            "hoist": 0,
                            "mentionable": 0,
                            "permissions": 1
                        }
                    ]
                }
            }
        ]
    }
}
```

## 发送频道聊天消息

### 接口说明

此接口与频道相关接口下的 [发送频道聊天消息](https://developer.kaiheila.cn/doc/http/channel#%E5%8F%91%E9%80%81%E9%A2%91%E9%81%93%E8%81%8A%E5%A4%A9%E6%B6%88%E6%81%AF) 功能相同。

|地址|请求方式|说明|
|--|--|--|
|`/api/v3/message/create`|POST| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| type | int  | 否    | POST | 消息类型, 见[objectName], 不传默认为 `1`, 代表文本类型。`2` 图片消息，`3` 视频消息，`4` 文件消息，`9` 代表 [kmarkdown](https://developer.kaiheila.cn/doc/kmarkdown) 消息, `10` 代表[卡片消息](https://developer.kaiheila.cn/doc/cardmessage)。|
| target_id | string  | 是    | POST | 目标频道 id                                        |
| content    | string  | 是   | POST | 消息内容                                          |
| quote    | string  | 否   | POST | 回复某条消息的 `msgId`                                          |
| nonce      | string  | 否    | POST | nonce, 服务端不做处理, 原样返回                   |
|temp_target_id|string|否|POST|用户id,如果传了，代表该消息是临时消息，该消息不会存数据库，但是会在频道内只给该用户推送临时消息。用于在频道内针对用户的操作进行单独的回应通知等。|

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

## 更新频道聊天消息

### 接口说明

目前只支持消息 `type `为 `1` 的修改。

|地址|请求方式|说明|
|--|--|--|
|`/api/v3/message/update`|POST| |

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

## 删除频道聊天消息

### 接口说明

普通用户只能删除自己的消息，有权限的用户可以删除权限范围内他人的消息。

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/message/delete` | POST     |      |

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
|`/api/v3/message/reaction-list`|GET| |

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
            "tag_info": {
                "color": "#34A853",
                "text": "机器人"
            },
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
|`/api/v3/message/add-reaction`|POST| |

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
|`/api/v3/message/delete-reaction`|POST| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| msg_id | string  | 是    | POST |频道消息的id|
| emoji |string|是|POST| emoji的id, 可以为GuilEmoji或者Emoji|
| user_id| string| 否| POST| 用户的id, 如果不填则为自己的id。删除别人的reaction需要有管理频道消息的权限 |

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
