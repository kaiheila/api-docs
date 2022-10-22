# Gateway

本文档主要列出 Gateway 相关接口。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kookapp.cn/doc/reference)。

| 接口                                       | 接口说明         | 维护状态 |
| ------------------------------------------ | ---------------- | -------- |
| [/api/v3/gateway/index](#获取网关连接地址) | 获取网关连接地址 | 正常     |

## 获取网关连接地址

### 接口说明

| 地址                    | 请求方式 | 说明 |
| ----------------------- | -------- | ---- |
| `/api/v3/gateway/index` | GET      |      |

### 参数列表

| 参数名   | 位置  | 类型    | 必需  | 说明                                 |
| -------- | ----- | ------- | ----- | ------------------------------------ |
| compress | query | integer | false | 下发数据是否压缩，默认为`1`,代表压缩 |

### 返回参数说明

| 参数名 | 类型   | 说明           |
| ------ | ------ | -------------- |
| url    | string | 网关的连接地址 |

### 返回示例

```javascript
{
    "code": 0,
    "message": "操作成功",
    "data": {
        "url": "wss://xxxx"
    }
}
```

## 关于重连

如果需要重连，请在连接 gateway 时加入 resume=1，如下方示例：

```php
if ($this->getSessionId()) {
    $gateWay = $gateWay.'&'.http_build_query([
        'sn' => $this->maxSn,
        'session_id' => $this->getSessionId(),
        'resume' => 1,
    ]);
}
```

```
wss://test.kaiheila.com:8888/gateway?{compress/token parameters}&resume=1&sn=5&sessionId=20****ae-1fa4-4d19-805f-6f0f****d534
```
