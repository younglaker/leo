---
layout: post
title:  不依赖jQuery也能做好动画
date:   2015-01-28 08:24:00
category: [翻译,JavaScript]
---
在开发者社区中有种错误的观念——认为在web中，CSS动画是唯一高性能的动画方式。这使很多开发者放弃基于JavaScript的动画。所以导致——（1）强制使用大量样式表来完成复杂的UI交互，（2）不能很好地支持IE8、9，（3）放弃只有JS才能完成的完美物理运动效果。

事实证明：基于JavaScript的动画和基于CSS的动画一样快，甚至有时更快。CSS动画通常是和非常慢的jQuery `$.animate()`比较。但是，JavaScript库如果能避免像jQuery那样大量的DOM操作，性能就会非常高。这些库能比jQuery快20倍。

所以，让我们来打破一些神话，通过一些动画实例，并在此过程中提高自己的设计技巧。

<!--more-->

## 为什么是JavaScript

CSS动画能方便地实现渐变效果，也不需要额外地加载库。但是它很难支持复杂的效果。代码不易管理、特性不能满足需求而导致失败。

最终CSS动画无法完成要求。但JavaScript和大多编程语言一样，支持大量的逻辑控制。JavaScript动画引擎用事实证明了这点，这里有些小技巧可以参考：

*   [cross-browser SVG support（跨浏览器的SVG）](http://codepen.io/sol0mka/full/jpecs/)<sup class="po" id="note-1">
*   [physics-based loader animations（物理加载动画）](http://codepen.io/timothyrourke/full/wojke/)<sup class="po" id="note-2">
*   [timeline control（时间控制）](http://codepen.io/GreenSock/full/yhEmn/)
*   [Bezier translations（贝塞尔渐变）](http://codepen.io/GreenSock/full/LuIJj/)




如果你对性能感兴趣，可以看看Julian Shapiro 的 “[CSS vs. JS Animation: Which Is Faster?](http://davidwalsh.name/css-js-animation)” 和
Jack Doyle 的 “[Myth Busting: CSS Animations vs. JavaScript](http://css-tricks.com/myth-busting-css-animations-vs-javascript/)” 。性能的演示可参考  Velocity 的 “[performance pane](http://velocityjs.org)” 和 GSAP 的 “[Library Speed Comparison](http://codepen.io/GreenSock/full/srfxA/)

## Velocity 和 GSAP

两个最流行的JavaScript动画库是[Velocity.js](http://velocityjs.org) 和 [GSAP](http://greensock.com/gsap/)。它们都不依赖于jQuery，使得性能提高。



假如你的网站已经用了 jQuery，那就可以像使用 jQuery 一样使用 Velocity 和 GSAP。例如： `$element.animate({ opacity: 0.5 }); ` 就可以写成 `$element.velocity({ opacity: 0.5 })`。

如果你没有使用 jQuery 也能使用这两个库。但是不能像绑定一系列动画到JQ元素上那样，要把元素传进动画函数里，例如：

```
/* Working without jQuery */

Velocity(element, { opacity: 0.5 }, 1000); // Velocity

TweenMax.to(element, 1, { opacity: 0.5 }); // GSAP
```

如上所示，在没有使用JQ的情况下，Velocity 的用法和JQ一样，把目标元素写到第一个参数位置，再把其他参数依次往右写。

GSAP与此不同，采用的是面向对象的API设计，和静态方法一样方便。所以你可以完全掌控整个动画。

在这两种情况下，你不再是使用一个jQuery的动画元素对象，而是一个原始的DOM节点。你可以通过`document.getElementByID`、`document.getElementsByTagName`、 `document.getElementsByClassName` 和 `document.querySelectorAll`（和jQuery的选择器很类似）。

## 不使用jQuery
（注：如果你要学习基本的jQuery  `$.animate()`的用法，可以参考Velocity文档开始的几段）

querySelectorAll是摆脱jQuery的好武器

    document.querySelectorAll("body"); // 获取body元素
    document.querySelectorAll(".squares"); // 获取所有包含square类的元素
    document.querySelectorAll("div"); // 获取所有div
    document.querySelectorAll("#main"); // "main"获取含有id为main的元素
    document.querySelectorAll("#main div"); // 获取#main里的div

如上面所示，你可以轻松地把CSS选择器传给`querySelectorAll`，它会返回一个包含所有匹配元素的数组。所以，你可以这样做：
```
/* 获取所有div */
var divs = document.querySelectorAll("div");

/* 给所有div加上动画 */
Velocity(divs, { opacity: 0.5 }, 1000); // Velocity
TweenMax.to(divs, 1, { opacity: 0.5 }); // GSAP
```

我们不再将元素绑定为jQuery对象，那如何一个接一个地实现动画呢？

    $element // jQuery 对象
        .velocity({ opacity: 0.5 }, 1000)
        .velocity({ opacity: 1 }, 1000);

在Velocity里，你只需一个接一个调用动画：

    Velocity(element, { opacity: 0.5 }, 1000);
    Velocity(element, { opacity: 1 }, 1000);

这种方式没有性能缺陷。要把做动画的目标元素用变量存储起来使用，而不是每次都用querySelectorAll查找一次。

（提示：使用Velocity的包，你可以创建自己的多操作的动画，并给他们取名字，你就可以像Velocity的第一参数一样操作它。[点击这里][1]查看更多。）

这种`one-Velocity-call-at-a-time`的方式有个好处：如果你使用promises，那么Velocity每次调用后会返回一个可使用的[promise][2]对象，这非常有用。你可以通过[Jake Archibald的文章][3]了解更多。

GSAP面对对象的方式允许把动画排入时间线，方便调度和同步控制。这样就不局限于一个接一个的链接动画。你可以嵌套时间表、使动画重叠等。

    var tl = new TimelineMax();
    /* GSAP默认使用tweens链，但你可以在时间线上指定精确的插入点，包括相对偏移 */
    tl
      .to(element, 1, { opacity: 0.5 })
      .to(element, 1, { opacity: 1 });

> 英文原文：[Animating Without jQuery][4]

> 本文是我为 [SegmentFault][5] 所译

  [1]: http://velocityjs.org/#uiPack
  [2]: http://velocityjs.org/#promises
  [3]: http://www.html5rocks.com/en/tutorials/es6/promises/
  [4]: http://www.smashingmagazine.com/2014/09/04/animating-without-jquery/?utm_source=tuicool
  [5]: http://segmentfault.com/blog/news/1190000002522213
