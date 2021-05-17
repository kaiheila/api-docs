# 邀请相关接口
本文档主要列出邀请相关的接口。  
本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kaiheila.cn/doc/reference)。


|接口|接口说明|维护状态|
|--|--|--|
|[/api/v3/invite/list](#获取邀请列表)|获取邀请列表|正常|
|[/api/v3/invite/create](#创建邀请链接)|创建邀请链接|正常|
|[/api/v3/invite/delete](#删除邀请链接)|删除邀请链接|正常|

## 获取邀请列表

### 接口说明

|地址|请求方式|说明|
|--|--|--|
|/api/v3/invite/list|GET| |

### 参数列表
|参数名|类型|参数区域|是否必填|说明|
|--|--|--|--|--|
|guild_id|string|GET|否|服务器id, 服务器id或者频道id必须填一个|
|channel_id|string|GET|否|频道id|

### 返回参数说明

|参数名|类型|说明|
|--|--|--|
|guild_id|string|服务器id|
|channel_id|string|频道id|
|url_code|string|url code|
|url|string|地址|
|user|object|用户,参见[user](https://developer.kaiheila.cn/doc/objects)|

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "items":[
            "channel_id": "xxxxx",
            "guild_id": "xxxx",
            "url_code": "xxx",
            "url": "https://kaihei.co/xxxx",
            "user": {}, //... 
        ],
        "meta": {
            "page": 1,
            "page_total": 1,
            "page_size": 50,
            "total": 1
        },
        "sort": {}
    }
}
```

## 创建邀请链接 

### 接口说明

|地址|请求方式|说明|
|--|--|--|
|/api/v3/invite/create|POST| |

### 参数列表
|参数名|类型|参数区域|是否必填|说明|
|--|--|--|--|--|
|guild_id|string|POST|否|服务器id, 服务器id或者频道id必须填一个|
|channel_id|string|POST|否|频道id|

### 返回参数说明

|参数名|类型|说明|
|--|--|--|
|url|string|地址|

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "url": "https://kaihei.co/xxxx",
    }
}
```

## 删除邀请链接 

### 接口说明

|地址|请求方式|说明|
|--|--|--|
|/api/v3/invite/delete|POST|  |

### 参数列表
|参数名|类型|参数区域|是否必填|说明|
|--|--|--|--|--|
|guild_id|string|POST|否|服务器id, 服务器id或者频道id必须填一个|
|channel_id|string|POST|否|频道id|
|url_code|string|POST|是|url_code|

### 返回参数说明

|参数名|类型|说明|
|--|--|--|

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {}
}
```

