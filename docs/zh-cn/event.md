# 事件列表及字段说明
当 websocket 或 webhook 收到 `s=0` 的消息时，代表当前收到的消息是事件(包含用户的聊天消息及系统的通知消息等)。本文会具体描述所有的事件类型，并且明确其字段的含义。开发者可以根据本文档做出相应的开发处理。

## 事件基本结构及含义说明

目前所有的消息都会有如下的结构：

```javascript
{
    s: 0, // 信令类型
    d: [...], //数据
}
```
本文主要讲述的是当 `s=0` 时，data 的数据结构，信令的具体含义参见[websocket](https://developer.kaiheila.cn/doc/websocket).


## 事件主要格式

### 格式说明

| 字段| 类型| 说明|
|---|---|---|
|channel_type| string| 消息频道类型, `GROUP` 为频道消息|
|type|int|1:文字消息, 2:图片消息，3:视频消息，4:文件消息， 8:音频消息，9:KMarkdown，10:card消息，255:系统消息, 其它的暂未开放|
|target_id|string|发送目的 id，如果为是 GROUP 消息，则 target_id 代表频道 id|
|author_id|string|发送者 id, 1 代表系统|
|content|string|消息内容, 文件，图片，视频时，content 为 url|
|msg_id|string|消息的 id|
|msg_timestamp|int|消息发送时间的毫秒时间戳|
|nonce|string|随机串，与用户消息发送 api 中传的 nonce 保持一致|
|extra|mixed|不同的消息类型，结构不一致|

### 文字频道消息extra说明

**当type非系统消息(255)时**

| 字段| 类型| 说明|
|---|---|---|
|type|int|同上面 type|
|guild_id|string|服务器 id|
|channel_name|string|频道名|
|mention|Array|提及到的用户 id 的列表|
|mention_all|boolean|是否 mention 所有用户|
|mention_roles|Array|mention 用户角色的数组|
|mention_here|boolean|是否 mention 在线用户|
|author|Map|用户信息, 见[对象-用户User](https://developer.kaiheila.cn/doc/objects#用户User)|

### 系统事件消息extra说明

**当type为系统消息(255)时**

| 字段| 类型| 说明|
|---|---|---|
|type|string|标识该事件的类型|
|body|Map|该事件关联的具体数据, 详见各系统消息事件示例|


## 文字频道消息格式示例

### 文本消息示例

```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 1,
        "target_id": "xxxxxx",
        "author_id": "xxxxx",
        "content": "dddd",
        "msg_id": "67637d4c-xxxx-xxxx-xxxx-xxxxx",
        "msg_timestamp": 1607674740160,
        "nonce": "",
        "extra": {
            "type": 1,
            "guild_id": "xxxxx",
            "channel_name": "文字频道",
            "mention": [],
            "mention_all": false,
            "mention_roles": [],
            "mention_here": false,
            "code": "",
            "author": {
                "identify_num": "xxxxx",
                "avatar": "https://img.kaiheila.cn/avatars/2020-11/r0j9.jpg/icon",
                "username": "xxxxx",
                "id": "xxxxx",
                "nickname": "xxxxx",
                "roles": []
            }
        }
    },
    "sn": 2199
}
```


### 图片消息示例

```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 2,
        "target_id": "xxxxx",
        "author_id": "xxxxx",
        "content": "https://img.kaiheila.cn/assets/2020-12/asasd.jpg",
        "msg_id": "67637d4c-xxxx-xxxx-xxxx-xxxxx",
        "msg_timestamp": 1607678646991,
        "nonce": "",
        "extra": {
            "type": 2,
            "code": "",
            "guild_id": "xxxxx",
            "attachments": {
                "type": "image",
                "name": "xxxx.jpg",
                "url": "https://img.kaiheila.cn/assets/2020-12/IHT5x5oSLA07o03m.jpg"
            },
            "author": {
                "identify_num": "xxxxx",
                "avatar": "https://img.kaiheila.cn/avatars/2020-11/r26z1e70f20j9.jpg/icon",
                "username": "xxxxx",
                "id": "xxxxx",
                "nickname": "xxxxx",
                "roles": []
            }
        }
    },
    "sn": 2499
}
```


### 视频消息

```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 3,
        "target_id": "xxxxx",
        "author_id": "xxxxx",
        "content": "https://img.kaiheila.cn/attachments/2020-12/11/asd.mp4",
        "msg_id": "67637d4c-xxxx-xxxx-xxxx-xxxxx",
        "msg_timestamp": 1607679613599,
        "nonce": "",
        "extra": {
            "type": 3,
            "guild_id": "xxxx",
            "code": "",
            "attachments": {
                "type": "video",
                "url": "https://img.kaiheila.cn/attachments/2020-12/11/asd.mp4",
                "name": "002iQMhagx07Fx0S41200323o0E010.mp4",
                "file_type": "video/mp4",
                "size": 722882,
                "duration": 15.673,
                "width": 360,
                "height": 635
            },
            "author": {
                "identify_num": "xxxxx",
                "avatar": "https://img.kaiheila.cn/avatars/2020-11/r20f20j9.jpg/icon",
                "username": "xxxxx",
                "id": "xxxxx",
                "nickname": "xxxxx",
                "roles": []
            }
        }
    },
    "sn": 2582
}
```


### 文件消息

```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 4,
        "target_id": "xxxx",
        "author_id": "xxxx",
        "content": "https://img.kaiheila.cn/attachments/2020-12/11/asd.txt",
        "msg_id": "67637d4c-xxxx-xxxx-xxxx-xxxxx",
        "msg_timestamp": 1607679683305,
        "nonce": "",
        "extra": {
            "type": 4,
            "guild_id": "xxxx",
            "code": "",
            "attachments": {
                "type": "file",
                "url": "https://img.kaiheila.cn/attachments/2020-12/11/asd.txt",
                "name": "voice-message.txt",
                "file_type": "text/plain",
                "size": 7320
            },
            "author": {
                "identify_num": "xxxx",
                "avatar": "https://img.kaiheila.cn/avatars/2020-11/asd.jpg/icon",
                "username": "xxxx",
                "id": "xxxx",
                "nickname": "xxxx",
                "roles": []
            }
        }
    },
    "sn": 2587
}
```


### KMarkdown 消息示例

```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 9,
        "target_id": "48818200000000000",
        "author_id": "2418200000",
        "content": "*Hello World*",
        "extra": {
            "type": 9,
            "guild_id": "6016389914000000",
            "channel_name": "123123",
            "mention": [],
            "mention_all": false,
            "mention_roles": [],
            "mention_here": false,
            "nav_channels": [],
            "code": "",
            "author": {
                "id": "2418200000",
                "username": "tz-un",
                "identify_num": "5618",
                "online": false,
                "os": "Websocket",
                "status": 1,
                "avatar": "https://img.kaiheila.cn/avatars/2020-02/xxxx.jpg/icon",
                "tag_info": {
                    "color": "#6666CC",
                    "text": "开黑啦"
                },
                "nickname": "12316993",
                "roles": [
                    111,
                    112
                ]
            },
            "kmarkdown": {
                "raw_content": "Hello World",
                "mention_part": [],
                "mention_role_part": []
            }
        },
        "msg_id": "789c0b23-xxxx-f7ae1a946f11",
        "msg_timestamp": 1613996877757,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 181
}
```


### Card 消息示例

```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 10,
        "target_id": "48818200000000000",
        "author_id": "2418200000",
        "content": "[{\"theme\":\"secondary\",\"color\":\"\",\"size\":\"lg\",\"modules\":[{\"type\":\"section\",\"mode\":\"left\",\"accessory\":null,\"text\":{\"type\":\"plain-text\",\"emoji\":true,\"content\":\"\\u5f00\\u9ed1\\u5566\\uff1a\\u4e13\\u5c5e\\u6e38\\u620f\\u73a9\\u5bb6\\u7684\\u6587\\u5b57\\u3001\\u8bed\\u97f3\\u4e0e\\u7ec4\\u961f\\u5de5\\u5177\\u3002\",\"elements\":[]},\"elements\":[]}],\"type\":\"card\"}]",
        "extra": {
            "type": 10,
            "guild_id": "6016389910000000",
            "channel_name": "文字频道",
            "mention": [],
            "mention_all": false,
            "mention_roles": [],
            "mention_here": false,
            "nav_channels": [],
            "code": "",
            "author": {
                "id": "2418200000",
                "username": "tz-un",
                "identify_num": "5618",
                "online": false,
                "os": "Websocket",
                "status": 1,
                "avatar": "https://img.kaiheila.cn/avatars/2020-02/xxxx.jpg/icon",
                "tag_info": {
                    "color": "#6666CC",
                    "text": "开黑啦"
                },
                "nickname": "12316993",
                "roles": [
                    111,
                    112
                ]
            },
            "kmarkdown": {
                "raw_content": "",
                "mention_part": [],
                "mention_role_part": []
            }
        },
        "msg_id": "553f1f78-xxxxx-39c65d9c5584",
        "msg_timestamp": 1613996743849,
        "nonce": "",
        "verify_token": "xxxxx"
    },
    "sn": 180
}
```


## 系统事件消息示例


### 事件：Card消息中的Button点击事件

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为message_btn_click|
|body|Map| |
|↳msg_id|string|用户点击的消息id|
|↳user_id|string|点击的用户|
|↳value|string|return-val的值|
|↳target_id|string|消息发送的目标id,频道消息为频道|

示例：
```javascript
{
    "s":0,
    "sn":1,
    "d":{
        "type":255,
        "channel_type":"PERSON",
        "target_id":"xxxx",
        "author_id":"xxxx",
        "content":"xxxx",
        "msg_id":"xxxx",
        "msg_timestamp":1611559482954,
        "nonce":"",
        "extra":{
            "type":"message_btn_click",
            "body":{
                "value": "123",
                "msg_id": "xxx",
                "user_id": "xxx",
                "target_id" : ""
            }
        }
    }
}
```


### 事件：频道内用户添加 reaction

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `added_reaction`|
|body|Map| |
|↳msg_id|string|用户点击的消息id|
|↳user_id|string|点击的用户|
|↳channel_id|string|频道id|
|↳emoji|Map|消息对象, 包含 `id` 表情id, `name` 表情名称|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "60163800000000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "added_reaction",
            "body": {
                "channel_id": "5823400000000",
                "emoji": {
                    "id": "[#128226;]",
                    "name": "[#128226;]"
                },
                "user_id": "2418000000",
                "msg_id": "59def270-xxxx-xxxx-xxxx-8db935e054a1"
            }
        },
        "msg_id": "xxxx-xxxx-xxxx",
        "msg_timestamp": 1612703779612,
        "nonce": "",
        "verify_token": "xxxx"
    },
    "sn": 1
}
```


### 事件：频道内用户取消 reaction

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `deleted_reaction`|
|body|Map| |
|↳msg_id|string|用户点击的消息id|
|↳user_id|string|点击的用户|
|↳channel_id|string|频道id|
|↳emoji|Map|消息对象, 包含 `id` 表情id, `name` 表情名称|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "60163800000000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "deleted_reaction",
            "body": {
                "channel_id": "5823400000000",
                "emoji": {
                    "id": "[#128226;]",
                    "name": "[#128226;]"
                },
                "user_id": "2418000000",
                "msg_id": "59def270-xxxx-xxxx-xxxx-8db935e054a1"
            }
        },
        "msg_id": "abd87680-xxxx-xxxx-xxxx-a56107a48e12",
        "msg_timestamp": 1612703776899,
        "nonce": "",
        "verify_token": "xxxx"
    },
    "sn": 1
}
```


