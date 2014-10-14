---
layout: page
title: Properties简介
permalink: /introduction-to-properties/

---

在使用`React.createClass()`创建任意组件时，我们可以通过`getDefaultProps`方法给他定义一些属性。

<div class="example-row-1">
  <div class="example">
  {% highlight javascript %}
/*** @jsx React.DOM */
var APP = React.createClass({
    getDefaultProps:function(){
        return {
            txt:'this is a prop'
        }
    },
    render:function(){
        return (
            <div>
              <h1>Hello React</h1>
              <p>{this.props.cat}</p>
              <p>{this.props.txt}</p>
            </div>
        )
    }
});

React.renderComponent(<APP cat={5} />, document.body)
  {% endhighlight %}
  </div>
</div>

从上面的例子中可以看出，当我们需要在`render`方法使用某些数据时，可以在`getDefaultProps()`
函数中定义这个属性，然后通过`{this.props.txt}`来进行获取。

另外一种就是继承父级元素定义的属性。例如这里的`cat={5}`，写法和在普通html标签上添加属性类似。


我们还可以通过`propTypes`来定义属性的类型。

<div class="example-row-1">
  <div class="example">
  {% highlight javascript %}
propTypes:{
    txt:React.PropTypes.string,
    cat:React.PropTypes.number.isRequired
}
  {% endhighlight %}
  </div>
</div>

这样的好处是可以对传入的属性的类型进行检查。例如这里如果我们定义`txt`的类型为字符串，而在实际使用时
却传入一个对象或者数字，React就会在console输出警告。

> Warning: Invalid prop `cat` of type `number` supplied to `APP`, expected `string`.

最后一个需要注意的是，如果在`<APP cat={5} />`里和`getDefaultProps`函数里同时定义了`cat`属性，
页面最后实际加载的是前者定义的值。

`getDefaultProps`顾名思义就是定义默认的值，所以在我们另外再次定义时会被覆盖。

<div class="example-row-1">
  <div class="example">
  {% highlight javascript %}
var APP = React.createClass({
  getDefaultProps: function() {
    return {
      txt: 'awesome txt from default props',
      cat: 'default prop cat'
    };
  },
  propTypes: {
    txt: React.PropTypes.string,
    cat: React.PropTypes.string.isRequired
  },
  render: function() {
    return (
      <div>
        <h1>cat: {this.props.cat}</h1>
        <h1>txt: {this.props.txt}</h1>
      </div>
    )
  }
});

React.renderComponent(<APP cat={'some string'} />, document.body)
  {% endhighlight %}
  </div>
</div>

所以如果执行以上代码，我们最终会看到的结果是：

```
cat: some string

txt: awesome txt from default props
```
另外一个与`getDefaultProps`类似的方法是`getInitialState`,都可以用来在render是传入数据。不同的是
`props`一般用于静态数据，而`state`则偏向与动态。我会在后面讲解`state`属性时再进行详细介绍。

<a href="{{ "/state-basics/" | prepend: site.baseurl }}" class="giant-button">
  Next
</a>



