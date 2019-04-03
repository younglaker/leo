---
layout: post
title:  Sublime3 中文文件夹乱码解决方案
date:   2015-08-26 08:24:00
category: [Sublime]
tags: [Sublime]
---

本人使用的版本是sublime 3 build 3065。文件树和标签的中文会乱码。

<!-- ![sublime 3 中文乱码][1] -->

<!--more-->

原因是当Windows 个性化显示 中的设置自定义文本大小(DPI)，大于默认的100%的时候触发这个BUG。

解决方案：在`菜单栏---Preferences---Setting-User` 添加以下代码，重启即可。这句话的意思是——选择“较小-100%”的模式。用于覆盖操作系统设置的DPI。

    "dpi_scale": 1.0

![解决完成][2]


  [1]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150828113827.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [2]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150828113958.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5