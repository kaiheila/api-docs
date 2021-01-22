# 卡片消息

卡片消息是结构化的消息,可以提供一个易用、统一的富交互形式。

## 整体结构说明
cardmessage主要由json构成，在卡片消息中，有四种类别的卡片结构：
- 卡片，目前只有card。
- 模块，主要有section, header, context等。
- 元素：主要有plain-text, image, button等。
- 结构：目前只有paragraph。

### 消息的主要结构
- 一个卡片消息最多只允许5个卡片
- 一个卡片可以有多个模块，但是一个卡片消息总共不允许超过50个模块

```javascript
[
    {
        "type": "card",
        //...
        "modules" : [
            // ...
        ]
    }
    // 其它card
]
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

|字段|类型|说明|
|--|--|--|
|theme|string|主题，可选的值为：primary,success,danger,warning,info,secondary.默认为primary。|
|size|string|大小，可选值为：xs,sm, md, lg, 一般默认为lg|

### 卡片消息发送说明
在消息发送时，卡片消息的发送类型为`10`, 在发送时，content字段为json的字符串。详情参见消息发送接口。


## 卡片

### card
**作用说明：** 标题模块只能支持展示标准文本（text），突出标题样式。

**主要结构**：
```javascript
{
    "type": "card",
    "theme" : "primary|warning|danger|info...", // 卡片风格，默认为primay
    "color":"#aaaaaa", //色值
    "size": "sm|lg", //目前只支持sm与lg, 如果不填为lg。 lg仅在PC端有效, 在移动端不管填什么，均为sm。
    "modules": [
        // modules...
    ]
}
```
**说明：**
- modules只能为模块
- 单个card模块数量不限制，但是总消息最多只能有50个模块
- theme, size参见[全局字段说明
](#一些全局字段说明),卡片中，size只允许lg和sm
- color代表卡片边框具体颜色，如果填了，则使用该color，如果未填，则使用theme来渲染卡片颜色。

## 模块

### 标题模块
**作用说明：** 标题用于卡片中，突出标题样式。  
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
- text 为文字元素且content不能超过100个字

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
- text可以为 plain-text, kmarkdown或者paragraph
- accessory可以为image或者button
- button不能放置在左侧
- mode代表accessory是放置在左侧还是在右侧

### 图片模块
**作用说明：** 1到多张图片的组合  
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
- elements只能有image元素，只能有1-9张图片

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
- elements中只能为button
- elements最多只能有4个

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
- elements中可以为：plain-text, kmarkdown, image
- elemetns最多可包含10个元素

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
- cover仅在音频的时候有效，是音频的封面图。


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
- mode主要是倒计时的样式，目前支持三种样式。
- startTime和endTime为毫秒时间戳，startTime和endTime不能小于服务器当前时间戳。

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
- emoji为布尔型，默认为true。如果为true,会把emoji的shortcut转为emoji 
- 为了方便书写，所有plain-text的使用处可以简单的用字符串代替。

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

### 图片
**作用说明：** 显示图片。  
**主要结构：**
```javascript
{
    "type": "image",
    "src" : "",
    "alt" : "",
    "size" ： "sm|lg", // size只用在图文混排  图片组大小固定
    "circle" : true|false,
}
```
**规则：**
- 图片类型（MimeType）限制说明：目前仅支持`image/jpeg`, `image/gif`, `image/png`这3种
- 图片的size默认为lg

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
- value只能为string
- text可以为plain-text, kmarkdown
- click代表用户点击的事件,默认为""，代表无任何事件。
    - 当为link时，会跳转到value代表的链接;
    - 当为return-val时，系统会通过系统消息将消息id,点击用户id和value发回给发送者，发送者可以根据自己的需求进行处理。

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
- cols是int,可以的取值为1-3
- fields可以的元素为text, kmarkdown或context
- paragraph最多有50个元素

