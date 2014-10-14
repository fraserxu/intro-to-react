---
layout: page
title: 编写第一个组件
permalink: /first-component/

---

React是由Facebook和Instagram共同维护的一个专注于“前端UI渲染“的JavaScript框架。它的重心是我们一般所说的MVC开发模式中的"V",而这些得益于React所提供的一种虚拟DOM的概念。

这个系列文章，目的在于记录个人的学习经历，也希望对有兴趣的朋友起到帮助作用。

本文是系列文章的第一篇，我们将会从编写第一个React组件开始。

<!-- ```
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>First Component</title>
    <script src="http://fb.me/react-0.11.1.js"></script>
    <script src="http://fb.me/JSXTransformer-0.11.1.js"></script>
</head>
<body>
<script type="text/jsx">
    /*** @jsx React.DOM */
    var APP = React.createClass({
        render:function(){
            return (
                <h1>Hello React</h1>
            )
        }
    });

    React.renderComponent(<APP />, document.body)
</script>
</body>
</html>
```
 -->
首先这里通过使用Facebook的CDN引入React的代码，你可以通过访问官方文档首页下载，或者点击[这个链接](http://facebook.github.io/react/downloads/react-0.11.1.zip).

除去其他我们常见的HTML标签，这里第一个需要注意的是`<script type="text/jsx"></script>`,
这段代码的目的在于配合`/*** @jsx React.DOM */`告诉JSXTransformer去将标签里的内容按照JSX
的语法来进行解析。

然后我们使用React的`createClass`方法创建一个组件。这里我们只需定义最基本的`render`方法。

如果你在这个时候刷新页面，发现页面内容为空。 那是因为我们这里只是创建了`App`这个变量，但是没有将变量加载到页面中。这时我们需要调用React的`renderComponent`方法，查找对应的DOM元素(这里我们使用document.body)并渲染我们的APP对象。

到这里我们的Hello World页面就编写完成了。可能还有一些概念我没有解释清楚，但是不用担心，会在后面介绍其他API时再进行详细讲解。

<a href="{{ "/render-method/" | prepend: site.baseurl }}" class="giant-button">
  Next
</a>


