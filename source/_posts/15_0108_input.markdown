---
layout: post
title:  小小标签，强大功能——深藏不露的 input
date:   2015-01-08 08:24:00
category: [翻译,HTML5]
---

`<input>` 虽只是一个看似简单的 HTML 表单元素，但它这么一个单一的元素，就有多达 30 多个属性（attribute），相信无论你是个小菜鸟还是像我一样写了 15 年 HTML 的老手，知道这点的时候还是会惊讶不已的。而且如果再加上全局属性那就更多了，例如最重要的 `type` 属性有超过20个可能的值！可以来简单看看 [MDN 文档][1]。



<!--more-->

## type 属性

在 input 标签中，type 属性可指定显示不同的表单控件，每个控件都有不同的目的和收集特定类型的数据。如果想看到所有的输入元素类型，可以查看[这里][2]（目前在 Chrome 里表现的最好），可能有一些你不知道的又新又有趣的类型。


### COLOR
许多 Web 应用会用到颜色选择器，可以让用户自定义选择颜色。传统做法是使用 JavaScript 框架（如 jQuery），而 W3C 推出了 input 标签的新值属性 `color`。下面这段代码在 Mac OS X chrome 里的表现就如下截图：

    <input type="color" value="#6fbc6d">

![Mac OS X的chrome input color.png](http://segmentfault.com/img/bVksss)

虽然最新版本的 Chrome 和 Firefox 都有自带的 color picker，但目前浏览器对 color 属性的支持仍然不是很好。不过你依旧可以通过设置颜色的十六进制值来改变默认的颜色。

### DATE, MONTH, AND WEEK

目前几乎所有的 Web 应用程序的表单都涉及到日期选择器，如预约医生、航班等，虽然可能是不同的形式。而与颜色选择器类似，传统的日期选择器控件通常是用 JavaScript 框架完成。

而现在，浏览器可以通过新的 input 类型 `date`、`month`、`week` 实现本地的日期选择器。下面这张截图是这三种类型的日期选择器的代码在 MAC OS X Chrome 上的表现：

```
<input type="date">
<input type="month">
<input type="week">
```

![clipboard.png](http://segmentfault.com/img/bVkvhs)

不幸的是，目前浏览器对这几个日期选择器的支持并不是特别好：最新版本的 Android 完全支持，Chrome 和 iOS 部分支持（主要是其对相关属性的不支持）。让浏览器对这几个新的本地日期选择器良好支持还是需要一段时间的，所以 JavaScript 控件仍是目前最好的解决方案。

### TEXT, EMAIL, TEL, URL

`text` 属性已经有很多年了，现在 `email`、`tel`、`url` 这几个新属性也加入了。普通浏览器里，这些新加的类型似乎和普通的文本输入没有什么差别，所以问题来了：如果没什么不同，为什么还要去用呢？

看看下图的这个 iOS 键盘：这 4 种不同的输入类型将自动使用一个特定的键盘 - `email` 的键盘有一个方便的 @ 符号，`tel` 使用数字键键盘，而 `url` 提供快速域名常用的`.`、`/`、`.com`。

```
<input type="text">
<input type="email"
<input type="tel">
<input type="url">
```

![clipboard.png](http://segmentfault.com/img/bVkvk2)

这些方法能提升以前在移动设备上让人感到沮丧的用户体验，而现在的浏览器都已经完全支持了这些属性。

### RANGE

在某些特定情况下，当数据精确度要求并不是很高的时候，可以让用户在某些值中选择即可。比如在一个照片编辑应用里让用户来控制图像的亮度或饱和度，这个时候使用文本输入绝对是一个糟糕的做法：会让用户不知该如何选择，而且程序员还要进行数值检测来确保数值在合适的范围内。这是不但加大了程序员的工作量，还会导致不好的用户体验。

这时候就该 `range` 上场了，使用一个滑块控件可以让用户在给定的最小值和最大值范围内进行特定选择。下面这段代码在 MAC OS X Chrome 上的效果截图：

```
<input type="range">
```

![clipboard.png](http://segmentfault.com/img/bVkvlA)

目前浏览器对范围滑块的支持还是相当不错的，iOS、Android（之前提到的演示页面可能会有问题）平台上都是完美支持，IE10 +、Firefox、Safari 以及 Chrome 也没有问题。所以，下次如果需要一个滑块，可以尝试使用 input 的 `range` 类型来替换传统的 JavaScript 解决方案。

### TIME

和 date 类型类似，`time` 也可以给你一个输入时间的界面，下面是这段代码在 MAC OS X Chrome 上的效果截图：

```
<input type="time">
```

![clipboard.png](http://segmentfault.com/img/bVkvlJ)

不过，和其它的 date 类型一样，`time` 目前也没有很好的浏览器支持。如果你需要一个实用的跨浏览器解决方案，多个文本输入或基于 JavaScript 的解决方案现在来看还是最佳的。

## 其他资源

正如引言中提到的，这只是 `input` 的一小部分类型举例，其他一些有趣的属性如 `required` `pattern` `list` `readonly` 等，如果还想继续学习，下面这些资源或许能帮到你：

* [Learn about &lt;input&gt; and other HTML elements on Treehouse](http://teamtreehouse.com/features/html)
* [View the demo page with every input type](http://codepen.io/nickpettit/full/jCndK)
* [W3C documentation for &lt;input&gt;](http://www.w3.org/TR/html5/forms.html#the-input-element)
* [MDN documentation for &lt;input&gt;](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input)
* [Cross browser support for &lt;input&gt; types on caniuse.com](http://caniuse.com/#search=input)


---

原文 [How to Use the Input Element][3]
[SegmentFault](http://segmentfault.com) 编译


  [1]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input
  [2]: http://codepen.io/nickpettit/full/jCndK
  [3]: http://blog.teamtreehouse.com/use-input-element
> 本文是我为  所译