### 事件：消息更新

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `updated_message`|
|body|Map| |
|↳msg_id|string|被更新的消息的id|
|↳content|string|更新后的文本|
|↳channel_id|string|频道id|
|↳mention|array|提及的用户id组成的列表|
|↳mention_all|boolean|是否提及 `全体成员`|
|↳mention_here|boolean|是否提及 `在线成员`|
|↳mention_roles|array|提及的角色id组成的列表|
|↳updated_at|int|更新时间戳(毫秒)|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "60163899100000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "updated_message",
            "body": {
                "channel_id": "5823470000000",
                "content": "1aaaaaa",
                "mention": [],
                "mention_all": false,
                "mention_here": false,
                "mention_roles": [],
                "updated_at": 1612703810779,
                "msg_id": "59def270-xxx-8db935e054a1"
            }
        },
        "msg_id": "cc523bf1-xxx-88c31ebc9fba",
        "msg_timestamp": 1612703810791,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 3
}
```


### 事件：消息被删除

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `deleted_message`|
|body|Map| |
|↳msg_id|string|被更新的消息的id|
|↳channel_id|string|频道id|

示例：
```javascript
{
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "60163000000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "deleted_message",
            "body": {
                "channel_id": "58234000000",
                "msg_id": "59def270-xxxx-8db935e054a1"
            }
        },
        "msg_id": "63d6a934-xxxx-a1f02c255213",
        "msg_timestamp": 1612704007683,
        "nonce": "",
        "verify_token": "xxx"
    },
    "s": 0,
    "sn": 5
}
```


### 事件：服务器信息更新

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `updated_guild`|
|body|Map| |
|↳id|string|服务器id|
|↳name|string|服务器名称|
|↳user_id|string|服务器主id|
|↳icon|string|服务器logo图片地址|
|↳notify_type|int|通知类型 `1`接受所有通知 `2`仅接收被提及消息 `3`不接收通知 |
|↳region|string|服务器所在区域|
|↳enable_open|int|是否为公开服务器, 1 or 0|
|↳open_id|int|公开服务器id|
|↳default_channel_id|string|默认文字频道id|
|↳welcome_channel_id|string|欢迎频道id|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "601630000000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "updated_guild",
            "body": {
                "id": "601630000000",
                "name": "test111",
                "user_id": "2418xxx",
                "icon": "https://xxx/icons/2020-05/YQyfHxxx.png/icon",
                "notify_type": 1,
                "region": "shanghai",
                "enable_open": 1,
                "open_id": 1123123123,
                "default_channel_id": "4881800000000",
                "welcome_channel_id": "4881800000000"
            }
        },
        "msg_id": "0108feaf-xxx-7d70145468f0",
        "msg_timestamp": 1612764956322,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 9
}
```


