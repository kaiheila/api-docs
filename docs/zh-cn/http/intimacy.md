# 亲密度相关接口列表

本文档主要列出亲密度相关的接口。机器人可以在后台配置默认的初始亲密度和形象，当用户触发某些事件时，机器人可以根据一些逻辑来更新与该用户的亲密度以及形象展示。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kookapp.cn/doc/reference)。

| 接口                                       | 接口说明         | 维护状态 |
| ------------------------------------------ | ---------------- | -------- |
| [/api/v3/intimacy/index](#获取用户亲密度)  | 获取用户的亲密度 | 正常     |
| [/api/v3/intimacy/update](#更新用户亲密度) | 更新用户的亲密度 | 正常     |

## 获取用户亲密度

### 接口说明

| 地址                     | 请求方式 | 说明 |
| ------------------------ | -------- | ---- |
| `/api/v3/intimacy/index` | GET      |      |

### 参数列表

| 参数名  | 位置  | 类型   | 必需 | 说明      |
| ------- | ----- | ------ | ---- | --------- |
| user_id | query | string | true | 用户的 id |

### 返回参数说明

| 参数名      | 类型   | 说明                           |
| ----------- | ------ | ------------------------------ |
| img_url     | string | 机器人给用户显示的形象图片地址 |
| social_info | string | 机器人显示给用户的社交信息     |
| last_read   | int    | 用户上次查看的时间戳           |
| score       | int    | 亲密度，0-2200                 |
| img_list    | Array  | 形象图片的总列表               |
| » id        | string | 形象图片的 id                  |
| » url       | string | 形象图片的地址                 |

### curl 示例

请求示例：

```bash
curl -H "Authorization: Bot your_token" "https://www.kaiheila.cn/api/v3/intimacy/index?user_id=xxx"
```

返回示例：

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "img_url": "",
    "social_info": "test",
    "last_modify": 1607432478030,
    "last_read": 0,
    "score": 123,
    "img_list": [
      {
        "id": "11",
        "url": ""
      },
      {
        "id": "8821",
        "url": ""
      }
    ]
  }
}
```

## 更新用户亲密度

### 接口说明

| 地址                      | 请求方式 | 说明      |
| ------------------------- | -------- | --------- |
| `/api/v3/intimacy/update` | POST     | post json |

### 参数列表

| 参数名        | 位置 | 类型    | 必需  | 说明                               |
| ------------- | ---- | ------- | ----- | ---------------------------------- |
| user_id     | body | string  | true  | 用户 id                            |
| score       | body | integer | false | 亲密度，0-2200                     |
| social_info | body | string  | false | 机器人与用户的社交信息，500 字以内 |
| img_id      | body | string  | false | 形象图片 ID                          |

### 返回参数说明

| 地址 | 请求方式 | 说明 |
| ---- | -------- | ---- |

### curl 示例

请求示例：

```bash
curl "https://www.kaiheila.cn/api/v3/intimacy/update" -L \
-H "Authorization: Bot xxx" -H "Content-type: application/json;" \
-d '{"user_id":"user_id", "social_info":"test", "score": 123, "img_id" : 1}'
```

返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {}
}
```
