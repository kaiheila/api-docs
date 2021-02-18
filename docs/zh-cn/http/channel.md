# 频道相关接口列表
本文档主要列出频道相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kaiheila.cn/doc/reference)。


|接口|接口说明|维护状态|
|--|--|--|
|[/api/v3/channel/message](https://developer.kaiheila.cn/doc/http/message#发送频道聊天消息)|发送频道聊天消息|已弃用|
|[/api/v3/channel-role/index](#频道角色权限详情)|获取频道角色权限详情|正常|
|[/api/v3/channel-role/create](#创建频道角色权限)|创建频道角色权限|正常|
|[/api/v3/channel-role/update](#更新频道角色权限)|更新频道角色权限|正常|
|[/api/v3/channel-role/delete](#删除频道角色权限)|删除频道角色权限|正常|

## 频道角色权限详情

### 接口说明
|地址|请求方式|说明|
|--|--|--|
|`/api/v3/channel-role/index`|GET| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
|channel_id|string|是|GET|频道id|

### 返回参数说明

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |
|permission_overwrites|Array|频道权限覆写的角色列表, role_id为角色id, 其它字段见下表|
|permission_users|Array|频道权限覆写的用户列表, user字段参见[用户接口](https://developer.kaiheila.cn/doc/http/user#%E8%8E%B7%E5%8F%96%E5%BD%93%E5%89%8D%E7%94%A8%E6%88%B7%E4%BF%A1%E6%81%AF), 其它的见下表|
|permission_sync|int|是否同步分组的权限|

其它参数说明：

|参数名|类型|说明|
|--|--|--|
|allow|int|最终修改成功后，允许的权限的结果集|
|deny|int|最终修改成功后，拒绝的权限的结果集|

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "permission_overwrites": [
            {
                "role_id": 7,
                "allow": 0,
                "deny": 0
            },
            {
                "role_id": 0,
                "allow": 0,
                "deny": 0
            }
        ],
        "permission_users": [
            {
                "user": {
                    "id": "0",
                    "username": "花荣",
                    "identify_num": "12",
                    "online": true,
                    "os": "Websocket",
                    "status": 1,
                    "avatar": "xxxx",
                    "mobile_verified": true,
                    "nickname": "test",
                    "roles": [],
                    "joined_at": 1602596021000,
                    "active_time": 1612703344396
                },
                "allow": 0,
                "deny": 0
            } 
        ],
        "permission_sync": 0 
    }
}
```


## 创建频道角色权限

### 接口说明
|地址|请求方式|说明|
|--|--|--|
|`/api/v3/channel-role/create`|POST| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
|channel_id|string|是|POST|频道id, 如果频道是分组的id,会同步给所有sync=1的子频道|
|type|string|否|POST|value的类型，只能为"role_id","user_id",不传则默认为"role_id"|
|value|string|否|POST|value的值|


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
## 更新频道角色权限

### 接口说明
|地址|请求方式|说明|
|--|--|--|
|`/api/v3/channel-role/update`|POST| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
|channel_id|string|是|POST|频道id, 如果频道是分组的id,会同步给所有sync=1的子频道|
|type|string|否|POST|value的类型，只能为"role_id","user_id",不传则默认为"role_id"|
|value|string|否|POST|value的值|
|allow|int|否|POST|默认为0,想要设置的允许的权限值|
|deny|int|否|POST|默认为0,想要设置的拒绝的权限值|

### 返回参数说明

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |
|user_id/role_id| int|根据用户的type，返回不同的参数名|
|allow|int|同上|
|deny|int|同上|

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "role" : 0,
        "allow" : 0,
        "deny" : 0
    }
}
```

## 删除频道角色权限

### 接口说明
|地址|请求方式|说明|
|--|--|--|
|`/api/v3/channel-role/delete`|POST| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
|channel_id|string|是|POST|频道id, 如果频道是分组的id,会同步给所有sync=1的子频道|
|type|string|否|POST|value的类型，只能为"role_id","user_id",不传则默认为"role_id"|
|value|string|否|POST|value的值，默认为0|

### 返回参数说明

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
    }
}
```