### 事件：服务器删除

extra字段说明：

|字段|类型|说明|
|--|--|--|
|type|string|消息的类型，本处为 `deleted_guild`|
|body|Map| |
|↳id|string|服务器id|
|↳name|string|服务器名称|
|↳user_id|string|服务器主id|
|↳icon|string|服务器logo图片地址|
|↳notify_type|int|通知类型 `1`接受所有通知 `2`仅接收被提及消息 `3`不接收通知 |
|↳region|string|服务器所在区域|
|↳enable_open|int|是否为公开服务器, 1 or 0|
|↳open_id|int|公开服务器id|
|↳default_channel_id|string|默认文字频道id|
|↳welcome_channel_id|string|欢迎频道id|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "xxx",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "deleted_guild",
            "body": {
                "id": "xxx",
                "name": "testDel",
                "user_id": "2418200000",
                "icon": "",
                "notify_type": 2,
                "region": "beijing",
                "enable_open": 0,
                "open_id": 0,
                "default_channel_id": "xxxx",
                "welcome_channel_id": "0"
            }
        },
        "msg_id": "3d2bdb08-xxxx-faa2b9e77394",
        "msg_timestamp": 1614086485182,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 210
}
```


### 事件：新成员加入服务器

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `joined_guild`|
|body|Map| |
|↳user_id|string|用户id|
|↳joined_at|int|加入服务器的时间|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "60163000000000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "joined_guild",
            "body": {
                "user_id": "3891000000",
                "joined_at": 1612774315000
            }
        },
        "msg_id": "bcc9abbd-xxxx-61c6a976be5d",
        "msg_timestamp": 1612774315732,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 15
}
```


