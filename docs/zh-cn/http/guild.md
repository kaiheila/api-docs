# 服务器相关接口列表

本文档主要列出服务器相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kookapp.cn/doc/reference)。

| 接口                                                | 接口说明                     | 维护状态 |
| --------------------------------------------------- | ---------------------------- | -------- |
| [/api/v3/guild/list](#获取当前用户加入的服务器列表) | 获取当前用户加入的服务器列表 | 正常     |
| [/api/v3/guild/view](#获取服务器详情)               | 获取服务器详情               | 正常     |
| [/api/v3/guild/user-list](#获取服务器中的用户列表)  | 获取服务器中的用户列表       | 正常     |
| [/api/v3/guild/nickname](#修改服务器中用户的昵称)   | 修改服务器中用户的昵称       | 正常     |
| [/api/v3/guild/leave](#离开服务器)                  | 离开服务器                   | 正常     |
| [/api/v3/guild/kickout](#踢出服务器)                | 踢出服务器                   | 正常     |
| [/api/v3/guild-mute/list](#服务器静音闭麦列表)      | 服务器静音闭麦列表           | 正常     |
| [/api/v3/guild-mute/create](#添加服务器静音或闭麦)  | 添加服务器静音或闭麦         | 正常     |
| [/api/v3/guild-mute/delete](#删除服务器静音或闭麦)  | 删除服务器静音或闭麦         | 正常     |
| [/api/v3/guild-boost/history](#服务器助力历史)      | 查询服务器的助力包历史       | 正常     |

## 获取当前用户加入的服务器列表

### 接口说明

| 地址                 | 请求方式 | 说明 |
| -------------------- | -------- | ---- |
| `/api/v3/guild/list` | GET      |      |

### 参数列表

| 参数名    | 位置  | 类型    | 必需  | 说明                                                                                                                 |
| --------- | ----- | ------- | ----- | -------------------------------------------------------------------------------------------------------------------- |
| page      | query | integer | false | 目标页数                                                                                                             |
| page_size | query | integer | false | 每页数据数量                                                                                                         |
| sort      | query | string  | false | 代表排序的字段, 比如-id 代表 id 按 DESC 排序，id 代表 id 按 ASC 排序。不一定有, 如果有，接口中会声明支持的排序字段。 |

### 返回参数说明

| 参数名             | 类型    | 说明                                                                                              |
| ------------------ | ------- | ------------------------------------------------------------------------------------------------- |
| id                 | string  | 服务器 id                                                                                         |
| name               | string  | 服务器名称                                                                                        |
| topic              | string  | 服务器主题                                                                                        |
| user_id            | string  | 服务器主的 id                                                                                     |
| icon               | string  | 服务器 icon 的地址                                                                                |
| notify_type        | int     | 通知类型, `0`代表默认使用服务器通知设置，`1`代表接收所有通知, `2`代表仅@被提及，`3`代表不接收通知 |
| region             | string  | 服务器默认使用语音区域                                                                            |
| enable_open        | boolean | 是否为公开服务器                                                                                  |
| open_id            | string  | 公开服务器 id                                                                                     |
| default_channel_id | string  | 默认频道 id                                                                                       |
| welcome_channel_id | string  | 欢迎频道 id                                                                                       |
| boost_num          | integer | 服务器助力数量                                                                                    |
| level              | integer | 服务器等级                                                                                        |

#### 枚举值

| 属性        | 属性值 |
| ----------- | ------ |
| notify_type | 0      |
| notify_type | 1      |
| notify_type | 2      |
| notify_type | 3      |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "items": [
      {
        "id": "91686000000",
        "name": "Hello",
        "topic": "string",
        "user_id": "2418200000",
        "icon": "https://xxx/icons/2020-05/YQyfHxxx.png/icon",
        "notify_type": 0,
        "region": "beijing",
        "enable_open": true,
        "open_id": "012312413",
        "default_channel_id": "5915900001396830",
        "welcome_channel_id": "5789900001312330",
        "boost_num": 3,
        "level": 0
      }
    ],
    "meta": {
      "page": 1,
      "page_total": 10,
      "page_size": 50,
      "total": 480
    },
    "sort": {
      "id": 1
    }
  }
}
```

## 获取服务器详情

### 接口说明

| 地址                 | 请求方式 | 说明 |
| -------------------- | -------- | ---- |
| `/api/v3/guild/view` | GET      |      |

### 参数列表

| 参数名   | 位置  | 类型   | 必需 | 说明      |
| -------- | ----- | ------ | ---- | --------- |
| guild_id | query | string | true | 服务器 id |

### 返回参数说明

| 参数名             | 类型    | 说明                                                                                              |
| ------------------ | ------- | ------------------------------------------------------------------------------------------------- |
| id                 | string  | 服务器 id                                                                                         |
| name               | string  | 服务器名称                                                                                        |
| topic              | string  | 服务器主题                                                                                        |
| user_id            | string  | 服务器主的 id                                                                                     |
| icon               | string  | 服务器 icon 的地址                                                                                |
| notify_type        | int     | 通知类型, `0`代表默认使用服务器通知设置，`1`代表接收所有通知, `2`代表仅@被提及，`3`代表不接收通知 |
| region             | string  | 服务器默认使用语音区域                                                                            |
| enable_open        | boolean | 是否为公开服务器                                                                                  |
| open_id            | string  | 公开服务器 id                                                                                     |
| default_channel_id | string  | 默认频道 id                                                                                       |
| welcome_channel_id | string  | 欢迎频道 id                                                                                       |
| roles              | array   | 角色列表                                                                                          |
| channels           | array   | 频道列表                                                                                          |

#### 枚举值

| 属性        | 属性值 |
| ----------- | ------ |
| notify_type | 0      |
| notify_type | 1      |
| notify_type | 2      |
| notify_type | 3      |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "roles": [
      {
        "role_id": 702,
        "name": "管理员",
        "color": 0,
        "position": 1,
        "hoist": 0,
        "mentionable": 0,
        "permissions": 2048
      }
    ],
    "channels": [
      {
        "id": 123,
        "guild_id": "91686000000",
        "user_id": "2418200000",
        "parent_id": 123,
        "name": "测试频道",
        "topic": "频道简介",
        "type": 1,
        "level": 10,
        "slow_mode": 0,
        "is_category": false
      }
    ],
    "id": "91686000000",
    "name": "Hello",
    "topic": "string",
    "user_id": "2418200000",
    "icon": "https://xxx/icons/2020-05/YQyfHxxx.png/icon",
    "notify_type": 0,
    "region": "beijing",
    "enable_open": true,
    "open_id": "012312413",
    "default_channel_id": "5915900001396830",
    "welcome_channel_id": "5789900001312330",
    "boost_num": 3,
    "level": 0
  }
}
```

## 获取服务器中的用户列表

### 接口说明

| 地址                      | 请求方式 | 说明 |
| ------------------------- | -------- | ---- |
| `/api/v3/guild/user-list` | GET      |      |

### 参数列表

| 参数名          | 位置  | 类型    | 必需  | 说明                                           |
| --------------- | ----- | ------- | ----- | ---------------------------------------------- |
| guild_id        | query | string  | true  | 服务器 id                                      |
| channel_id      | query | string  | false | 频道 id                                        |
| search          | query | string  | false | 搜索关键字，在用户名或昵称中搜索               |
| role_id         | query | integer | false | 角色 ID，获取特定角色的用户列表                |
| mobile_verified | query | integer | false | 只能为`0`或`1`，`0`是未认证，`1`是已认证       |
| active_time     | query | integer | false | 根据活跃时间排序，`0`是顺序排列，`1`是倒序排列 |
| joined_at       | query | integer | false | 根据加入时间排序，`0`是顺序排列，`1`是倒序排列 |
| page            | query | integer | false | 目标页数                                       |
| page_size       | query | integer | false | 每页数据数量                                   |
| filter_user_id  | query | string  | false | 获取指定 id 所属用户的信息                     |

#### 枚举值

| 参数            | 参数值 |
| --------------- | ------ |
| mobile_verified | 0      |
| mobile_verified | 1      |

### 返回参数说明

| 参数名        | 类型         | 说明         |
| ------------- | ------------ | ------------ |
| user_count    | int          | 服务器内用户总数量|
| online_count  | int          | 当前条件下，频道右侧显示的在线用户数量，会过滤权限，并将不与在线显示在一起的角色排除 |
| offline_count | int          | 当前条件下，离线用户数量|
| items         | array (User) | 用户列表     |

**注意：** user_count 不一定等于online_count + offline_count。 在服务器的角色设置中，可以设置某个角色不放在在线用户中（参考guild_role.hoist属性），而是单独显示。就会使得这些角色的数字不会放在online_count中。user_count是服务器内总数，当前条件下的总数可以从meta下的total中获取。

#### 枚举值

| 属性   | 属性值 |
| ------ | ------ |
| status | 0      |
| status | 10     |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "items": [
      {
        "id": "2418200000",
        "username": "tz-un",
        "identify_num": "5618",
        "online": false,
        "status": 0,
        "bot": false,
        "avatar": "https://img.kookapp.cn/avatars/2020-02/xxxx.jpg/icon",
        "vip_avatar": "https://img.kookapp.cn/avatars/2020-02/xxxx.jpg/icon",
        "nickname": "tz-unn",
        "roles": [702]
      }
    ],
    "meta": {
      "page": 1,
      "page_total": 10,
      "page_size": 50,
      "total": 480
    },
    "sort": {
      "id": 1
    },
    "user_count": 10,
    "online_count": 3,
    "offline_count": 7
  }
}
```

## 修改服务器中用户的昵称

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/guild/nickname` | POST     |      |

### 参数列表

| 参数名   | 位置 | 类型   | 必需  | 说明                                                  |
| -------- | ---- | ------ | ----- | ----------------------------------------------------- |
| guild_id | body | string | true  | 服务器的 ID                                           |
| nickname | body | string | false | 昵称，2 - 64 长度，不传则清空昵称                     |
| user_id  | body | string | false | 要修改昵称的目标用户 ID，不传则修改当前登陆用户的昵称 |

### 返回参数说明

| 名称      | 类型    | 必需  | 限制 | 说明                                                          |
| --------- | ------- | ----- | ---- | ------------------------------------------------------------- |
| » code    | integer | true  | none | 错误码，0 代表成功，非 0 代表失败，具体的错误码参见错误码一览 |
| » message | string  | true  | none | 错误消息，具体的返回消息会根据 Accept-Language 来返回。       |
| » data    | object  | false | none | 返回数据                                                      |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {}
}
```

## 离开服务器

### 接口说明

| 地址                  | 请求方式 | 说明 |
| --------------------- | -------- | ---- |
| `/api/v3/guild/leave` | POST     |      |

### 参数列表

| 参数名   | 位置 | 类型   | 必需 | 说明      |
| -------- | ---- | ------ | ---- | --------- |
| guild_id | body | string | true | 服务器 id |

### 返回参数说明

| 名称      | 类型    | 必需  | 限制 | 说明                                                          |
| --------- | ------- | ----- | ---- | ------------------------------------------------------------- |
| » code    | integer | true  | none | 错误码，0 代表成功，非 0 代表失败，具体的错误码参见错误码一览 |
| » message | string  | true  | none | 错误消息，具体的返回消息会根据 Accept-Language 来返回。       |
| » data    | object  | false | none | 返回数据                                                      |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {}
}
```

## 踢出服务器

### 接口说明

| 地址                    | 请求方式 | 说明 |
| ----------------------- | -------- | ---- |
| `/api/v3/guild/kickout` | POST     |      |

### 参数列表

| 参数名    | 位置 | 类型   | 必需 | 说明        |
| --------- | ---- | ------ | ---- | ----------- |
| guild_id  | body | string | true | 服务器 ID   |
| target_id | body | string | true | 目标用户 ID |

### 返回参数说明

| 名称      | 类型    | 必需  | 限制 | 说明                                                          |
| --------- | ------- | ----- | ---- | ------------------------------------------------------------- |
| » code    | integer | true  | none | 错误码，0 代表成功，非 0 代表失败，具体的错误码参见错误码一览 |
| » message | string  | true  | none | 错误消息，具体的返回消息会根据 Accept-Language 来返回。       |
| » data    | object  | false | none | 返回数据                                                      |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {}
}
```

## 服务器静音闭麦列表

### 接口说明

| 地址                      | 请求方式 | 说明 |
| ------------------------- | -------- | ---- |
| `/api/v3/guild-mute/list` | GET      |      |

### 参数列表

| 参数名      | 位置  | 类型   | 必需  | 说明                                         |
| ----------- | ----- | ------ | ----- | -------------------------------------------- |
| guild_id    | query | string | true  | 服务器 id                                    |
| return_type | query | string | false | 返回格式，建议为"detail", 其他情况仅作为兼容 |

### 返回参数说明

返回格式中，type 值,`1`代表麦克风闭麦，`2`代表耳机静音。

### 返回示例

```json
# 请设置return_typ为detail
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "mic": {
      "type": 1,
      "user_ids": [
        "2418200000"
      ]
    },
    "headset": {
      "type": 2,
      "user_ids": [
        "2418200200"
      ]
    }
  }
}
```

## 添加服务器静音或闭麦

### 接口说明

| 地址                        | 请求方式 | 说明 |
| --------------------------- | -------- | ---- |
| `/api/v3/guild-mute/create` | POST     |      |

### 参数列表

| 参数名   | 位置 | 类型   | 必需 | 说明                                         |
| -------- | ---- | ------ | ---- | -------------------------------------------- |
| guild_id | body | string | true | 服务器 id                                    |
| user_id  | body | string | true | 目标用户 id                                  |
| type     | body | int    | true | 静音类型，`1`代表麦克风闭麦，`2`代表耳机静音 |

### 返回参数说明

无

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {}
}
```

## 删除服务器静音或闭麦

### 接口说明

| 地址                        | 请求方式 | 说明 |
| --------------------------- | -------- | ---- |
| `/api/v3/guild-mute/delete` | POST     |      |

### 参数列表

| 参数名   | 位置 | 类型   | 必需 | 说明                                         |
| -------- | ---- | ------ | ---- | -------------------------------------------- |
| guild_id | body | string | true | 服务器 id                                    |
| user_id  | body | string | true | 用户 id                                      |
| type     | body | int    | true | 静音类型，`1`代表麦克风闭麦，`2`代表耳机静音 |

### 返回参数说明

无

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {}
}
```

## 服务器助力历史

### 接口说明

| 地址                           | 请求方式  | 说明                 |
| ----------------------------- | -------- | ------------------- |
| `/api/v3/guild-boost/history` | GET      | 需要有`服务器管理`权限 |

### 参数列表

| 参数名     | 位置  | 类型   | 必需  | 说明                            |
| ---------- | ----- | ------ | ----- | --------------------------- |
| guild_id   | query | string | true  | 服务器 id                    |
| start_time | query | int    | false | unix 时间戳，时间范围的开始时间 |
| end_time   | query | int    | false | unix 时间戳，时间范围的结束时间 |

### 返回参数说明

返回格式为标准分页格式，以 `start_time` 由大到小排列，其中 `items` 数据如下：

| 名称        | 类型   | 说明                              |
| ---------- | ------ | -------------------------------- |
| user_id    | string | 使用助力包的用户 ID                 |
| guild_id   | string | 服务器的 ID                       |
| start_time | int    | 助力包生效时间, Unix 时间戳 (单位: 秒)|
| end_time   | int    | 助力包失效时间, Unix 时间戳 (单位: 秒)|
| user       | object | 使用助力包的用户数据对象             |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "items": [
      {
        "user_id": "0000000000",
        "guild_id": "0000000000000000",
        "start_time": 1667814426,
        "end_time": 1670406426,
        "user": {
          "id": "0000000000",
          "username": "XXXX",
          "identify_num": "0000",
          "online": false,
          "os": "Websocket",
          "avatar": "",
          "vip_avatar": "",
          "banner": "",
          "nickname": "XXXX",
          "bot": false
        }
      }
    ],
    "meta": {
      "page": 1,
      "page_total": 106,
      "page_size": 1,
      "total": 106
    },
    "sort": {}
  }
}
```
