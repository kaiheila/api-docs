# 频道相关接口列表

本文档主要列出频道相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kookapp.cn/doc/reference)。

| 接口                                                                                      | 接口说明             | 维护状态 |
| ----------------------------------------------------------------------------------------- | -------------------- | -------- |
| [/api/v3/channel/message](https://developer.kookapp.cn/doc/http/message#发送频道聊天消息) | 发送频道聊天消息     | 已弃用   |
| [/api/v3/channel/list](#获取频道列表)                                                     | 获取频道列表         | 正常     |
| [/api/v3/channel/view](#获取频道详情)                                                     | 获取频道详情         | 正常     |
| [/api/v3/channel/create](#创建频道)                                                       | 创建频道             | 正常     |
| [/api/v3/channel/update](#编辑频道)                                                       | 编辑频道             | 正常     |
| [/api/v3/channel/delete](#删除频道)                                                       | 删除频道             | 正常     |
| [/api/v3/channel/user-list](#语音频道用户列表)                                             | 语音频道用户列表      | 正常     |
| [/api/v3/channel/move-user](#语音频道之间移动用户)                                        | 语音频道之间移动用户 | 正常     |
| [/api/v3/channel/kickout](#踢出语音频道中的用户)                                        | 踢出语音频道中的用户 | 正常     |
| [/api/v3/channel-role/index](#频道角色权限详情)                                           | 获取频道角色权限详情 | 正常     |
| [/api/v3/channel-role/create](#创建频道角色权限)                                          | 创建频道角色权限     | 正常     |
| [/api/v3/channel-role/update](#更新频道角色权限)                                          | 更新频道角色权限     | 正常     |
| [/api/v3/channel-role/sync](#同步频道角色权限)                                            | 同步频道角色权限     | 正常     |
| [/api/v3/channel-role/delete](#删除频道角色权限)                                          | 删除频道角色权限     | 正常     |

## 获取频道列表

### 接口说明

| 地址                   | 请求方式 | 说明 |
| ---------------------- | -------- | ---- |
| `/api/v3/channel/list` | GET      |      |

### 参数列表

| 参数名    | 位置  | 类型    | 必需  | 说明                                      |
| --------- | ----- | ------- | ----- | ----------------------------------------- |
| page      | query | integer | false | 目标页数                                  |
| page_size | query | integer | false | 每页数据数量                              |
| guild_id  | query | string  | true  | 服务器 id                                 |
| type      | query | integer | false | 频道类型, `1`为文字，`2`为语音, 默认为`1` |
|parent_id  | query | string  | false | 父分组频道 id |

### 返回参数说明

| 参数名       | 类型    | 说明           |
| ------------ | ------- | -------------- |
| id           | string  | 频道 id        |
| user_id      | string  | 频道创建者 id  |
| parent_id    | string  | 父分组频道 id  |
| name         | string  | 频道名称       |
| type         | int     | 频道类型       |
| level        | int     | 频道排序       |
| limit_amount | int     | 人数限制       |
| is_category  | boolean | 是否为分组类型 |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "items": [
      {
        "id": "7480000000000000",
        "user_id": "1700000",
        "parent_id": "",
        "name": "语音分组",
        "type": 0,
        "level": 100,
        "limit_amount": 0,
        "is_category": true
      },
      {
        "id": "3321010478582002",
        "user_id": "1700000",
        "parent_id": "7480000000000000",
        "name": "语音频道",
        "type": 2,
        "level": 100,
        "limit_amount": 25,
        "is_category": false
      }
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

| 地址                   | 请求方式 | 说明 |
| ---------------------- | -------- | ---- |
| `/api/v3/channel/view` | GET      |      |

### 参数列表

| 参数名    | 类型   | 必传 | 参数区域 | 说明    |
| --------- | ------ | ---- | -------- | ------- |
| target_id | string | 是   | GET      | 频道 id |
| need_children | bool | 否  | GET      | 是否需要获取子频道。true是 false否 默认为false |

### 返回参数说明

| 参数名                   | 类型      | 说明                             |
|-----------------------|---------|--------------------------------|
| id                    | string  | 频道 id                          |
| guild_id              | string  | 服务器 id                         |
| user_id               | string  | 频道创建者 id                       |
| parent_id             | string  | 父分组频道 id                       |
| name                  | string  | 频道名称                           |
| topic                 | string  | 频道简介                           |
| type                  | int     | 频道类型，`0` 分组，`1` 文字，`2` 语音      |
| level                 | int     | 频道排序                           |
| slow_mode             | int     | 慢速限制，用户发送消息之后再次发送消息的等待时间，单位秒   |
| has_password          | boolean | 是否已设置密码                        |
| limit_amount          | int     | 人数限制                           |
| is_category           | boolean | 是否为分组类型                        |
| permission_sync       | int     | 是否与分组频道同步权限                    |
| permission_overwrites | array   | 针对角色的频道权限覆盖                    |
| permission_users      | array   | 针对用户的频道权限覆盖                    |
| voice_quality         | string  | 语音频道质量级别，`1` 流畅，`2` 正常，`3` 高质量 |
| server_url            | string  | 语音服务器地址，`HOST:PORT/PATH`的格式    |
| children            | array  |  子频道的id列表    |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "id": "00000000000000000000000",
    "guild_id": "00000000000000000000000",
    "parent_id": "00000000000000000000000",
    "user_id": "00000000000000000000000",
    "name": "语音频道",
    "topic": "",
    "type": 1,
    "level": 100,
    "slow_mode": 0,
    "has_password": false,
    "limit_amount": 0,
    "is_category": false,
    "permission_sync": 0,
    "permission_overwrites": [
      {
        "role_id": 0,
        "allow": 8,
        "deny": 0
      }
    ],
    "permission_users": [],
    "voice_quality": "1",
    "server_url": "hostname:port/path",
    "children": [
        "0000000000000000",
        "0000000000000000"
    ]
  }
}
```

## 创建频道

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/channel/create` | POST     |      |

### 参数列表

| 参数名        | 位置 | 类型   | 必需  | 说明                                                               |
| ------------- | ---- | ------ | ----- |------------------------------------------------------------------|
| guild_id      | body | string | true  | 服务器 id                                                           |
| name          | body | string | true  | 频道名称                                                             |
| parent_id     | body | string | false | 父分组 id                                                           |
| type          | body | int    | false | 频道类型，`1` 文字，`2` 语音，默认为 `1`                                       |
| limit_amount  | body | int    | false | 语音频道人数限制，最大 `99`                                                 |
| voice_quality | body | string | false | 语音音质，默认为`2`。`1`流畅，`2`正常，`3`高质量                                   |
| is_category   | body | int    | false | 是否是分组，默认为 0。1 是，0 否。当该值传 1 时，只接收 guild_id、name、is_category 三个字段！ |

### 返回参数说明

返回参数为创建成功的频道信息，可以参考 [获取频道详情](#获取频道详情) 接口。

### 传参示例

分组频道

```
{
    "guild_id": "00000000000000000000000",
    "name":"xxx",
    "is_category": 1
}
```

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "id": "00000000000000000000000",
    "guild_id": "00000000000000000000000",
    "parent_id": "00000000000000000000000",
    "user_id": "00000000000000000000000",
    "name": "语音频道",
    "topic": "",
    "type": 1,
    "level": 100,
    "slow_mode": 0,
    "has_password": false,
    "limit_amount": 0,
    "is_category": false,
    "permission_sync": 1,
    "permission_overwrites": [
      {
        "role_id": 0,
        "allow": 0,
        "deny": 0
      }
    ],
    "permission_users": [],
    "voice_quality": "1",
    "server_url": "hostname:port"
  }
}
```

## 编辑频道

### 接口说明

| 地址                       | 请求方式 | 说明 |
|--------------------------|------|----|
| `/api/v3/channel/update` | POST |    |

### 参数列表

| 参数名           | 类型     | 必传 | 参数区域 | 说明                                                                                                                                  |
|---------------|--------|----|------|-------------------------------------------------------------------------------------------------------------------------------------|
| channel_id    | string | 是  | POST | 服务器中频道的 ID                                                                                                                          |
| name          | string | 否  | POST | 频道名称                                                                                                                                |
| level         | int    | 否  | POST | 频道排序                                                                                                                                |
| parent_id     | string | 否  | POST | 分组频道 ID，设置为 `0` 为移出分组                                                                                                               |
| topic         | string | 否  | POST | 频道简介，文字频道有效                                                                                                                         |
| slow_mode     | int    | 否  | POST | 慢速模式，单位 ms。目前只支持这些值：0, 5000, 10000, 15000, 30000, 60000, 120000, 300000, 600000, 900000, 1800000, 3600000, 7200000, 21600000，文字频道有效 |
| limit_amount  | int    | 否  | POST | 此频道最大能容纳的用户数量，最大值 99，语音频道有效                                                                                                         |
| voice_quality | string | 否  | POST | 声音质量，`1` 流畅，`2` 正常，`3` 高质量，语音频道有效                                                                                                   |
| password      | string | 否  | POST | 密码，语音频道有效                                                                                                                           |

### 返回参数说明

参考[对象-频道 Channel](https://developer.kookapp.cn/doc/objects#频道Channel)

### 传参示例

```json
{
  "channel_id": "1111111111111111",
  "name": "q'q-!!",
  "topic": "mmm"
}
```

### 返回示例

```json
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "id": "1111111111111111",
        "name": "q'q-!!",
        "user_id": "1111111111",
        "guild_id": "1111111111111111",
        "voice_quality": "2",
        "limit_amount": 0,
        "is_category": 0,
        "is_readonly": false,
        "parent_id": "1111111111111111",
        "is_private": false,
        "server_type": 1,
        "server_url": "rtc-new.kookapp.cn:39999/gateway/v1",
        "level": 3,
        "slow_mode": 0,
        "topic": "mmm",
        "is_master": false,
        "type": 1,
        "permission_overwrites": [
            {
                "role_id": 0,
                "allow": 5152,
                "deny": 8
            }
        ],
        "permission_users": [
            {
                "user": {
                    "id": "1111111111",
                    "username": "Ivy",
                    "identify_num": "9314",
                    "online": true,
                    "os": "Websocket",
                    "status": 1,
                    "avatar": "https://img.kookapp.cn/assets/avatar_4.jpg/icon",
                    "vip_avatar": "https://img.kookapp.cn/assets/avatar_4.jpg/icon",
                    "banner": "",
                    "nickname": "Ivy",
                    "roles": [
                        2127
                    ],
                    "is_vip": false,
                    "is_ai_reduce_noise": true,
                    "bot": false,
                    "tag_info": {
                        "color": "#6666CC",
                        "text": "KOOK"
                    },
                    "mobile_verified": true,
                    "joined_at": 1644204471000,
                    "active_time": 1648460218956
                },
                "allow": 1056,
                "deny": 0
            }
        ],
        "permission_sync": 1,
        "mode": 0,
        "has_password": false
    }
}
```

## 删除频道

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/channel/delete` | POST     |      |

### 参数列表

| 参数名     | 位置 | 类型   | 必需 | 说明    |
| ---------- | ---- | ------ | ---- | ------- |
| channel_id | body | string | true | 频道 id |

### 返回参数说明

### 返回示例

```json
{
    "code": 0,
    "message": "操作成功",
    "data": {}
}
```

## 语音频道用户列表

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/channel/user-list` | GET     |      |

### 参数列表

| 参数名     | 类型   | 必传 | 参数区域 | 说明    |
| ---------- | ------ | ---- | -------- | ------- |
| channel_id | string | 是   | GET      | 频道id |

### 返回参数说明
用户信息, 见[对象-用户 User](https://developer.kookapp.cn/doc/objects#用户User)

### 返回示例

```json
{
    "code": 0,
    "message": "操作成功",
    "data": [
        {
            "id": "999999999",
            "username": "XXX",
            "identify_num": "9999",
            "online": true,
            "os": "Websocket",
            "status": 1,
            "avatar": "XXX",
            "vip_avatar": "XXX",
            "banner": "",
            "nickname": "XXX",
            "roles": [
                4131873
            ],
            "is_vip": false,
            "is_ai_reduce_noise": true,
            "is_personal_card_bg": false,
            "bot": false,
            "mobile_verified": true,
            "joined_at": 1639808384000,
            "active_time": 1639808384000,
            "live_info": {
                "in_live": false,
                "audience_count": 0,
                "live_thumb": "",
                "live_start_time": 0
            }
        }
    ]
}
```

## 语音频道之间移动用户

### 接口说明

只能在语音频道之间移动，用户也必须在其他语音频道在线才能够移动到目标频道。

| 地址                        | 请求方式 | 说明 |
| --------------------------- | -------- | ---- |
| `/api/v3/channel/move-user` | POST     |      |

### 参数列表

| 参数名    | 位置 | 类型   | 必需 | 说明                        |
| --------- | ---- | ------ | ---- | --------------------------- |
| target_id | body | string | true | 目标频道 id, 需要是语音频道 |
| user_ids  | body | array  | true | 用户 id 的数组              |

### 返回参数说明

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |

### 返回示例

```json
{
    "code": 0,
    "message": "操作成功",
    "data": []
}
```

## 踢出语音频道中的用户

### 接口说明

只能踢出在语音频道中的用户。

| 地址                        | 请求方式 | 说明 |
| --------------------------- | -------- | ---- |
| `/api/v3/channel/kickout` | POST      |      |

### 参数列表

| 参数名    | 位置 | 类型   | 必需 | 说明                        |
| --------- | ---- | ------ | ---- | --------------------------- |
| channel_id | body | string | true | 目标频道 id, 需要是语音频道 |
| user_id  | body | string  | true | 用户 id               |

### 返回参数说明

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |

### 返回示例

```json
{
    "code": 0,
    "message": "操作成功",
    "data": []
}
```

## 频道角色权限详情

### 接口说明

| 地址                         | 请求方式 | 说明 |
| ---------------------------- | -------- | ---- |
| `/api/v3/channel-role/index` | GET      |      |

### 参数列表

| 参数名     | 类型   | 必传 | 参数区域 | 说明    |
| ---------- | ------ | ---- | -------- | ------- |
| channel_id | string | 是   | GET      | 频道 id |

### 返回参数说明

| 参数名                | 类型  | 说明                                                                                                                                                                                |
| --------------------- | ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| permission_overwrites | Array | 频道权限覆写的角色列表, role_id 为角色 id, 其它字段见下表                                                                                                                           |
| permission_users      | Array | 频道权限覆写的用户列表, user 字段参见[用户接口](https://developer.kookapp.cn/doc/http/user#%E8%8E%B7%E5%8F%96%E5%BD%93%E5%89%8D%E7%94%A8%E6%88%B7%E4%BF%A1%E6%81%AF), 其它的见下表 |
| permission_sync       | int   | 是否同步分组的权限                                                                                                                                                                  |

其它参数说明：

| 参数名 | 类型 | 说明                               |
| ------ | ---- | ---------------------------------- |
| allow  | int  | 最终修改成功后，允许的权限的结果集 |
| deny   | int  | 最终修改成功后，拒绝的权限的结果集 |

### 返回示例

```json
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

| 地址                          | 请求方式 | 说明 |
| ----------------------------- | -------- | ---- |
| `/api/v3/channel-role/create` | POST     |      |

### 参数列表

| 参数名     | 位置 | 类型   | 必需  | 说明                                                          |
| ---------- | ---- | ------ | ----- | ------------------------------------------------------------- |
| channel_id | body | string | true  | 频道 id, 如果频道是分组的 id,会同步给所有 sync=1 的子频道     |
| type       | body | string | false | value 的类型，只能为"role_id","user_id",不传则默认为"user_id" |
| value      | body | string | false | 根据 type 的值，为 用户 id 或 角色 id                         |

### 返回参数说明

| 参数名          | 类型 | 说明                            |
| --------------- | ---- | ------------------------------- |
| user_id/role_id | int  | 根据用户的 type，返回不同的参数 |
| allow           | int  | 同上                            |
| deny            | int  | 同上                            |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "user_id": "2418200000",
    "allow": 2048,
    "deny": 0
  }
}
```

## 更新频道角色权限

### 接口说明

| 地址                          | 请求方式 | 说明 |
| ----------------------------- | -------- | ---- |
| `/api/v3/channel-role/update` | POST     |      |

### 参数列表

| 参数名     | 位置 | 类型    | 必需  | 说明                                                          |
| ---------- | ---- | ------- | ----- | ------------------------------------------------------------- |
| channel_id | body | string  | true  | 频道 id, 如果频道是分组的 id,会同步给所有 sync=1 的子频道     |
| type       | body | string  | false | value 的类型，只能为"role_id","user_id",不传则默认为"user_id" |
| value      | body | string  | false | 根据 type 的值，为用户 id 或角色 id                           |
| allow      | body | integer | false | 默认为 0,想要设置的允许的权限值                               |
| deny       | body | integer | false | 默认为 0,想要设置的拒绝的权限值                               |

### 返回参数说明

| 参数名          | 类型 | 说明                            |
| --------------- | ---- | ------------------------------- |
| user_id/role_id | int  | 根据用户的 type，返回不同的参数 |
| allow           | int  | 同上                            |
| deny            | int  | 同上                            |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "user_id": "2418200000",
    "allow": 2048,
    "deny": 0
  }
}
```

## 同步频道角色权限

### 接口说明

| 地址                          | 请求方式 | 说明 |
|-----------------------------| -------- | ---- |
| `/api/v3/channel-role/sync` | POST     |      |

### 参数列表

| 参数名     | 位置 | 类型   | 必需  | 说明    |
| ---------- | ---- | ------ | ----- |-------|
| channel_id | body | string | true  | 频道 ID |

### 返回参数说明

| 参数名                   | 类型    | 说明                   |
|-----------------------|-------|----------------------|
| permission_overwrites | array | 针对角色在该频道的权限覆写规则组成的列表 |
| permission_users      | array | 针对用户在该频道的权限覆写规则组成的列表 |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "permission_overwrites": [
      {
        "role_id": 0,
        "allow": 0,
        "deny": 0
      }
    ],
    "permission_users": []
  }
}
```

## 删除频道角色权限

### 接口说明

| 地址                          | 请求方式 | 说明 |
| ----------------------------- | -------- | ---- |
| `/api/v3/channel-role/delete` | POST     |      |

### 参数列表

| 参数名     | 位置 | 类型   | 必需  | 说明                                                          |
| ---------- | ---- | ------ | ----- | ------------------------------------------------------------- |
| channel_id | body | string | true  | 频道 id, 如果频道是分组的 id,会同步给所有 sync=1 的子频道     |
| type       | body | string | false | value 的类型，只能为"role_id","user_id",不传则默认为"user_id" |
| value      | body | string | false | 根据 type，为用户 id 或角色 id                                |

### 返回参数说明

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {}
}
```