### 事件：服务器成员退出

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `exited_guild`|
|body|Map| |
|↳user_id|string|用户id|
|↳exited_at|int|退出服务器的事件|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "60163000000000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "exited_guild",
            "body": {
                "user_id": "3891000000",
                "exited_at": 1612774287628
            }
        },
        "msg_id": "ecec53c4-xxxx-16226c48487b",
        "msg_timestamp": 1612774287636,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 14
}
```


### 事件：服务器成员信息更新

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `updated_guild_member`|
|body|Map| |
|↳user_id|string|用户id|
|↳nickname|string|昵称|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "60163000000000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "updated_guild_member",
            "body": {
                "user_id": "3891600000",
                "nickname": "new_nick"
            }
        },
        "msg_id": "d22ae13c-xxxxxx-71f8398e16b5",
        "msg_timestamp": 1612774472181,
        "nonce": "",
        "verify_token": "xxxxx"
    },
    "sn": 17
}
```


### 事件：新增频道

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `added_channel`|
|body|Map| 参考[对象-频道 Channel](https://developer.kaiheila.cn/doc/objects#频道Channel) |

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "6016389000000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "added_channel",
            "body": {
                "id": "53002000000000",
                "name": "新的频道",
                "user_id": "2418239356",
                "guild_id": "6016389000000",
                "is_category": 0,
                "parent_id": "6016400000000000",
                "level": null,
                "slow_mode": 0,
                "topic": "新的频道的说明",
                "type": 1,
                "permission_overwrites": [
                    {
                        "role_id": 0,
                        "allow": 0,
                        "deny": 0
                    }
                ],
                "permission_users": [],
                "permission_sync": 1
            }
        },
        "msg_id": "70b60e52-xxx-4e8d0a995b1a",
        "msg_timestamp": 1612776265417,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 21
}
```


### 事件：修改频道信息

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `updated_channel`|
|body|Map| 参考[对象-频道Channel](https://developer.kaiheila.cn/doc/objects#频道Channel) |

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "6016389000000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
        "type": "updated_channel",
        "body": {
            "id": "53002000000000",
            "name": "更新后的频道",
            "user_id": "2418239356",
            "guild_id": "6016389000000",
            "is_category": 0,
            "parent_id": "6016400000000000",
            "level": null,
            "slow_mode": 0,
            "topic": "更新后的频道的说明",
            "type": 1,
            "permission_overwrites": [
                {
                    "role_id": 0,
                    "allow": 0,
                    "deny": 0
                }
            ],
            "permission_users": [],
            "permission_sync": 1
            }
        },
        "msg_id": "70b60e52-xxx-4e8d0a995b1a",
        "msg_timestamp": 1612776265417,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 21
}
```


