---
layout: post
title:  花式使用CSS3 transition
date:   2015-12-18 08:24:00
category: [CSS3]
tags: [JavaScript,CSS3]
---

本文讲介绍`:hover`、`:active`、`:focus`、`:checked`、`Media Queries`、`JavaScript控制`六种方法触发CSS3 transition，以及 `transitionend` 事件的使用。

<!--more-->

## :hover
最常见的是用hover：

```
<div class="hover">:hover</div>

.hover {
  width: 100px;
  height: 100px;
  background: #222;
  color: white;
  text-align: center;
  transition: all 2s ease;
}
.hover:hover {
  width: 200px;
  height: 200px;
}
```

**[Demo][1]**

## :active
mousedown s时触发：

```
<div class="active">:active</div>

.active {
  width: 100px;
  height: 100px;
  background: #222;
  color: white;
  text-align: center;
  transition: all 2s ease;
}
.active:active {
  width: 200px;
  height: 200px;
}
```

**[Demo][1]**

## :focus
文本框聚焦时（这个在很多网站的搜索框的动画效果里用到）：

```
<div class="focus">
  <input type="text" />
</div>
<div class="focus">
  <textarea name="" id="" cols="30" rows="10"></textarea>
</div>

.focus input, .focus textarea {
  width: 200px;
  transition: width 1s ease;
}

.focus input:focus, .focus textarea:focus {
  width: 300px;
}
```

**[Demo][1]**

## :checked
用于checkboxes 和 radio buttons 被选中时：

```
<div>
    <input type="checkbox" name="things" value="thing1"> Input 1<br>
    <input type="checkbox" name="things" value="thing2"> Input 2<br>
    <input type="checkbox" name="things" value="thing3"> Input 3<br>
  <input type="checkbox" name="things" value="thing4"> Input 4<br>
</div>
    
input[type="checkbox"]:checked {
  height: 20px;
  transition: all 1s ease;
}

input[type="checkbox"]:checked {
  width: 30px;
}
```

**[Demo][1]**

## Media Queries
改变浏览器窗口大小时触发：

```
<div class="media">media</div>

.media {
  width: 200px;
  height: 200px;
  background: #222;
  color: white;
  text-align: center;
  transition: width 1s ease;
}

@media only screen and (max-width : 960px) {
  .media {
    width: 100px;
    height: 100px;
  }
}
```

**[Demo][1]**

## JavaScript事件触发CSS3 transition

通过 JavaScript 或者 jQuery 添加、删除class来完成动画，CSS格式类似`:hover`。

例如：

## 简单Demo

以 click 事件为例，当点击方块时，变化长宽、背景色：

HTML:
```
<div class="box"></div>
```
CSS:
```
.box {
  width: 200px;
  height: 200px;
    background: black;
  -webkit-transition: all 2s ease;
  -moz-transition: all 2s ease;
  -o-transition: all 2s ease;
  transition: all 2s ease;
}

.box.clicked {
  width: 300px;
  height: 300px;
    background: blue;
}
```
JavaScript：
```
$(".box").click(function() {
    $(this).toggleClass("clicked");
});
```

**[Demo][2]**

如果用原生JavaScript，可以自己写个添加和删除类的函数。

## transitionend 事件

transitionend 事件会在 CSS transition 结束后触发。兼容Chrome、Firefox、Safari、IE10+：

```
element.addEventListener('transitionend', callback, false);
```

为保证低版本兼容性可以写webkitTransitionEnd（WebKit ）、otransitionend（Opera）、MSTransitionEnd（IE 10+）、transitionend（Mozilla）。[详见此讨论][3]。

> 有没有渐变开始的事件？目前只有IE 10+ 有 [transionstart 事件][4]，W3C目前未有此标准。



  [1]: http://codepen.io/younglaker/pen/WrweNe
  [2]: http://codepen.io/younglaker/pen/xZZvQq
  [3]: http://stackoverflow.com/questions/5023514/how-do-i-normalize-css3-transition-functions-across-browsers
  [4]: https://msdn.microsoft.com/zh-cn/library/dn632683%28v=vs.85%29.aspx