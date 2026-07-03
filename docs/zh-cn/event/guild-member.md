# 服务器成员相关事件

### 事件格式说明：请查看 \[[事件结构/格式说明](https://developer.kookapp.cn/doc/event/event-introduction)\]

## 新成员加入服务器

#### extra 字段说明：

| 字段        | 类型   | 说明                              |
| ----------- | ------ | --------------------------------- |
| type        | string | 消息的类型，本处为 `joined_guild` |
| body        | Map    |                                   |
| » user_id   | string | 用户 id                           |
| » joined_at | int    | 加入服务器的时间                  |

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

#### extra 字段说明：

| 字段        | 类型   | 说明                              |
| ----------- | ------ | --------------------------------- |
| type        | string | 消息的类型，本处为 `exited_guild` |
| body        | Map    |                                   |
| » user_id   | string | 用户 id                           |
| » exited_at | int    | 退出服务器的时间                  |

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

> 推送此消息的时机包括:
> - 服务器成员获得或失去角色时
> - 服务器成员在此服务器下的昵称变更时

#### extra 字段说明：

| 字段                | 类型       | 说明                                     |
|-------------------|----------|----------------------------------------|
| type              | string   | 消息的类型，本处为 `updated_guild_member`       |
| body              | Map      |                                        |
| » user_id         | string   | 用户 id                                  |
| » id              | string   | 用户的 id                                 |
| » username        | string   | 用户的名称                                  |
| » nickname        | string   | 用户在当前服务器的昵称                            |
| » identify_num    | string   | 用户名的认证数字，用户名正常为：user_name#identify_num |
| » online          | boolean  | 当前是否在线                                 |
| » bot             | boolean  | 是否为机器人                                 |
| » status          | int      | 用户的状态, 0 和 1 代表正常，10 代表被封禁             |
| » avatar          | string   | 用户的头像的 url 地址                          |
| » vip_avatar      | string   | vip 用户的头像的 url 地址，可能为 gif 动图           |
| » mobile_verified | boolean  | 是否手机号已验证                               |
| » roles           | Array    | 用户在当前服务器中的角色 id 组成的列表                  |
| » boost_start_at  | int/null | 用户在当前服务器中开始助力的起始时间, 为 `null` 代表未助力     |

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
        "nickname": "new_nick",
        "id": "2418200000",
        "username": "tz-un",
        "identify_num": "5618",
        "online": false,
        "avatar": "https://img.kookapp.cn/avatars/2020-02/xxxx.jpg/icon",
        "vip_avatar": "https://img.kookapp.cn/avatars/2020-02/xxxx.jpg/icon",
        "bot": false,
        "status" : 0,
        "mobile_verified": true,
        "roles": [
          111,
          112
        ],
        "boost_start_at": 1783049826000
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

#### extra 字段说明：

| 字段         | 类型   | 说明                                                 |
| ------------ | ------ | ---------------------------------------------------- |
| type         | string | 消息的类型，本处为 `guild_member_online`             |
| body         | Map    |                                                      |
| » user_id    | string | 用户 id                                              |
| » event_time | int    | 事件发生的时间                                       |
| » guilds     | array  | 服务器 id 组成的数组, 代表与该用户所在的共同的服务器 |

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
        "guilds": ["601638990000000"]
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

#### extra 字段说明：

| 字段         | 类型   | 说明                                                 |
| ------------ | ------ | ---------------------------------------------------- |
| type         | string | 消息的类型，本处为 `guild_member_offline`            |
| body         | Map    |                                                      |
| » user_id    | string | 用户 id                                              |
| » event_time | int    | 事件发生的时间                                       |
| » guilds     | array  | 服务器 id 组成的数组, 代表与该用户所在的共同的服务器 |

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
        "guilds": ["601638990000000"]
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
