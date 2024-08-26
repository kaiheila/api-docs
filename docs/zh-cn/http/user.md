# 用户相关接口列表

本文档主要列出用户相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kookapp.cn/doc/reference)。

| 接口                              | 接口说明     | 维护状态  |
|---------------------------------|----------|-------|
| [/api/v3/user/me](#获取当前用户信息)    | 获取当前用户信息 | 正常    |
| [/api/v3/user/view](#获取目标用户信息)  | 获取目标用户信息 | 正常    |
| [/api/v3/user/offline](#下线机器人)  | 下线机器人    | 正常    |
| [/api/v3/user/online](#上线机器人)  | 上线机器人    | 正常    |
| [/api/v3/user/get-online-status](#获取在线状态)  | 获取机器人在线状态    | 正常    |

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
| os              | string  | 当前连接方式                                           |
| status          | int     | 用户的状态, 0 和 1 代表正常，10 代表被封禁             |
| avatar          | string  | 用户的头像的 url 地址                                  |
| vip_avatar      | string  | vip用户的头像的 url 地址                            |
| banner          | string  | 用户的横幅的 url 地址                                  |
| nickname        | string  | 用户的昵称                                           |
| roles           | map     | 用户的角色信息                                       |
| is_vip          | boolean | 用户是否为vip					|
| vip_amp	  | boolean | 用户是否为年度vip					|
| bot             | boolean | 用户是否为机器人                                       |
| bot_status	  | boolean | 机器人状态						|
| tag_info	  | map     | 用户标签信息  					|
| mobile_verified | boolean | 是否手机号已验证                                       |
| is_sys	  | boolean | 是否为系统账号					|
| client_id	  | string  | 客户端id						|
| verified  	  | boolean | 是否验证过						|
| mobile_prefix   | string  | 手机区号,如中国为 86                                   |
| mobile          | string  | 用户手机号，带掩码                                     |
| invited_count   | int     | 当前邀请注册的人数                                     |

### 返回示例

```json
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "id": "57655610",
        "username": "test",
        "identify_num": "4357",
        "online": false,
        "os": "Websocket",
        "status": 0,
        "avatar": "https://xxx/assets/bot.png?x-oss-process=style/icon",
        "vip_avatar": "https://xxx/assets/bot.png?x-oss-process=style/icon",
        "banner": "",
        "nickname": "test",
        "roles": [],
        "is_vip": false,
        "vip_amp": false,
        "bot": true,
        "bot_status": 0,
        "tag_info": {
            "color": "#0096FF",
            "bg_color": "#0096FF33",
            "text": "机器人"
        },
        "mobile_verified": true,
        "is_sys": false,
        "client_id": "xxxxxxxxxx",
        "verified": false,
        "mobile_prefix": "86",
        "mobile": "****",
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
| os              | string  | 当前连接方式                                           |
| status          | int     | 用户的状态, 0 和 1 代表正常，10 代表被封禁             |
| avatar          | string  | 用户的头像的 url 地址                                  |
| vip_avatar      | string  | vip 用户的头像的 url 地址，可能为 gif 动图             |
| banner	  | string  | 用户横幅的 url 地址 				|
| is_vip          | boolean | 是否为会员                                             |
| vip_amp	  | boolean | 是否为年度会员					|
| bot             | boolean | 是否为机器人                                           |
| mobile_verified | boolean | 是否手机号已验证                                       |
| roles           | Array   | 用户在当前服务器中的角色 id 组成的列表                 |
| is_sys	  | boolean | 是否为系统账户 					|
| joined_at       | int     | 加入服务器时间                                         |
| active_time     | int     | 活跃时间                                               |

### 返回示例

```json
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "id": "123456789",
        "username": "test",
        "identify_num": "0001",
        "online": true,
        "os": "Websocket",
        "status": 1,
        "avatar": "https://xxx/avatars/k/2.png?x-oss-process=style/icon",
        "vip_avatar": "https://xxx/avatars/k/2.png?x-oss-process=style/icon",
        "banner": "",
        "nickname": "test",
        "roles": [
            8615,
            8616,
            8617
        ],
        "is_vip": true,
        "vip_amp": true,
        "bot": false,
        "mobile_verified": true,
        "is_sys": false,
        "joined_at": 1721096255000,
        "active_time": 1723029489498
    }
}
```

## 下线机器人

### 接口说明

| 地址                   | 请求方式 | 说明       |
| ---------------------- | -------- | ---------- |
| `/api/v3/user/offline` | POST     | 下线机器人, 仅限webhook使用。websocket断开即视为下线 |


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

## 上线机器人

### 接口说明

| 地址                   | 请求方式 | 说明       |
| ---------------------- | -------- | ---------- |
| `/api/v3/user/online` | POST     | 上线机器人, 仅限webhook使用。websocket直接连上信令服务器即视为上线。 |
  
**注意:** 该接口的允许调用频率较低,仅用于允许开发者不经过界面上线机器人。当出现过多错误下线时，请尽量先排查问题再上线，而不是直接调用该接口。

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

## 获取在线状态

### 接口说明

| 地址                   | 请求方式 | 说明       |
| ---------------------- | -------- | ---------- |
| `/api/v3/user/get-online-status` | GET     | 获取机器人在线状态，可以用来保证机器人在线 |

### 参数列表

| 参数名 | 类型 | 必传 | 参数区域 | 说明 |
| ------ | ---- | ---- | -------- | ---- |


### 返回参数说明

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |
| online | boolean | 是否在线|
| online_os| Array[String]| 在线的平台|



### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "online": true,
    "online_os": ["Webhook"]
  }
}
```
