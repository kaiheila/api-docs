# 服务器相关接口列表
本文档主要列出服务器相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kaiheila.cn/doc/reference)。

| 接口                                             | 接口说明           | 维护状态 |
| ------------------------------------------------ | ------------------ | -------- |
| [/api/v3/guild/list](#获取当前用户加入的服务器列表)    | 获取当前用户加入的服务器列表     | 正常 |
| [/api/v3/guild/view](#获取服务器详情)    | 获取服务器详情     | 正常 |
| [/api/v3/guild/user-list](#获取服务器中的用户列表)    | 获取服务器中的用户列表     | 正常 |
| [/api/v3/guild/nickname](#修改服务器中用户的昵称)    | 修改服务器中用户的昵称     | 正常 |
| [/api/v3/guild/leave](#离开服务器)    | 离开服务器     | 正常 |
| [/api/v3/guild/kickout](#踢出服务器)    | 踢出服务器     | 正常 |
| [/api/v3/guild-mute/list](#服务器静音闭麦列表)    | 服务器静音闭麦列表     | 正常 |
| [/api/v3/guild-mute/create](#添加服务器静音或闭麦)    | 添加服务器静音或闭麦     | 正常 |
| [/api/v3/guild-mute/delete](#删除服务器静音或闭麦)    | 删除服务器静音或闭麦     | 正常 |

## 获取当前用户加入的服务器列表

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/guild/list` | GET     |      |

### 参数列表

| 参数名   | 类型   | 必传 | 参数区域 | 说明                                                  |
| -------- | ------ | ---- | -------- | ----------------------------------------------------- |

### 返回参数说明

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |
|id|string|服务器id|
|name|string|服务器名称|
|topic|string|服务器主题|
|master_id|string|服务器主的id|
|is_master|boolean|当前用户是否为服务器主|
|icon|string|服务器icon的地址|
|invite_enabled|boolean|是否开启邀请|
|notify_type|int|通知类型, `0`代表默认使用服务器通知设置，`1`代表接收所有通知, `2`代表仅@被提及，`3`代表不接收通知|
|region|string|服务器默认使用语音区域|
|enable_open|boolean|是否为公开服务器|
|open_id|string|公开服务器id|
|default_channel_id|string|默认频道id|
|welcome_channel_id|string|欢迎频道id|


### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "items": [
            {
                "id": "xxx",
                "name": "test",
                "topic": "",
                "master_id": "xxx",
                "is_master": false,
                "icon": "",
                "invite_enabled": 1,
                "notify_type": 2,
                "region": "beijing",
                "enable_open": 0,
                "open_id": "0",
                "default_channel_id": "xxx",
                "welcome_channel_id": "xxx"
            }
        ],
        "meta": {
            "page": 1,
            "page_total": 1,
            "page_size": 100,
            "total": 2
        },
        "sort": {
            "id": 1
        }
    }
}
```

## 获取服务器详情

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/guild/view` | GET     |      |

### 参数列表

| 参数名   | 类型   | 必传 | 参数区域 | 说明     |
| -------- | ------ | ---- | -------- | -------- |
| guild_id | string | 是   | GET      | 服务器id |

### 返回参数说明

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |
|id|string|服务器id|
|name|string|服务器名称|
|topic|string|服务器主题|
|master_id|string|服务器主的id|
|icon|string|服务器icon的地址|
|invite_enabled|boolean|是否开启邀请|
|notify_type|int|通知类型, `0`代表默认使用服务器通知设置，`1`代表接收所有通知, `2`代表仅@被提及，`3`代表不接收通知|
|region|string|服务器默认使用语音区域|
|enable_open|boolean|是否为公开服务器|
|open_id|string|公开服务器id|
|default_channel_id|string|默认频道id|
|welcome_channel_id|string|欢迎频道id|
|roles|array|角色列表|
|channels|array|频道列表|


### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "id": "91686000000",
        "name": "Hello",
        "topic": "",
        "master_id": "17000000",
        "is_master": false,
        "icon": "",
        "invite_enabled": true,
        "notify_type": 2,
        "region": "beijing",
        "enable_open": true,
        "open_id": "1600000",
        "default_channel_id": "2710000000",
        "welcome_channel_id": "0",
        "features": [],
        "roles": [
            {
                "role_id": 0,
                "name": "@全体成员",
                "color": 0,
                "position": 999,
                "hoist": 0,
                "mentionable": 0,
                "permissions": 148691464
            }
        ],
        "channels": [
            {
                "id": "37090000000",
                "user_id": "1780000000",
                "parent_id": "0",
                "name": "Hello World",
                "type": 1,
                "level": 100,
                "limit_amount": 0,
                "is_category": false,
                "is_readonly": false,
                "is_private": false
            }
        ],
        "emojis": [
            {
                "name": "ceeb65XXXXXXX0j60jpwfu",
                "id": "9168XXXXX53/4c43fcb7XXXXX0c80ck"
            }
        ],
        "user_config": {
            "notify_type": null,
            "nickname": "XX",
            "role_ids": [
                702
            ],
            "chat_setting": "1"
        }
    }
}
```

## 获取服务器中的用户列表

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/guild/user-list` | GET     |      |

### 参数列表

| 参数名   | 类型   | 必传 | 参数区域 | 说明        |
| -------- | ------ | ---- | -------- | ----------- |
| guild_id | string | 是   | GET      | 服务器的 ID |
| channel_id | string | 否   | GET      | 服务器中频道的 ID |
| search | string | 否   | GET      | 搜索关键字，在用户名或昵称中搜索 |
| role_id | int | 否   | GET      | 角色 ID，获取特定角色的用户列表 |
| mobile_verified | int | 否   | GET      | 只能为`0`或`1`，`0`是未认证，`1`是已认证 |
| active_time | int | 否   | GET      | 根据活跃时间排序，`0`是顺序排列，`1`是倒序排列 |
| joined_at | int | 否   | GET      | 根据加入时间排序，`0`是顺序排列，`1`是倒序排列 |
| page | int | 否   | GET      | 目标页 |
| page_size | int | 否   | GET      | 每页数据数量 |

### 返回参数说明

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |
|user_count|int|用户数量|
|online_count|int|在线用户数量|
|offline_count|int|离线用户数量|
|items|array (User)|用户列表|

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "items": [
            {
                "id": "444",
                "username": "***",
                "avatar": "https://**.jpg",
                "online": true,
                "nickname": "***",
                "joined_at": 1611743334000,
                "active_time": 1612691445583,
                "roles": [],
                "is_master": true,
                "abbr": "***",
            }
        ],
        "user_count": 2,
        "online_count": 1,
        "offline_count": 1
    }
}
```

##  修改服务器中用户的昵称

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/guild/nickname` | POST     |      |

### 参数列表

| 参数名   | 类型   | 必传 | 参数区域 | 说明                                                  |
| -------- | ------ | ---- | -------- | ----------------------------------------------------- |
| guild_id | string | 是   | POST     | 服务器的 ID                                           |
| nickname | string | 否   | POST     | 昵称，2 - 64 长度，不传则清空昵称                     |
| user_id  | string | 否   | POST     | 要修改昵称的目标用户 ID，不传则修改当前登陆用户的昵称 |

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

## 离开服务器

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/guild/leave` | POST     |      |

### 参数列表

| 参数名   | 类型   | 必传 | 参数区域 | 说明                                                  |
| -------- | ------ | ---- | -------- | ----------------------------------------------------- |
| guild_id | string | 是 | POST |服务器id|

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

## 踢出服务器

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/guild/kickout` | POST     |      |

### 参数列表

| 参数名   | 类型   | 必传 | 参数区域 | 说明                                                  |
| -------- | ------ | ---- | -------- | ----------------------------------------------------- |
| guild_id | string | 是 | POST |服务器ID|
| target_id | string | 是 | POST |目标用户ID|

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

## 服务器静音闭麦列表

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/guild-mute/list` | GET     |      |

### 参数列表

| 参数名   | 类型   | 必传 | 参数区域 | 说明                                                  |
| -------- | ------ | ---- | -------- | ----------------------------------------------------- |
| guild_id | string | 是 | GET |服务器id|
| return_type | string | 否 | GET |返回格式，建议为"detail"|

### 返回参数说明
返回格式中，type值,`1`代表麦克风闭麦，`2`代表耳机静音。

### 返回示例

```javascript
//如果return_type = "detail", 返回如下：
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "mic": {
            "type": 1,
            "user_ids": [
                "xxx"
            ]
        },
        "headset": {
            "type": 2,
            "user_ids": []
        }
    }
}
// 否则返回这个格式
{
    "code": 0,
    "message": "操作成功",
    "data": {
        1 : ["1212", "121"],
        2 : ["123"],
    }
}

```


## 添加服务器静音或闭麦

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/guild-mute/create` | POST     |      |

### 参数列表

| 参数名   | 类型   | 必传 | 参数区域 | 说明                                                  |
| -------- | ------ | ---- | -------- | ----------------------------------------------------- |
| guild_id | string | 是 | POST |服务器id|
| user_id | string | 是 | POST |用户id|
| type | string | 是 | POST |`1`代表麦克风闭麦，`2`代表耳机静音|

### 返回参数说明
无

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": []
}
```


## 删除服务器静音或闭麦

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/guild-mute/delete` | POST     |      |

### 参数列表

| 参数名   | 类型   | 必传 | 参数区域 | 说明                                                  |
| -------- | ------ | ---- | -------- | ----------------------------------------------------- |
| guild_id | string | 是 | POST |服务器id|
| user_id | string | 是 | POST |用户id|
| type | string | 是 | POST |`1`代表麦克风闭麦，`2`代表耳机静音|

### 返回参数说明
无

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": []
}
```




