# 服务器相关接口列表

本文档主要列出服务器相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kookapp.cn/doc/reference)。

| 接口                                       | 接口说明           | 维护状态 |
|------------------------------------------|----------------|------|
| [/api/v3/guild/list](#获取当前用户加入的服务器列表)    | 获取当前用户加入的服务器列表 | 正常   |
| [/api/v3/guild/view](#获取服务器详情)           | 获取服务器详情        | 正常   |
| [/api/v3/guild/user-list](#获取服务器中的用户列表)  | 获取服务器中的用户列表    | 正常   |
| [/api/v3/guild/nickname](#修改服务器中用户的昵称)   | 修改服务器中用户的昵称    | 正常   |
| [/api/v3/guild/leave](#离开服务器)            | 离开服务器          | 正常   |
| [/api/v3/guild/kickout](#踢出服务器)          | 踢出服务器          | 正常   |
| [/api/v3/guild-mute/list](#服务器静音闭麦列表)    | 服务器静音闭麦列表      | 正常   |
| [/api/v3/guild-mute/create](#添加服务器静音或闭麦) | 添加服务器静音或闭麦     | 正常   |
| [/api/v3/guild-mute/delete](#删除服务器静音或闭麦) | 删除服务器静音或闭麦     | 正常   |
| [/api/v3/guild-boost/history](#服务器助力历史)  | 查询服务器的助力包历史    | 正常   |

## 获取当前用户加入的服务器列表

### 接口说明

| 地址                   | 请求方式 | 说明 |
|----------------------|------|----|
| `/api/v3/guild/list` | GET  |    |

### 参数列表

| 参数名       | 位置    | 类型      | 必需    | 说明                                                                                |
|-----------|-------|---------|-------|-----------------------------------------------------------------------------------|
| page      | query | integer | false | 目标页数，默认值 `1`                                                                      |
| page_size | query | integer | false | 每页数据数量，默认值 `100`，最大值 `100`                                                        |
| sort      | query | string  | false | 代表排序的字段，及其排序方式<br>例如：`id` 表示按 `id` 字段升序排序，`-id` 表示按 `id` 字段降序排序<br>支持排序的字段包括：`id` |

### 返回参数说明

| 参数名                | 类型      | 说明                                                                     |
|--------------------|---------|------------------------------------------------------------------------|
| id                 | string  | 服务器 ID                                                                 |
| name               | string  | 服务器名称                                                                  |
| topic              | string  | 服务器主题                                                                  |
| user_id            | string  | 服务器主用户的 ID                                                             |
| is_master          | boolean | 当前用户是否为该服务器的服务器主                                                       |
| icon               | string  | 服务器图标地址，若服务器从未设置过图标，则此值为空字符串                                           |
| notify_type        | int     | 服务器默认通知类型，枚举值 `notify_type` 见表后                                        |
| region             | string  | 服务器默认语音区域，枚举值 `region` 见表后                                             |
| enable_open        | boolean | 是否为公开服务器                                                               |
| open_id            | string  | 服务器的公开 ID，若服务器从未设置为公开状态，则此值为 `0`                                       |
| default_channel_id | string  | 服务器默认频道 ID，若服务器的默认文字频道设置为无默认频道，则此值为服务器的首个文字频道的频道 ID，若服务器无文字频道，则此值为 `0` |
| welcome_channel_id | string  | 服务器欢迎通知频道 ID，若服务器的欢迎通知频道设置为无欢迎通知，则此值为 `0`                              |

#### 枚举值

- `notify_type`

| 属性值 | 说明     |
|-----|--------|
| 1   | 接收所有消息 |
| 2   | 仅@被提及  |

- `region`

| 属性值      | 说明         |
|----------|------------|
| chengdu  | 西南(成都)     |
| beijing  | 华北(北京)     |
| shanghai | 华东(上海)     |
| shenzhen | 华南(深圳)     |
| hk       | 亚太(香港)     |
| vnga     | 国际专线(助力专享) |

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
        "welcome_channel_id": "5789900001312330"
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

| 地址                   | 请求方式 | 说明 |
|----------------------|------|----|
| `/api/v3/guild/view` | GET  |    |

### 参数列表

| 参数名      | 位置    | 类型     | 必需   | 说明     |
|----------|-------|--------|------|--------|
| guild_id | query | string | true | 服务器 ID |

### 返回参数说明

| 参数名                | 类型                     | 说明                                                                     |
|--------------------|------------------------|------------------------------------------------------------------------|
| id                 | string                 | 服务器 ID                                                                 |
| name               | string                 | 服务器名称                                                                  |
| topic              | string                 | 服务器主题                                                                  |
| user_id            | string                 | 服务器主用户的 ID                                                             |
| is_master          | boolean                | 当前用户是否为该服务器的服务器主                                                       |
| icon               | string                 | 服务器图标地址，若服务器从未设置过图标，则此值为空字符串                                           |
| notify_type        | int                    | 服务器默认通知类型，枚举值 `notify_type` 见表后                                        |
| region             | string                 | 服务器默认语音区域，枚举值 `region` 见表后                                             |
| enable_open        | boolean                | 是否为公开服务器                                                               |
| open_id            | string                 | 服务器的公开 ID，若服务器从未设置为公开状态，则此值为 `0`                                       |
| default_channel_id | string                 | 服务器默认频道 ID，若服务器的默认文字频道设置为无默认频道，则此值为服务器的首个文字频道的频道 ID，若服务器无文字频道，则此值为 `0` |
| welcome_channel_id | string                 | 服务器欢迎通知频道 ID，若服务器的欢迎通知频道设置为无欢迎通知，则此值为 `0`                              |
| features           | array                  | 服务器特性，数组成员为 `string` 类型，其枚举值 `feature` 见表后                             |
| boost_num          | integer                | 服务器助力包数量                                                               |
| buffer_boost_num   | integer                | 由拥有 BUFF 会员的用户为服务器提供的助力包数量（存疑）                                         |
| level              | integer                | 服务器助力等级                                                                |
| status             | integer                | TODO                                                                   |
| auto_delete_time   | string                 | TODO                                                                   |
| recommend_info     | object (RecommendInfo) | 服务器推荐信息，当服务器不为推荐服务器时，此字段不存在                                            |
| roles              | array (Role)           | 服务器角色列表，数组成员为表示服务器角色的 `object`                                         |
| channels           | array (Channel)        | 服务器频道列表，数组成员为表示服务器频道的 `object`                                         |
| user_config        | object                 | 当前用户在该服务器的配置                                                           |

#### 枚举值

- `notify_type`

| 属性值 | 说明     |
|-----|--------|
| 1   | 接收所有消息 |
| 2   | 仅@被提及  |

- `region`

| 属性值      | 说明         |
|----------|------------|
| chengdu  | 西南(成都)     |
| beijing  | 华北(北京)     |
| shanghai | 华东(上海)     |
| shenzhen | 华南(深圳)     |
| hk       | 亚太(香港)     |
| vnga     | 国际专线(助力专享) |

- `feature`

| 属性值      | 说明      |
|----------|---------|
| official | 官方服务器   |
| partner  | 合作伙伴服务器 |
| ka       | 重要客户服务器 |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "id": "35420000000000000",
    "name": "服务器名称",
    "topic": "",
    "user_id": "2298765067",
    "is_master": false,
    "icon": "https://img.kookapp.cn/icons/2022-04/xxxx.gif",
    "notify_type": 2,
    "region": "shanghai",
    "enable_open": true,
    "open_id": "16900000",
    "default_channel_id": "7600000000000",
    "welcome_channel_id": "6100000000000",
    "features": [
      "official"
    ],
    "boost_num": 100,
    "buffer_boost_num": 5,
    "level": 1,
    "status": 0,
    "auto_delete_time": "",
    "recommend_info": {
      "guild_id": "3542195235225538",
      "open_id": "16975053",
      "enable_open": 1,
      "default_channel_id": "7619070122429812",
      "name": "「KOOK」活动中心",
      "icon": "https://img.kookapp.cn/icons/2022-04/Sr1nKh3p0t050050.gif?x-oss-process=style/icon",
      "banner": "https://img.kaiheila.cn/assets/2022-06/l0uMPxcFf00ls0cs.png?x-oss-process=style/ld",
      "banner_preview": "https://img.kaiheila.cn/assets/2022-06/l0uMPxcFf00ls0cs.png?x-oss-process=style/preview",
      "desc": "KOOK官方服务器，帮助大家解决使用KOOK时遇到的问题，还有各种有趣的活动哦~",
      "status": 1,
      "guild_status": 0,
      "tag": "其他社群",
      "features": [
        "official",
        "ka"
      ],
      "certifications": [
        {
          "type": 1,
          "title": "KOOK官方服务器",
          "pic": "https://img.kookapp.cn/assets/2023-12/fR650xKxiF0ew0ew.jpg",
          "desc": ""
        }
      ],
      "level": 6,
      "custom_id": "kook",
      "is_official_partner": 1,
      "sort": 9999,
      "gradient": {
        "id": 4,
        "color_map": [
          "0x487796",
          "0x3E1A1F"
        ],
        "limit": 5,
        "theme": "dark"
      },
      "audit_status": 1,
      "update_day_gap": 0
    }
  },
  "roles": [
    {
      "role_id": 100,
      "name": "管理员",
      "desc": "描述",
      "color": 15844367,
      "color_type": 1,
      "color_map": {
        "color_list": [
          15627601,
          15391536
        ]
      },
      "position": 1,
      "hoist": 0,
      "mentionable": 0,
      "permissions": 134217729,
      "type": 0
    }
  ],
  "channels": [
    {
      "id": "490000000000",
      "guild_id": "800000000000",
      "master_id": "2800000000",
      "parent_id": "520000000000",
      "user_id": "2800000000",
      "name": "频道名称",
      "topic": "频道说明",
      "type": 1,
      "level": 4,
      "slow_mode": 0,
      "last_msg_content": "内容",
      "last_msg_id": "2e1bffb6-0000-0000-0000-000000000000",
      "has_password": false,
      "limit_amount": 0,
      "is_category": false,
      "permission_sync": 1,
      "permission_overwrites": [],
      "permission_users": []
    }
  ]
}
```

## 获取服务器中的用户列表

### 接口说明

| 地址                        | 请求方式 | 说明 |
|---------------------------|------|----|
| `/api/v3/guild/user-list` | GET  |    |

### 参数列表

| 参数名             | 位置    | 类型      | 必需    | 说明                                         |
|-----------------|-------|---------|-------|--------------------------------------------|
| guild_id        | query | string  | true  | 服务器 ID                                     |
| channel_id      | query | string  | false | 频道 ID，如果指定，则获取可见该频道的用户                     |
| search          | query | string  | false | 搜索关键字，如果指定，则获取用户名或昵称包含该关键字，或用户 ID 为该关键字的用户 |
| role_id         | query | integer | false | 角色 ID，如果指定，则获取具有该角色的用户                     |
| mobile_verified | query | integer | false | 是否已认证手机号码，枚举值 `mobile_verified` 见表后        |
| active_time     | query | integer | false | 根据活跃时间排序，枚举值 `sort` 见表后                    |
| joined_at       | query | integer | false | 根据加入时间排序，枚举值 `sort` 见表后                    |
| page            | query | integer | false | 目标页数                                       |
| page_size       | query | integer | false | 每页数据数量                                     |
| filter_user_id  | query | string  | false | 获取拥有指定用户 ID 的用户的信息                         |

#### 枚举值

- `mobile_verified`

| 属性值 | 说明  |
|-----|-----|
| 0   | 未认证 |
| 1   | 已认证 |

- `sort`

| 属性值 | 说明 |
|-----|----|
| 0   | 升序 |
| 1   | 降序 |

### 返回参数说明

| 参数名           | 类型                | 说明                  |
|---------------|-------------------|---------------------|
| items         | array (GuildUser) | 服务器用户列表             |
| user_count    | int               | 服务器总用户数量            |
| online_count  | int               | 符合筛选条件的所有用户中的在线用户数量 |
| offline_count | int               | 符合筛选条件的所有用户中的离线用户数量 |

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "items": [
      {
        "id": "2418200000",
        "username": "用户名",
        "nickname": "昵称",
        "identify_num": "1234",
        "online": true,
        "bot": false,
        "status": 0,
        "banner": "",
        "avatar": "https://img.kookapp.cn/assets/2022-01/OpoNctfPgt334334.png?x-oss-process=style/icon",
        "vip_avatar": "https://img.kookapp.cn/assets/2022-01/OpoNctfPgt334334.png?x-oss-process=style/icon",
        "mobile_verified": true,
        "joined_at": 1671000000000,
        "active_time": 1721000000000,
        "roles": [
          123456
        ],
        "is_master": false,
        "abbr": "",
        "color": 0
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

| 地址                       | 请求方式 | 说明 |
|--------------------------|------|----|
| `/api/v3/guild/nickname` | POST |    |

### 参数列表

| 参数名      | 位置   | 类型     | 必需    | 说明                                          |
|----------|------|--------|-------|---------------------------------------------|
| guild_id | body | string | true  | 服务器 ID                                      |
| nickname | body | string | false | 要设置的昵称，长度 2 至 64 个字符，空字符串、`null`、或不传均表示清空昵称 |
| user_id  | body | string | false | 要修改昵称的目标用户的 ID，空字符串、`null`、或不传均表示当前登陆的用户    |

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

## 离开服务器

### 接口说明

| 地址                    | 请求方式 | 说明 |
|-----------------------|------|----|
| `/api/v3/guild/leave` | POST |    |

### 参数列表

| 参数名      | 位置   | 类型     | 必需   | 说明     |
|----------|------|--------|------|--------|
| guild_id | body | string | true | 服务器 ID |

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

## 踢出服务器

### 接口说明

| 地址                      | 请求方式 | 说明 |
|-------------------------|------|----|
| `/api/v3/guild/kickout` | POST |    |

### 参数列表

| 参数名       | 位置   | 类型     | 必需   | 说明            |
|-----------|------|--------|------|---------------|
| guild_id  | body | string | true | 服务器 ID        |
| target_id | body | string | true | 要踢出服务器的用户的 ID |

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

## 服务器静音闭麦列表

### 接口说明

| 地址                        | 请求方式 | 说明 |
|---------------------------|------|----|
| `/api/v3/guild-mute/list` | GET  |    |

### 参数列表

| 参数名         | 位置    | 类型     | 必需    | 说明                           |
|-------------|-------|--------|-------|------------------------------|
| guild_id    | query | string | true  | 服务器 ID                       |
| return_type | query | string | false | 返回格式，建议为 `detail`, 其他情况仅作为兼容 |

### 返回参数说明

返回格式中，type 值,`1`代表麦克风闭麦，`2`代表耳机静音。

| 名称         | 类型      | 说明              |
|------------|---------|-----------------|
| mic        | object  | 服务器闭麦信息         |
| - type     | integer | 值为 `1`          |
| - user_ids | array   | 所有被服务器闭麦的用户的 ID |
| headset    | object  | 服务器静音信息         |
| - type     | integer | 值为 `2`          |
| - user_ids | array   | 所有被服务器静音的用户的 ID |

### 返回示例

参数 `return_typ` 为 `detail`

```json
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

| 地址                          | 请求方式 | 说明 |
|-----------------------------|------|----|
| `/api/v3/guild-mute/create` | POST |    |

### 参数列表

| 参数名      | 位置   | 类型     | 必需   | 说明                  |
|----------|------|--------|------|---------------------|
| guild_id | body | string | true | 服务器 ID              |
| user_id  | body | string | true | 目标用户 ID             |
| type     | body | int    | true | 静音类型，枚举值 `type` 见表后 |

#### 枚举值

- `type`

| 属性值 | 说明    |
|-----|-------|
| 1   | 麦克风闭麦 |
| 2   | 耳机静音  |

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

| 地址                          | 请求方式 | 说明 |
|-----------------------------|------|----|
| `/api/v3/guild-mute/delete` | POST |    |

### 参数列表

| 参数名      | 位置   | 类型     | 必需   | 说明                  |
|----------|------|--------|------|---------------------|
| guild_id | body | string | true | 服务器 ID              |
| user_id  | body | string | true | 目标用户 ID             |
| type     | body | int    | true | 静音类型，枚举值 `type` 见表后 |

#### 枚举值

- `type`

| 属性值 | 说明    |
|-----|-------|
| 1   | 麦克风闭麦 |
| 2   | 耳机静音  |

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

| 地址                            | 请求方式 | 说明           |
|-------------------------------|------|--------------|
| `/api/v3/guild-boost/history` | GET  | 需要有`管理服务器`权限 |

### 参数列表

| 参数名        | 位置    | 类型     | 必需    | 说明                               |
|------------|-------|--------|-------|----------------------------------|
| guild_id   | query | string | true  | 服务器 ID                           |
| start_time | query | int    | false | Unix 秒时间戳，如果指定，则获取生效时间不早于该时间的助力包 |
| end_time   | query | int    | false | Unix 秒时间戳，如果指定，则获取生效时间不晚于该时间的助力包 |

### 返回参数说明

返回格式为标准分页格式，以 `start_time` 由大到小排列，其中 `items` 数据如下：

| 名称         | 类型                 | 说明                 |
|------------|--------------------|--------------------|
| user_id    | string             | 使用助力包的用户 ID        |
| guild_id   | string             | 服务器的 ID            |
| start_time | int                | 助力包生效时间, Unix 秒时间戳 |
| end_time   | int                | 助力包失效时间, Unix 秒时间戳 |
| user       | object (GuildUser) | 使用助力包的服务器用户        |

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
          "status": 1,
          "avatar": "https://img.kookapp.cn/avatars/2021-07/xxxxxxxxxxxxx.png",
          "vip_avatar": "https://img.kookapp.cn/avatars/2021-07/xxxxxxxxxxx.png",
          "banner": "https://img.kookapp.cn/assets/2022-06/xxxxxxxxx.png",
          "nickname": "XXX",
          "roles": [],
          "is_vip": true,
          "vip_amp": true,
          "bot": false,
          "nameplate": [],
          "decorations_id_map": {
            "join_voice": 10000,
            "background": 10000,
            "nameplate": 10000,
            "nameplates": [
              10000
            ]
          },
          "is_sys": false
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
