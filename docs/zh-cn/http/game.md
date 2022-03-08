# 用户动态相关接口-游戏/进程/音乐
本文档主要列出用户动态相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kaiheila.cn/doc/reference)。


|接口|接口说明|维护状态|
|---|---|---|
|[/api/v3/game](#游戏列表)|游戏列表|正常|
|[/api/v3/game/create](#添加游戏)|添加游戏|正常|
|[/api/v3/game/update](#更新游戏)|更新游戏|正常|
|[/api/v3/game/delete](#删除游戏)|删除游戏|正常|
|[/api/v3/game/activity](#添加游戏记录-开始玩)|添加游戏记录(开始玩)|正常|
|[/api/v3/game/delete-activity](#删除游戏记录-结束玩)|删除游戏记录(结束玩)|正常|

## 游戏列表

### 接口说明

| 地址                   | 请求方式 | 说明 |
| ---------------------- | -------- | ---- |
| /api/v3/game | GET     |      |


### 返回参数说明
## object-game
| 参数名 | 类型 | 说明 |
| -------------------- | ---- | ---- |
|id | int | 主键id |
|name | string | 名称（游戏/状态名称） |
|type | int | 类型 0游戏 1VUP 2进程 |
|options | string | 进程额外信息 |
|kmhook_admin | bool | 是否以管理员权限启动开黑啦 |
|process_name | array | 进程名称 |
|product_name | array | 产品名称 |
|icon | string | 游戏图标 |


### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "items": [
            {
                "id": 111,
                "name": "CS",
                "type": 0,
                "options": "",
                "kmhook_admin": false,
                "process_name": [
                    "cstrike"
                ],
                "product_name": [],
                "icon": "https://img.chuanyuapp.com/assets/2022-01/12fe639ebc762e0e5347d197b9686c0c.ico/icon"
            },
        ],
        "meta": {
            "page": 2,
            "page_total": 2,
            "page_size": 100,
            "total": 103
        },
        "sort": {}
    }
}
```

## 添加游戏

### 接口说明

| 地址                   | 请求方式 | 说明 |
| ---------------------- | -------- | ---- |
| /api/v3/game/create | POST     |      |

### 参数列表

| 参数名 | 类型 | 是否必填| 说明 |
| ----- | ---- | ---- | ---- | 
|name | string | 是 | 名称 |
|process_name| string | 否 | 进程名 |

### 返回参数说明 
<[object-game](#object-game)>

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "id": 111,
        "name": "开黑啦",
        "type": 0,
        "options": "",
        "kmhook_admin": false,
        "process_name": [],
        "product_name": [],
        "icon": ""
    }
}
```

## 更新游戏

### 接口说明

| 地址                   | 请求方式 | 说明 |
| ---------------------- | -------- | ---- |
| /api/v3/game/update | POST     |      |

### 参数列表

| 参数名 | 类型 | 是否必填| 说明 |
| ----- | ---- | ---- | ---- | 
|id | int | 是 | 名称 |
|name | string | 否 | 名称 |
|icon| string | 否 | 图标 |

### 返回参数说明 
<[object-game](#object-game)>

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "id": 111,
        "name": "开黑啦",
        "type": 0,
        "options": "",
        "kmhook_admin": false,
        "icon": "https://xxx.com/xxxxxxxxx...",
        "process_name": [],
        "product_name": []
    }
}
```

## 删除游戏

### 接口说明

| 地址                   | 请求方式 | 说明 |
| ---------------------- | -------- | ---- |
| /api/v3/game/delete | POST     |      |

### 参数列表

| 参数名 | 类型 | 是否必填| 说明 |
| ----- | ---- | ---- | ---- | 
|id | int | 是 | 主键id |

### 返回参数说明 


### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {}
}
```

## 添加游戏记录-开始玩

### 接口说明

| 地址                   | 请求方式 | 说明 |
| ---------------------- | -------- | ---- |
| /api/v3/game/activity | POST     |      |

### 参数列表

| 参数名     | 类型   | 必传 | 参数区域 | 说明   |
| ---------- | ------ | ---- | -------- | ------ |
| id      | int | 是  | POST    | 游戏id |
| data_type | int | 是  | POST  | 请求数据类型 固定传1(游戏)  |

### 返回参数说明 

### 传参示例

### 返回示例
```
{"id":466,"data_type":1}
```

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {}
}
```

## 删除游戏记录-结束玩

### 接口说明

| 地址                   | 请求方式 | 说明 |
| ---------------------- | -------- | ---- |
| /api/v3/game/delete-activity | POST     |      |

### 参数列表

### 返回参数说明 
| data_type | int | 是  | POST  | 请求数据类型 固定传1(游戏)   |

### 传参示例
```
{"data_type": 1}
```

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {}
}
```












