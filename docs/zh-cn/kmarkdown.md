# KMarkdown

在发送聊天消息时，为了支持用户的复杂的消息需求，以及有更好的用户体验，我们引入了 markdown，同时，基于 markdown 的标准规范，我们加入了自己的一些适配和扩展。为了与 markdown 进行区分，在本文档中，我们统一称之为 KMarkdown。

我们仅支持在文档中的一些语法，如果某个语法在 markdown 中，但是却没在文档中提及，那么它属于我们目前不支持的语法，建议用户不要使用。

我们还提供了kmarkdown消息编辑器，方便可视化编辑：[点击使用](https://kookapp.cn/tools/message-builder.html#/kmarkdown)

## 主要格式规范

1. 语法来源大部分来自于默认的 markdown 语法。如果无特殊说明，用户只需遵守 markdown 语法即可。
2. 自定义的语法大部分会保证这样的格式：`(tagName)value(tagName)[attributes]`, 如果这个标签没有属性，那么 `[attributes]` 会被省略。
3. 大部分标签都支持换行。

|格式|语法来源| 说明|
|--|--|--|
|`**加粗文字**`| markdown| 加粗|
|`*斜体文字*`|markdown|斜体|
|`***加粗斜体***`|markdown|加粗斜体|
|`~~删除线~~`|markdown|删除线|
|`[链接文字](链接地址)`|markdown|链接，仅允许 http, https 的链接。如果我们希望链接在下面显示缩略图(即链接解析)，需要保证链接文字与链接地址完全一致才可以|
|`---`|markdown|分隔线|
|`> hello world`|markdown|引用：换行会一直作用，直到遇见两个换行(\n\n),这两个换行实际不会显示换行|
|`(ins)下划线内容(ins)`|自定义|下划线|
|`(spl)剧透(spl)`|自定义|内容默认是遮住的，只有用户点击才会显示|
|`:emoji:`|emoji|基本与emoji的 [shortcode](https://www.webfx.com/tools/emoji-cheat-sheet/) 写法保持一致, [KOOK表情json文件](https://img.kookapp.cn/assets/emoji.json)|
|`(emj)服务器表情名(emj)[服务器表情id]`|自定义| 服务器表情，需要有服务器发送服务器表情的权限|
|`(chn)频道ID(chn)`|自定义|频道，提及频道|
|`(met)用户id/here/all(met)`|自定义|@用户，all 代表 @所有用户，here 代表 @所有在线用户|
|`(rol)角色ID(rol)`|自定义|@某角色所有用户|
|``` `行内代码` ```|markdown|行内代码|
|` ```语言\n ``` `|markdown|代码块|
|`\特殊字符`|markdown|转义，比如将命中语法的特殊字符原样显示|

## KMarkDown 消息 content 介绍

KMarkDown 消息的 content 本质上是一个 长文本字符串  
它会通过 JS 调用 一个 C++编写的wasm方法（后续会考虑使用 JS 编写解析器） 解析为一个 json 对象   
最后基于这个 JSON 在 react 中遍历后渲染成对应视图   

## 单个语法解析为对应 JSON 描述

### 加粗文字

`**加粗文字**`

``` json
// 行渲染
{
  "type": "control",
  "tagName": "line",
  "children": [
    {
      "type": "tag",
      // 使用 strong 标签
      "tagName": "strong",
      // 标签内的内容
      "children": [
        // 普通文本
        { "type": "text", "content": "加粗文字" }
      ]
    }
  ]
}
```

### 斜体文字

`*斜体文字*`

``` json
// 行渲染
{
  "type": "control",
  "tagName": "line",
  "children": [
    {
      "type": "tag",
      // 使用 em 标签
      "tagName": "em",
      // 标签内的内容
      "children": [
        // 普通文本
        { "type": "text", "content": "斜体文字" }
      ]
    }
  ]
}
```

### 删除线

`~~删除线~~`

``` json
// 行渲染
{
  "type": "control",
  "tagName": "line",
  "children": [
    // 行渲染
    {
      "type": "control",
      "tagName": "line",
      "children": [
        {
          "type": "tag",
          // del 标签
          "tagName": "del",
          "children": [{ "type": "text", "content": "删除线" }]
        }
      ]
    }
  ]
}
```

### 链接

`[链接文字](https://www.baidu.com/)`

``` json
// 行渲染
{
  "type": "control",
  "tagName": "line",
  "children": [
    // 行渲染
    {
      "type": "control",
      "tagName": "line",
      "children": [
        // 行内链接
        {
          "type": "tag",
          // a 标签
          "tagName": "a",
          "attrs": { "href": "https://www.baidu.com/" },
          "children": [{ "type": "text", "content": "链接文字" }]
        }
      ]
    }
  ]
}
```

### 分隔线

`---`

``` json
// 行渲染
{
  "type": "control",
  "tagName": "line",
  "children": [
    // hr 标签
    { "type": "tag", "tagName": "hr" }
  ]
}
```

### 引用

```
> 引用第一行
引用第二行
```

``` json
// 行渲染
{
  "type": "control",
  "tagName": "line",
  "children": [
    // 块引用
    {
      "type": "tag",
      "tagName": "blockquote",
      "children": [
        // 行渲染
        {
          "type": "control",
          "tagName": "line",
          "children": [{ "type": "text", "content": "引用第一行" }]
        },
        // 换行
        { "type": "text", "content": "\n" },
        // 行渲染
        {
          "type": "control",
          "tagName": "line",
          "children": [{ "type": "text", "content": "引用第二行" }]
        }
      ]
    }
  ]
}
```

### 下划线

`(ins)下划线内容(ins)`

``` json
// 行渲染
{
  "type": "control",
  "tagName": "line",
  "children": [
    // 行渲染
    {
      "type": "control",
      "tagName": "line",
      "children": [
        // 内下划线
        {
          "type": "tag",
          // ins 标签
          "tagName": "ins",
          "attrs": [],
          "children": [{ "type": "text", "content": "下划线内容" }]
        }
      ]
    }
  ]
}
```

### 剧透

`(spl)剧透内容(spl)`

``` json
// 行渲染
{
  "type": "control",
  "tagName": "line",
  "children": [
    // 行渲染
    {
      "type": "control",
      "tagName": "line",
      "children": [
        // 行内剧透
        {
          "type": "tag",
          "tagName": "spl",
          "attrs": [],
          "children": [{ "type": "text", "content": "剧透内容" }]
        }
      ]
    }
  ]
}
```

### 行内代码

```
`console.log()`
``` 

``` json
// 行渲染
{
  "type": "control",
  "tagName": "line",
  "children": [
    // 行渲染
    {
      "type": "control",
      "tagName": "line",
      "children": [
        // 行内代码
        {
          "type": "tag",
          "tagName": "code",
          "children": [{ "type": "text", "content": "console.log()" }]
        }
      ]
    }
  ]
}
```

### 代码块
` ```js\n console.log()``` `

``` json
// 行渲染
{
  "type": "control",
  "tagName": "line",
  "children": [
    {
      "type": "tag",
      // 代码快
      "tagName": "codeblock",
      // 语言
      "attrs": ["js"],
      "children": [{ "type": "text", "content": "console.log()\n" }]
    }
  ]
}
```

### 转义特殊字符
` \n `

``` json
// 行渲染
{
  "type": "control",
  "tagName": "line",
  "children": [
    {
      "type": "control",
      "tagName": "line",
      "children": [{ "type": "text", "content": "\\n" }]
    }
  ]
}
```

## 完整示例
如 kmarkdown消息基本使用 例子中所示 该内容为
```
**KOOK**
专属游戏玩家的*文字、语音和组队工具*
(ins)安全免费(ins)，(ins)没有广告(ins)，(ins)低资源占用(ins)，(ins)高通话质量(ins)
KOOK是最好的~~语音~~软件
[KOOK](https://kookapp.cn)
\`/help\`
(spl)Talk is cheap.Make it happen.(spl)
> Talk is cheap.
Make it Happen.

---

\`\`\`js
function factorial(n, total) {
    if (n === 1) return total;
    return factorial(n - 1, n * total);
}
                
factorial(5)
\`\`\`
```

它会解析为以下 json
```json
{
  "type": "tag",
  "tagName": "body",
  "children": [
    // 换行符
    { "type": "text", "content": "\n" },
    // 行 渲染
    {
      "type": "control",
      "tagName": "line",
      "children": [
        // 加粗文本
        {
          "type": "tag",
          "tagName": "strong",
          "children": [{ "type": "text", "content": "KOOK" }]
        }
      ]
    },
    // 换行符
    { "type": "text", "content": "\n" },
    // 行 渲染
    {
      "type": "control",
      "tagName": "line",
      "children": [
        // 普通文本
        { "type": "text", "content": "专属游戏玩家的" },
        // 斜体文本
        {
          "type": "tag",
          "tagName": "em",
          "children": [{ "type": "text", "content": "文字、语音和组队工具" }]
        }
      ]
    },
    // 换行符
    { "type": "text", "content": "\n" },
    // 行 渲染
    {
      "type": "control",
      "tagName": "line",
      "children": [
        // 下划线文本
        {
          "type": "tag",
          "tagName": "ins",
          "attrs": [],
          "children": [{ "type": "text", "content": "安全免费" }]
        },
        // 普通文本
        { "type": "text", "content": "，" },
        // 下划线文本
        {
          "type": "tag",
          "tagName": "ins",
          "attrs": [],
          "children": [{ "type": "text", "content": "没有广告" }]
        },
        // 普通文本
        { "type": "text", "content": "，" },
        // 下划线文本
        {
          "type": "tag",
          "tagName": "ins",
          "attrs": [],
          "children": [{ "type": "text", "content": "低资源占用" }]
        },
        // 普通文本
        { "type": "text", "content": "，" },
        // 下划线文本
        {
          "type": "tag",
          "tagName": "ins",
          "attrs": [],
          "children": [{ "type": "text", "content": "高通话质量" }]
        }
      ]
    },
    // 换行符
    { "type": "text", "content": "\n" },
    // 行 渲染
    {
      "type": "control",
      "tagName": "line",
      "children": [
        // 普通文本
        { "type": "text", "content": "KOOK是最好的" },
        // 删除线文本
        {
          "type": "tag",
          "tagName": "del",
          "children": [{ "type": "text", "content": "语音" }]
        },
        // 普通文本
        { "type": "text", "content": "软件" }
      ]
    },
    // 换行符
    { "type": "text", "content": "\n" },
    // 行 渲染
    {
      "type": "control",
      "tagName": "line",
      "children": [
        // 链接
        {
          "type": "tag",
          "tagName": "a",
          "attrs": { "href": "https://kookapp.cn" },
          "children": [{ "type": "text", "content": "KOOK" }]
        }
      ]
    },
    // 换行符
    { "type": "text", "content": "\n" },
    // 行 渲染
    {
      "type": "control",
      "tagName": "line",
      "children": [
        // 行内代码
        {
          "type": "tag",
          "tagName": "code",
          "children": [{ "type": "text", "content": "/help" }]
        }
      ]
    },
    // 换行符
    { "type": "text", "content": "\n" },
    // 行 渲染
    {
      "type": "control",
      "tagName": "line",
      "children": [
        // 剧透
        {
          "type": "tag",
          "tagName": "spl",
          "attrs": [],
          "children": [
            { "type": "text", "content": "Talk is cheap" },
            { "type": "text", "content": "." },
            { "type": "text", "content": "Make it happen" },
            { "type": "text", "content": "." }
          ]
        }
      ]
    },
    // 换行符
    { "type": "text", "content": "\n" },
    // 块引用
    {
      "type": "tag",
      "tagName": "blockquote",
      "children": [
        {
          "type": "control",
          "tagName": "line",
          "children": [
            { "type": "text", "content": "Talk" },
            { "type": "text", "content": " " },
            { "type": "text", "content": "is" },
            { "type": "text", "content": " " },
            { "type": "text", "content": "cheap" },
            { "type": "text", "content": "." }
          ]
        },
        // 换行符
        { "type": "text", "content": "\n" },
        // 行 渲染
        {
          "type": "control",
          "tagName": "line",
          "children": [
            { "type": "text", "content": "Make" },
            { "type": "text", "content": " " },
            { "type": "text", "content": "it" },
            { "type": "text", "content": " " },
            { "type": "text", "content": "Happen" },
            { "type": "text", "content": "." }
          ]
        },
        { "type": "text", "content": "\n" }
      ]
    },
    // 分隔线
    { "type": "tag", "tagName": "hr" },
    { "type": "text", "content": "\n" },
    // 代码快
    {
      "type": "tag",
      "tagName": "codeblock",
      "attrs": ["js"],
      "children": [
        {
          "type": "text",
          "content": "function factorial(n, total) {\n    if (n === 1) return total;\n    return factorial(n - 1, n * total);\n}\n                \nfactorial(5)\n"
        }
      ]
    }
  ]
}

```

