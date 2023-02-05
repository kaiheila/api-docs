# 标准对象格式

本文档列出了常见实例的标准格式，如果不做特殊说明，用户可以参照该文档格式。

## 用户 User

| 参数名          | 类型    | 说明                                                   |
| --------------- | ------- | ------------------------------------------------------ |
| id              | string  | 用户的 id                                              |
| username        | string  | 用户的名称                                             |
| nickname        | string  | 用户在当前服务器的昵称                                 |
| identify_num    | string  | 用户名的认证数字，用户名正常为：user_name#identify_num |
| online          | boolean | 当前是否在线                                           |
| bot             | boolean | 是否为机器人                                           |
| status          | int     | 用户的状态, 0 和 1 代表正常，10 代表被封禁             |
| avatar          | string  | 用户的头像的 url 地址                                  |
| vip_avatar      | string  | vip 用户的头像的 url 地址，可能为 gif 动图             |
| mobile_verified | boolean | 是否手机号已验证                                       |
| roles           | Array   | 用户在当前服务器中的角色 id 组成的列表                 |

**示例**

```javascript
{
    "id": "2418200000",
    "username": "tz-un",
    "identify_num": "5618",
    "online": false,
    "avatar": "https://img.kookapp.cn/avatars/2020-02/xxxx.jpg/icon",
    "vip_avatar": "https://img.kookapp.cn/avatars/2020-02/xxxx.jpg/icon",
    "bot": false,
    "status" : 0,
    "mobile_verified": true,
    "nickname": "12316993",
    "roles": [
        111,
        112
    ],
}
```

## 服务器 Guild

| 字段               | 类型    | 说明                                                                                              |
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

**示例**

```javascript
{
  "id": "2405000000000",
  "name": "工具",
  "topic": "",
  "user_id": "9200000000",
  "icon": "",
  "notify_type": 1,
  "region": "beijing",
  "enable_open": false,
  "open_id": "0",
  "default_channel_id": "2369000000000",
  "welcome_channel_id": "0",
  "roles": [
      {
          "role_id": 109472,
          "name": "管理员",
          "color": 0,
          "position": 1,
          "hoist": 0,
          "mentionable": 0,
          "permissions": 1
      }
  ],
  "channels": [
      {
          "id": "2369000000000",
          "user_id": "9200000000",
          "parent_id": "",
          "name": "你好",
          "type": 1,
          "level": 1,
          "limit_amount": 0,
          "is_category": false
      },
  ]
}
```

## 角色 Role

| 字段        | 类型   | 说明                               |
| ----------- | ------ | ---------------------------------- |
| role_id     | int    | 角色 id                            |
| name        | string | 角色名称                           |
| color       | int    | 颜色色值                           |
| position    | int    | 顺序位置                           |
| hoist       | int    | 是否为角色设定(与普通成员分开显示) |
| mentionable | int    | 是否允许任何人@提及此角色          |
| permissions | int    | 权限码                             |

**示例**

```javascript
{
    "role_id": 11111,
    "name": "新角色",
    "color": 0,
    "position": 5,
    "hoist": 0,
    "mentionable": 0,
    "permissions": 142924296
}
```

## 频道 Channel

| 字段                  | 类型    | 说明                                          |
| --------------------- | ------- | --------------------------------------------- |
| id                    | string  | 频道 id                                       |
| name                  | string  | 频道名称                                      |
| user_id               | string  | 创建者 id                                     |
| guild_id              | string  | 服务器 id                                     |
| topic                 | string  | 频道简介                                      |
| is_category           | boolean | 是否为分组，事件中为 int 格式                 |
| parent_id             | string  | 上级分组的 id (若没有则为 0 或空字符串)        |
| level                 | int     | 排序 level                                    |
| slow_mode             | int     | 慢速模式下限制发言的最短时间间隔, 单位为秒(s) |
| type                  | int     | 频道类型: `1` 文字频道, `2` 语音频道          |
| permission_overwrites | Array   | 针对角色在该频道的权限覆写规则组成的列表      |
| permission_users      | array   | 针对用户在该频道的权限覆写规则组成的列表      |
| permission_sync       | int     | 权限设置是否与分组同步, `1` or `0`            |
| has_password          | bool    | 是否有密码                                    |

**示例**

```javascript
{
    "id": "53002000000000",
    "name": "新的频道",
    "user_id": "2418239356",
    "guild_id": "6016389000000",
    "is_category": false,
    "parent_id": "6016400000000000",
    "level": 12,
    "slow_mode": 0,
    "topic": "新的频道的说明",
    "type": 1,
    "permission_overwrites": [
        {
            "role_id": 0,
            "allow": 0,
            "deny": 0
        }
    ],
    "permission_users": [
        {
            //user字段参见 https://developer.kookapp.cn/doc/objects#%E7%94%A8%E6%88%B7User
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
    "permission_sync": 1
}
```

## 引用消息 Quote

| 字段      | 类型   | 说明                     |
| --------- | ------ | ------------------------ |
| id        | string | 引用消息 id              |
| type      | int    | 引用消息类型             |
| content   | string | 引用消息内容             |
| create_at | int    | 引用消息创建时间（毫秒） |
| author    | map    | 作者的用户信息           |

**示例**

```javascript
{
  "id": "1c4532f6-*********-93e9-6347f410f91c",
  "type": 1,
  "content": "hello world",
  "create_at": 1628069285358,
  "author": {
    "id": "308****000",
    "username": "盖 伦",
    "identify_num": "**10",
    "online": true,
    "os": "Websocket",
    "status": 1,
    "avatar": "https://xxx.jpg/icon",
    "vip_avatar": "",
    "nickname": "***11377",
    "roles": [
      102,
      816
    ],
    "is_vip": false,
    "bot": false,
    "mobile_verified": true,
    "joined_at": 1573816459000,
    "active_time": 1628229821490
  }
}
```

## 附加的多媒体数据 Attachments

| 字段  | 类型   | 说明           |
| ---- | ------ | ------------- |
| type | string | 多媒体类型     |
| url  | string | 多媒体地址     |
| name | string | 多媒体名       |
| size | int    | 大小 单位 Byte |

**示例**

```javascript
{
  "type": "video",
  "url": "https://***.mp4",
  "name": "***.mp4",
  "size": 2575670,
}
```

含有附件的消息示例详见[消息相关事件](https://developer.kookapp.cn/doc/event/message)
