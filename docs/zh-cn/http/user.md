# 用户相关接口列表

本文档主要列出用户相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kaiheila.cn/doc/reference)。

| 接口                                   | 接口说明         | 维护状态 |
| -------------------------------------- | ---------------- | -------- |
| [/api/v3/user/me](#获取当前用户信息)   | 获取当前用户信息 | 正常     |
| [/api/v3/user/view](#获取目标用户信息) | 获取目标用户信息 | 正常     |

## 获取当前用户信息

### 接口说明

| 地址              | 请求方式 | 说明                     |
| ----------------- | -------- | ------------------------ |
| `/api/v3/user/me` | GET      | 获取当前登录的用户的信息 |

### 参数列表

| 参数名 | 类型 | 必传 | 参数区域 | 说明 |
| ------ | ---- | ---- | -------- | ---- |

### 返回参数说明

| 参数名          | 类型    | 说明                                                   |
| --------------- | ------- | ------------------------------------------------------ |
| id              | string  | 用户的 id                                              |
| username        | string  | 用户的名称                                             |
| identify_num    | string  | 用户名的认证数字，用户名正常为：user_name#identify_num |
| online          | boolean | 当前是否在线                                           |
| status          | int     | 用户的状态, 0 和 1 代表正常，10 代表被封禁             |
| avatar          | string  | 用户的头像的 url 地址                                  |
| bot             | boolean | 用户是否为机器人                                       |
| mobile_verified | boolean | 是否手机号已验证                                       |
| mobile_prefix   | string  | 手机区号,如中国为 86                                   |
| mobile          | string  | 用户手机号，带掩码                                     |
| invited_count   | int     | 当前邀请注册的人数                                     |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "id": "364862",
    "username": "test",
    "identify_num": "1670",
    "online": false,
    "status": 0,
    "avatar": "https://xxx.com/assets/bot.png/icon",
    "bot": true,
    "mobile_verified": true,
    "client_id": "b64kJF7HHFKXXX",
    "mobile_prefix": "86",
    "mobile": "110****2333",
    "invited_count": 0
  }
}
```

## 获取目标用户信息

### 接口说明

| 地址                | 请求方式 | 说明                    |
| ------------------- | -------- | ---------------------- |
| `/api/v3/user/view` | GET      | 获取当前登录的用户的信息 |

### 参数列表

| 参数名   | 位置  | 类型   | 必需  | 说明      |
| -------- | ----- | ------ | ----- | --------- |
| user_id  | query | string | true  | none      |
| guild_id | query | string | false | 服务器 id |

### 返回参数说明

| 参数名          | 类型    | 说明                                                   |
| --------------- | ------- | ------------------------------------------------------ |
| id              | string  | 用户的 id                                              |
| username        | string  | 用户的名称                                             |
| nickname        | string  | 用户在当前服务器的昵称                                 |
| identify_num    | string  | 用户名的认证数字，用户名正常为：user_name#identify_num |
| online          | boolean | 当前是否在线                                           |
| status          | int     | 用户的状态, 0 和 1 代表正常，10 代表被封禁             |
| avatar          | string  | 用户的头像的 url 地址                                  |
| vip_avatar      | string  | vip 用户的头像的 url 地址，可能为 gif 动图             |
| is_vip          | boolean | 是否为会员                                             |
| bot             | boolean | 是否为机器人                                           |
| mobile_verified | boolean | 是否手机号已验证                                       |
| roles           | Array   | 用户在当前服务器中的角色 id 组成的列表                 |
| mobile_verified | boolean | 是否手机号已验证                                       |
| joined_at       | int     | 加入服务器时间                                         |
| active_time     | int     | 活跃时间                                               |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "id": "2418200000",
    "username": "tz-un",
    "identify_num": "5618",
    "online": false,
    "status": 0,
    "bot": true,
    "avatar": "https://img.kaiheila.cn/avatars/2020-02/xxxx.jpg/icon",
    "vip_avatar": "https://img.kaiheila.cn/avatars/2020-02/xxxx.jpg/icon",
    "mobile_verified": true,
    "roles": [113],
    "joined_at": 1621338425000,
    "active_time": 1628688607719
  }
}
```

## 下线机器人

### 接口说明

| 地址                   | 请求方式 | 说明       |
| ---------------------- | -------- | ---------- |
| `/api/v3/user/offline` | POST     | 下线机器人 |

### 参数列表

| 参数名 | 类型 | 必传 | 参数区域 | 说明 |
| ------ | ---- | ---- | -------- | ---- |

### 返回参数说明

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {}
}
```
