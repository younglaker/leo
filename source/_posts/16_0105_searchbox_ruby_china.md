---
layout: post
title:  如何看源码之Ruby China搜索框动画实现
date:   2016-01-05 08:24:00
category: [CSS3]
tags: [CSS3,JavaScript]
---

<!-- ![如何看源码之Ruby China搜索框动画实现][1] -->

<!-- 不要脸的自恋一下——我觉得我看源码的能力越来越强了，2333~ -->

想看到 [Ruby China][2] 搜索框动画效果很不错，想试着实现一下。最初我的想法是用jQuery的animate：

<!--more-->

```
$('input').animate({width: 'toggle'});
```

> 题外话，toggle值意味着宽度在0和原本宽度之间切换.

如果这样用的话，input就要设为`display: none;` 并且给input一个初始的长度。

例如 **[Demo][3]** (只做了输入框的显示隐藏)。

但是看 [Ruby China][4] 源码没有设置`display: none;`，有两个属性引起我的注意：`width: 0px;` 和 `transition: all .3s;`， 可以猜测这个动画的实现由 transition 实现 width 的渐变。

在不断点击搜索和取消搜索中可以看到，form 上在增加、删除 .active，所以搜索是否被触发的标记绑定在 form 上。

![form][5]

再看CSS，发现搜索框、查询按钮、关闭按钮都在动画触发后有个新的样式出现，名字如`.header .form-search.active .XXX`，看到这个`.form-search.active`就确定他们的动画是通过 form 上的 .active 来标记的。

然后我抠出以下主要代码：

> 本例中将会用到JavaScript触发 CSS transition ，详细介绍请看我的另一篇文章[《花式使用CSS3 transition》][6]。

HTML:
```
    <div class="header">
      <div class="search-block">
        <form class="navbar-form form-search" action="/search/all" method="get">
          <div class="form-group">
            <input class="form-control search-box" name="searchKey" type="text" value="" placeholder="搜索本站内容">
          </div>
          <i class="fa btn-search fa-search"></i>
          <i class="fa btn-close fa-times-circle"></i>
        </form>
      </div>
    </div>

```

CSS:
```
.header {
  width: 250px;
  height: 50px;
  position: relative;
  display: block;
}
.search-block {
  float: right;
}
.header .form-search .fa {
    color: #333;
}
.header .form-search {
    font-size: 14px;
    position: relative;
    margin-top: 13px;
    margin-right: 10px;
    padding: 0 15px;
    width: auto;
}
.header .form-search .form-control {
  font-size: 12px;
  border: none;
  width: 0px;
  height: 100%;
  padding: 6px 1px 4px 1px;
  margin-left: 4px;
  background: transparent;
  -webkit-transition: all .3s;
  -moz-transition: all .3s;
  transition: all .3s;
  box-sizing: border-box;
  color: #333;
}

//输入框的动画部分
.header .form-search.active .form-control {
    width: 150px !important;
    cursor: text;
}
.fa-search:before {
    content: "\f002";
}
.header .form-search .fa-search {
  cursor: pointer;
  position: absolute;
  top: 6px;
  right: 0;
  -webkit-transition: all .3s;
  -moz-transition: all .3s;
  transition: all .3s;
}

// 搜索按钮的动画部分
.header .form-search.active .fa-search {
  left: 0;
  right: auto;
}
.header .form-search .btn-close {
  position: absolute;
  top: 6px;
  right: 0px;
  cursor: pointer;
  -webkit-transform: scale(0, 0);
  -moz-transform: scale(0, 0);
  transform: scale(0, 0);
  -webkit-transition: all .3s;
  -moz-transition: all .3s;
  transition: all .3s;
}

// 取消搜索的动画部分
.header .form-search.active .btn-close {
  -webkit-transform: scale(1, 1);
  -moz-transform: scale(1, 1);
  transform: scale(1, 1);
}
```

JavaScript：
```
  $('.btn-search').on('click', function() {
    $('.form-search').addClass('active');
  });

  $('.btn-close').on('click', function() {
    $('.form-search').removeClass('active');
  });
```

**[View Demo][7]**

## 小结

我也不是一眼就看出来的，抠这个效果花了大半天，也是蛮菜的。

分享自己一点点小经验：

- 长期写代码的经验积累
- 多猜测多尝试，不断重复原网站的效果，看看代码有什么变化
- 把想到的关键词就google一下，也许能得到启发
- 多看源码，刚开始很累，后来就习惯的。我经常会看各种网站源码，框架也大致看过jQuery、Framework 7。前端这块的源码还是比较容易看的。
- 多模仿多练习。光看别人的代码不够，试着用自己的方式写写，然后对照别人的代码比对不足。我仿jQuery写了[Octjs][8]，仿jCanvas写了[EasyCanvas][9]（我从初学开始就有个毛病，如果不能理解一个框架、插件的原理，我用着心里就不踏实 >_<）。

想起老博客里写过读豆瓣源码的文章，是我大三时候写的，算是第一次看复杂源码，毕竟文件多、代码已压缩混淆，以供参考：[《豆瓣绑定事件的方法初探》][10] （大学时候的博客真是蛮逗比的，哈哈）


  [1]: http://77g54f.com1.z0.glb.clouddn.com/bgt-306435.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/South/dy/5
  [2]: https://ruby-china.org
  [3]: http://codepen.io/younglaker/pen/jWygzm
  [4]: https://ruby-china.org/
  [5]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151214144634.png
  [6]: http://laker.me/blog/2015/12/18/15_1218_css3_transition/
  [7]: http://codepen.io/younglaker/pen/MKKwyp/
  [8]: https://github.com/younglaker/octjs
  [9]: https://github.com/younglaker/EasyCanvas
  [10]: http://www.cnblogs.com/younglaker/archive/2013/05/16/3081065.html