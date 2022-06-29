# KMarkdown

在发送聊天消息时，为了支持用户的复杂的消息需求，以及有更好的用户体验，我们引入了 markdown，同时，基于 markdown 的标准规范，我们加入了自己的一些适配和扩展。为了与 markdown 进行区分，在本文档中，我们统一称之为 KMarkdown。

我们仅支持在文档中的一些语法，如果某个语法在 markdown 中，但是却没在文档中提及，那么它属于我们目前不支持的语法，建议用户不要使用。

我们还提供了 kmarkdown 消息编辑器，方便可视化编辑：[点击使用](https://kookapp.cn/tools/message-builder.html#/kmarkdown)

## 主要格式规范

1. 语法来源大部分来自于默认的 markdown 语法。如果无特殊说明，用户只需遵守 markdown 语法即可。
2. 自定义的语法大部分会保证这样的格式：`(tagName)value(tagName)[attributes]`, 如果这个标签没有属性，那么 `[attributes]` 会被省略。
3. 大部分标签都支持换行。

| 格式                                   | 语法来源 | 说明                                                                                     |
| -------------------------------------- | -------- | ---------------------------------------------------------------------------------------- |
| `**加粗文字**`                         | markdown | 加粗                                                                                     |
| `*斜体文字*`                           | markdown | 斜体                                                                                     |
| `***加粗斜体***`                       | markdown | 加粗斜体                                                                                 |
| `~~删除线~~`                           | markdown | 删除线                                                                                   |
| `[链接文字](链接地址)`                 | markdown | 链接，仅允许 http, https 的链接                                                          |
| `---`                                  | markdown | 分隔线                                                                                   |
| `> hello world`                        | markdown | 引用：换行会一直作用，直到遇见两个换行(\n\n),这两个换行实际不会显示换行                  |
| `(ins)下划线内容(ins)`                 | 自定义   | 下划线                                                                                   |
| `(spl)剧透(spl)`                       | 自定义   | 内容默认是遮住的，只有用户点击才会显示                                                   |
| `:emoji:`                              | emoji    | 基本与 emoji 的 [shortcode](https://www.webfx.com/tools/emoji-cheat-sheet/) 写法保持一致 |
| `(emj)服务器表情名(emj)[服务器表情id]` | 自定义   | 服务器表情，需要有服务器发送服务器表情的权限                                             |
| `(chn)频道ID(chn)`                     | 自定义   | 频道，提及频道                                                                           |
| `(met)用户id/here/all(met)`            | 自定义   | @用户，all 代表 @所有用户，here 代表 @所有在线用户                                       |
| `(rol)角色ID(rol)`                     | 自定义   | @某角色所有用户                                                                          |
| `` `行内代码` ``                       | markdown | 行内代码                                                                                 |
| ` ```语言\n ``` `                      | markdown | 代码块                                                                                   |

# 卡片消息

卡片消息是结构化的消息,可以提供一个易用、统一的富交互形式。

我们还提供了卡片消息编辑器，方便可视化编辑：[点击使用](https://kookapp.cn/tools/message-builder.html#/card)

## 整体结构说明

cardmessage 主要由 json 构成，在卡片消息中，有四种类别的卡片结构：

- 卡片，目前只有 card。
- 模块，主要有 section, header, context 等。
- 元素：主要有 plain-text, image, button 等。
- 结构：目前只有 paragraph。

### 消息的主要结构

- 一个卡片消息最多只允许 5 个卡片
- 一个卡片可以有多个模块，但是一个卡片消息总共不允许超过 50 个模块

```javascript
[
  {
    type: 'card',
    //...
    modules: [
      // ...
    ],
  },
  // 其它card
];
```

### 主要结构说明

所有的元素都有相似的结构，大体如下：

```javascript
{
    "type" : "类别"，
    "foo" : "bar",   //属性参数
    "modules|elements|fields": [], //子元素，根据type类别有不同的值，卡片的为modules,模块的子元素为elements,结构的为fields。
}
```

### 一些全局字段说明

在很多结构中，有一些字段都是一样的，因此在此处说明，后面就不单独说明了：

| 字段  | 类型   | 说明                                                                                                           |
| ----- | ------ | -------------------------------------------------------------------------------------------------------------- |
| theme | string | 主题，可选的值为：primary,success,danger,warning,info,secondary, none.默认为 primary，为 none 时不显示侧边框。 |
| size  | string | 大小，可选值为：xs,sm, md, lg, 一般默认为 lg                                                                   |

### 卡片消息发送说明

在消息发送时，卡片消息的发送类型为`10`, 在发送时，content 字段为 json 的字符串。详情参见消息发送接口。发送前请调用各语言自带的 json 序列化方法进行序列化再进行发送，直接发送未经序列化的 json 字符串通常会产生错误。

### 关于卡片中包含的媒体

**如果卡片中包含第三方媒体链接，我们将会自行转存媒体后再完成发送。**推荐大家优先调用 asset 接口上传媒体文件后再进行发送，以防由于转存失败导致卡片发送不成功。

## 卡片

### card

**主要结构**：

```javascript
{
    "type": "card",
    "theme" : "primary|warning|danger|info|none...", // 卡片风格，默认为primay
    "color":"#aaaaaa", //色值
    "size": "sm|lg", //目前只支持sm与lg, 如果不填为lg。 lg仅在PC端有效, 在移动端不管填什么，均为sm。
    "modules": [
        // modules...
    ]
}
```

**说明：**

- modules 只能为模块
- 单个 card 模块数量不限制，但是总消息最多只能有 50 个模块
- theme, size 参见[全局字段说明
  ](#一些全局字段说明),卡片中，size 只允许 lg 和 sm
- color 代表卡片边框具体颜色，如果填了，则使用该 color，如果未填，则使用 theme 来渲染卡片颜色。

## 模块

### 标题模块

**作用说明：** 标题模块只能支持展示标准文本（text），突出标题样式。
**主要结构：**

```javascript
{
    "type": "header",
    "text" : {
        "type": "plain-text",
        "content": "标题1"
    }
}
```

**说明：**

- text 为文字元素且 content 不能超过 100 个字

### 内容模块

**作用说明：** 结构化的内容，显示文本+其它元素。  
**主要结构：**

```javascript
{
    "type": "section",
    "mode" : "left|right", //accessory在左侧还是在右侧
    "text" : {
        "type": "plain-text|kmarkdown|paragraph",
        //...
    },
    "accessory": {
        "type": "image|button",
        //...
    }
}
```

**说明：**

- text 可以为 plain-text, kmarkdown 或者 paragraph
- accessory 可以为 image 或者 button
- button 不能放置在左侧
- mode 代表 accessory 是放置在左侧还是在右侧

### 图片组模块

**作用说明：** 1 到多张图片的组合  
**主要结构:**

```javascript
{
    "type" : "image-group",
    "elements": [
        //图片元素，其它元素无效
    ],
}
```

**说明：**

- elements 只能有 image 元素，只能有 1-9 张图片

### 容器模块

**作用说明：** 1 到多张图片的组合，与图片组模块不同，图片并不会裁切为正方形。多张图片会纵向排列。  
**主要结构:**

```javascript
{
    "type" : "container",
    "elements": [
        //图片元素，其它元素无效
    ],
}
```

**说明：**

- elements 只能有 image 元素，只能有 1-9 张图片

### 交互模块

**作用说明：** 交互模块中包含交互控件元素，目前支持的交互控件为按钮（button）  
**主要结构:**

```javascript
{
    "type": "action-group",
    "elements": [
        // buttons
    ],
}
```

**说明：**

- elements 中只能为 button
- elements 最多只能有 4 个

### 备注模块

**作用说明：** 展示图文混合的内容。  
**主要结构：**

```javascript
{
    "type": "context",
    "elements": [],
}
```

**说明：**

- elements 中可以为：plain-text, kmarkdown, image
- elements 最多可包含 10 个元素

### 分割线模块

**作用说明：** 展示分割线。  
**主要结构：**

```javascript
{
    "type": "divider",
}
```

### 文件模块

**作用说明：** 展示文件，目前有三种，文件，视频和音频。  
**主要结构：**

```javascript
{
    "type": "file|audio|video",
    "src": "", //文件|音频|视频地址
    "title": "标题",
    "cover": "" //封面图
}
```

规则：

- cover 仅在音频的时候有效，是音频的封面图。

### 倒计时模块

**作用说明：** 展示倒计时。  
**主要结构：**

```javascript
{
    "type": "countdown",
    "endTime" : 1608819168000, //到期的毫秒时间戳
    "startTime" : 1608819168000, //起始的毫秒时间戳，仅当mode为second才有这个字段
    "mode" : "day,hour,second", //倒计时样式, 按天显示，按小时显示或者按秒显示
}
```

规则：

- mode 主要是倒计时的样式，目前支持三种样式。
- startTime 和 endTime 为毫秒时间戳，startTime 和 endTime 不能小于服务器当前时间戳。

### 邀请模块

**作用说明：** 提供服务器邀请/语音频道邀请
**主要结构：**

```json
{ "type": "invite", "code": "邀请链接或者邀请码" }
```

## 元素

### 普通文本

**作用说明：** 显示文字。  
**主要结构：**

```javascript
{
    "type": "plain-text",
    "content" : "",
    "emoji": true|false,
}
```

**规则：**

- emoji 为布尔型，默认为 true。如果为 true,会把 emoji 的 shortcut 转为 emoji
- 为了方便书写，所有 plain-text 的使用处可以简单的用字符串代替。
- 最大 2000 个字

```javascript
// "hello world" 等价于：
{
    "type" : "plain-text",
    "emoji": true,
    "content" : "hello world",
}
```

### kmarkdown

**作用说明：** 显示文字。  
**主要结构：**

```javascript
{
    "type": "kmarkdown",
    "content" : "**hello**",
}
```

**规则：**

- 最大 5000 个字

### 图片

**作用说明：** 显示图片。  
**主要结构：**

```javascript
{
    "type": "image",
    "src" : "",
    "alt" : "",
    "size" : "sm|lg", // size只用在图文混排  图片组大小固定
    "circle" : true|false,
}
```

**规则：**

- 图片类型（MimeType）限制说明：目前仅支持`image/jpeg`, `image/gif`, `image/png`这 3 种
- 图片的 size 默认为 lg

### 按钮

**作用说明：** 提供交互的功能

```javascript
{
    "type": "button",
    "theme": "primary|warning|info|danger|...", //按钮的主题颜色
    "value": "", //要传递的value，为string
    "click": "", //click时的事件类型， return-val 返回value值
    "text": "",
}
```

- value 只能为 string
- text 可以为 plain-text, kmarkdown
- click 代表用户点击的事件,默认为""，代表无任何事件。
  - 当为 link 时，会跳转到 value 代表的链接;
  - 当为 return-val 时，系统会通过系统消息将消息 id,点击用户 id 和 value 发回给发送者，发送者可以根据自己的需求进行处理,消息事件参见[button 点击事件](https://developer.kookapp.cn/doc/event/user#Card%E6%B6%88%E6%81%AF%E4%B8%AD%E7%9A%84Button%E7%82%B9%E5%87%BB%E4%BA%8B%E4%BB%B6)。当前仅在频道中有效，私聊无法使用点击事件。

## 结构体

### 区域文本

**作用说明：** 支持分栏结构，将模块分为左右两栏，根据顺序自动排列，支持更自由的文字排版模式，提高可维护性  
**主要结构：**

```javascript
{
    "type": "paragraph",
    "cols": 3, //移动端忽略该参数
    "fields" : [
    ],
}
```

**规则：**

- cols 是 int,可以的取值为 1-3
- fields 可以的元素为 text, kmarkdown 或 context
- paragraph 最多有 50 个元素