### 事件：删除频道

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `deleted_channel`|
|body|Map|  |
|↳id|string|被删掉的频道id|
|↳deleted_at|string|删除时间(毫秒)|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "60163899100000000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "deleted_channel",
            "body": {
                "id": "69972200000000",
                "deleted_at": 1612777405595
            }
        },
        "msg_id": "3968a7e3-xxxx-0c8bac275fb4",
        "msg_timestamp": 1612777238358,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 24
}
```


### 事件：私聊消息更新

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `updated_private_message`|
|body|Map| |
|↳msg_id|string|被更新的消息的id|
|↳author_id|string|被更新的消息的创建者id|
|↳target_id|string|被更新的消息的目标用户id|
|↳content|string|更新后的文本|
|↳chat_code|string|私聊code|
|↳updated_at|int|更新时间戳(毫秒)|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "PERSON",
        "type": 255,
        "target_id": "2862900000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "updated_private_message",
            "body": {
                "author_id": "2862900000",
                "target_id": "2862900000",
                "msg_id": "93262503-xxxx-0d814f7b416a",
                "content": "asdaaad",
                "updated_at": 1612778254183,
                "chat_code": "xxxxxxxxxxxxxxxxx"
            }
        },
        "msg_id": "8cb11d28-xxxxx-5700aa4c1b58",
        "msg_timestamp": 1612778254192,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 32
}
```


