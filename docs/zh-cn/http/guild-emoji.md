# 服务器表情相关接口列表

本文档主要列出服务器表情相关接口。

本文档中的接口均符合接口规范。如有疑问，建议先查阅[接口引言](https://developer.kookapp.cn/doc/reference)。

| 接口                                            | 接口说明           | 维护状态 |
| ----------------------------------------------- | ------------------ | -------- |
| [/api/v3/guild-emoji/list](#获取服务器表情列表) | 获取服务器表情列表 | 正常     |
| [/api/v3/guild-emoji/create](#创建服务器表情)   | 创建服务器表情     | 正常     |
| [/api/v3/guild-emoji/update](#更新服务器表情)   | 更新服务器表情     | 正常     |
| [/api/v3/guild-emoji/delete](#删除服务器表情)   | 删除服务器表情     | 正常     |

## 获取服务器表情列表

### 接口说明

| 地址                       | 请求方式 | 说明 |
| -------------------------- | -------- | ---- |
| `/api/v3/guild-emoji/list` | GET      |      |

### 参数列表

| 参数名    | 位置  | 类型    | 必需  | 说明         |
| --------- | ----- | ------- | ----- | ------------ |
| page      | query | integer | false | 目标页数     |
| page_size | query | integer | false | 每页数据数量 |
| guild_id  | query | string  | true  | 服务器 id    |

### 返回参数说明

| 参数名    | 类型   | 说明                                                                           |
| --------- | ------ | ------------------------------------------------------------------------------ |
| name      | string | 表情的名称                                                                     |
| id        | string | 表情的 ID                                                                      |
| user_info | map    | 上传用户，具体参考 [用户相关接口](https://developer.kookapp.cn/doc/http/user) |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "items": [
      {
        "name": "ceeb653ely1gm1ayxhrnnj20j60jpwfu",
        "id": "XXXXXXXXX/4c43XXXXXXX",
        "user_info": {
          "id": "17000",
          "username": "用户名",
          "identify_num": "467",
          "online": true,
          "os": "Websocket",
          "status": 1,
          "avatar": "https://XXXXXXXXXXXX"
        }
      },
      {
        "name": "ceeb653ely1gm6d2213ycj20go0gogvj",
        "id": "916864XXX464X/c74XXXXXXXX",
        "user_info": {
          "id": "10000",
          "username": "用户名",
          "identify_num": "0123",
          "online": true,
          "os": "Websocket",
          "status": 1,
          "avatar": "https://XXXXXXXXXXX"
        }
      }
    ],
    "meta": {
      "page": 1,
      "page_total": 10,
      "page_size": 50,
      "total": 480
    },
    "sort": {
      "id": 1
    }
  }
}
```

## 创建服务器表情

### 接口说明

| 地址                         | 请求方式 | 说明                                                  |
| ---------------------------- | -------- | ----------------------------------------------------- |
| `/api/v3/guild-emoji/create` | POST     | Header 中 `Content-Type` 必须为 `multipart/form-data` |

### 参数列表

| 参数名     | 位置 | 类型           | 必需  | 说明                                                   |
| ---------- | ---- | -------------- | ----- | ------------------------------------------------------ |
| name     | body | string         | false | 表情名。长度限制 2 - 32 字符，如果不写，则为随机字符串 |
| guild_id | body | string         | true  | 服务器 id                                              |
| emoji    | body | string(binary) | true  | 表情文件。必须为 PNG 类型，大小不能超过 256 KB         |

### 返回参数说明

| 参数名    | 类型   | 说明                                                                           |
| --------- | ------ | ------------------------------------------------------------------------------ |
| name      | string | 表情的名称                                                                     |
| id        | string | 表情的 ID                                                                      |
| user_info | map    | 上传用户，具体参考 [用户相关接口](https://developer.kookapp.cn/doc/http/user) |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "name": "ceeb653ely1gm1ayxhrnnj20j60jpwfu",
    "id": "1333609240026275/zTpnkSnMZH0c80ck.",
    "user_info": {
      "id": "1780328444",
      "username": "用户名",
      "identify_num": "3249",
      "online": true,
      "status": 0,
      "avatar": "https://img.kookapp.cn/assets/bot.png/icon",
      "vip_avatar": "https://img.kookapp.cn/avatars/2020-02/xxxx.jpg/icon"
    }
  }
}
```

## 更新服务器表情

### 接口说明

| 地址                         | 请求方式 | 说明 |
| ---------------------------- | -------- | ---- |
| `/api/v3/guild-emoji/update` | POST     |      |

### 参数列表

| 参数名 | 位置 | 类型   | 必需  | 说明                                                   |
| ------ | ---- | ------ | ----- | ------------------------------------------------------ |
| name | body | string | true  | 表情名。长度限制 2 - 32 字符，如果不写，则为随机字符串 |
| id   | body | string | true  | 表情 ID                                                |

### 返回参数说明

无返回参数

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {}
}
```

## 删除服务器表情

### 接口说明

| 地址                         | 请求方式 | 说明 |
| ---------------------------- | -------- | ---- |
| `/api/v3/guild-emoji/delete` | POST     |      |

### 参数列表

| 参数名 | 位置 | 类型   | 必需  | 说明    |
| ------ | ---- | ------ | ----- | ------- |
| id   | body | string | true  | 表情 ID |

### 返回参数说明

无返回参数

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {}
}
```
