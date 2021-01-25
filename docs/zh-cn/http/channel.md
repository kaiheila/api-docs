# 频道相关接口列表
本文档主要列出频道相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kaiheila.cn/doc/reference)。


|接口|接口说明|维护状态|
|--|--|--|
|[/api/v3/channel/message](#发送频道聊天消息)|发送频道聊天消息|正常|


## 发送频道聊天消息

### 接口说明
|地址|请求方式|说明|
|--|--|--|
|`/api/v3/channel/message`|POST| |

### 参数列表

| 参数名     | 类型 | 必传 | 参数区域 | 说明                                              |
| ---------- | ---- | ---- | -------  | ------------------------------------------------- |
| type | int  | 否    | POST | 消息类型, 见[objectName], 不传默认为 `1`, 代表文本类型。`2` 图片消息，`3` 视频消息，`4` 文件消息，`9` 代表 [kmarkdown](https://developer.kaiheila.cn/doc/kmarkdown) 消息, `10` 代表[卡片消息](https://developer.kaiheila.cn/doc/cardmessage)。|
| channel_id | string  | 是    | POST | 目标频道 id                                        |
| content    | string  | 是   | POST | 消息内容                                          |
| quote    | string  | 否   | POST | 回复某条消息的 `msgId`                                          |
| nonce      | string  | 否    | POST | nonce, 服务端不做处理, 原样返回                   |
|temp_target_id|string|否|POST|用户id,如果传了，代表该消息是临时消息，该消息不会存数据库，但是会在频道内只给该用户推送临时消息。用于在频道内针对用户的操作进行单独的回应通知等。|

### 返回参数说明

| 参数名   | 类型         | 说明                                                         |
| -------- | ------------ | ------------------------------------------------------------ |
| msg_id | string       | 服务端生成的消息 id                                       |     
| msg_timestamp | int          | 消息发送时间(服务器时间戳)                                          |     
| nonce | string |随机字符串，见参数列表 |    

### 返回示例

```json
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "msg_id": "50974c-364c983fa6cb",
        "msg_timestamp": 1607072537177,
        "nonce": "xxxx"
    }
}
```
