---
layout: post
title:  VirtualBox:寄主Ubuntu访问宿主Windows分区文件
date:   2015-12-28 08:24:00
category: [Ubuntu]
tags: [Ubuntu,VirtualBox,Windows]
---

- VirtualBox对Ubuntu系统设置共享文件

![共享文件][1]

<!--more-->

- 安装Virtual Box Guest Additions

![Guest Additions][2]

- 挂载

在Ubuntu下建个目录，例如`c`
```
mkdir c
```
挂载Windows C盘

```
sudo mount -t vboxsf c c/
```

![mount][3]

- 效果

![效果][4]


  [1]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151228153347.png
  [2]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151228154117.png
  [3]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151228154908.png
  [4]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151228154040.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/South/dy/5