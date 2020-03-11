---
layout: post
title: uniapp 构建小程序报错 initAutoImportComponents is not a function
date:   2020-02-22 08:24:00
category: [Vue.js]
tags: [JavaScript,HTML5,Vue.js,CSS3,Web]
---


在使用uniapp开发小程序的时候，经常会遇到 initAutoImportComponents is not a function，这个问题很奇怪，团队里不是每个人都会遇到。看网上蛮多开发者遇到了，但是还没有很好的解决方案。

<!--more-->

记录一下我尝试过的方案：

- 删除node_module重新npm i，按照提示执行了 npm audit fix

删了很多次，重装未果。害怕是墙的问题，还开了全局也不行。

- 按照网友的建议在所有版本号2.0.0后面加了 -alpha

[网友讨论](https://ask.dcloud.net.cn/question/87346)
[另一个方案](https://copyfuture.com/blogs-details/20200303164053977ra97r2nlsa52e4h)
都未成功

- 换了个目录重新安装

可以运行、编译，但是到了第二天又编译不成功。

- 又换了个目录，重新安装

安装的时候发现pakage.json在audit后的版本号里加了个alpha，考虑是不是audit出的问题。然后就不audit，虽然有很多warn，但是总算能执行了

initAutoImportComponents 这个关键词只在uniapp的论坛里出现，应该就是uniapp本身的问题，还不太稳定。而且有时候安装步骤是一样的，但是就不成功，得多删除几次node_module来npm重装。



> Exchange blogroll： [http://laker.me/blog]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