### 事件：私聊消息被删除

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `deleted_private_message`|
|body|Map| |
|↳msg_id|string|被删除的消息的id|
|↳author_id|string|被删除的消息的创建者id|
|↳target_id|string|被删除的消息的目标用户id|
|↳chat_code|string|私聊code|
|↳deleted_at|int|删除的时间戳(毫秒)|

示例：
```javascript
{
    "d": {
        "channel_type": "PERSON",
        "type": 255,
        "target_id": "2862900000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "deleted_private_message",
            "body": {
                "chat_code": "3b4aa448b8e8b9c87a1b3770792e7433",
                "msg_id": "44874c6f-xxxx-f987b77f0c25",
                "author_id": "2862900000",
                "target_id": "2862900000",
                "deleted_at": 1612778754838
            }
        },
        "msg_id": "93b59c53-xxxx-546964356eac",
        "msg_timestamp": 1612778754846,
        "nonce": "",
        "verify_token": "xxx"
    },
    "s": 0,
    "sn": 35
}
```


### 事件：私聊内用户添加 reaction

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `private_added_reaction`|
|body|Map| |
|↳msg_id|string|用户点击的消息id|
|↳user_id|string|点击的用户的id|
|↳chat_code|string|私聊code|
|↳emoji|Map|消息对象, 包含 `id` 表情id, `name` 表情名称|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "PERSON",
        "type": 255,
        "target_id": "2862900000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "private_added_reaction",
            "body": {
                "emoji": {
                    "id": "[#128512;]",
                    "name": "[#128512;]"
                },
                "user_id": "2418200000",
                "chat_code": "3b4aa448b8e8b9c87a1xxxxx",
                "msg_id": "024f7bc7-xxxx-1de632f19512"
            }
        },
        "msg_id": "abaccacb-xxxx-5f6d1f72c29a",
        "msg_timestamp": 1612779382613,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 39
}
```


### 事件：私聊内用户取消 reaction

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `private_deleted_reaction`|
|body|Map| |
|↳msg_id|string|用户点击的消息id|
|↳user_id|string|点击的用户的id|
|↳chat_code|string|私聊code|
|↳emoji|Map|消息对象, 包含 `id` 表情id, `name` 表情名称|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "PERSON",
        "type": 255,
        "target_id": "2862900000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "private_deleted_reaction",
            "body": {
                "emoji": {
                    "id": "[#128578;]",
                    "name": "[#128578;]"
                },
                "user_id": "2418200000",
                "chat_code": "3b4aa448b8e8b9c8xxxx",
                "msg_id": "024f7bc7-xxxx-1de632f19512"
            }
        },
        "msg_id": "e4bad0e6-xxxx-9dc6a0a5dbbf",
        "msg_timestamp": 1612779051034,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 38
}
```


### 事件：用户加入语音频道

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `joined_channel`|
|body|Map| |
|↳user_id|string|用户id|
|↳channel_id|string|加入的频道id|
|↳joined_at|int|加入时间|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "6016389910000000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "joined_channel",
            "body": {
                "user_id": "2418200000",
                "channel_id": "9219038000000",
                "joined_at": 1612790368279
            }
        },
        "msg_id": "30a7f591-xxxx-322f35105524",
        "msg_timestamp": 1612790368279,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 42
}
```


### 事件：用户退出语音频道

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `exited_channel`|
|body|Map| |
|↳user_id|string|用户id|
|↳channel_id|string|加入的频道id|
|↳exited_at|int|退出时间|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "6016389910000000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "exited_channel",
            "body": {
                "user_id": "2418200000",
                "channel_id": "9219038000000",
                "exited_at": 1612790411267
            }
        },
        "msg_id": "386e533c-xxxxx-7ee2bded364e",
        "msg_timestamp": 1612790411274,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 43
}
```


