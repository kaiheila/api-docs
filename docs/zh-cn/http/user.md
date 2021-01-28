# 用户相关接口列表
本文档主要列出用户相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kaiheila.cn/doc/reference)。


|接口|接口说明|维护状态|
|--|--|--|
|[/api/v3/user/me](#获取当前用户信息)|获取当前用户信息|正常|


## 获取当前用户信息

### 接口说明
|地址|请求方式|说明|
|--|--|--|
|`/api/v3/user/me`|GET|获取当前登录的用户的信息|

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |

### 返回参数说明

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |
|id | string       | 用户的id                                       |     
|username | string          | 用户的名称                                         |     
|identify_num | string |用户名的认证数字，用户名正常为：user_name#identify_num |
|online| boolean| 当前是否在线|
|status|int|用户的状态, 0代表正常，10代表被封禁|
|avatar|string|用户的头像的url地址|
|bot|boolean|用户是否为机器人|
|mobile_verified|boolean|是否手机号已验证|
|system|boolean|是否为官方账号|
|mobile_prefix|string|手机区号,如中国为86|
|mobile|string|用户手机号，带掩码|
|invited_count|int|当前邀请注册的人数|


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
        "mobile": "****",
        "invited_count" : 0,
    }
}
```
