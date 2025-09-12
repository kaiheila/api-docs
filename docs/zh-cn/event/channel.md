# 频道相关事件列表

### 事件格式说明：请查看 \[[事件结构/格式说明](https://developer.kookapp.cn/doc/event/event-introduction)\]

## 频道内用户添加 reaction

#### extra 字段说明：

| 字段             | 类型     | 说明                               |
|----------------|--------|----------------------------------|
| type           | string | 消息的类型，本处为 `added_reaction`       |
| body           | Map    |                                  |
| » msg_id       | string | 用户点击的消息 id                       |
| » user_id      | string | 点击的用户                            |
| » channel_id   | string | 频道 id                            |
| » emoji        | Map    | 消息对象, 包含 `id` 表情 id, `name` 表情名称 |
| » channel_type | int    | 频道类型 1：文字 2：语音                   |

#### 示例

```json
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
        "channel_type": 1,
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

## 频道内用户取消 reaction

#### extra 字段说明：

| 字段         | 类型   | 说明                                         |
| ------------ | ------ | -------------------------------------------- |
| type         | string | 消息的类型，本处为 `deleted_reaction`        |
| body         | Map    |                                              |
| » msg_id     | string | 用户点击的消息 id                            |
| » user_id    | string | 点击的用户                                   |
| » channel_id | string | 频道 id                                      |
| » emoji      | Map    | 消息对象, 包含 `id` 表情 id, `name` 表情名称 |
| » channel_type | int    | 频道类型 1：文字 2：语音                   |
#### 示例：

```json
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
        "channel_type": 1,
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

###

## 频道消息更新

#### extra 字段说明：

| 字段            | 类型    | 说明                                 |
| --------------- | ------- | ------------------------------------ |
| type            | string  | 消息的类型，本处为 `updated_message` |
| body            | Map     |                                      |
| » msg_id        | string  | 被更新的消息的 id                    |
| » content       | string  | 更新后的文本                         |
| » channel_id    | string  | 频道 id                              |
| » mention       | array   | 提及的用户 id 组成的列表             |
| » mention_all   | boolean | 是否提及 `全体成员`                  |
| » mention_here  | boolean | 是否提及 `在线成员`                  |
| » mention_roles | array   | 提及的角色 id 组成的列表             |
| » updated_at    | int     | 更新时间戳(毫秒)                     |
| » channel_type | int    | 频道类型 1：文字 2：语音                   |
#### 示例：

```json
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
        "msg_id": "59def270-xxx-8db935e054a1",
        "channel_type": 1
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

## 频道消息被删除

#### extra 字段说明：

| 字段         | 类型   | 说明                                 |
| ------------ | ------ | ------------------------------------ |
| type         | string | 消息的类型，本处为 `deleted_message` |
| body         | Map    |                                      |
| » msg_id     | string | 被更新的消息的 id                    |
| » channel_id | string | 频道 id                              |
| » channel_type | int    | 频道类型 1：文字 2：语音                   |
#### 示例：

```json
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
        "msg_id": "59def270-xxxx-8db935e054a1",
        "channel_type": 1
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

###

## 新增频道

#### extra 字段说明：

| 字段 | 类型   | 说明                                                                           |
| ---- | ------ | ------------------------------------------------------------------------------ |
| type | string | 消息的类型，本处为 `added_channel`                                             |
| body | Map    | 参考[对象-频道 Channel](https://developer.kookapp.cn/doc/objects#频道Channel) |

#### 示例：

```json
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
        "level": 12,
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
        "permission_users": [
          {
            "user": {
              "id": "0",
              "username": "花荣",
              "identify_num": "12",
              "online": true,
              "os": "Websocket",
              "status": 1,
              "avatar": "xxxx",
              "mobile_verified": true,
              "nickname": "test",
              "roles": [],
              "joined_at": 1602596021000,
              "active_time": 1612703344396
            },
            "allow": 0,
            "deny": 0
          }
        ],
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

## 修改频道信息

#### extra 字段说明：

| 字段 | 类型   | 说明                                                                           |
| ---- | ------ | ------------------------------------------------------------------------------ |
| type | string | 消息的类型，本处为 `updated_channel`                                           |
| body | Map    | 参考[对象-频道 Channel](https://developer.kookapp.cn/doc/objects#频道Channel) |

#### 示例

```json
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
        "level": 12,
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

## 删除频道

#### extra 字段说明：

| 字段           | 类型   | 说明                                 |
|--------------| ------ | ------------------------------------ |
| type         | string | 消息的类型，本处为 `deleted_channel` |
| body         | Map    |                                      |
| » id         | string | 被删掉的频道 id                      |
| » deleted_at | int    | 删除时间(毫秒)                       |
| » type          | int    | 频道类型 1：文字 2：语音                   |

#### 示例：

```json
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
        "deleted_at": 1612777405595,
        "type" : 1
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

## 新的频道置顶消息

#### extra 字段说明：

| 字段          | 类型   | 说明                                |
| ------------- | ------ | ----------------------------------- |
| type          | string | 消息的类型，本处为 `pinned_message` |
| body          | Map    |                                     |
| » channel_id  | string | 频道 id                             |
| » operator_id | string | 操作人 id                           |
| » msg_id      | string | 被置顶的消息 id                     |
| » channel_type | int    | 频道类型 1：文字 2：语音                   |

#### 示例：

```json
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
        "msg_id": "4d5ef7ae-xxxx-b03e57cdf2e9",
        "channel_type": 1
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

## 取消频道置顶消息

#### extra 字段说明：

| 字段          | 类型   | 说明                                  |
| ------------- | ------ | ------------------------------------- |
| type          | string | 消息的类型，本处为 `unpinned_message` |
| body          | Map    |                                       |
| » channel_id  | string | 频道 id                               |
| » operator_id | string | 操作人 id                             |
| » msg_id      | string | 被取消置顶的消息 id                   |
| » channel_type | int    | 频道类型 1：文字 2：语音                   |

#### 示例：

```json
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
        "msg_id": "4d5ef7ae-xxxx-b03e57cdf2e9",
        "channel_type": 1
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
