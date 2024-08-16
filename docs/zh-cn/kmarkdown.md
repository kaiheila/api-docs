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

