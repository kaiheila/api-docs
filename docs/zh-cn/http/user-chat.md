# 私信聊天会话接口列表
本文档主要列出私聊消息相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kaiheila.cn/doc/reference)。


|接口|接口说明|维护状态|
|--|--|--|
|[/api/v3/user-chat/index](#获取私信聊天会话列表)|获取私信聊天会话列表|正常|
|[/api/v3/user-chat/view](#获取私信聊天会话详情)|获取私信聊天会话详情|正常|
|[/api/v3/user-chat/create](#创建私信聊天会话)|创建私信聊天会话|正常|
|[/api/v3/user-chat/delete](#删除私信聊天会话)|删除私信聊天会话|正常|

## 获取私信聊天会话列表

### 接口说明

|地址|请求方式|说明|
|--|--|--|
|`/api/v3/user-chat/index`|GET| |

### 参数列表

无请求参数

### 返回参数说明

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |
| code | string | 私信会话 Code                        |
| last_read_time | int | 上次阅读消息的时间 |
| latest_msg_time | int | 最新消息时间 |
| unread_count | int | 未读消息数 |
| target_info | map | 目标用户信息 |
| ↳ id | string        | 目标用户 ID |
| ↳ username | string        | 目标用户名 |
| ↳ online | boolean  | 是否在线 |
| ↳ avatar | string        | 头像图片链接 |


### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": [
        {
            "code": "sderwrw**",
            "last_read_time": 1612696873000,
            "latest_msg_time": 1612696873000,
            "unread_count": 0,
            "target_info": {
                "id": "415212",
                "username": "工具",
                "online": false,
                "avatar": "https://***.jpg"
            },
        }
    ]
}
```

## 获取私信聊天会话详情

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/user-chat/view` | GET      |      |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| chat_code | string  | 是    | GET | 私聊会话 Code                          |

### 返回参数说明

| 参数名       | 类型          | 说明          |
| ------------ | ------------- | ------------- |
| code         | string        | 私信会话 Code |
| last_read_time | int | 上次阅读消息的时间 |
| latest_msg_time | int | 最新消息时间 |
| unread_count | int           | 未读消息数    |
| is_friend | boolean   | 是否是好友                                     |
| is_blocked | boolean |是否已屏蔽对方 |
| is_target_blocked | boolean    | 是否已被对方屏蔽                                  |
| target_info | map | 目标用户信息 |
| ↳ id | string        | 目标用户 ID |
| ↳ username | string        | 目标用户名 |
| ↳ avatar | string        | 头像图片链接 |

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "code": "5c7ec6d021216c136c9198285c15ed47",
        "last_read_time": 1612175653000,
        "latest_msg_time": 1612160693000,
        "unread_count": 0,
        "is_friend": false,
        "is_blocked": false,
        "is_target_blocked": false,
        "target_info": {
            "id": "3903536527",
            "username": "夏天1",
            "avatar": "https://chuanyuapp.oss-cn-qingdao.aliyuncs.com/assets/avatar_10.jpg/icon",
        }
    }
}
```

## 创建私信聊天会话

### 接口说明

|地址|请求方式|说明|
|--|--|--|
|`/api/v3/user-chat/create`|POST| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| target_id | string  | 是    | POST | 目标用户 id                                  |

### 返回参数说明

具体参数参考列表与详情

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "code": "3547b7*****2476dd9d7777f32a",
        "last_read_time": 1612697864000,
        "latest_msg_time": 1612168629000,
        "unread_count": 0,
        "is_friend": false,
        "is_blocked": false,
        "is_target_blocked": false,
        "target_info": {
            "id": "325***0",
            "username": "工具",
            "online": false,
            "avatar": "https://**.jpg"
        }
    }
}
```

## 删除私信聊天会话

### 接口说明

只能删除自己的消息。

| 地址                       | 请求方式 | 说明 |
| -------------------------- | -------- | ---- |
| `/api/v3/user-chat/delete` | POST     |      |

### 参数列表

| 参数名    | 类型   | 必传 | 参数区域 | 说明          |
| --------- | ------ | ---- | -------- | ------------- |
| chat_code | string | 是   | POST     | 私信会话 Code |

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
