# message
本文档主要列出私聊消息相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kaiheila.cn/doc/reference)。


|接口|接口说明|维护状态|
|--|--|--|
|[/api/v3/user-chat/reaction-list](#获取频道消息某回应的用户列表)|获取频道消息某个回应的用户列表|正常|
|[/api/v3/user-chat/add-reaction](#给某个消息添加回应)|给某个消息添加回应|正常|
|[/api/v3/user-chat/reaction-list](#删除消息的某个回应)|删除消息的某个回应|正常|


## 获取频道消息某回应的用户列表 

### 接口说明
|地址|请求方式|说明|
|--|--|--|
|`/api/v3/user-chat/reaction-list`|GET| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| msg_id | string  | 是    | GET |频道消息的id|
| emoji |string|是|GET| emoji的id, 可以为GuilEmoji或者Emoji, 注意：在get中，应该进行urlencode|

### 返回参数说明

返回的是用户的列表，参数如下：

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |
| id | string       |   用户的id                                    |     
|username | string          | 用户的名称                                         |     
|nickname | string          | 用户在服务器内的呢称                               |     
|identify_num | string |用户名的认证数字，用户名正常为：user_name#identify_num |
|online| boolean| 当前是否在线|
|status|int|用户的状态, 0代表正常，10代表被封禁|
|avatar|string|用户的头像的url地址|
|bot|boolean|用户是否为机器人|
|reaction_time|intval|用户点击reaction的毫秒时间戳|

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        {
            "id": "xxxx",
            "username": "test",
            "identify_num": "xxx",
            "online": false,
            "status": 0,
            "avatar": "xxxx",
            "bot": true,
            "nickname": "xxxx",
            "reaction_time": 1612323994414
        } 
    }
}
```

## 给某个消息添加回应 

### 接口说明
|地址|请求方式|说明|
|--|--|--|
|`/api/v3/user-chat/add-reaction`|POST| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| msg_id | string  | 是    | POST |频道消息的id|
| emoji |string|是|POST| emoji的id, 可以为GuilEmoji或者Emoji|

### 返回参数说明

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": []
}
```

## 删除消息的某个回应

### 接口说明
|地址|请求方式|说明|
|--|--|--|
|`/api/v3/user-chat/delete-reaction`|POST| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| msg_id | string  | 是    | POST |频道消息的id|
| emoji |string|是|POST| emoji的id, 可以为GuilEmoji或者Emoji|

### 返回参数说明

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": []
}
```
