# gitlab配置消息转发示例

## 创建消息模板

参考[gitlab的push Event文档](https://docs.gitlab.com/ee/user/project/integrations/webhook_events.html#push-events) 我们可以看到如下的描述：

![](https://img.kookapp.cn/assets/2024-11/12/ybUO5dqK3I1400n9.png)

将payload example的内容复制。然后打开开发者中心的模板管理页，点击添加模板：

![](https://img.kookapp.cn/assets/2024-11/12/706zFClyOW0oc0bv.png)

在表单中，我们填一下相关的标题，然后将前面拷贝的数据粘贴至测试数据处，如下所示：

![](https://img.kookapp.cn/assets/2024-11/12/TAnnr5qFpa0nc0hp.png)

我们选择`twig`模板，并选择`卡片消息-json`。接下来我们就可以写模板了，模板使用了twig的语法加json格式，大家可以直接copy我的内容， 至模板内容中：
```
[
    {
        "type": "card",
        "theme": "secondary",
        "size" : "lg",
        "modules" : [
            {
                "type":"section",
                "text":{
                    "type":"kmarkdown",
                    {# 注释：引用传来的变量中的数据，将其格式化并打印出来 #}
                    "content": "{{data.user_username}}<{{data.user_email}}> 向仓库[{{data.repository.name}}]({{data.repository.git_http_url}})提交了Push请求，本次提交共{{data.total_commits_count}}次commit"
                }
            },
{# 注释：使用for循环，输出commits #}
{% for commit in data.commits %}
            {
                "type": "divider"
            },
            {
                "type":"section",
                "text": {
                    "type": "kmarkdown",
                    "content": " 提交人：{{commit.author.name}}<{{commit.author.email}}>\n内容：[{{commit.message|json_escape()}}]({{commit.url}})\n时间：{{commit.timestamp}}"
                }
            }{%if commit.id != (data.commits|last).id %},{%endif%}
{% endfor %}
        ]
    }    
    
]
```
点击保存，这样我们就创建好了一个模板。当然，大家也可以点击测试或者copy来直接使用该模板试试。

## 创建消息接收管道
在开发者平台中，点击创建消息接收管道，如下图所示：

![](https://img.kookapp.cn/assets/2024-11/12/aHHRzSLers0m507r.png)

在弹出的界面中输入标题，选择要发送消息的频道，并选择上面已经创建好的模板：

![](https://img.kookapp.cn/assets/2024-11/12/862UU1kUIG0c40h8.png)

点击提交即可。我们可以点击复制回调地址，将消息的url copy出来。

# 在gitlab中填入回调地址
打开gitlab，将上面复制好的回调地址，copy进url中，然后保存。如下图所示：

![](https://img.kookapp.cn/assets/2024-11/12/eVblAicBiX0d905x.png)
![](https://img.kookapp.cn/assets/2024-11/12/q4ferMRSZ70ts09l.png)

# 结果展示
在完成上述操作后，我们就可以实现gitlab的事件在KOOK中展示了。如下图所示：

![](https://img.kookapp.cn/assets/2024-11/12/qmm0wZV47B0ij064.png)

大家可以根据实际的需求，更改模板，就可以得到更好看的界面了。