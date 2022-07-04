# OAuth2.0
OAuth2 是 OAuth2.0 的版本。OAuth 是 Open Authentication 缩写，译为“开放授权”，利用 OAuth2，用户可以把自己的一些权限开放给第三方。

通过 OAuth2 允许用户使用 KOOK 账号登录访问第三方网站等功能.

## 接口

| 接口                                                                         | 说明                                 | 
|----------------------------------------------------------------------------|------------------------------------|
| [获取AccessToken](https://developer.kookapp.cn/doc/http/oauth#获取AccessToken) | 用户完成授权后, 可通过该接口获取 AccessToken 授权凭证 |


## Web 应用接入流程

**配置OAuth客户端**
- 第一步: 取得机器人 OAuth 相关资质, 详情咨询开发者中心工作人员
- 第二步: 登录开发者中心 -> 应用详情 -> OAuth2 -> 获取 OAuth 客户端的 client_id 及 client_secret -> 配置 OAuth 授权回调地址(redirect_uri)

示例:
![oauth2-配置页面](https://img.kookapp.cn/assets/2022-07/1rIQiuEnvv1hc0u0.png)

**接入流程**
> 目前 KOOK 仅支持 `authorization_code` 授权方式

你可以通过配置页面的 *OAuth2链接生成器* 或自行按照规则拼接生成 OAuth 链接(需在机器人配置中的白名单内), 你的应用应当引导用户点击或跳转到该链接，他们会跳转到相应的授权页面。

示例:
![oauth2-授权页](https://img.kookapp.cn/assets/2022-07/EPjUXJWcDX0dh0eq.png)

当用户完成授权后, KOOK 会引导用户跳转至你链接参数当中的回调地址(需在机器人配置中的白名单内), 并将携带 `authorization_code` 的参数作为 HTTP query (GET 参数) 传递.

示例: 
```
https://xxx.xxx.xx/oauth/?code=099096fxxxxx32f489&state=c2275ac413bxxxxx5055
```

你的应用获取到该 `code` 参数后, 即可调用 [获取AccessToken](https://developer.kookapp.cn/doc/http/oauth#获取AccessToken) 接口获取授权凭证 AccessToken

> 当 AccessToken 过期后需再次引导用户重新授权

此时整个授权流程已经完成, 你可以使用该 token 作为进行用户授权范围内(scope)的动作

接口请求header示例:
Authorization: Bearer xxxxxxxxxxxx

> 参考 [http 接口规范 - 鉴权](https://developer.kookapp.cn/doc/reference#鉴权)


## 目前支持的 Scope 及对应能力范围

scope: **get_user_info** *允许读取用户信息*

| 接口               | 说明                                                              | 备注                           |
|------------------|-----------------------------------------------------------------|------------------------------|
| `api/v3/user/me` | [获取用户基本信息](https://developer.kookapp.cn/doc/http/user#获取当前用户信息) | 此接口当发生在 OAuth 访问时, 仅返回用户基本信息 |

scope: **get_user_guilds** *允许获取用户加入的服务器信息*

| 接口                  | 说明                                                                           | 备注  |
|---------------------|------------------------------------------------------------------------------|-----|
| `api/v3/guild/list` | [获取当前用户加入的服务器列表](https://developer.kookapp.cn/doc/http/guild#获取当前用户加入的服务器列表) |     |