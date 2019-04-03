---
layout: post
title:  自开发的EasyCanvas绘图库实践、Pixeler项目开发小结
date:   2018-05-04 08:24:00
category: [HTML5]
tags: [JavaScript,HTML5,Canvas]
---

 <!-- ![EasyCanvas绘图库实践][1] -->

<!--more-->

> 欢迎交换友链： [laker.me--进击的程序媛]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
> V信: lakerHQ （请注明‘来自博客’）


## 涉及的两个项目

[Pixler][2]：一个用于设计像素图片（拼豆）的应用。

[Easycanvas.js][3]： Canvas 绘图库

![Pixler][4]

## 开发背景

我对拼豆感兴趣，在做拼豆前要设计图纸，类似画像素图。我试用了网上能搜到的几个拼豆图纸设计的应用，但是没有适合我的，我就想着自己开发一个。

![拼豆][5]

## 算法原理

拼豆图纸就类似于像素图，我刚开始构思如何开发的时候，想着它有点像下棋。所以我参考了五子棋的下棋原理。我在五子棋的算法上优化了鼠标点击时落脚的位置的计算方法，即鼠标点击时，获取点击位置，计算出它处于哪个方格中，在那个方格中画上一个像素点，用一个二维数组记录方格中已绘制的位置。这就完成了初步的拼豆像素图的算法设计。

在以往的开发中，我都要求每一步都精益求精，导致整体进度缓慢，常常停留在初步阶段，就把自己绕晕。所以在此次开发中，尝试了小步快跑、快速迭代的方法。

## 第一版：快速开发

第一版本开发的时候，我尽量减少对性能、代码优化的思考，在最快的速度完成基本功能，也就是如何绘制像素点和删除像素图。

这样没有束缚的情况下，只需要集中精力完成功能的算法，很快就实现基本功能。

当然，代码也是很简单粗暴的，就需要第二版的完善。


## 第二版：性能和代码优化

首先，把画布分为两层，一层是参考线画布，一层是绘图画布。参考线画布在初始化后就不需要修改，所有操作只需要在绘图画布上进行，减少了绘图时候的工作量。

然后，把通用功能的代码封装成公共函数，减少冗余。

## 第三版：封装绘图库，并在应用中不断完善

Pixler 主要代码是 Canvas 绘图，所以可以把 Canvas 主要绘图功能封装一下，单独成一个绘图库，减少主代码冗余，也方便在其他项目中引用。

在大学期间，我研究 jQuery 的时候就仿着写了一个链式结构的 JavaScript 框架 [Oct.js][6]，加上第一、第二版本对 Canvas 接口的熟悉，所以开发起来并不困难。但在接口设计上重复弄了几次，这部分的经验我也写了一篇文章 [《EasyCanvas：连续画图的一些总结》][7] 记录了一下。

开发 Easycanvas.js，不仅是在 JavaScript 开发、Canvas 运用上的提升，还是一个开源项目的完整实践。期间有一个小伙伴加入参与了合作，可惜没参与太多功能就退出了，但还是一次很好的开源项目的体验。

在开发代码的过程中，还编写了相关的文档。接口不断优化修改，文档也不断的调整，就连文档格式也做了多次调整，工作量是不小，但也不厌其烦。

由于时间原因，在开发完 Easycanvas.js 基础版本后就去做别的项目。间隔一段时间回来再看，基本没有有最初开发时候的熟悉感，这就得靠我之前写的文档了。所以，好的文档是项目的开门钥匙。

就这样，我像一个刚接触这个绘图库的用户一样，参照文档，把 Easycanvas.js 重构了 Pixler 的绘图代码。同时，在应用的过程中发现了 Easycanvas.js 的不足，又反过来进行完善。两个项目相辅相成。

![Easycanvas][8]


## 小结

相比之前开发的 [Oct.js][9]，只有开发和单元测试，并没有大规模地应用到实际项目中（我也尝试过，但一旦项目做大，就涉及到 jQuery 插件 ，就不得不引入 jQuery，就和 Oct.js 重复了，就只好把 Oct.js 删掉）。

所以，这次 Pixler 和 Easycanvas.js 的开发，从0到1再到100，是一个很好的经历。不仅是编程技能上的提升，还是项目管理上积累了经验。

至此 Pixler 和 Easycanvas.js 完成了一个较为稳定的版本，但还有很大的提升空间，我都一一记录在 Todolist 上了，等我一一突破。


  [1]: http://77g54f.com1.z0.glb.clouddn.com/bgt-20180503.jpg?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [2]: https://github.com/younglaker/pixeler
  [3]: https://github.com/younglaker/EasyCanvas
  [4]: https://camo.githubusercontent.com/1d13f30b16d7e66731cab36a3433bf27d4f10e9e/687474703a2f2f3737673534662e636f6d312e7a302e676c622e636c6f7564646e2e636f6d2f626c6f6732303135313232393131333032322e706e67
  [5]: http://77g54f.com1.z0.glb.clouddn.com/QQ2018050301.jpg
  [6]: https://github.com/younglaker/octjs
  [7]: http://laker.me/blog/2017/06/15/17_0615_easy_canvas/
  [8]: http://77g54f.com1.z0.glb.clouddn.com/blog20151229112337.png
  [9]: https://github.com/younglaker/octjs