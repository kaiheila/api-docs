# 标准对象格式

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