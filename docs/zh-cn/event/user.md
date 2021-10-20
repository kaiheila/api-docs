# 用户相关事件列表

### 事件格式说明：请查看 \[[事件结构/格式说明]\]( https://developer.kaiheila.cn/doc/event/event-introduction )

## 用户加入语音频道

#### extra 字段说明:

| 字段         | 类型   | 说明                                |
| ------------ | ------ | ----------------------------------- |
| type         | string | 消息的类型，本处为 `joined_channel` |
| body         | Map    |                                     |
| » user_id    | string | 用户 id                             |
| » channel_id | string | 加入的频道 id                       |
| » joined_at  | int    | 加入时间                            |

#### 示例：

```json
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

## 用户退出语音频道

#### extra 字段说明:

| 字段         | 类型   | 说明                                |
| ------------ | ------ | ----------------------------------- |
| type         | string | 消息的类型，本处为 `exited_channel` |
| body         | Map    |                                     |
| » user_id    | string | 用户 id                             |
| » channel_id | string | 加入的频道 id                       |
| » exited_at  | int    | 退出时间                            |

#### 示例：

```json
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

## 用户信息更新

**该事件与服务器无关, 遵循以下条件**

1. 仅当用户的 **用户名** 或 **头像** 变更时;
2. 仅通知与该用户存在关联的用户或 Bot:
   a. 存在聊天会话
   b. 双方好友关系

#### extra 字段说明:

| 字段       | 类型   | 说明                              |
| ---------- | ------ | --------------------------------- |
| type       | string | 消息的类型，本处为 `user_updated` |
| body       | Map    |                                   |
| » user_id  | string | 用户 id                           |
| » username | string | 用户名                            |
| » avatar   | string | 头像图片地址                      |

#### 示例：

```json
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

###

## 自己新加入服务器

**_当自己被邀请或主动加入新的服务器时, 产生该事件_**

#### extra 字段说明:

| 字段       | 类型   | 说明                                   |
| ---------- | ------ | -------------------------------------- |
| type       | string | 消息的类型，本处为 `self_joined_guild` |
| body       | Map    |                                        |
| » guild_id | string | 服务器 id                              |

#### 示例：

```json
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

## 自己退出服务器

**_当自己被踢出服务器或被拉黑或主动退出服务器时, 产生该事件_**

#### extra 字段说明:

| 字段       | 类型   | 说明                                   |
| ---------- | ------ | -------------------------------------- |
| type       | string | 消息的类型，本处为 `self_exited_guild` |
| body       | Map    |                                        |
| » guild_id | string | 服务器 id                              |

#### 示例：

```json
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

## Card 消息中的 Button 点击事件

#### extra 字段说明:

| 字段        | 类型   | 说明                                 |
| ----------- | ------ | ------------------------------------ |
| type        | string | 消息的类型，本处为 message_btn_click |
| body        | Map    |                                      |
| » msg_id    | string | 用户点击的消息 id                    |
| » user_id   | string | 点击的用户                           |
| » value     | string | return-val 的值                      |
| » target_id | string | 消息发送的目标 id,频道消息为频道     |
| » user_info | Map    | 用户信息，同 User Object             |

#### 示例：

```json
{
  "s": 0,
  "sn": 1,
  "d": {
    "type": 255,
    "channel_type": "PERSON",
    "target_id": "xxxx",
    "author_id": "xxxx",
    "content": "xxxx",
    "msg_id": "xxxx",
    "msg_timestamp": 1611559482954,
    "nonce": "",
    "extra": {
      "type": "message_btn_click",
      "body": {
        "value": "123",
        "msg_id": "xxx",
        "user_id": "xxx",
        "target_id": ""
      }
    }
  }
}
```
