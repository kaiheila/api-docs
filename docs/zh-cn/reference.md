# 简介

KOOK 的 API 正常分为两个核心层：

- 常规的 http 接口，你可以用它来做一些常规操作。
- 消息实时通知，你可以通过（webhook/websocket）来订阅系统的实时消息及事件，然后做出相应的操作等。

通过上述两层的接口，我们可以在 KOOK 中做出机器人，或者提供服务等。

## 常规 http 接口规范

### BaseUrl

```
https://www.kookapp.cn/api
```

### API 版本管理

KOOK 后续可能会有不同版本的 API。您可以通过像 `https://www.kookapp.cn/api/v{version_number}` 这样在请求路径中明确指定所要使用的 API 版本。如果省略掉 version_number, 它会指向默认的版本。目前支持的版本列表如下所示：

| 版本 | 状态   | 默认 |
| ---- | ------ | ---- |
| 3    | 开发中 | 是   |

### 鉴权

在开发者中心，在创建机器人后，我们可以得到一个 token，在请求所有的 KOOK 接口时，我们需要在 http header 的 `Authorization` 中加入该 token 以进行鉴权,格式为 `Authorization: TOKEN_TYPE TOKEN`。目前支持两种格式的鉴权：

- 机器人。TOKEN_TYPE = Bot。
- Oauth2。TOKEN_TYPE = Bearer。

如下为机器人的鉴权示例:

```
Authorization: Bot BHsTZ4232tLatgV5AFyjoqZGAHHmpl9mTxYQ/u4/80=
```

### 速度限制

为了保护我们的系统，我们在 [RFC 6585](https://tools.ietf.org/html/rfc6585#section-4) 的基础上做了一些扩展，来限制用户的接口调用速度。经常达到限速阀值或者忽略速度限制的 API 用户将会被撤销 API 密钥，并且被限制登录。有关速度限制的问题，请参阅[速率限制](https://developer.kookapp.cn/doc/rate-limit)一节

### i18N

如果希望本地化，可以在 http 头中加入 `Accept-Language` 头，如下为一个示例：

```
Accept-Language: en-US
```

系统如果支持该语言，系统会以该语言返回错误消息等。如果系统不支持，系统会以默认的 zh-cn 来返回接口的消息、提示等。

### 接口格式及返回说明

- 接口分为 GET 请求和 POST 请求，所有找服务器拿数据均使用 GET 请求，提交数据给服务器使用 POST 请求
- POST 请求若无特殊说明，均为 POST JSON 格式，即在 http header 中加入`Content-type: application/json`，并将数据以 json 字符串传递。
- 所有的接口返回如下的格式：

```javascript
{
    "code" : 0, // integer, 错误码，0代表成功，非0代表失败，具体的错误码参见错误码一览
    "message" : "error info", // string, 错误消息，具体的返回消息会根据Accept-Language来返回。
    "data" : [], // mixed, 具体的数据。
}
```

### 接口字段说明

由于一些历史原因，接口中可能会有一些不在文档中的字段，请大家务必使用文档中的字段，不在文档中的字段后续可能会更改。

### 请求参数

在 KOOK 整个 API 体系中，有一些参数是一致的，会在此处统一列出，后续不会再单独详细说明。

正常的列表页，一般会有类似如下的参数：

| 参数名    | 类型   | 区域 | 说明                                                                                                                   |
| --------- | ------ | ---- | ---------------------------------------------------------------------------------------------------------------------- |
| page      | int    | GET  | 列表页中有，代表页                                                                                                     |
| page_size | int    | GET  | 列表页中有，每页数据大小，默认为 50, 常规情况下 page_size 最大为 50                                                    |
| sort      | string | GET  | 代表排序的字段, 比如`-id`代表`id`按`DESC`排序，`id`代表`id`按`ASC`排序。不一定有, 如果有，接口中会声明支持的排序字段。 |

正常的列表页的返回参数会保持如下的格式:

| 参数名       | 类型  | 说明                                                                    |
| ------------ | ----- | ----------------------------------------------------------------------- |
| items        | Array | 数据列表                                                                |
| meta         | Map   | 分页的信息                                                              |
| » page       | int   | 页码                                                                    |
| » page_total | int   | 总页数                                                                  |
| » page_size  | int   | 每一页的数据                                                            |
| » total      | int   | 总数据量                                                                |
| sort         | Map   | 分页的排序, key:+-1, 如果为 1 代表按 key 升序，如果为-1 代表按 key 降序 |

## 消息通知

消息通知在整个 KOOK 体系中比较复杂，我们目前支持两种消息通知机制：

- [Webhook](https://developer.kookapp.cn/doc/webhook)
- [Websocket](https://developer.kookapp.cn/doc/websocket)

不论是以何种方式来接受消息，它们都遵循着相同的规范：

- 消息推送时，可能会有压缩(压缩默认采用 zlib 压缩【deflate】)。
- 消息的含义，结构格式等基本保持一致。
- webhook推送时sn 在到达 65535 后会重新从 1 开始计算, websocket推送时sn从1开始保持自增，没有65535的上限限制。
