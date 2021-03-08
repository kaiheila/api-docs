# 服务器成员相关事件

### 事件格式说明：请查看 [[事件结构/格式说明]](  https://developer.kaiheila.cn/doc/event/event-introduction )

## 新成员加入服务器

#### extra字段说明：

| 字段       | 类型   | 说明                              |
| ---------- | ------ | --------------------------------- |
| type       | string | 消息的类型，本处为 `joined_guild` |
| body       | Map    |                                   |
| ↳user_id   | string | 用户id                            |
| ↳joined_at | int    | 加入服务器的时间                  |

#### 示例：

```json
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



## 服务器成员退出

#### extra字段说明：

| 字段       | 类型   | 说明                              |
| ---------- | ------ | --------------------------------- |
| type       | string | 消息的类型，本处为 `exited_guild` |
| body       | Map    |                                   |
| ↳user_id   | string | 用户id                            |
| ↳exited_at | int    | 退出服务器的事件                  |

#### 示例：

```json
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



## 服务器成员信息更新

#### extra字段说明：

| 字段      | 类型   | 说明                                      |
| --------- | ------ | ----------------------------------------- |
| type      | string | 消息的类型，本处为 `updated_guild_member` |
| body      | Map    |                                           |
| ↳user_id  | string | 用户id                                    |
| ↳nickname | string | 昵称                                      |

#### 示例：

```json
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



## 服务器成员上线

#### extra字段说明：

| 字段        | 类型   | 说明                                               |
| ----------- | ------ | -------------------------------------------------- |
| type        | string | 消息的类型，本处为 `guild_member_online`           |
| body        | Map    |                                                    |
| ↳user_id    | string | 用户id                                             |
| ↳event_time | int    | 事件发生的时间                                     |
| ↳guilds     | array  | 服务器id组成的数组, 代表与该用户所在的共同的服务器 |

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



## 服务器成员下线

#### extra字段说明：

| 字段        | 类型   | 说明                                               |
| ----------- | ------ | -------------------------------------------------- |
| type        | string | 消息的类型，本处为 `guild_member_offline`          |
| body        | Map    |                                                    |
| ↳user_id    | string | 用户id                                             |
| ↳event_time | int    | 事件发生的时间                                     |
| ↳guilds     | array  | 服务器id组成的数组, 代表与该用户所在的共同的服务器 |

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
