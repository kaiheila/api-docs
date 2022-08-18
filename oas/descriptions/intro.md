<br>
<div style="background-color: #F0F0F0;padding: 12px 0px 12px 12px;border-left: 5px solid #F90258;">
这不是一份官方文档，仅用于查看官方提供的OAS文件。
</div>  
<br>

## 引言

此文档仅用于方便开发者查看、确认 KOOK 机器人 API 接口，官方文档地址：[KOOK 开发者平台](https://developer.kookapp.cn/doc/)

两份文档内容基本相同，你可以选择自己习惯的查看方式。

建议使用[rapidoc](https://mrin9.github.io/RapiDoc/index.html)查看此 OpenAPI 描述文件，示例链接：[文档查看示例](https://fi6.github.io/kaiheila-api-docs/oas/rapidoc-view.html)

如果发现有任何问题，请提交 Issue/Pull Request，我们将尽快进行修复与合并。

## 简介

欢迎来到开发者酒馆，快找个位置随便坐！开发者中心的文档提供了丰富的 API 接口，介绍了机器人的开发语言、能力、调试等内容，帮助你快速了解机器人开发的方方面面，相信你在这里永远都不会空手而归。

我们将所有文档都藏在了 [GitHub](https://github.com/kaiheila/api-docs) 上，而且我们会不断添加新的功能！

### Bugs

如果你在使用 KOOK 的 API 过程中遇见了 Bug，并且希望上报给我们来纠正这个错误的话，我们提供了两种反馈方式。

- 你可以直接在 KOOK 官方的[开发者内测](https://kook.top/rc6aEk)中进行实时反馈，我们的技术会跟实时跟进你们的问题；
- 同时我们我们也提供了在 [GitHub](https://github.com/kaiheila/api-docs) 中的 [issue tracker](https://github.com/kaiheila/api-docs) 中进行反馈。

### SDK

热心的社区开发者们已经为大家准备了多种语言的 SDK，无需重复造轮子，上手即可轻松使用！如果希望你的 SDK 展示在此处，请于开发者服务器内联系`小波波#9366`。

| 语言                  | 仓库名                             | 仓库地址                                                          | 服务器邀请                            |
| --------------------- | ---------------------------------- | ----------------------------------------------------------------- | ------------------------------------- |
| PHP                   | kaiheila/php-bot                   | [仓库链接](https://github.com/kaiheila/php-bot)                   | 暂无                                  |
| JavaScript/TypeScript | fi6/KBotify & shugen002/BotRoot    | [仓库链接](https://github.com/fi6/kBotify)                        | [服务器邀请](https://kook.top/GO6qHj) |
| JavaScript/TypeScript | kookts/kook.ts                     | [仓库链接](https://github.com/kookts/kook.ts)                     | [服务器邀请](https://kook.top/GO6qHj) |
| Python                | TWT233/khl.py                      | [仓库链接](https://github.com/TWT233/khl.py)                      | [服务器邀请](https://kook.top/JJE0Es) |
| Python                | Tian-que/nonebot-adapter-kaiheila  | [仓库链接](https://github.com/Tian-que/nonebot-adapter-kaiheila)  | 暂无                                  |
| Python                | OlivOS-Team/OlivOS                 | [仓库链接](https://github.com/OlivOS-Team/OlivOS)                 | [服务器邀请](https://kook.top/8orLDo) |
| Ruby                  | DessertShop/KHL                    | [仓库链接](https://github.com/DessertShop/KHL)                    | [服务器邀请](https://kook.top/ie2ymJ) |
| 易语言                | 大鑫/酷黑                          | 暂无                                                              | [服务器邀请](https://kook.top/GymA7P) |
| 易语言                | Cyerol/Mengko 梦果框架             | 暂无                                                              | [服务器邀请](https://kook.top/OMWqzw) |
| Go                    | lonelyevil/khl                     | [仓库链接](https://github.com/lonelyevil/khl)                     | [服务器邀请](https://kook.top/r5s1WO) |
| Java                  | FightingGuys/rabbit（停止维护）    | [仓库链接](https://github.com/FightingGuys/rabbit)                | [服务器邀请](https://kook.top/O9A5AY) |
| Java                  | DeeChael/Kaiheila.java             | [仓库链接](https://github.com/DeeChael/Kaiheila.java)             | [服务器邀请](https://kook.top/9RB96R) |
| Java                  | Enaium/kook-spring-boot-starter    | [仓库链接](https://github.com/Enaium/kook-spring-boot-starter)    | [服务器邀请](https://kook.top/YaP12f) |
| Java                  | SNWCreations/JKook                 | [仓库链接](https://github.com/SNWCreations/JKook)                 | 暂无                                  |
| C#                    | PoH98/KHLSharp                     | [仓库链接](https://github.com/PoH98/KHLBotSharp)                  | 暂无                                  |
| C#                    | gehongyan/KaiHeiLa.Net             | [仓库链接](https://github.com/gehongyan/KaiHeiLa.Net)             | [服务器邀请](https://kook.top/EvxnOb) |
| Kotlin & Java         | KookyBot/KookyBot                  | [仓库链接](https://github.com/KookyBot/KookyBot)                  | [服务器邀请](https://kook.top/wnWOP9) |
| Kotlin & Java         | simple-robot/simbot-component-kook | [仓库链接](https://github.com/simple-robot/simbot-component-kook) | 暂无                                  |

### 机器人

机器人是增加聊天乐趣和提升管理服务器效率的新方式。你可以通过调整机器人的[亲密度](https://developer.kookapp.cn/bot)设置，来赋予它们独特的生命力，让它们与用户产生更为亲密的交互。当然你也可以创造一个严肃的管理机器人，或将他变成任何你想象中的样子，充分发挥你的想象力，让你的机器人变得与众不同！

快去创建一个属于你的[机器人](https://developer.kookapp.cn/bot)吧！

### 隐私政策

**更新日期：2020 年 12 月 9 日**

**生效日期：2020 年 12 月 9 日**

欢迎使用由**北京逍遥一下科技有限公司**（简称**“我们”**或**“KOOK”**）提供服务或运营控制的“KOOK”系列产品和服务，包括 KOOK 应用程序、 KOOK 移动端产品和服务（以下简称“**本平台**”）。

本隐私政策构成您与我们之间具法律约束力的协议，我们在此特别提醒您认真阅读、充分理解本协议各条款，特别是其中所涉及的免除、减轻我们责任的条款、对您权利限制条款、争议解决和法律适用等。**其中，限制、免责条款可能以黑体加粗或加下划线的形式提示您重点注意**。请您审慎阅读并选择接受或不接受本协议。若您不同意本隐私政策，请您停止访问或使用本平台。同时您也可以通过本隐私政策提供的联系方式与我们联系，我们将在我们的能力范围内配合您处理相关事宜。

### 用户信息

** KOOK API 不得用于以下用途：**

- **未经 KOOK 用户的明确许可**，修改 KOOK 用户的账号信息。例如，未经用户允许，机器人主动将用户加入到一个新的服务器当中；
- 替代 KOOK 用户**发送消息、上传文件或播放音频**；
- 无论在何种情况下，**未经 KOOK 用户的明确许可**，**获取用户的密码或网页证书**。

### 数据信息

** KOOK API 不得用于以下用途：**

- **抓取**任何 KOOK 数据；
- 将 KOOK 的数据用于运营机器人以外的其他用途；
- 未经用户明确许可，**分享**或**披露**任何用户的 KOOK 的相关数据；
- 向任何**第三方**网络广告，数据服务商或其他**获利渠道**披露 KOOK 的相关数据；
- **保留相关数据的时间**超出机器人正常运营所需要的时间；
- 违反 KOOK 的**用户隐私政策**；
- 获取 KOOK **用户密码**访问 KOOK 进行操作；
- **出售，许可**或以**其他方式**将 KOOK 的数据商业化；
- 以违反常识或违反用户预期的方式处理 KOOK 数据。

### 法律规定

** KOOK API 不得用于以下用途：**

- 推送包含**违反法律规定的信息**（色情、赌博、毒品、政治、人身攻击、欺诈信息等）；
- **导致死亡**，**人身伤害**或**破坏环境**等任何活动；
- 鼓励或促进**非法活动**或侵犯**第三方权益**；
- **诽谤**，**骚扰**，**跟踪**，**威胁他人**或以**其他方式**违反 KOOK **用户社区准则**。

### 滥用

**允许：**

- 要求您的最终用户**遵守**（非故意违反）法律、法规；
- 仅允许使用**开发者平台文档中规定的方式**访问 KOOK 的 API

**禁止**

- **删除、模糊或更改** KOOK 的服务条款或这些条款中的任何**链接**、**通知**、**内容**；
- **鼓励或为用户创建**违反 KOOK 服务条款的功能；
- 将 API**转授权**给第三方使用；
- 向 KOOK 的产品和服务中引入**任何病毒，蠕虫，缺陷，特洛伊木马，恶意软件**或**任何具有破坏性**的内容；
- **逆向工程**或尝试从任何 API 或相关软件中**提取源代码**；
- 使用**虚假**的身份登记、登录 KOOK 的开发者账户；
- 鼓励或允许第三方**违反 KOOK 开发者隐私政策**；
- **干扰**或**中断** KOOK 的 API 服务器或网络。

### 限制

KOOK 规定了对 API 的**使用限制**（例如：单位时间内发送 API 请求的数量，机器人所在服务器的数量，机器人可以服务的用户数量）。
如果您想使用超出此类限制的任何 API，必须获得 KOOK 的书面授权。

### 投诉与处罚规范

KOOK 的机器人已启用用户投诉处理机制，我们会根据用户的投诉，视违规程度予以不同程度的处罚措施。

我们理解你的违规行为可能基于失误、疏忽等过失，因此，若你的机器人存在不符合法律法规和平台规则等情形而被处理， KOOK 提供了邮件申诉渠道，你可以对你的机器人进行整改后，通过申诉渠道重新向 KOOK 提交发布审核。

### 变更

本隐私政策一旦发生任何重大变更，我们将尽合理努力向所有用户广而告之，例如通过在本平台上发布通知；但您应定期查看本隐私政策，以查看有关变更。我们还会更新本隐私政策顶部的“更新日期”和“生效日期”。您在本隐私政策更新之后继续访问或使用本平台，即视为您接受更新后的隐私政策。如果您不同意更新后的隐私政策，请您停止访问或使用本平台。

### 联系方式

与本政策相关的任何疑问、意见或请求，请发送至
[service@kookapp.cn](mailto:service@kookapp.cn)。
一般情况下，我们会在收到您相关联系信息并核实您身份后的【15】日内回复。

### 其他

（一）本隐私政策仅适用于您在中国大陆（仅为本条款之目的，不含香港、澳门、台湾地区）境内使用本平台服务的情形。本隐私政策可能存在多种语言版本，如各语言版本条款出现不一致或冲突，以中文版本为准。

（二）本隐私政策中的标题仅为方便及阅读而设，并不影响本隐私政策中任何规定的含义或解释。

## 参考

KOOK 的 API 正常分为两个核心层：

- 常规的 http 接口，你可以用它来做一些常规操作。
- 消息实时通知，你可以通过（webhook/websocket）来订阅系统的实时消息及事件，然后做出相应的操作等。

通过上述两层的接口，我们可以在 KOOK 中做出机器人，或者提供服务等。

### 常规 http 接口规范

#### BaseUrl

```
https://www.kookapp.cn/api
```

#### API 版本管理

KOOK 后续可能会有不同版本的 API。您可以通过像 `https://www.kookapp.cn/api/v{version_number}` 这样在请求路径中明确指定所要使用的 API 版本。如果省略掉 version_number, 它会指向默认的版本。目前支持的版本列表如下所示：

| 版本 | 状态   | 默认 |
| ---- | ------ | ---- |
| 3    | 开发中 | 是   |

#### 鉴权

在开发者中心，在创建机器人后，我们可以得到一个 token，在请求所有的 KOOK 接口时，我们需要在 http header 的 `Authorization` 中加入该 token 以进行鉴权,格式为 `Authorization: TOKEN_TYPE TOKEN`。目前支持两种格式的鉴权：

- 机器人。TOKEN_TYPE = Bot。
- Oauth2。TOKEN_TYPE = Bearer。

如下为机器人的鉴权示例:

```
Authorization: Bot BHsTZ4232tLatgV5AFyjoqZGAHHmpl9mTxYQ/u4/80=
```

#### 速度限制

为了保护我们的系统，我们在 [RFC 6585](https://tools.ietf.org/html/rfc6585#section-4) 的基础上做了一些扩展，来限制用户的接口调用速度。经常达到限速阀值或者忽略速度限制的 API 用户将会被撤销 API 密钥，并且被限制登录。有关速度限制的问题，请参阅[速率限制](https://developer.kookapp.cn/doc/rate-limit)一节

#### i18N

如果希望本地化，可以在 http 头中加入 `Accept-Language` 头，如下为一个示例：

```
Accept-Language: en-us
```

系统如果支持该语言，系统会以该语言返回错误消息等。如果系统不支持，系统会以默认的 zh-cn 来返回接口的消息，提示等。

#### 接口格式及返回说明

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

#### 接口字段说明

由于一些历史原因，接口中可能会有一些不在文档中的字段，请大家务必使用文档中的字段，不在文档中的字段后续可能会更改。

#### 请求参数

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

### 消息通知

消息通知在整个 KOOK 体系中比较复杂，我们目前支持两种消息通知机制：

- [Webhook](https://developer.kookapp.cn/doc/webhook)
- [Websocket](https://developer.kaiheila.cn/doc/websocket)

不论是以何种方式来接受消息，它们都遵循着相同的规范：

- 消息推送时，可能会有压缩(压缩默认采用 zlib 压缩【deflate】)。
- 消息的含义，结构格式等基本保持一致。

## 速率限制

为了防止接口滥用和超速，我们会通过速率限制来限制 API 接口请求。

### http 头格式

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

### 超速响应

当触犯速度限制时，系统会返回 http 429 响应。返回的消息格式与标准格式也是一致的。同时，上文中提到的 http 头也依旧会传。

### 封禁措施

如果多次超速，系统会发出警告信息。bot 需要按照 rate limit 的头进行速度控制。  
如果多次警告后依然不更改，系统可能会禁用 bot。
