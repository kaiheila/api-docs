# 黑名单相关接口

本文档主要列出服务器黑名单相关的接口, 目前所有接口需要有[封禁用户](https://developer.kookapp.cn/doc/http/guild-role#权限说明)权限才能正常访问。  
本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kookapp.cn/doc/reference)。

| 接口                                    | 接口说明       | 维护状态 |
| --------------------------------------- | -------------- | -------- |
| [/api/v3/blacklist/list](#获取黑名单)   | 获取黑名单列表 | 正常     |
| [/api/v3/blacklist/create](#加入黑名单) | 加入黑名单     | 正常     |
| [/api/v3/blacklist/delete](#移除黑名单) | 移除黑名单     | 正常     |

## 获取黑名单列表

### 接口说明

| 地址                     | 请求方式 | 说明                                                             |
| ------------------------ | -------- | ---------------------------------------------------------------- |
| `/api/v3/blacklist/list` | GET      | [分页参数](https://developer.kookapp.cn/doc/reference#请求参数) |

### 参数列表

| 参数名   | 位置  | 类型   | 必需 | 说明      |
| -------- | ----- | ------ | ---- | --------- |
| guild_id | query | string | true | 服务器 id |

### 返回参数说明

| 参数名       | 类型   | 说明                                                       |
| ------------ | ------ | ---------------------------------------------------------- |
| user_id      | string | 用户 id                                                    |
| created_time | int    | 加入黑名单的时间戳(毫秒)                                   |
| remark       | string | 加入黑名单的原因                                           |
| user         | object | 用户,参见[user](https://developer.kookapp.cn/doc/objects) |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "items": [
      {
        "user_id": "26954***",
        "created_time": 1640340668000,
        "remark": "***",
        "user": {
          "id": "26954***",
          "username": "***",
          "identify_num": "2826",
          "online": true,
          "os": "Websocket",
          "status": 1,
          "avatar": "**",
          "vip_avatar": "**",
          "banner": "",
          "nickname": "***",
          "roles": [],
          "is_vip": false,
          "bot": false
        }
      }
    ],
    "meta": {
      "page": 1,
      "page_total": 1,
      "page_size": 50,
      "total": 1
    },
    "sort": {}
  }
}
```

## 加入黑名单

### 接口说明

| 地址                       | 请求方式 | 说明 |
| -------------------------- | -------- | ---- |
| `/api/v3/blacklist/create` | POST     |      |

### 参数列表

| 参数名       | 位置 | 类型   | 必需  | 说明                                  |
| ------------ | ---- | ------ | ----- | ------------------------------------- |
| guild_id     | body | string | true  | 服务器 id                             |
| target_id    | body | string | true  | 目标用户 id                           |
| remark       | body | string | false | 加入黑名单的原因                      |
| del_msg_days | body | int    | false | 删除最近几天的消息，最大 7 天, 默认 0 |

### 返回参数说明

无

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {}
}
```

## 移除黑名单

### 接口说明

| 地址                       | 请求方式 | 说明 |
| -------------------------- | -------- | ---- |
| `/api/v3/blacklist/delete` | POST     |      |

### 参数列表

| 参数名    | 位置 | 类型   | 必需 | 说明        |
| --------- | ---- | ------ | ---- | ----------- |
| guild_id  | body | string | true | 服务器 id   |
| target_id | body | string | true | 目标用户 id |

### 返回参数说明

无

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {}
}
```
