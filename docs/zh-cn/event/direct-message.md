# 私聊消息事件

### 事件格式说明：请查看 \[[事件结构/格式说明]\]( https://developer.kaiheila.cn/doc/event/event-introduction )

## 私聊消息更新

#### extra 字段说明：

| 字段        | 类型   | 说明                                         |
| ----------- | ------ | -------------------------------------------- |
| type        | string | 消息的类型，本处为 `updated_private_message` |
| body        | Map    |                                              |
| »msg_id     | string | 被更新的消息的 id                            |
| »author_id  | string | 被更新的消息的创建者 id                      |
| »target_id  | string | 被更新的消息的目标用户 id                    |
| »content    | string | 更新后的文本                                 |
| »chat_code  | string | 私聊 code                                    |
| »updated_at | int    | 更新时间戳(毫秒)                             |

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

## 私聊消息被删除

#### extra 字段说明：

| 字段        | 类型   | 说明                                         |
| ----------- | ------ | -------------------------------------------- |
| type        | string | 消息的类型，本处为 `deleted_private_message` |
| body        | Map    |                                              |
| »msg_id     | string | 被删除的消息的 id                            |
| »author_id  | string | 被删除的消息的创建者 id                      |
| »target_id  | string | 被删除的消息的目标用户 id                    |
| »chat_code  | string | 私聊 code                                    |
| »deleted_at | int    | 删除的时间戳(毫秒)                           |

#### 示例：

```json
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

## 私聊内用户添加 reaction

#### extra 字段说明：

| 字段       | 类型   | 说明                                         |
| ---------- | ------ | -------------------------------------------- |
| type       | string | 消息的类型，本处为 `private_added_reaction`  |
| body       | Map    |                                              |
| »msg_id    | string | 用户点击的消息 id                            |
| »user_id   | string | 点击的用户的 id                              |
| »chat_code | string | 私聊 code                                    |
| »emoji     | Map    | 消息对象, 包含 `id` 表情 id, `name` 表情名称 |

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

## 私聊内用户取消 reaction

#### extra 字段说明：

| 字段       | 类型   | 说明                                          |
| ---------- | ------ | --------------------------------------------- |
| type       | string | 消息的类型，本处为 `private_deleted_reaction` |
| body       | Map    |                                               |
| »msg_id    | string | 用户点击的消息 id                             |
| »user_id   | string | 点击的用户的 id                               |
| »chat_code | string | 私聊 code                                     |
| »emoji     | Map    | 消息对象, 包含 `id` 表情 id, `name` 表情名称  |

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
