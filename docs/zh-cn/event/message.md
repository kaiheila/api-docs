# 消息相关事件列表

### 事件格式说明：请查看 \[[事件结构/格式说明](https://developer.kookapp.cn/doc/event/event-introduction)\]

## 文字消息

#### extra 字段说明

| 字段          | 类型    | 说明                                                                             |
| ------------- | ------- | -------------------------------------------------------------------------------- |
| type          | int     | 同上面 type                                                                      |
| guild_id      | string  | 服务器 id                                                                        |
| channel_name  | string  | 频道名                                                                           |
| mention       | Array   | 提及到的用户 id 的列表                                                           |
| mention_all   | boolean | 是否 mention 所有用户                                                            |
| mention_roles | Array   | mention 用户角色的数组                                                           |
| mention_here  | boolean | 是否 mention 在线用户                                                            |
| author        | Map     | 用户信息, 见[对象-用户 User](https://developer.kookapp.cn/doc/objects#用户User) |

#### 文字消息示例

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

## 图片消息

#### extra 字段说明

| 字段        | 类型   | 说明                                                                             |
| ----------- | ------ | -------------------------------------------------------------------------------- |
| type        | int    | 同上面 type                                                                      |
| code        | string |                                                                                  |
| guild_id    | string | 服务器 id                                                                        |
| attachments | Map    | 附件                                                                             |
| author      | Map    | 用户信息, 见[对象-用户 User](https://developer.kookapp.cn/doc/objects#用户User) |

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

## 视频消息

#### extra 字段说明

| 字段        | 类型   | 说明                                                                             |
| ----------- | ------ | -------------------------------------------------------------------------------- |
| type        | int    | 同上面 type                                                                      |
| code        | string |                                                                                  |
| guild_id    | string | 服务器 id                                                                        |
| attachments | Map    | 附件                                                                             |
| author      | Map    | 用户信息, 见[对象-用户 User](https://developer.kookapp.cn/doc/objects#用户User) |

#### 视频消息示例

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

## 文件消息
文件消息已转为卡片消息，详情请直接参考卡片消息
#### extra 字段说明

| 字段        | 类型   | 说明                                                                             |
| ----------- | ------ | -------------------------------------------------------------------------------- |
| type        | int    | 同上面 type                                                                      |
| code        | string |                                                                                  |
| guild_id    | string | 服务器 id                                                                        |
| attachments | Map    | 附件                                                                             |
| author      | Map    | 用户信息, 见[对象-用户 User](https://developer.kookapp.cn/doc/objects#用户User) |

#### 文件消息示例

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

## KMarkdown 消息

#### extra 字段说明

| 字段          | 类型    | 说明                                                                             |
| ------------- | ------- | -------------------------------------------------------------------------------- |
| type          | int     | 同上面 type                                                                      |
| guild_id      | string  | 服务器 id                                                                        |
| channel_name  | string  | 频道名                                                                           |
| mention       | Array   | 提及到的用户 id 的列表                                                           |
| mention_all   | boolean | 是否 mention 所有用户                                                            |
| mention_roles | Array   | mention 用户角色的数组                                                           |
| mention_here  | boolean | 是否 mention 在线用户                                                            |
| nav_channels  | Array   |                                                                                  |
| code          | string  |                                                                                  |
| author        | Map     | 用户信息, 见[对象-用户 User](https://developer.kookapp.cn/doc/objects#用户User) |
| kmarkdown     | Map     |                                                                                  |

#### KMarkdown 消息示例

```json
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
          "text": "KOOK"
        },
        "nickname": "12316993",
        "roles": [111, 112]
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

## Card 消息

#### extra 字段说明

| 字段          | 类型    | 说明                                                                             |
| ------------- | ------- | -------------------------------------------------------------------------------- |
| type          | int     | 同上面 type                                                                      |
| guild_id      | string  | 服务器 id                                                                        |
| channel_name  | string  | 频道名                                                                           |
| mention       | Array   | 提及到的用户 id 的列表                                                           |
| mention_all   | boolean | 是否 mention 所有用户                                                            |
| mention_roles | Array   | mention 用户角色的数组                                                           |
| mention_here  | boolean | 是否 mention 在线用户                                                            |
| nav_channels  | Array   |                                                                                  |
| code          | string  |                                                                                  |
| author        | Map     | 用户信息, 见[对象-用户 User](https://developer.kookapp.cn/doc/objects#用户User) |

#### Card 消息示例

```json
{
  "s": 0,
  "d": {
    "channel_type": "GROUP",
    "type": 10,
    "target_id": "48818200000000000",
    "author_id": "2418200000",
    // 卡片内容省略
    "content": "",
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
          "text": "KOOK"
        },
        "nickname": "12316993",
        "roles": [111, 112]
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

## 道具 消息

#### content 字段说明

| 字段          | 类型    | 说明                                                                             |
| ------------- | ------- | -------------------------------------------------------------------------------- |
| type          | string  |  枚举string，动作：item                                                                  |
| data          | Array   |      见下    |
#### content-data 字段说明
| 字段          | 类型    | 说明                                                                             |
| ------------- | ------- | -------------------------------------------------------------------------------- |
| user_id        | string  |      发起用户id                                                                |
| target_id      | string  |      目标用户id                                                                |
| item_id        | int     |      动作道具id                                                              |

#### extra 字段说明

| 字段          | 类型    | 说明                                                                             |
| ------------- | ------- | -------------------------------------------------------------------------------- |
| type          | int     | 同上面 type                                                                      |
| mention       | Array   | 提及到的用户 id 的列表                                                           |
| author        | Map     | 用户信息, 见[对象-用户 User](https://developer.kookapp.cn/doc/objects#用户User) |

#### 道具 消息示例

```json
{
  "s": 0,
  "d": {
    "channel_type": "GROUP",
    "type": 12,
    "target_id": "48818200000000000",
    "author_id": "2418200000",
    "content": {
       "type":"item",
       "data":{
          "user_id":"2418200000",
          "target_id":"2418200000",
          "item_id":10001
       }
    },
    "extra": {
      "type": 12,
      "mention": ["2418200000"],
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
          "text": "KOOK"
        },
        "nickname": "12316993",
        "roles": [111, 112]
      },
      "kmarkdown": {
          "mention":["2418200000"],
          "mention_part": [
           {
               "id":"2418200000",
               "username":"tz-un",
               "full_name":"tz-un#5618",
               "avatar":"https://img.kaiheila.cn/avatars/2020-02/xxxx.jpg/icon"
           }],
          // 道具内容省略
          "item_part": []
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