### 事件：服务器成员上线

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `guild_member_online`|
|body|Map| |
|↳user_id|string|用户id|
|↳event_time|int|事件发生的时间|
|↳guilds|array|服务器id组成的数组, 代表与该用户所在的共同的服务器|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "PERSON",
        "type": 255,
        "target_id": "2862900000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "guild_member_online",
            "body": {
                "user_id": "2418200000",
                "event_time": 1612930480315,
                "guilds": [
                    "601638990000000"
                ]
            }
        },
        "msg_id": "35f19bd2-xxxx-3eef019abb84",
        "msg_timestamp": 1612930480347,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 72
}
```


### 事件：服务器成员下线

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `guild_member_offline`|
|body|Map| |
|↳user_id|string|用户id|
|↳event_time|int|事件发生的时间|
|↳guilds|array|服务器id组成的数组, 代表与该用户所在的共同的服务器|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "PERSON",
        "type": 255,
        "target_id": "2862900000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "guild_member_offline",
            "body": {
                "user_id": "2418200000",
                "event_time": 1612938960033,
                "guilds": [
                    "601638990000000"
                ]
            }
        },
        "msg_id": "35f19bd2-xxxx-3eef019abb84",
        "msg_timestamp": 1612938960033,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 74
}
```


### 事件：服务器封禁用户

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `added_block_list`|
|body|Map| |
|↳operator_id|string|操作人id|
|↳remark|string|封禁理由|
|↳user_id|Array|被封禁成员id列表|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "xxxx",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "added_block_list",
            "body": {
                "operator_id": "xxxx",
                "remark": "频繁发广告",
                "user_id": [
                    "3751918xx",
                    "xxxxxxxxx"
                ]
            }
        },
        "msg_id": "6dfaf089-xxxxx-63e8d55602d4",
        "msg_timestamp": 1613997198323,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 183
}
```


### 事件：服务器取消封禁用户

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `deleted_block_list`|
|body|Map| |
|↳operator_id|string|操作人id|
|↳user_id|Array|被封禁成员id列表|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "xxxx",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "deleted_block_list",
            "body": {
                "operator_id": "xxx",
                "user_id": [
                    "3751918xx",
                ]
            }
        },
        "msg_id": "14230d28-xxxx-b84609119e01",
        "msg_timestamp": 1613997311786,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 184
}
```


### 事件：服务器角色增加

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `added_role`|
|body|Map| 参考[对象-角色Role](https://developer.kaiheila.cn/doc/objects#角色Role) |

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "xxx",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "added_role",
            "body": {
                "role_id": 11111,
                "name": "新角色",
                "color": 0,
                "position": 5,
                "hoist": 0,
                "mentionable": 0,
                "permissions": 142924296
            }
        },
        "msg_id": "c804a6a6-xxxx-e041ec3bb887",
        "msg_timestamp": 1613998615411,
        "nonce": "",
        "verify_token": "xxxx"
    },
    "sn": 186
}
```


### 事件：服务器角色删除

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `deleted_role`|
|body|Map| 参考[对象-角色Role](https://developer.kaiheila.cn/doc/objects#角色Role) |

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "xxx",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "deleted_role",
            "body": {
                "role_id": 11111,
                "name": "新角色",
                "color": 0,
                "position": 5,
                "hoist": 0,
                "mentionable": 0,
                "permissions": 142924296
            }
        },
        "msg_id": "61f1dc5a-xxxx-47776deacd0c",
        "msg_timestamp": 1614054458292,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 192
}
```


### 事件：服务器角色更新


extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `updated_role`|
|body|Map| 参考[对象-角色Role](https://developer.kaiheila.cn/doc/objects#角色Role) |

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "xxx",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "updated_role",
            "body": {
                "role_id": 599,
                "name": "新角色xxx",
                "color": 0,
                "position": 6,
                "hoist": 0,
                "mentionable": 0,
                "permissions": 142924316
            }
        },
        "msg_id": "a1071327-xxxx-8fec42ae74bd",
        "msg_timestamp": 1614054560619,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 194
}
```


### 事件：新的频道置顶消息


extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `pinned_message`|
|body|Map| |
|↳channel_id|string|频道id|
|↳operator_id|string|操作人id|
|↳msg_id|string|被置顶的消息id|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "xxx",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "pinned_message",
            "body": {
                "channel_id": "xxxx",
                "operator_id": "2418200000",
                "msg_id": "4d5ef7ae-xxxx-b03e57cdf2e9"
            }
        },
        "msg_id": "d2bad9e9-xxxx-265f74dc35bb",
        "msg_timestamp": 1614054656178,
        "nonce": "",
        "verify_token": "xxxx"
    },
    "sn": 196
}
```


### 事件：取消频道置顶消息


extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `unpinned_message`|
|body|Map| |
|↳channel_id|string|频道id|
|↳operator_id|string|操作人id|
|↳msg_id|string|被取消置顶的消息id|

示例：
```javascript
{
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "xxx",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "unpinned_message",
            "body": {
                "channel_id": "xxxxx",
                "operator_id": "2418200000",
                "msg_id": "4d5ef7ae-xxxx-b03e57cdf2e9"
            }
        },
        "msg_id": "9b269469-xxxx-9e526ea8f7f0",
        "msg_timestamp": 1614054894618,
        "nonce": "",
        "verify_token": "xxxx"
    },
    "s": 0,
    "sn": 197
}
```


### 事件：用户信息更新

**该事件与服务器无关, 遵循以下条件**

1. 仅当用户的 **用户名** 或 **头像** 变更时;
2. 仅通知与该用户存在关联的用户或Bot:
a. 存在聊天会话
b. 双方好友关系

extra字段说明：

|字段|类型|说明|
|---|---|---|
|type|string|消息的类型，本处为 `user_updated`|
|body|Map| |
|↳user_id|string|用户id|
|↳username|string|用户名|
|↳avatar|string|头像图片地址|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "PERSON",
        "type": 255,
        "target_id": "2862900000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "user_updated",
            "body": {
                "user_id": "2418200000",
                "username": "ThisIsANewUsername",
                "avatar": "https://img.kaiheila.cn/avatars/2020-02/xxxx.jpg/icon"
            }
        },
        "msg_id": "02106a94-xxxx-d60f660485dd",
        "msg_timestamp": 1614055075487,
        "nonce": "",
        "verify_token": "xxxx"
    },
    "sn": 199
}
```


### 事件：自己新加入服务器

> 当自己被邀请或主动加入新的服务器时, 产生该事件

extra字段说明：

|字段|类型|说明|
|--|--|--|
|type|string|消息的类型，本处为 `self_joined_guild`|
|body|Map| |
|↳guild_id|string|服务器id|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "PERSON",
        "type": 255,
        "target_id": "2862900000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "self_joined_guild",
            "body": {
                "guild_id": "xxx"
            }
        },
        "msg_id": "238063ab-xxxx-cd90c3cfb92f",
        "msg_timestamp": 1614140348008,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 214
}
```


### 事件：自己退出服务器

> 当自己被踢出服务器或被拉黑或主动退出服务器时, 产生该事件

extra字段说明：

|字段|类型|说明|
|--|--|--|
|type|string|消息的类型，本处为 `self_exited_guild`|
|body|Map| |
|↳guild_id|string|服务器id|

示例：
```javascript
{
    "s": 0,
    "d": {
        "channel_type": "PERSON",
        "type": 255,
        "target_id": "2862900000",
        "author_id": "1",
        "content": "[系统消息]",
        "extra": {
            "type": "self_exited_guild",
            "body": {
                "guild_id": "xxx"
            }
        },
        "msg_id": "xxxx",
        "msg_timestamp": 1614140348008,
        "nonce": "",
        "verify_token": "xxx"
    },
    "sn": 215
}
```