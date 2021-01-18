# 事件列表及字段说明
当 websocket 或 webhook 收到 `s=0` 的消息时，代表当前收到的消息是事件(包含用户的聊天消息及系统的通知消息等)。本文会具体描述所有的事件类型，并且明确其字段的含义。开发者可以根据本文档做出相应的开发处理。

## 事件基本结构及含义说明

目前所有的消息都会有如下的结构：

```json
{
    s: 0, // 信令类型
    d: [...], //数据
}
```
本文主要讲述的是当 `s=0` 时，data 的数据结构，信令的具体含义参见[信令【暂未开放】](https://developer.kaiheila.cn/protocol).


## 事件主要格式

### 格式说明

| 字段| 类型| 说明|
|--|--|--|
|channel_type| string| 消息频道类型, `GROUP` 为频道消息，其它暂未开放|
|type|int|1:文字消息, 2:图片消息，3:视频消息，4:文件消息， 8:音频消息，9:kmarkdown 消息，255:系统消息, 其它的暂未开放|
|target_id|string|发送目的 id，如果为是 GROUP 消息，则 target_id 代表频道 id|
|author_id|string|发送者 id, 1 代表系统|
|content|string|消息内容, 文件，图片，视频时，content 为 url|
|msg_id|string|消息的 id|
|msg_timestamp|int|消息发送时间的毫秒时间戳|
|nonce|string|随机串，与用户消息发送 api 中传的 nonce 保持一致|
|extra|mixed|不同的消息类型，结构不一致|

#### 文字频道消息 extra说明

| 字段| 类型| 说明|
|--|--|--|
|type|string|同上面 type|
|guild_id|string|服务器 id|
|channel_name|string|频道名|
|mention|Array|提及到的用户 id 的列表|
|mention_all|boolean|是否 mention 所有用户|
|mention_roles|Array|mention 用户角色的数组|
|mention_here|boolean|是否 mention 在线用户|
|author|Map|用户信息, 见下|

**author 对象说明**

| 字段| 类型| 说明|
|--|--|--|
|id|string|用户 id|
|username|string|用户名|
|nickname|string|用户在当前服务器的昵称|
|identify_num|string|用户名 `#` 后的 4 位识别 id|
|online|bool|用户在线状态|
|avatar|string|头像图片地址|
|roles|Array|用户在当前服务器中的角色 id 组成的列表|
|bot|bool|是否是机器人|

### 格式示例

#### 系统消息示例

```json
{
    "s": 0,
    "d": {
        "channel_type": "GROUP",
        "type": 255,
        "target_id": "xxxxx",
        "author_id": "1",
        "content": "[系统消息]",
        "msg_id": "67637d4c-xxxx-xxxx-xxxx-xxxxx",
        "msg_timestamp": 1607674307956,
        "nonce": "",
        "extra": {
            "type": "joined_guild",
            "body": {
                "id": "xxxxx",
                "username": "xxxxx",
                "identify_num": "xxx",
                "online": true,
                "os": "Websocket",
                "status": 1,
                "avatar": "https://img.kaiheila.cn/avatars/2020-04/A2kq6iF1hc1hc.jpg/icon",
                "mobile_verified": true,
                "nickname": "xxxxx",
                "roles": [],
                "joined_at": 1607674307000,
                "active_time": 1607674307582
            }
        }
    },
    "sn": 2156
}
```

#### 文本消息示例

```json
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
            "type": "1",
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

#### 图片消息示例

```json
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
            "type": "2",
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

#### 视频消息

```json
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
            "type": "3",
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

#### 文件消息

```json
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
            "type": "4",
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
