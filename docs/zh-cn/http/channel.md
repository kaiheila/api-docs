# 频道相关接口列表
本文档主要列出频道相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kaiheila.cn/doc/reference)。


|接口|接口说明|维护状态|
|--|--|--|
|[/api/v3/channel/message](https://developer.kaiheila.cn/doc/http/message#发送频道聊天消息)|发送频道聊天消息|已弃用|
|[/api/v3/channel/list](#获取频道列表)|获取频道列表|正常|
|[/api/v3/channel/view](#获取频道详情)|获取频道详情|正常|
|[/api/v3/channel/create](#创建频道)|创建频道|正常|
|[/api/v3/channel/delete](#删除频道)|删除频道|正常|
|[/api/v3/channel/move-user](#语音频道之间移动用户)|语音频道之间移动用户|正常|
|[/api/v3/channel-role/index](#频道角色权限详情)|获取频道角色权限详情|正常|
|[/api/v3/channel-role/create](#创建频道角色权限)|创建频道角色权限|正常|
|[/api/v3/channel-role/update](#更新频道角色权限)|更新频道角色权限|正常|
|[/api/v3/channel-role/delete](#删除频道角色权限)|删除频道角色权限|正常|

## 获取频道列表

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/channel/list` | GET     |      |

### 参数列表

| 参数名   | 类型   | 必传 | 参数区域 | 说明                                                  |
| -------- | ------ | ---- | -------- | ----------------------------------------------------- |
| guild_id | string | 是 | GET | 服务器id |

### 返回参数说明

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |
|id|string|频道id|
|master_id|string|频道创建者id|
|parent_id|string|父分组频道id|
|name|string|频道名称|
|type|int|频道类型|
|level|int|频道排序|
|limit_amount|int|人数限制|
|is_category|boolean|是否为分组类型|


### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "items": [
            {
                "id": "7480000000000000",
                "master_id": "1700000",
                "parent_id": "",
                "name": "语音分组",
                "type": 0,
                "level": 100,
                "limit_amount": 0,
                "is_category": true
            },
            {
                "id": "3321010478582002",
                "master_id": "1700000",
                "parent_id": "7480000000000000",
                "name": "语音频道",
                "type": 2,
                "level": 100,
                "limit_amount": 25,
                "is_category": false
            },
        ],
        "meta": {
            "page": 1,
            "page_total": 1,
            "page_size": 50,
            "total": 2
        },
        "sort": []
    }
}
```

## 获取频道详情

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/channel/view` | GET     |      |

### 参数列表

| 参数名   | 类型   | 必传 | 参数区域 | 说明                                                  |
| -------- | ------ | ---- | -------- | ----------------------------------------------------- |
| target_id | string | 是 | GET | 频道id |

### 返回参数说明

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |
|id|string|频道id|
|guild_id|string|服务器id|
|master_id|string|频道创建者id|
|parent_id|string|父分组频道id|
|name|string|频道名称|
|topic|string|频道简介|
|type|int|频道类型，`1` 文字，`2` 语音|
|level|int|频道排序|
|slow_mode|int|慢速限制，单位秒。用户发送消息之后再次发送消息的等待时间。|
|limit_amount|int|人数限制|
|is_category|boolean|是否为分组类型|
|server_url|string|语音服务器地址，`HOST:PORT`的格式|


### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "id": "00000000000000000000000",
        "guild_id": "00000000000000000000000",
        "master_id": "00000000000000000000000",
        "parent_id": "00000000000000000000000",
        "name": "语音频道",
        "topic": "",
        "type": 1,
        "level": 100,
        "slow_mode": 0,
        "limit_amount": 0,
        "voice_quality": 1,
        "is_category": false,
        "server_url": "hostname:prot"
    }
}
```

## 创建频道

### 接口说明
|地址|请求方式|说明|
|--|--|--|
|`/api/v3/channel/create`|POST| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
|guild_id|string|是|POST|服务器id|
|parent_id|string|否|POST|父分组id|
|name|string|是|POST|频道名称|
|type|int|否|POST|频道类型，`1` 文字，`2` 语音，默认为`1`|
|limit_amount|int|否|POST|语音频道人数限制，最大`99`|
|voice_quality|int|否|POST|语音音质，默认为`2`。`1`流畅，`2`正常，`3`高质量|


### 返回参数说明

返回参数为创建成功的频道信息，可以参考 [获取频道详情](#获取频道详情) 接口。

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "id": "00000000000000000000000",
        "guild_id": "00000000000000000000000",
        "master_id": "00000000000000000000000",
        "parent_id": "00000000000000000000000",
        "name": "语音频道",
        "topic": "",
        "type": 1,
        "level": 100,
        "slow_mode": 0,
        "limit_amount": 0,
        "voice_quality": 1,
        "is_category": false,
        "server_type": 0,
        "server_url": "hostname:prot"
    }
}
```

## 删除频道

### 接口说明
|地址|请求方式|说明|
|--|--|--|
|`/api/v3/channel/delete`|POST| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
|channel_id|string|是|POST|频道id|


### 返回参数说明


### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {}
}
```


## 语音频道之间移动用户

### 接口说明

只能在语音频道之间移动，用户也必须在其他语音频道在线才能够移动到目标频道。

|地址|请求方式|说明|
|--|--|--|
|`/api/v3/channel/move-user`|POST| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
|target_id|string|是|POST|目标频道id, 需要是语音频道|
|user_ids|array|是|POST|用户id的数组|


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
|type|string|否|POST|value的类型，只能为"role_id","user_id",不传则默认为"user_id"|
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
|type|string|否|POST|value的类型，只能为"role_id","user_id",不传则默认为"user_id"|
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
|type|string|否|POST|value的类型，只能为"role_id","user_id",不传则默认为"user_id"|
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


