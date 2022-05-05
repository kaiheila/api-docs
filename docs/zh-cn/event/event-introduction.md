# 事件结构/格式说明

当 websocket 或 webhook 收到 `s=0` 的消息时，代表当前收到的消息是事件(包含用户的聊天消息及系统的通知消息等)。本文会具体描述所有的事件类型，并且明确其字段的含义。开发者可以根据本文档做出相应的开发处理。

## 事件基本结构及含义说明

目前所有的消息都会有如下的结构：

```json
{
  "s": 0, // 信令类型
  "d": {} //数据
}
```

本文主要讲述的是当 `s=0` 时，data 的数据结构，信令的具体含义参见[websocket](https://developer.kaiheila.cn/doc/websocket).

## 事件主要格式

### 格式说明

| 字段          | 类型   | 说明                                                                                               |
| ------------- | ------ |--------------------------------------------------------------------------------------------------|
| channel_type  | string | 消息通道类型, `GROUP` 为组播消息, `PERSON` 为单播消息, `BROADCAST` 为广播消息                                         |
| type          | int    | 1:文字消息, 2:图片消息，3:视频消息，4:文件消息， 8:音频消息，9:KMarkdown，10:card 消息，255:系统消息, 其它的暂未开放                    |
| target_id     | string | 发送目的, 频道消息类时, 代表的是频道 channel_id，如果 channel_type 为 `GROUP` 组播且 type 为 `255` 系统消息时，则代表服务器 guild_id |
| author_id     | string | 发送者 id, 1 代表系统                                                                                   |
| content       | string | 消息内容, 文件，图片，视频时，content 为 url                                                                    |
| msg_id        | string | 消息的 id                                                                                           |
| msg_timestamp | int    | 消息发送时间的毫秒时间戳                                                                                     |
| nonce         | string | 随机串，与用户消息发送 api 中传的 nonce 保持一致                                                                   |
| extra         | mixed  | 不同的消息类型，结构不一致                                                                                    |

### 文字频道消息 extra 说明

**当 type 非系统消息(255)时**

| 字段          | 类型    | 说明                                                                             |
| ------------- | ------- | -------------------------------------------------------------------------------- |
| type          | int     | 同上面 type                                                                      |
| guild_id      | string  | 服务器 id                                                                        |
| channel_name  | string  | 频道名                                                                           |
| mention       | Array   | 提及到的用户 id 的列表                                                           |
| mention_all   | boolean | 是否 mention 所有用户                                                            |
| mention_roles | Array   | mention 用户角色的数组                                                           |
| mention_here  | boolean | 是否 mention 在线用户                                                            |
| author        | Map     | 用户信息, 见[对象-用户 User](https://developer.kaiheila.cn/doc/objects#用户User) |

### 系统事件消息 extra 说明

**当 type 为系统消息(255)时**

| 字段 | 类型   | 说明                                         |
| ---- | ------ | -------------------------------------------- |
| type | string | 标识该事件的类型                             |
| body | Map    | 该事件关联的具体数据, 详见各系统消息事件示例 |
