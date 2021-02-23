# 标准对象格式

## 用户User

| 字段| 类型| 说明|
|---|---|---|
|id|string|用户 id|
|username|string|用户名|
|identify_num|string|用户名 `#` 后的 4 位识别 id|
|online|bool|用户在线状态|
|avatar|string|头像图片地址|
|bot|bool|是否是机器人|
|nickname|string|用户在当前服务器的昵称|
|roles|Array|用户在当前服务器中的角色 id 组成的列表|

> 注: 仅当与服务器有关的API, 或产生自服务器的消息会携带`nickname`, `roles`等参数

**示例**

```javascript
{
    "id": "2418200000",
    "username": "tz-un",
    "identify_num": "5618",
    "online": false,
    "avatar": "https://img.kaiheila.cn/avatars/2020-02/xxxx.jpg/icon",
    "nickname": "12316993",
    "roles": [
        111,
        112
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