# 频道消息相关接口列表

本文档主要列出频道消息相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kookapp.cn/doc/reference)。

| 接口                                                           | 接口说明                       | 维护状态 |
| -------------------------------------------------------------- | ------------------------------ | -------- |
| [/api/v3/message/list](#获取频道聊天消息列表)                  | 获取频道聊天消息列表           | 正常     |
| [/api/v3/message/view](#获取频道聊天消息详情)                  | 获取频道聊天消息详情           | 正常     |
| [/api/v3/message/create](#发送频道聊天消息)                    | 发送频道聊天消息               | 正常     |
| [/api/v3/message/update](#更新频道聊天消息)                    | 更新频道聊天消息               | 正常     |
| [/api/v3/message/delete](#删除频道聊天消息)                    | 删除频道聊天消息               | 正常     |
| [/api/v3/message/reaction-list](#获取频道消息某回应的用户列表) | 获取频道消息某个回应的用户列表 | 正常     |
| [/api/v3/message/add-reaction](#给某个消息添加回应)            | 给某个消息添加回应             | 正常     |
| [/api/v3/message/delete-reaction](#删除消息的某个回应)         | 删除消息的某个回应             | 正常     |
| [/api/v3/message/send-pipemsg](#发送管道消息)         | 发送管道消息             | 正常     |

## 消息详情参数说明

| 参数名              | 类型    | 说明                                                                                                           |
| ------------------- | ------- | -------------------------------------------------------------------------------------------------------------- |
| id                  | string  | 消息 id                                                                                                        |
| type                | int     | 消息类型                                                                                                       |
| author              | map     | 作者的用户信息                                                                                                 |
| content             | string  | 消息内容（为了保障消息正常发出，请不要超过 8000 字符）                                                         |
| mention             | array   | `@特定用户` 的用户 ID 数组，与 `mention_info` 中的数据对应                                                     |
| mention_all         | boolean | 是否含有 `@全体人员`                                                                                           |
| mention_roles       | array   | `@特定角色` 的角色 ID 数组，与 `mention_info` 中的数据对应                                                     |
| mention_here        | boolean | 是否含有 `@在线人员`                                                                                           |
| embeds              | array   | 超链接解析数据                                                                                                 |
| attachments         | map     | 附加的多媒体数据 参考[对象-Attachments](https://developer.kookapp.cn/doc/objects#附加的多媒体数据Attachments) |
| reactions           | array   | 回应数据                                                                                                       |
| quote               | map     | 引用消息 参考[对象-Quote](https://developer.kookapp.cn/doc/objects#引用消息Quote)                             |
| mention_info        | map     | 引用特定用户或特定角色的信息                                                                                   |
| » mention_part      | array   | `@特定用户` 详情                                                                                               |
| » mention_role_part | array   | `@特定角色` 详情                                                                                               |

## 获取频道聊天消息列表

### 接口说明

| 地址                   | 请求方式 | 说明                                                   |
| ---------------------- | -------- | ------------------------------------------------------ |
| `/api/v3/message/list` | GET      | 此接口非标准分页，需要根据参考消息来查询相邻分页的消息 |

### 参数列表

| 参数名    | 类型         | 必传 | 参数区域 | 说明                                                             |
| --------- | ------------ | ---- | -------- | ---------------------------------------------------------------- |
| target_id | string       | 是   | GET      | 频道 id                                                          |
| msg_id    | string       | 否   | GET      | 参考消息 id，不传则查询最新消息                                  |
| pin       | unsigned int | 否   | GET      | 只能为 0 或者 1，是否查询置顶消息。 置顶消息只支持查询最新的消息 |
| flag      | string       | 否   | GET      | 查询模式，有三种模式可以选择。不传则默认查询最新的消息           |
| page_size | int          | 否   | GET      | 当前分页消息数量, 默认 50                                        |

### 查询模式说明

| 查询模式 |                  详细说明                  |
| :------: | :----------------------------------------: |
|  before  |  查询参考消息之前的消息，不包括参考消息。  |
|  around  | 查询以参考消息为中心，前后一定数量的消息。 |
|  after   |  查询参考消息之后的消息，不包括参考消息。  |

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
        "id": "bac34958-2c73-45c8",
        "type": 1,
        "content": "11111111111111111111111",
        "mention": ["12314**"],
        "mention_all": false,
        "mention_roles": [],
        "mention_here": false,
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
        "attachments": null,
        //文件
        //                "attachments": {
        //                    "type": "file",
        //                    "url": "https://xxx.txt",
        //                    "name": "***.txt",
        //                    "file_type": "text/plain",
        //                    "size": 540579
        //                },
        //视频
        // "attachments": {
        //     "type": "video",
        //     "url": "https://xxxxx.mp4",
        //     "name": "***.mp4",
        //     "duration": 15.472,
        //     "size": 2575670,
        //     "width": 480,
        //     "height": 960
        // },
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
        //引用消息
        //                "quote": {
        //                    "id": "1c4532f6-********-1234-6347f410f91c",
        //                    "type": 1,
        //                    "content": "hello World",
        //                    "create_at": 1628069285358,
        //                    "author": {
        //                        "id": "308****000",
        //                        "username": "盖 伦",
        //                        "identify_num": "**10",
        //                        "online": true,
        //                        "os": "Websocket",
        //                        "status": 1,
        //                        "avatar": "https://***.jpg/icon",
        //                        "vip_avatar": "",
        //                        "nickname": "***11377",
        //                        "roles": [
        //                            102,
        //                            816
        //                        ],
        //                        "is_vip": false,
        //                        "bot": false,
        //                        "mobile_verified": true,
        //                        "joined_at": 1573816459000,
        //                        "active_time": 1628229821490
        //                    }
        //                },
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

## 获取频道聊天消息详情

### 接口说明

| 地址                   | 请求方式 | 说明 |
| ---------------------- | -------- | ---- |
| `/api/v3/message/view` | GET      |      |

### 参数列表

| 参数名 | 类型   | 必传 | 参数区域 | 说明    |
| ------ | ------ | ---- | -------- | ------- |
| msg_id | string | 是   | GET      | 消息 id |

### 返回参数说明

| 参数名 | 类型  | 说明     |
| ------ | ----- | -------- |
| channel_id  | string | 消息所属的频道id |

其余返回值字段参考 [消息详情参数说明](#消息详情参数说明)

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "id": "058a5f2d-329f-******-f2e156148716",
    "type": 9,
    "content": "(met)1780***(met) (met)hell(met) (met)all(met) (rol)702(rol) (rol)711(rol)",
    "mention": ["1780***"],
    "mention_all": true,
    "mention_roles": [],
    "mention_here": false,
    "embeds": [],
    "attachments": null,
    "create_at": 1614922734322,
    "updated_at": 0,
    "reactions": [],
    "author": {
      "id": "1780***",
      "username": "**",
      "identify_num": "5788",
      "online": false,
      "os": "Websocket",
      "status": 1,
      "avatar": "**",
      "vip_avatar": "**",
      "banner": "",
      "nickname": "**",
      "roles": [],
      "is_vip": true,
      "bot": false
    },
    "image_name": "",
    "read_status": false,
    "quote": null,
    "mention_info": {
      "mention_part": [],
      "mention_role_part": []
    }
  }
}
```

## 发送频道聊天消息

### 接口说明

此接口与频道相关接口下的 [发送频道聊天消息](https://developer.kookapp.cn/doc/http/channel#%E5%8F%91%E9%80%81%E9%A2%91%E9%81%93%E8%81%8A%E5%A4%A9%E6%B6%88%E6%81%AF) 功能相同。

**注意：** 强烈建议过滤掉机器人发送的消息，再进行回应。否则会很容易形成两个机器人循环自言自语导致发送量过大，进而导致机器人被封禁。如果确实需要机器人联动的情况，慎重进行处理，防止形成循环。

若发送的消息为诸如图片一类的资源，消息内容必须由机器人创建，否则会提示: "找不到资源"。

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/message/create` | POST     |      |

### 参数列表

| 参数名         | 类型   | 必传 | 参数区域 | 说明                                                                                                                                                                                            |
| -------------- | ------ | ---- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type           | int    | 否   | POST     | 消息类型, 见[type], 不传默认为 `9`, 代表kmarkdown。 `9` 代表 [kmarkdown](https://developer.kookapp.cn/doc/kmarkdown) 消息, `10` 代表[卡片消息](https://developer.kookapp.cn/doc/cardmessage)。 |
| target_id      | string | 是   | POST     | 目标频道 id                                                                                                                                                                                     |
| content        | string | 是   | POST     | 消息内容                                                                                                                                                                                        |
| quote          | string | 否   | POST     | 回复某条消息的 `msgId`                                                                                                                                                                          |
| nonce          | string | 否   | POST     | nonce, 服务端不做处理, 原样返回                                                                                                                                                                 |
| temp_target_id | string | 否   | POST     | 用户 id,如果传了，代表该消息是临时消息，该消息不会存数据库，但是会在频道内只给该用户推送临时消息。用于在频道内针对用户的操作进行单独的回应通知等。                                              |
| template_id| string| 否| POST|模板消息id, 如果使用了，content会作为模板消息的input，参见[模板消息](https://developer.kookapp.cn/doc/http/template)|

### 参数示例

为了演示方便，以下示例仅提供 `type` 与 `content` 字段，其余必须提供的参数仍然需要你自行提供。

普通的文本消息:
```javascript
{
		"type": 9,
		"content":"Hello world"
}
```

一个图片消息:
```javascript
{
		"type": 2,
		"content": "https://img.kookapp.cn/xxxxxxx"
}
```

**注意，发送的图片必须由你的机器人上传，否则将失败，并提示"找不到资源"。此规则对视频消息也适用。**

### 返回参数说明

| 参数名        | 类型   | 说明                       |
| ------------- | ------ | -------------------------- |
| msg_id        | string | 服务端生成的消息 id        |
| msg_timestamp | int    | 消息发送时间(服务器时间戳) |
| nonce         | string | 随机字符串，见参数列表     |

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

目前支持消息 `type `为 `9、10` 的修改，即 KMarkdown 和 CardMessage

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/message/update` | POST     |      |

### 参数列表

| 参数名         | 类型   | 必传 | 参数区域 | 说明                                                                                                    |
| -------------- | ------ | ---- | -------- | ------------------------------------------------------------------------------------------------------- |
| msg_id         | string | 是   | POST     | 消息 id                                                                                                 |
| content        | string | 是   | POST     | 消息内容                                                                                                |
| quote          | string | 否   | POST     | 回复某条消息的 `msgId`。如果为空，则代表删除回复，不传则无影响。                                        |
| temp_target_id | string | 否   | POST     | 用户 id，针对特定用户临时更新消息，必须是正常消息才能更新。与发送临时消息概念不同，但同样不保存数据库。 |
| template_id| string| 否| POST|模板消息id, 如果使用了，content会作为模板消息的input，参见[模板消息](https://developer.kookapp.cn/doc/http/template)|

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

| 参数名 | 类型   | 必传 | 参数区域 | 说明    |
| ------ | ------ | ---- | -------- | ------- |
| msg_id | string | 是   | POST     | 消息 id |

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

| 地址                            | 请求方式 | 说明 |
| ------------------------------- | -------- | ---- |
| `/api/v3/message/reaction-list` | GET      |      |

### 参数列表

| 参数名 | 类型   | 必传 | 参数区域 | 说明                                                                          |
| ------ | ------ | ---- | -------- | ----------------------------------------------------------------------------- |
| msg_id | string | 是   | GET      | 频道消息的 id                                                                 |
| emoji  | string | 是   | GET      | emoji 的 id, 可以为 GuilEmoji 或者 Emoji, 注意：在 get 中，应该进行 urlencode |

### 返回参数说明

返回的是用户的列表，参数如下：

| 参数名        | 类型    | 说明                                                   |
| ------------- | ------- | ------------------------------------------------------ |
| id            | string  | 用户的 id                                              |
| username      | string  | 用户的名称                                             |
| nickname      | string  | 用户在服务器内的呢称                                   |
| identify_num  | string  | 用户名的认证数字，用户名正常为：user_name#identify_num |
| online        | boolean | 当前是否在线                                           |
| status        | int     | 用户的状态, 0 和 1 代表正常，10 代表被封禁             |
| avatar        | string  | 用户的头像的 url 地址                                  |
| bot           | boolean | 用户是否为机器人                                       |
| reaction_time | intval  | 用户点击 reaction 的毫秒时间戳                         |

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

| 地址                           | 请求方式 | 说明 |
| ------------------------------ | -------- | ---- |
| `/api/v3/message/add-reaction` | POST     |      |

### 参数列表

| 参数名 | 类型   | 必传 | 参数区域 | 说明                                     |
| ------ | ------ | ---- | -------- | ---------------------------------------- |
| msg_id | string | 是   | POST     | 频道消息的 id                            |
| emoji  | string | 是   | POST     | emoji 的 id, 可以为 GuilEmoji 或者 Emoji |

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

| 地址                              | 请求方式 | 说明 |
| --------------------------------- | -------- | ---- |
| `/api/v3/message/delete-reaction` | POST     |      |

### 参数列表

| 参数名  | 类型   | 必传 | 参数区域 | 说明                                                                           |
| ------- | ------ | ---- | -------- | ------------------------------------------------------------------------------ |
| msg_id  | string | 是   | POST     | 频道消息的 id                                                                  |
| emoji   | string | 是   | POST     | emoji 的 id, 可以为 GuilEmoji 或者 Emoji                                       |
| user_id | string | 否   | POST     | 用户的 id, 如果不填则为自己的 id。删除别人的 reaction 需要有管理频道消息的权限 |

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

## 发送管道消息

### 接口说明

| 地址                              | 请求方式 | 说明 |
| --------------------------------- | -------- | ---- |
| `/api/v3/message/send-pipemsg` | POST     | 需要在开发者后台先创建管道，并选择是否使用模板等 |

### 参数列表
注：GET参数基本与 [/api/v3/message/create](#发送频道聊天消息) 一致

| 参数名  | 类型   | 必传 | 参数区域 | 说明                                                                           |
| ------- | ------ | ---- | -------- | ------------------------------------------------------------------------------ |
| access_token| string | 是   | GET  |                                                                  |
| type | int| 否  | GET     | 消息发送的类型。如果不填，如果有模板以模板为准，无模板则为kmd                                   |
| target_id| string | 否   | GET     | 频道id。如果不填，则以消息管道的设置为准，如果填了，只允许填与消息管道所填频道相同服务器的文字频道 |

POST区域的使用有些区别：
- 如果使用了模板，整个post区域的内容会作为模板的input的传参，不需要额外写形如`{"content":xxx}`的格式。
- 如果未使用模板，要发的消息需要写成形如`{"content": "hello world"}`的格式 ，其中"hello world"是我们想发的内容 。
- content的格式参见 [/api/v3/message/create](#发送频道聊天消息)
 


### 返回参数说明

无返回参数

### 返回示例

```javascript
{
    "code":0,
     "message":"操作成功",
     "data":{
         "msg_id":"xxxx-xxxx-xxxx-xxxx-xxxx",
          "msg_timestamp":1731486368297,
          "nonce":"",
          "not_permissions_mention":[]
     }
}
```
