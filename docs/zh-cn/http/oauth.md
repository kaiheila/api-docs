# OAuth2.0相关接口

本文档主要列出 OAuth2 相关的接口。  
本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kookapp.cn/doc/reference)。

| 接口                                  | 接口说明          | 维护状态 |
|-------------------------------------|---------------|------|
| [/api/oauth2/token](#获取AccessToken) | 获取AccessToken | 正常   |

## 获取AccessToken

### 接口说明

| 地址                  | 请求方式 | 说明  |
|---------------------|------|-----|
| `/api/oauth2/token` | POST |     |

### 参数列表

| 参数名           | 位置   | 类型     | 必需   | 说明                                        |
|---------------|------|--------|------|-------------------------------------------|
| grant_type    | POST | string | true | 授权类型, 目前仅支持 `authorization_code`          |
| client_id     | POST | string | true | 当前 OAuth 客户端的 `client_id`, 可在机器人详情页查看     |
| client_secret | POST | string | true | 当前 OAuth 客户端的 `client_secret`, 可在机器人详情页查看 |
| code          | POST | string | true | 用户授权成功回调后获得的 `authorization_code`         |
| redirect_uri  | POST | string | true | 本次授权所使用的回调地址 (需为机器人 OAuth 配置白名单中的地址)      |

### 返回参数说明

| 参数名         | 类型     | 说明                       |
|-------------|--------|--------------------------|
| access_token | string | AccessToken              |
| expire_in   | int    | 有效期时间(单位秒)               |
| token_type  | string | Token类型, 目前固定为 `Bearer`  |
| scope       | string | 用户授权给该应用的OAuth能力范围, 空格分隔 |

### 返回示例

```json
{
    "access_token": "7d3012xxxxxxxxxxxxxxdc8f1",
    "expires_in": 2678400,
    "token_type": "Bearer",
    "scope": "get_user_info"
}
```
