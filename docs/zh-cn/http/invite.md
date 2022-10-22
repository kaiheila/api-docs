# 邀请相关接口

本文档主要列出邀请相关的接口。  
本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kookapp.cn/doc/reference)。

| 接口                                   | 接口说明     | 维护状态 |
| -------------------------------------- | ------------ | -------- |
| [/api/v3/invite/list](#获取邀请列表)   | 获取邀请列表 | 正常     |
| [/api/v3/invite/create](#创建邀请链接) | 创建邀请链接 | 正常     |
| [/api/v3/invite/delete](#删除邀请链接) | 删除邀请链接 | 正常     |

## 获取邀请列表

### 接口说明

| 地址                  | 请求方式 | 说明 |
| --------------------- | -------- | ---- |
| `/api/v3/invite/list` | GET      |      |

### 参数列表

服务器 id 或者频道 id 必须填一个

| 参数名     | 位置  | 类型    | 必需  | 说明         |
| ---------- | ----- | ------- | ----- | ------------ |
| guild_id   | query | string  | false | 服务器 id    |
| channel_id | query | string  | false | 频道 id      |
| page       | query | integer | false | 目标页数     |
| page_size  | query | integer | false | 每页数据数量 |

### 返回参数说明

| 参数名     | 类型   | 说明                                                       |
| ---------- | ------ | ---------------------------------------------------------- |
| guild_id   | string | 服务器 id                                                  |
| channel_id | string | 频道 id                                                    |
| url_code   | string | url code                                                   |
| url        | string | 地址                                                       |
| user       | object | 用户,参见[user](https://developer.kookapp.cn/doc/objects) |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "items": [
      {
        "channel_id": "9219038000000",
        "guild_id": "91686000000",
        "url_code": "XXX",
        "url": "https://kook.top/XXX",
        "user": {
          "id": "2418200000",
          "username": "tz-un",
          "identify_num": "5618",
          "online": false,
          "status": 0,
          "bot": true,
          "avatar": "https://img.kaiheila.cn/avatars/2020-02/xxxx.jpg/icon",
          "vip_avatar": "https://img.kaiheila.cn/avatars/2020-02/xxxx.jpg/icon"
        }
      }
    ],
    "meta": {
      "page": 1,
      "page_total": 10,
      "page_size": 50,
      "total": 480
    },
    "sort": {}
  }
}
```

## 创建邀请链接

### 接口说明

| 地址                    | 请求方式 | 说明 |
| ----------------------- | -------- | ---- |
| `/api/v3/invite/create` | POST     |      |

### 参数列表

服务器 id 或者频道 id 必须填一个

| 参数名        | 位置 | 类型    | 必需  | 说明                                                                                                                                                                  |
| ------------- | ---- | ------- | ----- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| guild_id      | body | string  | false | 服务器 id                                                                                                                                                             |
| channel_id    | body | string  | false | 服务器频道 id                                                                                                                                                         |
| duration      | body | integer | false | 邀请链接有效时长（秒），默认 7 天。可选值： 0 => 永不； 1800 => 0.5 小时； 3600 => 1 个小时； 21600 => 6 个小时； 43200 => 12 个小时； 86400 => 1 天； 604800 => 7 天 |
| setting_times | body | integer | false | 设置的次数，默认-1。可选值： -1 => 无限制； 1 => 1 次使用； 5 => 5 次使用； 10 => 10 次使用 ；25 => 25 次使用； 50 => 50 次使用； 100 => 100 次使用                   |

### 返回参数说明

| 参数名 | 类型   | 说明 |
| ------ | ------ | ---- |
| url    | string | 地址 |

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "url": "https://kook.top/xxxx",
    }
}
```

## 删除邀请链接

### 接口说明

| 地址                    | 请求方式 | 说明 |
| ----------------------- | -------- | ---- |
| `/api/v3/invite/delete` | POST     |      |

### 参数列表

| 参数名     | 位置 | 类型   | 必需  | 说明          |
| ---------- | ---- | ------ | ----- | ------------- |
| url_code   | body | string | true  | 邀请码        |
| guild_id   | body | string | false | 服务器 id     |
| channel_id | body | string | false | 服务器频道 ID |

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
