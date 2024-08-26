# 消息预览

我们针对卡片消息和 KMarkdown 消息封装了一套消息预览开发工具：[点击使用](https://github.com/laiyuzenb/kook_message_preview)

## 加载 wasm scripts

有以下两种加载方式

1. 下载 https://cdn.jsdelivr.net/npm/@kookapp/kook-message-preview@0.0.3/dist/markdown-parse.0.0.10.js 复制代码 至 html 文件中 的 script 标签中

```html
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>

  <body>
    <script>
      //cdn.jsdelivr.net/npm/@kookapp/kook-message-preview@0.0.3/dist/markdown-parse.0.0.10.js
      https: 里面的代码
    </script>
  </body>
</html>
```

2. 使用组件时 传入参数 `external=cdn地址`
   例如以下代码示例都使用 external https://cdn.jsdelivr.net/npm/@kookapp/kook-message-preview@0.0.3/dist/markdown-parse.0.0.10.js

```js
import { MessagePreview } from '@kookapp/kook-message-preview'

export default () => (
  <MessagePreview external="https://cdn.jsdelivr.net/npm/@kookapp/kook-message-preview@0.0.3/dist/markdown-parse.0.0.10.js" />
)
```

## 卡片消息基本使用

这是一个简单的卡片消息例子

```jsx
import { MessagePreview } from '@kookapp/kook-message-preview'

const content = [
  {
    type: 'card',
    size: 'lg',
    theme: 'warning',
    modules: [
      {
        type: 'header',
        text: {
          type: 'plain-text',
          content: '近期活动公告',
        },
      },
      {
        type: 'divider',
      },
      {
        type: 'section',
        mode: 'left',
        accessory: {
          type: 'image',
          src: 'https://img.kaiheila.cn/assets/2021-01/FckX3MDe6S02i020.png',
          circle: true,
        },
        text: {
          type: 'plain-text',
          content:
            '社区将在1月20日开启副本速通挑战，参与本次活动的小伙伴均有礼品相送！',
        },
      },
      {
        type: 'section',
        text: {
          type: 'kmarkdown',
          content: '**报名方法**',
        },
      },
      {
        type: 'section',
        mode: 'right',
        accessory: {
          type: 'button',
          theme: 'primary',
          value: '123',
          text: {
            type: 'plain-text',
            content: '报名',
          },
        },
        text: {
          type: 'kmarkdown',
          content: '点击右侧“报名”按钮，即可完成报名。',
        },
      },
      {
        type: 'section',
        text: {
          type: 'kmarkdown',
          content: '**挑战奖励**\n',
        },
      },
      {
        type: 'section',
        accessory: {},
        text: {
          type: 'paragraph',
          cols: 3,
          fields: [
            {
              type: 'kmarkdown',
              content: '第一名',
            },
            {
              type: 'kmarkdown',
              content: '第二名',
            },
            {
              type: 'kmarkdown',
              content: '参与奖',
            },
            {
              type: 'kmarkdown',
              content: '游戏加速器年卡',
            },
            {
              type: 'kmarkdown',
              content: '游戏加速器季卡',
            },
            {
              type: 'kmarkdown',
              content: '游戏加速器月卡',
            },
          ],
        },
      },
    ],
  },
]

export default () => (
  <MessagePreview
    type="card"
    content={content}
    external="https://cdn.jsdelivr.net/npm/@kookapp/kook-message-preview@0.0.3/dist/markdown-parse.0.0.10.js"
  />
)
```

## KMarkDown 消息基本使用

这是一个简单的 kmarkdown 消息例子

```jsx
import { MessagePreview } from '@kookapp/kook-message-preview'

const content = `~~删除线~~`

export default () => (
  <MessagePreview
    type="kmd"
    content={content}
    external="https://cdn.jsdelivr.net/npm/@kookapp/kook-message-preview@0.0.3/dist/markdown-parse.0.0.10.js"
  />
)
```

## API

| 属性名   | 描述                                                                                                                                                                      | 类型              | 默认值    |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- | --------- |
| type     | 消息类型 `'card'`(卡片消息) `'kmd'`（KMarkDown 消息）                                                                                                                     | `string`          | `'card'`  |
| theme    | 主题色 `'light' 或 'dark'`                                                                                                                                                | `string`          | `'light'` |
| content  | 消息内容：具体可查看[消息编辑器](https://www.kookapp.cn/tools/message-builder.html#/card) 或者 [卡片消息说明](/card_desc) 和 [KMarkDown 消息说明](/kmd_desc) | `string 或 array` | `[]`      |
| external | wasm 资源地址                                                                                                                                                             | `string`          | `''`      |
