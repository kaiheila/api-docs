# 标准对象格式
本文档列出了常见实例的标准格式，如果不做特殊说明，用户可以参照该文档格式。

## 用户User
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
|nickname|string|用户在当前服务器的昵称|
|roles|Array|用户在当前服务器中的角色 id 组成的列表|

**示例**

```javascript
{
    "id": "2418200000",
    "username": "tz-un",
    "identify_num": "5618",
    "online": false,
    "avatar": "https://img.kaiheila.cn/avatars/2020-02/xxxx.jpg/icon",
    "bot": false,
    "mobile_verified": true,
    "system": false,
    "mobile_prefix": "86",
    "mobile": "123****7890",
    "invited_count": 33,
    "nickname": "12316993",
    "roles": [
        111,
        112
    ]
}
```

## 服务器Guild

| 字段| 类型| 说明|
|---|---|---|
|id|string|服务器id|
|name|string|服务器名称|
|topic|string|服务器主题|
|master_id|string|服务器主的id|
|icon|string|服务器icon的地址|
|notify_type|int|通知类型, `0`代表默认使用服务器通知设置，`1`代表接收所有通知, `2`代表仅@被提及，`3`代表不接收通知|
|region|string|服务器默认使用语音区域|
|enable_open|boolean|是否为公开服务器|
|open_id|string|公开服务器id|
|default_channel_id|string|默认频道id|
|welcome_channel_id|string|欢迎频道id|
|roles|array|角色列表|
|channels|array|频道列表|

**示例**

```javascript
{
  "id": "2405000000000",
  "name": "工具",
  "topic": "",
  "master_id": "9200000000",
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
          "master_id": "9200000000",
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

## 角色Role

| 字段| 类型| 说明|
|---|---|---|
|role_id|int|角色id|
|name|string|角色名称|
|color|int|颜色色值|
|position|int|顺序位置|
|hoist|int|是否为角色设定(与普通成员分开显示)|
|mentionable|int|是否允许任何人@提及此角色|
|permissions|int|权限码|

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


## 频道Channel

|字段|类型|说明|
|---|---|---|
|id|string|频道id|
|name|string|频道名称|
|user_id|string|创建者id|
|guild_id|string|服务器id|
|topic|string|频道简介|
|is_category|int|是否为分组|
|parent_id|string|上级分组的id|
|level|int|排序level|
|slow_mode|int|慢速模式下限制发言的最短时间间隔, 单位为秒(s)|
|type|string|频道类型: `1` 文字频道, `2` 语音频道|
|permission_overwrites|string|针对角色在该频道的权限覆写规则组成的列表|
|permission_users|array|针对用户在该频道的权限覆写规则组成的列表|
|permission_sync|int|权限设置是否与分组同步, `1` or `0`|

**示例**
```javascript
{
    "id": "53002000000000",
    "name": "新的频道",
    "user_id": "2418239356",
    "guild_id": "6016389000000",
    "is_category": 0,
    "parent_id": "6016400000000000",
    "level": null,
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
    "permission_users": [],
    "permission_sync": 1
}
```
