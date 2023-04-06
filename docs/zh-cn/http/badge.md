# Badge 相关文档

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kookapp.cn/doc/reference)。

| 接口                                        | 接口说明         | 维护状态 |
| ------------------------------------------- | ---------------- | -------- |
| [/api/v3/badge/guild](#获取服务器%20Badge) | 获取服务器 Badge | 正常     |

## 获取服务器 Badge

### 接口说明

| 地址                | 请求方式 | 说明 |
| ------------------- | -------- | ---- |
| /api/v3/badge/guild | GET      |      |

### 参数列表

| 参数名   | 位置  | 类型   | 必需  | 说明               |
| -------- | ----- | ------ | ----- | ------------------ |
| guild_id | query | string | true  | 服务器 id          |
| style    | query | int    | false | 样式类型，默认为 0 |

### 样式说明

| 样式类型 | 描述          | 示例                                                                                                                                    |
| -------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| 0        | 服务器名称    | [![「猎杀：对决」官方中文社区](https://www.kookapp.cn/api/v3/badge/guild?style=0&guild_id=5417470909511807)](https://kook.top/ESH4Ar) |
| 1        | 在线数        | [![War Selection官方中文社区](https://www.kookapp.cn/api/v3/badge/guild?style=1&guild_id=8838958323965995)](https://kook.top/hG4OJH)  |
| 2        | 在线数/总人数 | [![原神 ｜ 异世相遇](https://www.kookapp.cn/api/v3/badge/guild?style=2&guild_id=8258926332013541)](https://kook.top/C1rg7G)           |

### 返回参数说明

返回是一张图片，可以按照自己的需求使用。
