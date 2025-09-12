# 帖子相关接口列表

本文档主要列出帖子相关接口。

帖子频道是一种新的服务器频道类型，允许用户在内产生帖子内容，沉淀知识、经验与分享到服务器内。

| 关键词   | 解释     |
|-------|--------|
| 主楼	    | 特指帖子频道的帖子主楼，为发帖者在发送帖子时的内容。|
| 回复  | 指帖子的一级回复，所有回复某条帖子的内容。 |
| 楼中楼 | 指帖子回复的回复|
分区（Category）分为全部（综合）与用户自行创建的分区。 在发帖时，可选指定一个存在的有权限的分区发送。 若不选择，则视为其“未选择分区”，仅会在“综合”页面显示。若用户选择了分区，则会同时显示在“综合”页面与对应的分区页面。

帖子（Thread）相当于一个区域，所有评论/回复（包括主楼）都属于该帖子。主楼和回复使用图文混排的模式呈现内容，楼中楼仅支持KMD和表情。

本文档中的接口均符合接口规范，如有疑问，建议先查阅[接口引言](https://developer.kookapp.cn/doc/reference)。

| 接口                                 | 接口说明     | 维护状态 |
|------------------------------------|----------| -------- |
| [/api/v3/category/list](#获取帖子分区列表) | 获取帖子分区列表 | 正常     |
| [/api/v3/thread/create](#创建帖子)     | 创建帖子     | 正常     |
| [/api/v3/thread/reply](#评论/回复)     | 评论/回复    | 正常     |
| [/api/v3/thread/view](#帖子详情)       | 帖子详情     | 正常     |
| [/api/v3/thread/list](#帖子列表)       | 帖子列表     | 正常     |
| [/api/v3/thread/delete](#帖子/评论/回复删除)     | 帖子删除     | 正常     |
| [/api/v3/thread/post](#回复列表)     | 回复列表     | 正常     |


## Category帖子分区详情参数说明

| 名称       | 类型   | 说明                |
|----------| ------ |-------------------|
| id       | string | 帖子分区ID            |
| name     | string | 分区名               |
| allow    | int    | 默认为 0,想要设置的允许的权限值 |
| deny | int    | 默认为 0,想要设置的拒绝的权限值 |
| roles     | object | 角色或者用户在该分区下的权限值   |

## Thread帖子详情参数说明

 帖子属于某个分区，若无则默认综合分区，帖子相当于一个区域，所有评论/回复（包括主楼）都属于该帖子。

| 参数名             | 类型     | 说明                                   |
| ------------------ |--------|--------------------------------------|
| id                 | string | 帖子 id                                |
| status               | int    | 帖子状态, `1`代表审核中，`2`代表审核通过, `3`代表编辑审核中 |
| title        | string | 标题                                   |
| cover            | string | 封面url                                |
| category              | string | 分区id                                 |



## Post评论/回复详情参数说明

| 参数名             | 类型      | 说明                                   |
| ------------------ |---------|--------------------------------------|
| id                 | string  | 评论/回复 id                             |
| category_id               | string  | 分区id                                 |
| thread_id              | string  | _所属帖子id_                             |
| reply_id            | string  | 回复对象的id（回复主贴为0）                      |
| belong_to_post_id               | string  | 所属的评论的post_id                        |
| content        | string  | 卡片消息                                 |
| status             | int     | 回复状态, `1`代表审核中，`2`代表审核通过, `3`代表编辑审核中 |
| mention           | array   | `@特定用户` 的用户 ID 数组                                 |
| mention_all           | boolean | 是否含有 `@全体人员`                         |
| mention_here           | boolean | 是否含有 `@在线人员`                         |
| mention_part              | array   | `@特定用户` 详情                           |
| mention_role_part              | array   | `@特定角色` 详情                           |

## 获取帖子分区列表

### 接口说明

| 地址                           | 请求方式  | 说明                 |
| ----------------------------- | -------- | ------------------- |
| `/api/v3/category/list` | GET      |  |

### 参数列表

| 参数名     | 位置  | 类型   | 必需  | 说明      |
| ---------- | ----- | ------ | ----- |---------|
| channel_id   | query | string | true  | 帖子频道 id |

### 返回参数说明

返回值字段参考 [Category帖子分区详情参数说明](#Category帖子分区详情参数说明)

### 返回示例

```json
{
  "code":0,
  "message":"操作成功",
  "data":{
    "list":[
      {
        "id":"6",
        "name":"test",
        "allow":0,
        "deny":0,
        "roles":[]
      },
      {
        "id":"7",
        "name":"test",
        "allow":0,
        "deny":2048,
        "roles":[
          {
            "type":"user",
            "role_id":0,
            "user_id":"111111",
            "allow":2048
          },
          {
            "type":"role",
            "role_id":11111,
            "user_id":"",
            "allow":2048
          }
        ]
      },
      {
        "id":"8",
        "name":"test2",
        "allow":0,
        "deny":0,
        "roles":[]
      }
    ]
  }
}
```

## 创建帖子

### 接口说明

| 地址                 | 请求方式 | 说明 |
| -------------------- |------| ---- |
| `/api/v3/thread/create` | POST |      |

### 参数列表

| 参数名   | 位置    | 类型       | 必需    | 说明                 |
| -------- |-------|----------|-------|--------------------|
| channel_id | body  | string   | true  | 频道 id              |
| guild_id | body | string   | true  | 服务器 id             |
| category_id | body | string   | false | 帖子分区 id（若无默认为综合分区） |
| title | body | string   | true  | 标题                 |
| cover | body | string   | false | 封面url              |
| content | body | string   | true  | 卡片消息内容             |

### 返回参数说明

| 参数名             | 类型      | 说明                                                                   |
| ------------------ |---------|----------------------------------------------------------------------|
| post_id             | string  | 主楼id                                                                 |
| medias | array   | 卡片消息附加图片数组                                                           |
| preview_content          | string  | 预览文本                                                                 |
| user              | map     | 创建帖子用户数据参考[用户 User](https://developer.kookapp.cn/doc/objects#用户User) |
| category              | map     | 分区字段参考 [Category帖子分区详情参数说明](#Category帖子分区详情参数说明)                     |
| tags              | array   | 话题数组                                                                 |
其余返回值字段参考 [Thread帖子详情参数说明](#Thread帖子详情参数说明)以及（主楼数据）[Post评论/回复详情参数说明](#Post评论/回复详情参数说明)
### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "id": "111111",
    "status": 2,
    "title": "apitest",
    "cover": "https://xxx.com/xxxxx.png",
    "post_id": "xxxxxx",
    "medias": [
      {
        "type": 2,
        "src": "https://xxx.com/xxxxx.png",
        "title": ""
      }
    ],
    "preview_content": "机器人新闻播报：今日要闻 @全体成员  test@",
    "user": {
      "id": "xxxxx",
      "identify_num": "xxxx",
      "username": "test",
      "avatar": "https://xxx.com/xxxxx.png",
      "is_vip": false,
      "vip_avatar": "https://xxx.com/xxxxx.png",
      "nickname": "",
      "roles": [
        10219
      ]
    },
    "category": {
      "id": "xxx",
      "name": "xxx",
      "allow": 0,
      "deny": 0
    },
    "tags": [],
    "content": "",
    "mention": [],
    "mention_all": true,
    "mention_here": false,
    "mention_part": [],
    "mention_role_part": [],
    "channel_part": [],
    "item_part": []
  }
}
```
## 评论/回复

### 接口说明

| 地址                      | 请求方式 | 说明 |
| ------------------------- |------| ---- |
| `/api/v3/thread/reply` | POST  |      |

### 参数列表

| 参数名          | 位置    | 类型    | 必需    | 说明                                 |
| ------------- |-------| ------- |-------|------------------------------------|
| channel_id	   | body  | string  | true  | 频道 id                              |
| thread_id	    | body | string  | true  | 帖子 id                              |
| reply_id        | body | string  | false | 回复的post_id，如果是评论主楼则不传，回复其它楼和楼中楼则必传 |
| content       | body | string | true  | 文本                                 |


### 返回参数说明

返回值字段参考 [Post评论/回复详情参数说明](#Post评论/回复详情参数说明)

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "id": "xxxxxx",
    "reply_id": "0",
    "thread_id": "xxxxx",
    "is_updated": false,
    "mention": [],
    "mention_all": false,
    "mention_here": false,
    "content": "",
    "mention_part": [],
    "mention_role_part": [],
    "channel_part": [],
    "item_part": []
  }
}
```

## 帖子详情

### 接口说明

| 地址                    | 请求方式 | 说明 |
|-----------------------|------| ---- |
| `/api/v3/thread/view` | GET  |      |

### 参数列表

| 参数名          | 位置    | 类型    | 必需    | 说明                                 |
| ------------- |-------| ------- |-------|------------------------------------|
| channel_id	   | query  | string  | true  | 频道 id                              |
| thread_id	    | query | string  | true  | 帖子 id                              |


### 返回参数说明

| 参数名             | 类型    | 说明                                                                   |
| ------------------ |-------|----------------------------------------------------------------------|
| latest_active_time        | int   | 最后活跃时间                                                                |
| create_time             | int   | 创建时间                                                                 |
| is_updated | bool  | 是否被编辑过                                                           |
| content_deleted          | bool  | 内容是否被删除                                                                 |
| content_deleted_type              | int   | 删除类型：1作者自己删除 2管理员删除 3审核删除 |
| collect_num              | int   | 收藏数量                     |
| post_count              | int | 回复总数                                                                 |
其余返回值字段参考 [Thread帖子详情参数说明](#Thread帖子详情参数说明)以及（主楼数据）[Post评论/回复详情参数说明](#Post评论/回复详情参数说明)
### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "id": "xxxxxxxx",
    "status": 2,
    "title": "apitest",
    "cover": "https://xxx.com/xxxxx.png",
    "post_id": "78329392526262528",
    "medias": [
      {
        "type": 2,
        "src": "https://xxx.com/xxxxx.png",
        "title": ""
      }
    ],
    "preview_content": "机器人新闻播报：今日要闻 @全体成员  test@",
    "user": {
      "id": "xxxx",
      "identify_num": "xxx",
      "username": "test",
      "avatar": "https://xxx.com/xxxxx.png",
      "is_vip": false,
      "vip_avatar": "https://xxx.com/xxxxx.png",
      "nickname": "",
      "roles": []
    },
    "category": {
      "id": "1",
      "name": "10",
      "allow": 0,
      "deny": 0
    },
    "tags": [],
    "content": "",
    "mention": [],
    "mention_all": true,
    "mention_here": false,
    "mention_part": [],
    "mention_role_part": [],
    "channel_part": [],
    "item_part": [],
    "latest_active_time": 11111111111,
    "create_time": 111111111111,
    "is_updated": false,
    "content_deleted": false,
    "content_deleted_type": 0,
    "collect_num": 0,
    "post_count": 1
  }
}
```

## 帖子列表

### 接口说明

| 地址                    | 请求方式 | 说明 |
|-----------------------|------| ---- |
| `/api/v3/thread/list` | GET  |      |

### 参数列表

| 参数名   | 位置    | 类型     | 必需    | 说明                        |
| -------- |-------|--------|-------|---------------------------|
| channel_id | query  | string | true  | 频道 id                     |
| category_id | query | string | false | 帖子分区 id（若无默认为综合分区）        |
| sort | query | int    | false  | 排序规则，1最新回复 2最新创建，默认按频道设置来 |
| page_size | query | int    | false | 分页，默认30                   |
| time | query | int    | false  | 翻页时，从什么时间开始找(传最后一个帖子的对应时间，sort=1时取latest_active_time，sort=2时取create_time)            |

### 返回参数说明

返回值字段参考 [帖子详情](#帖子详情)
### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "items": [
      {
        "id": "111111",
        "status": 2,
        "title": "apitest",
        "cover": "https://xxx.com/xxxxx.png",
        "post_id": "xxxxxx",
        "medias": [
          {
            "type": 2,
            "src": "https://xxx.com/xxxxx.png",
            "title": ""
          }
        ],
        "preview_content": "机器人新闻播报：今日要闻test@",
        "user": {},
        "category": {
          "id": "",
          "name": "",
          "allow": 0,
          "deny": 0
        },
        "tags": [],
        "latest_active_time": 11111111111,
        "create_time": 11111111111,
        "is_updated": false,
        "content_deleted": false,
        "content_deleted_type": 0,
        "collect_num": 0,
        "post_count": 0
      },
      {
        "id": "0000",
        "status": 2,
        "title": "0000",
        "cover": "",
        "post_id": "0",
        "medias": [],
        "preview_content": "111",
        "user": {},
        "category": {
          "id": "xxxx",
          "name": "分区1",
          "allow": 0,
          "deny": 2048
        },
        "tags": [
          {
            "id": 111,
            "name": "xxx",
            "icon": ""
          }
        ],
        "latest_active_time": 1111111111111,
        "create_time": 1111111111111,
        "is_updated": false,
        "content_deleted": false,
        "content_deleted_type": 0,
        "collect_num": 0,
        "post_count": 0
      }
    ]
  }
}
```

## 帖子/评论/回复删除

### 接口说明

| 地址                      | 请求方式 | 说明 |
|-------------------------|------| ---- |
| `/api/v3/thread/delete` | POST |      |

### 参数列表

| 参数名          | 位置    | 类型    | 必需    | 说明                                                  |
| ------------- |-------| ------- |-------|-----------------------------------------------------|
| channel_id	   | body  | string  | true  | 频道 id                                               |
| thread_id	    | body | string  | false | 帖子id，删除整个贴子时必传，如果同时有post_id只会删除对应post	 |
| post_id	    | body | string  | false | 评论or回复的id，删除评论/回复时必传	                               |


### 返回参数说明
无返回参数

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {}
}
```


## 回复列表

### 接口说明

| 地址                    | 请求方式 | 说明 |
|-----------------------|------| ---- |
| `/api/v3/thread/post` | GET  |      |

### 参数列表

| 参数名          | 位置    | 类型     | 必需    | 说明                    |
| ------------- |-------|--------|-------|-----------------------|
| channel_id	   | query  | string | true  | 频道id                  |
| post_id	   | query  | string | false | 某一楼评论的post_id，查看楼中楼需要 |
| thread_id	    | query | string | true  | 帖子id	                 |
| time	    | query | string | false | 回复的create_time用于分页    |
| page_size		    | query | string | false | 一页几个	                 |
| order	    | query | string | true  | 'asc'升序 'desc'降序      |
| page	    | query | string | true  | 页码	                   |


### 返回参数说明
| 参数名             | 类型    | 说明                                                                   |
| ------------------ |-------|----------------------------------------------------------------------|
| create_time             | int   | 创建时间                                                                 |
| replies              | array | 这条回复的下的楼中楼，最多返回两条，其余需再次分页查询                                          |
| user              | map   | 创建帖子用户数据参考[用户 User](https://developer.kookapp.cn/doc/objects#用户User) |
其余返回值字段参考 [Post评论/回复详情参数说明](#Post评论/回复详情参数说明)

### 返回示例

```json
{
  "code": 0,
  "message": "操作成功",
  "data": {
    "meta": {
      "total": 3,
      "page": 1,
      "page_size": 10,
      "page_total": 1
    },
    "items": [
      {
        "id": "xxxx",
        "reply_id": "0",
        "thread_id": "xxxxx",
        "is_updated": false,
        "mention": [],
        "mention_all": false,
        "mention_here": false,
        "content": "",
        "mention_part": [],
        "mention_role_part": [],
        "channel_part": [],
        "item_part": [],
        "belong_to_post_id": "0",
        "create_time": 1111111111,
        "user": {
          "id": "111111",
          "identify_num": "1111",
          "username": "xxxxxxx",
          "avatar": "https://xxxxx.com/avatars/",
          "is_vip": true,
          "vip_avatar": "https://xxxxx.com/avatars/",
          "nickname": "xxx",
          "roles": []
        },
        "replies": [
          {
            "id": "1111111111",
            "reply_id": "xxxx",
            "thread_id": "xxxxx",
            "is_updated": false,
            "mention": [],
            "mention_all": false,
            "mention_here": false,
            "content": "",
            "mention_part": [],
            "mention_role_part": [],
            "channel_part": [],
            "item_part": [],
            "belong_to_post_id": "11111",
            "create_time": 11111111,
            "user": {}
          },
          {
            "id": "",
            "reply_id": "",
            "thread_id": "",
            "is_updated": false,
            "mention": [],
            "mention_all": false,
            "mention_here": false,
            "content": "",
            "mention_part": [],
            "mention_role_part": [],
            "channel_part": [],
            "item_part": [],
            "belong_to_post_id": "",
            "create_time": 1111111111,
            "user": {}
          }
        ]
      },
      {
        "id": "",
        "reply_id": "",
        "thread_id": "",
        "is_updated": false,
        "mention": [],
        "mention_all": false,
        "mention_here": false,
        "content": "",
        "mention_part": [],
        "mention_role_part": [],
        "channel_part": [],
        "item_part": [],
        "belong_to_post_id": "0",
        "create_time": 111111111,
        "user": {},
        "replies": []
      },
      {
        "id": "",
        "reply_id": "",
        "thread_id": "",
        "is_updated": false,
        "mention": [],
        "mention_all": false,
        "mention_here": false,
        "content": "",
        "mention_part": [],
        "mention_role_part": [],
        "channel_part": [],
        "item_part": [],
        "belong_to_post_id": "0",
        "create_time": 111111111,
        "user": {},
        "replies": []
      }
    ]
  }
}
```





