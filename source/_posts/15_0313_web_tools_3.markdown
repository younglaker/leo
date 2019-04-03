---
layout: post
title:  Web开发利器推荐（三）
date:   2015-03-13 08:24:00
category: [翻译,Tools]
---
看到一个很棒的系列，介绍了很多对web开发很有帮助的利器，解决了很多开发中遇到的繁琐事，翻译来分享一下：

## [Cloudconvert][1]

<!-- ![clipboard.png](http://segmentfault.com/img/bVk27X) -->

出色的在线转换器，支持超过150种格式，支持音频、CAD、文档、电子书、图像、表格、演示文稿、视频文件。 与Dropbox和 Google Drive同步，适用于所有智能手机。 最棒的是，它提供功能强大但使用简单的API。

<!--more-->

## [Munee][2]

![clipboard.png](http://segmentfault.com/img/bVk27Y)

Munee 是一个功能强大的PHP库，能编译 LESS、 SCSS、CoffeeScript，在云端处理图片，压缩CSS、JS，本地缓存和快速远程访问。 不需要改变你的模板资源。 可以通过[Composer][3]、[Phar File][4] 或从 [GitHub][5]下载安装。

## [Brunch][6]

![clipboard.png](http://segmentfault.com/img/bVk272)

基于Node.js的第一个项目汇编程序。 从优化的角度来看类似Munee（ 刚才说过的PHP库，这样高能的工具在PHP界里不常见）。 Brunch 能用于很多流行的框架：Boilerplate、Bootstrap、Skeleton、Angular.js、 Backbone.js、Jade、 Phonegap等。

## [Favico.js][7]

![clipboard.png](http://segmentfault.com/img/bVk28F)

一个小小的图标元素对适当的交互非常有用。 这个脚本可以让你轻易地操纵各种方法来显示项目的图标，甚至流媒体视频或摄像头的记录。 类似的还有  [jQuery Notify Better][8] ，但功能没这么强大。

## [Animo.js][9]

![clipboard.png](http://segmentfault.com/img/bVk28G)

现在可以通过  [Effeckt.css][10] 和 [Animate.css][11] 轻易的操作CSS动画。 Animo.js是个智能库（大小只有7KB），能方便的制作CSS动画 (animate+animo.css) ，还增加了跨浏览器的模糊效果。 配合 jQuery 2 能更好的使用。

语法很简单：

    $('#demo-a').animo({animation: "fadeOutLeft", duration: 0.5, keep: true}, function() {
        $('#demo-n').animo({animation: "fadeOutUp", duration: 0.5, keep: true}, function() {
            $('#demo-i').animo({animation: "fadeOutDown", duration: 0.5, keep: true}, function() {
                $('#demo-m').animo({animation: "fadeOutLeft", duration: 0.5, keep: true}, function() {
                    $('#demo-o').animo({animation: "fadeOutRight", duration: 0.5, keep: true}, doMagicIn()); // function to fade them back in
                });
            });
        });
    });

## [Gridism][12]

![clipboard.png](http://segmentfault.com/img/bVk28K)

如果你还没有使用过CSS框架（Bootstrap、Foundation 等），我推荐Gridism，我认为它是创建响应式网站最简单、最轻量级的框架。

## [Rework][13]

![clipboard.png](http://segmentfault.com/img/bVk28N)

在Node.js 里进行 CSS 预处理的插件。 很好地结合了LESS、 SCSS 和 Stylus，因为它有很好的JavaScript功能，内置 Compass，能自由地操作前缀、透明等属性，优化在 retina 屏幕的显示等。

## [Basiliq][14]

![clipboard.png](http://segmentfault.com/img/bVk276)


Basiliq是拥有者大量UI元素的线框图工具，用于创建桌面或移动模型。 我个人非常喜欢“写意”的风格，看完产品介绍的视频后更喜欢了。 它是由 Samara 市的 CloudCastle 设计工作室开发的。 是个高质量、高品味的产品。

## [Cleaver][15]

![clipboard.png](http://segmentfault.com/img/bVk28P)

《30-second Slideshows for Hackers》已经说完我想说的话了。

> npm install -g cleaver
> cleaver path/to/something.md


    title: Basic Example
    author:
      name: "Jordan Scales"
      twitter: "@jdan"
      url: "http://jordanscales.com"
    output: basic.html
    controls: true

    --

    # Cleaver 101
    ## A first look at quick HTML presentations

    --

    ### A textual example

    Content can be written in **Markdown!** New lines no longer need two angle brackets.

    This will be in a separate paragraph

    --

    ### A list of things

    * Item 1
    * Item B
    * Item gamma

    No need for multiple templates!

而最后我们会得到[这样的介绍][16]。

## 最后

1.看看我的 [Shade.less][17]。

2.最近我一直在寻找一个类似Kuler的工具来确定扁平化的配色，只发现这个[调色板][18]。

3.有趣的CSS作品： [the Client-side full-text search in CSS][19], [Mona Lisa pure CSS][20] 。

---

> 英文原文：[Awesomeness & Usefulness for Web Developers #3][21]

> 本文是我为 [SegmentFault][22] 所译

  [1]: https://cloudconvert.org/
  [2]: http://mun.ee/
  [3]: http://mun.ee/Installating_Munee/With_Composer
  [4]: http://mun.ee/Installating_Munee/Using_Phar_File
  [5]: https://github.com/meenie/munee
  [6]: http://brunch.io/
  [7]: https://github.com/ejci/favico.js
  [8]: http://www.thepetedesign.com/demos/notify_better_demo.html
  [9]: https://github.com/ThrivingKings/animo.js
  [10]: https://github.com/h5bp/Effeckt.css
  [11]: https://github.com/daneden/animate.css
  [12]: http://cobyism.com/gridism/
  [13]: https://github.com/visionmedia/rework
  [14]: http://cloudcastlegroup.com/blog/basiliq
  [15]: https://github.com/jdan/cleaver
  [16]: http://jdan.github.io/cleaver/
  [17]: https://github.com/Pestov/Shade
  [18]: http://flatuicolors.com/
  [19]: http://redotheweb.com/2013/05/15/client-side-full-text-search-in-css.html
  [20]: http://codepen.io/jaysalvat/pen/HaqBf
  [21]: http://ipestov.com/awesomeness-and-usefulness-for-web-developers-3/
  [22]: http://segmentfault.net/blog/news/1190000002594623

