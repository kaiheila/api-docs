# 服务器角色相关事件

### 事件格式说明：请查看 \[[事件结构/格式说明]\]( https://developer.kaiheila.cn/doc/event/event-introduction )

## 服务器角色增加

#### extra 字段说明：

| 字段 | 类型   | 说明                                                                     |
| ---- | ------ | ------------------------------------------------------------------------ |
| type | string | 消息的类型，本处为 `added_role`                                          |
| body | Map    | 参考[对象-角色 Role](https://developer.kaiheila.cn/doc/objects#角色Role) |

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

## 服务器角色删除

#### extra 字段说明：

| 字段 | 类型   | 说明                                                                     |
| ---- | ------ | ------------------------------------------------------------------------ |
| type | string | 消息的类型，本处为 `deleted_role`                                        |
| body | Map    | 参考[对象-角色 Role](https://developer.kaiheila.cn/doc/objects#角色Role) |

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

## 服务器角色更新

#### extra 字段说明：

| 字段 | 类型   | 说明                                                                     |
| ---- | ------ | ------------------------------------------------------------------------ |
| type | string | 消息的类型，本处为 `updated_role`                                        |
| body | Map    | 参考[对象-角色 Role](https://developer.kaiheila.cn/doc/objects#角色Role) |

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
