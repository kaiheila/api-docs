# 速率限制

为了防止接口滥用和超速，我们会通过速率限制来限制 API 接口请求。

## http 头格式

在每个 API 请求中，我们会在需要速率控制的请求的 http 响应的 header 中，包含如下的速度控制的头：

```
// 一段时间内允许的最大请求次数
X-Rate-Limit-Limit: 5
// 一段时间内还剩下的请求数
X-Rate-Limit-Remaining: 0
// 回复到最大请求次数需要等待的时间
X-Rate-Limit-Reset: 14
// 请求数的bucket
X-Rate-Limit-Bucket: user/info
// 触犯全局请求次数限制
X-Rate-Limit-Global
```

## 超速响应

当触犯速度限制时，系统会返回 http 429 响应。返回的消息格式与标准格式也是一致的。同时，上文中提到的 http 头也依旧会传。

## 封禁措施

如果多次超速，系统会发出警告信息。bot 需要按照 rate limit 的头进行速度控制。  
如果多次警告后依然不更改，系统可能会禁用 bot。
