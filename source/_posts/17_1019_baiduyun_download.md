---
layout: post
title:  用迅雷下载百度云，突破大文件和速度限制
date:   2017-10-19 08:24:00
category: [Tools]
tags: [Tools,效率,小工具]
---

<!-- ![用迅雷下载百度云][1] -->

<!--more-->

> 欢迎交换友链： [laker.me--进击的程序媛]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
> V信: lakerHQ （请注明‘来自博客’）

百度云网页版有限制下载大文件，必须使用客户端，而客户端又有速度限制。要么使用破解版的客户端，安全性不敢保证。迅雷大家都有，可以考虑用迅雷下载百度云的资料。根据[知乎上的讨论][2]，尝试了大家的方法，最后选择了其中一种，并在原答主的基础上有所改进。

## 1、下载浏览器脚本管理器插件
这里选用[tampermonkey][3]，也可以选用其他的

官网下载：http://tampermonkey.net/index.php?version=4.0.69&ext=dhdg&show=gcal
备用下载：https://pan.baidu.com/s/1c2CdKFu

## 2、安装脚本

到 [greasyfork][4] 下载解决百度云大文件下载限制的脚本

## ３、到百度云网页版下载东西

打开百度云网页版，脚本就开始运行

![tampermonkey][5]

### chrome

选择文件下载

![step][6]

可以选择在chrome里下载，但是比较慢。
所以暂停下载，获取下载地址：

![step][7]

到迅雷新建下载任务，可以一次性下载多个任务

![step][8]

刚开始是0B，没事

![step][9]

解析、链接之后就正常了

![step][10]

### 360 极速浏览器

如果文件比较多，这样获取下载地址比较麻烦。国内的浏览器有些有直接点击迅雷下载。如果没有的可以重新安装迅雷以便重新安装迅雷插件。不想下载的也可以手动复制下载链接。

我刚下载的360极速可以直接显示下载地址，也比较方便。

![step][11]

批量下载，速度比较可观。不过不支持断点续传能力较弱，并且会出现下载到一半自动停掉，显示地址错误的提醒，大概是百度云的地址会有更换的机制。

![step][12]

如果长时间没下载完成，可能是百度云的某种机制使下载地址会失效，需要重新获取地址。我就是下了一晚上，没有限制下载个数，所有东西只下载了一半然后全部失效，以后都吸取教训限制下载个数，减少损失。建议文件不要太大，多分几个压缩包下载。


  [1]: http://77g54f.com1.z0.glb.clouddn.com/bgt-20171019.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [2]: https://www.zhihu.com/question/22085759
  [3]: http://tampermonkey.net/index.php?version=4.0.69&ext=dhdg&show=gcal
  [4]: https://greasyfork.org/zh-CN/scripts/17800-%E8%A7%A3%E5%86%B3%E7%99%BE%E5%BA%A6%E4%BA%91%E5%A4%A7%E6%96%87%E4%BB%B6%E4%B8%8B%E8%BD%BD%E9%99%90%E5%88%B6
  [5]: http://77g54f.com1.z0.glb.clouddn.com/QQ20170604164848.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [6]: http://77g54f.com1.z0.glb.clouddn.com/QQ20170604165104.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [7]: http://77g54f.com1.z0.glb.clouddn.com/QQ20170604165126.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [8]: http://77g54f.com1.z0.glb.clouddn.com/QQ20170604165231.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [9]: http://77g54f.com1.z0.glb.clouddn.com/QQ20170604165252.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [10]: http://77g54f.com1.z0.glb.clouddn.com/QQ20170604165326.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [11]: http://77g54f.com1.z0.glb.clouddn.com/QQ20170604165648.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [12]: http://77g54f.com1.z0.glb.clouddn.com/QQ20170604181619.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10

