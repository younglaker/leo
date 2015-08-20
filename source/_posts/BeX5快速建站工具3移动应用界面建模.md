---
layout: post
title:  BeX5快速建站工具（三）移动应用界面建模
date:   2015-07-31 08:24:00
category: [ERP,BeX5]
tags: [ERP,BeX5,Web,HTML5,BootStrap]
---

来自[Laker's Blog][1]，转载请注明出处，欢迎交换友链

##新建W文件
`UIZ > erp > buy > process > goods ` 右键新建W文件，选择`移动 > 列表/详细 > 列表+表单 ` 

<!--more-->

![新建W文件][2]

配置设置同上一篇文章，唯一不同的是要在文件名后加`.m`，表示移动端文件：

![起名字][3]

##预览

此时不同像上篇文章中说的要新建角色、开发权限，因为这个文件是同名网页的移动版，数据和权限共享。

移动端访问地址：http://127.0.0.1:8080/x5/m

把浏览器缩窄后可以看到主界面：

![主界面][4]

进入物品信息维护的列表页：

![列表页][5]

表单:

![表单][6]

对比一下web版在窄屏下的样子：

![web版在窄屏下的样子][7]

![web版在窄屏下的样子][8]

很快就把移动版的界面做好了，相比响应式的界面更符合移动端设计，后期还可以打包成移动app。


  [1]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150729100950.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [2]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150729100950.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [3]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150729101058.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [4]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150729101213.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [5]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150729101551.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [6]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150729101606.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [7]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150729101659.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [8]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150729101736.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10