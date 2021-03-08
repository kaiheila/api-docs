# 服务器相关事件

### 事件格式说明：请查看 [[事件结构/格式说明]](  https://developer.kaiheila.cn/doc/event/event-introduction )

## 服务器信息更新

#### extra字段说明：

| 字段                | 类型   | 说明                                                       |
| ------------------- | ------ | ---------------------------------------------------------- |
| type                | string | 消息的类型，本处为 `updated_guild`                         |
| body                | Map    |                                                            |
| ↳id                 | string | 服务器id                                                   |
| ↳name               | string | 服务器名称                                                 |
| ↳user_id            | string | 服务器主id                                                 |
| ↳icon               | string | 服务器logo图片地址                                         |
| ↳notify_type        | int    | 通知类型 `1`接受所有通知 `2`仅接收被提及消息 `3`不接收通知 |
| ↳region             | string | 服务器所在区域                                             |
| ↳enable_open        | int    | 是否为公开服务器, 1 or 0                                   |
| ↳open_id            | int    | 公开服务器id                                               |
| ↳default_channel_id | string | 默认文字频道id                                             |
| ↳welcome_channel_id | string | 欢迎频道id                                                 |

#### 示例：

```json
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


## 服务器删除

#### extra字段说明：

| 字段                | 类型   | 说明                                                       |
| ------------------- | ------ | ---------------------------------------------------------- |
| type                | string | 消息的类型，本处为 `deleted_guild`                         |
| body                | Map    |                                                            |
| ↳id                 | string | 服务器id                                                   |
| ↳name               | string | 服务器名称                                                 |
| ↳user_id            | string | 服务器主id                                                 |
| ↳icon               | string | 服务器logo图片地址                                         |
| ↳notify_type        | int    | 通知类型 `1`接受所有通知 `2`仅接收被提及消息 `3`不接收通知 |
| ↳region             | string | 服务器所在区域                                             |
| ↳enable_open        | int    | 是否为公开服务器, 1 or 0                                   |
| ↳open_id            | int    | 公开服务器id                                               |
| ↳default_channel_id | string | 默认文字频道id                                             |
| ↳welcome_channel_id | string | 欢迎频道id                                                 |

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


## 服务器封禁用户

#### extra字段说明：

| 字段         | 类型   | 说明                                  |
| ------------ | ------ | ------------------------------------- |
| type         | string | 消息的类型，本处为 `added_block_list` |
| body         | Map    |                                       |
| ↳operator_id | string | 操作人id                              |
| ↳remark      | string | 封禁理由                              |
| ↳user_id     | Array  | 被封禁成员id列表                      |

#### 示例：

```json
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


### 


## 服务器取消封禁用户

#### extra字段说明：

| 字段         | 类型   | 说明                                    |
| ------------ | ------ | --------------------------------------- |
| type         | string | 消息的类型，本处为 `deleted_block_list` |
| body         | Map    |                                         |
| ↳operator_id | string | 操作人id                                |
| ↳user_id     | Array  | 被封禁成员id列表                        |

#### 示例：

```json
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

