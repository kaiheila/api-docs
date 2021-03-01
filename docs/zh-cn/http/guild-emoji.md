# 服务器表情相关接口列表

本文档主要列出服务器表情相关接口。

本文档中的接口均符合接口规范。如有疑问，建议先查阅[接口引言](https://developer.kaiheila.cn/doc/reference)。

| 接口                                             | 接口说明           | 维护状态 |
| ------------------------------------------------ | ------------------ | -------- |
| [/api/v3/guild-emoji/list](#获取服务器表情列表) | 获取服务器表情列表 | 正常     |
| [/api/v3/guild-emoji/create](#创建服务器表情)    | 创建服务器表情     | 正常     |
| [/api/v3/guild-emoji/update](#更新服务器表情)    | 更新服务器表情     | 正常     |
| [/api/v3/guild-emoji/delete](#删除服务器表情)    | 删除服务器表情     | 正常     |

## 获取服务器表情列表

### 接口说明
|地址|请求方式|说明|
|--|--|--|
|`/api/v3/guild-emoji/list`|GET| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| guild_id   | string  | 是    | GET | 服务器的id                 |

### 返回参数说明

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |
|name|string|表情的名称|
|id|string|表情的 ID|
|user_info|map|上传用户，具体参考 [用户相关接口](https://developer.kaiheila.cn/doc/http/user) |


### 返回示例

```javascript
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
        meta: {//参考标准格式},
        sort: {//参考标准格式}
    }
}
```

## 创建服务器表情

### 接口说明
| 地址                         | 请求方式 | 说明 |
| ---------------------------- | -------- | ---- |
| `/api/v3/guild-emoji/create` | POST     | Header 中 `Content-Type` 必须为 `multipart/form-data`      |

### 参数列表

| 参数名   | 类型   | 必传 | 参数区域 | 说明                                                   |
| -------- | ------ | ---- | -------- | ------------------------------------------------------ |
| name     | string | 否   | POST     | 表情名。长度限制 2 - 32 字符，如果不写，则为随机字符串 |
| guild_id | string | 是   | POST     | 服务器 ID                                              |
| emoji    | file   | 是   | POST     | 表情文件。必须为 PNG 类型，大小不能超过 256 KB         |

### 返回参数说明

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |
|name|string|表情的名称|
|id|string|表情的 ID|
|user_info|map|上传用户，具体参考 [用户相关接口](https://developer.kaiheila.cn/doc/http/user) |

### 返回示例

```javascript
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
            "os": "Websocket",
            "status": 1,
            "avatar": "https://chuanyuapp.oss-cn-qingdao.aliyuncs.com/assets/bot.png/icon"
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

| 参数名 | 类型   | 必传 | 参数区域 | 说明                                                   |
| ------ | ------ | ---- | -------- | ------------------------------------------------------ |
| name   | string | 是   | POST     | 表情名。长度限制 2 - 32 字符，如果不写，则为随机字符串 |
| id     | string | 是   | POST     | 表情 ID                                                |


### 返回参数说明

无返回参数

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": []
}
```

## 删除服务器表情

### 接口说明

| 地址                         | 请求方式 | 说明 |
| ---------------------------- | -------- | ---- |
| `/api/v3/guild-emoji/delete` | POST     |      |

### 参数列表

| 参数名 | 类型   | 必传 | 参数区域 | 说明                                                   |
| ------ | ------ | ---- | -------- | ------------------------------------------------------ |
| id     | string | 是   | POST     | 表情 ID                                                |


### 返回参数说明

无返回参数

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": []
}
```

