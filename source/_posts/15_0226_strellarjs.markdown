---
layout: post
title:  用 Stellar.js 制作视差滚动效果
date:   2015-02-26 08:24:00
category: [翻译,JavaScript]
---

近些年讨论得很热烈的设计趋势是视觉差滚动效果。不管你喜不喜欢，很多网站都在用它。在本教程中，我会介绍视觉差滚动和用jQuery插件Stellar.js来制作视觉差滚动效果。


<!--more-->

## 视差滚动（Parallax Scrolling）是什么？

视差滚动是当用户滚动页面时，前景和背景以不同的速度移动，从而创造出3D效果。 这种效果可以给网站一个很好的补充，但如果滥用，就会很烦人。 有些完全由这种效果驱动的网站会让人觉得不优雅。 因为这种效果通常使用大图像做背景，网站资源大量增加，导致加载非常缓慢。

有些这样滥用的例子，比如介绍[Kinvara saukoni 3的网站][1]， 和大小有20MB（以前是50MB的！）的 [Oakley – I am invincible][2] 。

现在有了对这个效果的认识，让我们看看如何使用stellar.js来创造它。

## Stellar.js是什么？
[stellar.js][3] 是一个 jQuery插件，能很容易地给网站添加视差滚动效果。 尽管已经停止了维护，但它非常稳定，与最新版本的jQuery兼容，很多开发者也在使用它。 这个插件在[jQuery插件库][4]里很流行，你可能早已听说过了。

现在，让我们看看如何使用它。

## Stellar.js入门
Stellar.js很容易上手。 第一步是下载插件并将它链接到你的页面。 可以通过Bower访问[Stellar.js的GitHub 仓库][5]。 如果你想使用Bower，可以通过以下命令：
```
bower install jquery.stellar
```
下载好后，在页面中引用：

    <script src="path/to/jquery/jquery.min.js"></script>
    <script src="path/to/jquery.stellar.min.js"></script>

完成后，开始给页面添加视觉差滚动效果。 这个插件允许将效果添加到任何滚动的元素，例如`window`对象，或者其他元素。 要使用jQuery的选择器选中所需要的元素，在绑定`stellar()`方法即可。


    $('#someElement').stellar();
对于`window`对象可以用下面的方法：

    $.stellar();

这样，Stellar.js库就会在元素滚动时搜索parallax背景或元素，并重新定位。
在一个页面运用stellar.js创建一个视差滚动效果的[示例][6]。

## 选项
stellar.js像其他插件一样有一定的灵活性。 可以设置很多参数来满足需求。 stellar.js允许定义普通选项，会应用到每个元素。 设置普通配置必须通过`stellar()`方法，而对应的元素要设置`data-*`属性。 我不一一介绍每个配置的用法，具体可以看[这里][7]。

第一个普通选项是设置效果的方向。 经典的滚动效果是从上到下，或者反过来。也可以指定一个从左到右的效果，或者反过来。 通过设置`horizontalScrolling` 和`verticalScrolling`的bool值完成。 其默认值是`true`。

另一个有趣的选项是`responsive`。 它是用来指定`load `或`resize `事件触发时，是否刷新页面。 默认是`false`。

最后介绍一下`hideDistantElements`选项。 指定是否要隐藏移出视线的元素。 如果不想隐藏，就设置为`false`。

单个元素选项中`data-stellar-background-ratio`比较常用。 接受一个正整数的值，可以改变它被应用到元素的影响速度。 例如，`data-stellar-background-ratio="0.5"`意味着改变速度为自然滚动速度的一半。 如果想使这个属性值低于1，建议在样式表里设置`background-attachment: fixed;`。

现在你知道这个插件，你可以配置它，它的时间去看比赛。

## 演示

利用上面介绍的属性做一个例子。 首先，我们需要设置标记。 在下面的代码中将创建6个包含一些文本`div`：

    <div class="content" id="content1">
        <p>TEXT HERE</p>
    </div>
    <div class="content" id="content2">
        <p>TEXT HERE</p>
    </div>
    <div class="content" id="content3" data-stellar-background-ratio="0.5">
        <p>TEXT HERE</p>
    </div>
    <div class="content" id="content4" data-stellar-background-ratio="0.5">
        <p>TEXT HERE</p>
    </div>
    <div class="content" id="content5" data-stellar-background-ratio="0.5">
        <p>TEXT HERE</p>
    </div>
    <div class="content" id="content6" data-stellar-background-ratio="0.5">
        <p>TEXT HERE</p>
    </div>

添加一些CSS： 在演示中将使用三个图像，每个重复两次。 因为要给最后桑元素添加`data-stellar-background-ratio`属性，所以还要设置`background-attachment: fixed;`。
CSS代码如下所示：


    body {
        font-size: 20px;
        color: white;
        text-shadow: 0 1px 0 black, 0 0 5px black;
    }
    p {
        padding: 0 0.5em;
        margin: 0;
    }
    .content {
        background-attachment: fixed;
        height: 400px;
    }
    #content1 {
        background-image: url("http://www.tamperlock.com/blog/wp-content/uploads/2014/08/london-england.jpg");
    }
    #content2 {
        background-image: url("http://ocdn.eu/images/pulscms/ZjU7MDQsMCwzMiwzODQsMWZhOzA2LDMyMCwxYzI_/1eb29a70dabd0994cdefaad01ca3c884.jpg");
    }
    #content3 {
        background-image: url("http://www.zeus.aegee.org/magazine/wp-content/uploads/napoli-golfo-vesuvio.jpg");
    }
    #content4 {
        background-image: url("http://www.tamperlock.com/blog/wp-content/uploads/2014/08/london-england.jpg");
    }
    #content5 {
        background-image: url("http://ocdn.eu/images/pulscms/ZjU7MDQsMCwzMiwzODQsMWZhOzA2LDMyMCwxYzI_/1eb29a70dabd0994cdefaad01ca3c884.jpg");
    }
    #content6 {
        background-image: url("http://www.zeus.aegee.org/magazine/wp-content/uploads/napoli-golfo-vesuvio.jpg");
    }

最后，我们需要踢的invokingstellar()启动效应。在这个演示中我们也会设置一些常用选项：

    $.stellar({
        horizontalScrolling: false,
        responsive: true
    });

##效果：

https://jsfiddle.net/fb301gve/embedded/result/

> 英文原文：[An Introduction to Parallax Scrolling Using Stellar.js][8]

> 本文是我为 [SegmentFault][9] 所译

  [1]: http://community.saucony.com/kinvara3/
  [2]: http://moto.oakley.com/
  [3]: https://github.com/markdalgleish/stellar.js/
  [4]: http://plugins.jquery.com/
  [5]: https://github.com/markdalgleish/stellar.js/
  [6]: http://markdalgleish.com/projects/stellar.js/demos/backgrounds.html
  [7]: https://github.com/markdalgleish/stellar.js#configuring-everything
  [8]: http://www.sitepoint.com/introduction-parallax-scrolling-using-stellar-js/
  [9]: http://segmentfault.com/blog/news/1190000002566463
