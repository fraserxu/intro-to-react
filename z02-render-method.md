---
layout: page
title: Render渲染方法
permalink: /render-method/

---

在使用`React.createClass()`创建任意组件时，我们都需要给它定义`render`函数。

<!-- ```
/*** @jsx React.DOM */
var APP = React.createClass({
    render:function(){
        return (
            <h1>Hello React</h1>
            <Widget />
        )
    }
});
``` -->

render方法在被调用时首先会检查所在实例化对象下面定义的`this.props`和`this.state`属性，然后将其数据添加到对应的DOM中去。
函数内部的返回值可以包含其他的原生DOM对象，例如`<div />`， 也可以是`React.DOM.div`对象，另外还有自定义的组件。

查看一下`React.createClass()`方法的[源码](https://github.com/facebook/react/blob/master/src/core/ReactCompositeComponent.js#L1355)，可以发现它会首先检查`render`方法是否存在，如果没定义则会报错。

```
invariant(
  Constructor.prototype.render,
  'createClass(...): Class specification must implement a `render` method.'
);
```

如果你不想要渲染任何东西，可以将返回值设置为`null`或者`false`. 在这种情况下React实际会渲染一个`<noscript>`标签，然后在执行diff算法时会被用到。

最后一个需要注意的是在组件创建完成后，一定要记得调用`React.renderComponent(<APP />, document.body)`将我们所创建的内容真正渲染到页面中。

下面是一个完整的例子。

<!-- ```
<!doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Render Method</title>
  <script src="http://fb.me/react-0.11.1.js"></script>
  <script src="http://fb.me/JSXTransformer-0.11.1.js"></script>
</head>
<body>
<script type="text/jsx">
  /*** @jsx React.DOM */
  var APP = React.createClass({
    render:function(){
      return (
        <div>
          <h1>Hello World</h1>
          <b>bold</b>
        </div>
      )

    }
  });

  React.renderComponent(<APP />, document.body)
</script>
</body>
</html>
``` -->

在实际的使用过程中，经常会遇到一种错误。如果我们这里的`return`内容中，没有选择将`h1`和`b`标签内容写在`div`内，React将会报错。反之，如果最外层有一个或者多个标签时则不会报错。

但是有一种情况下可以不用在最外层用一个标签包裹，那就是返回的内容是单行的。例如`return <h1>hi</h1>`. 初步推测是由`JSX`在解析时的需要。

总结以上两点，得出一个基本结论，在使用`render`方法时，尽量确保只返回一个节点(节点内可包含任意数目子节点)。而且大多数情况下使用`()`括号将返回结果包住。

<a href="{{ "/introduction-to-properties/" | prepend: site.baseurl }}" class="giant-button">
  Next
</a>