---
layout: page
title: state基础
permalink: /state-basics/

---

上篇文章介绍了如何使用`props`属性将数据渲染到组件中，这里我们开始介绍`state`属性。两者的共同点就是都可以作为属性传入组件。不同的是`props`一般用于静态数据，定义之后数据一般不会再发生改变。 而`state`属性则相反。


两者的使用方法也很类似。我们通过使用`getInitialState`方法定义组件的初始`state`属性。

<div class="example-row-1">
  <div class="example">
  {% highlight javascript %}
/*** @jsx React.DOM */
var APP = React.createClass({
    getInitialState: function() {
        return {
            txt: 'this is some text from initial state'
        }
    },
    render: function(){
        return (
            <div>
              <h1>Hello React</h1>
              <p>{this.state.txt}</p>
            </div>
        )
    }
});

React.renderComponent(<APP />, document.body)
  {% endhighlight %}
  </div>
</div>

在组件完成加载之后，我们可以通过`setState`方法来改变我们设置的属性的值。

首先在`render`函数中加入一个`input`元素，用于触发`onChange`事件，然后调用`setState`方法。

<div class="example-row-1">
  <div class="example">
  {% highlight javascript %}
/*** @jsx React.DOM */
var APP = React.createClass({
    getInitialState: function() {
        return {
            txt: 'this is some text from initial state'
        }
    },
    updateTxt: function(e) {
        this.setState({txt: e.target.value})
    },
    render: function(){
        return (
            <div>
              <input type="text" onChange={this.updateTxt} />
              <p>{this.state.txt}</p>
            </div>
        )
    }
});
  {% endhighlight %}
  </div>
</div>

运行以上代码后，当我们在文本框中输入任意文本后，就会触发绑定的`onChange`事件，之后调用我们定义好的`updateTxt`方法，从而最终通过`setState`方法来更新`state`的数据。

以上为`state`的基本用法，不要觉得简单。之后我们会在再次遇到时进行深入讲解。

<a href="{{ "/react-component-lifecycle/" | prepend: site.baseurl }}" class="giant-button">
  Next
</a>


