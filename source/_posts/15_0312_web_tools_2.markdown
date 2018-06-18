---
layout: post
title:  Web开发利器推荐（二）
date:   2015-03-12 08:24:00
category: [翻译,Tools]
---
看到一个很棒的系列，介绍了很多对web开发很有帮助的利器，解决了很多开发中遇到的繁琐事，翻译来分享一下：

## [Webflow][1]

![clipboard.png](http://segmentfault.com/img/bVk2Cu)

通过这些服务，一个没有HTML/CSS知识的人，就能在[55分钟][2]内搭建一个跨浏览器的页面。 这是为网页设计师准备的完美解决方案，已经有超过26 000人在使用Webflow。 只能免费创建两个项目，想要创建更多项目的收费也很合理。 这个工具真的很酷。

如果你和我一样是个不喜欢GUI的前端，就可以在Webflow上导出几个免费的响应式布局模板。 我还想推荐[responsive layout generator][3] 和 [Responsive Patterns][4]。

<!--more-->

## [Parallax.js][5]

![clipboard.png](http://segmentfault.com/img/bVk2Da)

功能强大、使用简单的视差效果库。

可以给所有的元素应用视觉差效果，通过设置`data-depth`控制速度。 Parallax.js有一系列的参数：

    <ul id="scene"
      data-calibrate-x="false" 
      data-calibrate-y="true"  
      data-invert-x="false"     
      data-invert-y="true"  
      data-limit-x="false"
      data-limit-y="10"
      data-scalar-x="2"
      data-scalar-y="8"
      data-friction-x="0.2"
      data-friction-y="0.8"> 
      <li class="layer" data-depth="0.00"><img src="layer6.png"></li>
      <li class="layer" data-depth="0.20"><img src="layer5.png"></li>
      <li class="layer" data-depth="0.40"><img src="layer4.png"></li>
      <li class="layer" data-depth="0.60"><img src="layer3.png"></li>
      <li class="layer" data-depth="0.80"><img src="layer2.png"></li>
      <li class="layer" data-depth="1.00"><img src="layer1.png"></li>
    </ul>


传递父元素：

    var scene = document.getElementById('scene');
    var parallax = new Parallax(scene);

## [Intention.js][6]

很小，但很有用的库，简化了创建完全自适应布局的开发过程。 用起来很简单。 操作原理如图所示：

![clipboard.png](http://segmentfault.com/img/bVk2CB)

## [Device.js][7]

![clipboard.png](http://segmentfault.com/img/bVk2Db)

该脚本类似Modernizr，包含了 ios/android/windows/blackberry phone/tablet landscape/portrait 的 HTML 类。

谈到跨设备开发，我想提及 [Risizer][8] -响应设计测试的工具。 有很多类似的服务，但是我认为这种方法是最方便的。

## [GistBox][9]

GistBox能同步你的Github 的 Gist。 可以通过标签排序，管理方便，随时查看。 它是一个Chrome扩展。

![clipboard.png](http://segmentfault.com/img/bVk2CW)

## [CSS Modal][10]

![clipboard.png](http://segmentfault.com/img/bVk2Dd)

起初，该项目是由一个团队成员创建的HTML5样板。 CSS Modal-轻松让网站能自适应窗口变化。 首先要添加此代码：

    <section class="semantic-content" id="modal-text" tabindex="-1"
            role="dialog" aria-labelledby="modal-label" aria-hidden="true">
    
        <div class="modal-inner">
            <header id="modal-label"><!-- Header --></header>
            <div class="modal-content"><!-- The modals content --></div>
            <footer><!-- Footer --></footer>
        </div>
    
        <a href="#!" class="modal-close" title="Close this modal" data-close="Close"
            data-dismiss="modal">×</a>
    </section>

然后在`body`的结束标记之前添加modal.js。 这是完成了！

## Dotdotdot.js, Uikit, HTML2PDF

最近，我需要用省略号来表明有更多的文字。 但标准文本溢出只能在一句中。 我发现一个好脚本[dotdotdot.js][11]，它完美地解决了这个问题。

![clipboard.png](http://segmentfault.com/img/bVk2De)

[UIKit][12]——轻量级的web开发框架。

![clipboard.png](http://segmentfault.com/img/bVk2Df)

[HTML2PDF][13]——基于phantom.js。 还可以在线把HTML转换成PDF。

![clipboard.png](http://segmentfault.com/img/bVk2Dg)

---

> 英文原文：[Awesomeness & Usefulness for Web Developers #2][14]

> 本文是我为 [SegmentFault][15] 所译

  [1]: https://webflow.com/
  [2]: http://vimeo.com/71633297
  [3]: http://www.responsivewebcss.com/
  [4]: http://bradfrost.github.io/this-is-responsive/patterns.html
  [5]: https://github.com/wagerfield/parallax
  [6]: https://github.com/wsjdesign/intentionjs
  [7]: https://github.com/matthewhudson/device.js
  [8]: http://lab.maltewassermann.com/viewport-resizer/
  [9]: http://www.gistboxapp.com/
  [10]: https://github.com/drublic/css-modal
  [11]: http://dotdotdot.frebsite.nl/
  [12]: https://github.com/uikit/uikit
  [13]: https://github.com/Muscula/html2pdf.it
  [14]: http://ipestov.com/awesomeness-and-usefulness-for-web-developers-2/
  [15]: http://segmentfault.net/blog/news/1190000002592665

