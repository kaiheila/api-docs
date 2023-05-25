# 好友相关接口列表

本文档主要列出好友相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kookapp.cn/doc/reference)。

| 接口                                           | 接口说明     | 维护状态 |
| ---------------------------------------------- | ------------ | -------- |
| [/api/v3/friend](#好友列表)                    | 好友列表     | 正常     |
| [/api/v3/friend/request](#好友申请)            | 好友申请     | 正常     |
| [/api/v3/friend/handle-request](#处理好友申请) | 处理好友申请 | 正常     |
| [/api/v3/friend/delete](#删除好友)             | 删除好友     | 正常     |
| [/api/v3/friend/block](#屏蔽用户)             | 屏蔽用户     | 正常    |
| [/api/v3/friend/unblock](#取消屏蔽用户)         | 取消屏蔽用户   | 正常    |

## 好友列表

### 接口说明

| 地址             | 请求方式 | 说明 |
| ---------------- | -------- | ---- |
| `/api/v3/friend` | GET      |      |

### 参数列表

| 参数名    | 类型   | 是否必填 | 说明                         |
| --------- | ------ | -------- | ---------------------------- |
| type | string | 否       | friend 仅返回好友 request 仅返回申请列表 block 仅返回屏蔽列表                  |

### 返回参数说明

| 参数名  | 类型  | 说明         |
| ------- | ----- | ------------ |
| friend  | array | 好友列表     |
| request | array | 好友申请列表 |
| block   | array | 屏蔽用户列表 |

### 返回实例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "request": [
      {
        "id": 6576047,
        "type": "request",
        "friend_info": {
          "id": "2810246202",
          "username": "戈小荷",
          "identify_num": "0439",
          "online": true,
          "os": "iOS",
          "status": 1,
          "avatar": "https://img.kookapp.cn/avatars/2021-07/ggB1h1kCvS06j06j.png/icon",
          "vip_avatar": "https://img.kookapp.cn/avatars/2021-07/ggB1h1kCvS06j06j.png/icon",
          "banner": "https://img.kookapp.cn/assets/2022-06/3rLkCSMdhW0hg06y.png",
          "nickname": "戈小荷",
          "roles": [],
          "is_vip": true,
          "is_ai_reduce_noise": true,
          "is_personal_card_bg": false,
          "bot": false,
          "decorations_id_map": {
            "join_voice": 10017,
            "background": 10018
          }
        },
        "own": false
      }
    ],
    "friend": [
      {
        "id": 6547839,
        "type": "friend",
        "friend_info": {
          "id": "982587531",
          "username": "DeeChael",
          "identify_num": "0001",
          "online": true,
          "os": "Websocket",
          "status": 1,
          "avatar": "https://img.kookapp.cn/avatars/2022-01/HA5jda2Ya604w04w.png/icon",
          "vip_avatar": "https://img.kookapp.cn/avatars/2022-01/HA5jda2Ya604w04w.png/icon",
          "banner": "https://img.kookapp.cn/assets/2022-12/SC9Rijissy0hg06y.png",
          "nickname": "DeeChael",
          "roles": [],
          "is_vip": true,
          "is_ai_reduce_noise": true,
          "is_personal_card_bg": false,
          "bot": false,
          "decorations_id_map": {
            "join_voice": 10017,
            "background": 10018
          },
          "game": {
            "id": 194884,
            "name": "PyCharm",
            "type": 1,
            "icon": "",
            "start_time": 1671164634
          }
        },
        "own": false
      }
    ],
    "blocked": []
  }
}
```

## 好友申请

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/friend/request` | POST     |      |

### 参数列表

| 参数名    | 类型   | 是否必填 | 说明                         |
| --------- | ------ | -------- | ---------------------------- |
| user_code | string | 是       | 用户名#编号                  |
| from      | int    | 是       | 添加方式 0 搜索 2 服务器     |
| guild_id  | string | 否       | 当添加方式为服务器时该项必填 |

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

## 处理好友申请

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/friend/handle-request` | POST     |      |

### 参数列表

| 参数名 | 类型    | 是否必填 | 说明          |
| ------ | ------- | -------- | ------------- |
| id     | int     | 是       | 好友申请的id  |
| accept | boolean | 是       | 0 拒绝 1 同意  |

### 返回参数说明

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": true
}
```

## 删除好友

### 接口说明

| 地址                    | 请求方式 | 说明 |
| ----------------------- | -------- | ---- |
| `/api/v3/friend/delete` | POST     |      |

### 参数列表

| 参数名  | 类型   | 是否必填 | 说明    |
| ------- | ------ | -------- | ------- |
| user_id | string | 是       | 用户 id |

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

## 屏蔽用户

### 接口说明

| 地址                     | 请求方式 | 说明 |
|------------------------| -------- | ---- |
| `/api/v3/friend/block` | POST     |      |

### 参数列表

| 参数名  | 类型   | 是否必填 | 说明    |
| ------- | ------ | -------- |-------|
| user_id | string | 是       | 用户 ID |

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

## 取消屏蔽用户

### 接口说明

| 地址                       | 请求方式 | 说明 |
|--------------------------| -------- | ---- |
| `/api/v3/friend/unblock` | POST     |      |

### 参数列表

| 参数名  | 类型   | 是否必填 | 说明    |
| ------- | ------ | -------- |-------|
| user_id | string | 是       | 用户 ID |

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
