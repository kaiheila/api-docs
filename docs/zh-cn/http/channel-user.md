# 频道用户相关接口列表

本文档主要列出频道用户相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kookapp.cn/doc/reference)。

| 接口                                                                    | 接口说明                                     | 维护状态 |
|-----------------------------------------------------------------------| -------------------------------------------- | -------- |
| [/api/v3/channel-user/get-joined-channel](#根据用户%20id%20和服务器%20id%20获取用户所在语音频道) | 根据用户 id 和服务器 id 获取用户所在语音频道 | 正常     |

## 根据用户 id 和服务器 id 获取用户所在语音频道

### 接口说明

| 地址                                      | 请求方式 | 说明 |
| ----------------------------------------- | -------- | ---- |
| `/api/v3/channel-user/get-joined-channel` | GET      |      |

### 参数列表

| 参数名    | 位置  | 类型    | 必需  | 说明         |
| --------- | ----- | ------- | ----- | ------------ |
| page      | query | integer | false | 目标页数     |
| page_size | query | integer | false | 每页数据数量 |
| guild_id  | query | string  | true  | 服务器 id    |
| user_id   | query | string  | true  | 用户 id      |

### 返回参数说明

| 参数名                | 类型    | 说明                                                                                                                                                                     |
| --------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| id                    | string  | 频道 id                                                                                                                                                                  |
| guild_id              | string  | 服务器 id                                                                                                                                                                |
| user_id               | string  | 频道创建者 id                                                                                                                                                            |
| parent_id             | string  | 父分组频道 id                                                                                                                                                            |
| name                  | string  | 频道名称                                                                                                                                                                 |
| topic                 | string  | 频道简介                                                                                                                                                                 |
| type                  | int     | 频道类型                                                                                                                                                                 |
| level                 | int     | 频道排序                                                                                                                                                                 |
| slow_mode             | int     | 慢速限制，单位秒。用户发送消息之后再次发送消息的等待时间。                                                                                                               |
| limit_amount          | int     | 人数限制                                                                                                                                                                 |
| is_category           | boolean | 是否为分组类型                                                                                                                                                           |
| permission_overwrites | Array   | 频道权限覆写的角色列表, 详情见[频道角色权限详情](https://developer.kookapp.cn/doc/http/channel#%E9%A2%91%E9%81%93%E8%A7%92%E8%89%B2%E6%9D%83%E9%99%90%E8%AF%A6%E6%83%85) |
| permission_users      | Array   | 频道权限覆写的用户列表, 详情见[频道角色权限详情](https://developer.kookapp.cn/doc/http/channel#%E9%A2%91%E9%81%93%E8%A7%92%E8%89%B2%E6%9D%83%E9%99%90%E8%AF%A6%E6%83%85) |
| permission_sync       | int     | 是否同步分组的权限                                                                                                                                                       |

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "items": [
            {
                "id": "100000000000000",
                "guild_id": "1111111111111111",
                "user_id": "1111111111",
                "parent_id": "",
                "name": "测试",
                "topic": "",
                "type": 2,
                "level": 200,
                "slow_mode": 0,
                "limit_amount": 50,
                "is_category": false,
                "permission_sync": 0,
                "permission_overwrites": [
                    {
                        "role_id": 0,
                        "allow": 0,
                        "deny": 0
                    }
                ],
                "permission_users": []
            }
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
