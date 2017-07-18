---
layout: post
title:  在VirtualBox里访问本地硬盘
date:   2015-09-08 08:24:00
category: [VirtualBox]
---

## 背景

* VirtualBox 5.0
* 宿主系统 win7 64bit（windows 其他版本通用）
* 寄宿系统 win7 32bit（windows 其他版本通用）

<!--more-->

## 安装VirtualBox功能增强包

VirtualBox 4 需要自行到orale/virtualbox目录下寻找安装文件，5.0可以直接点击选项安装：

![安装增强功能][1]

运行安装：

![运行][2]

## 添加共享文件夹
设备---共享文件夹---共享文件夹

![添加共享文件夹][3]

新增分配

![新增][4]

选择一个盘符（C、D已经被寄宿系统占用），并选择本地分区，可以多次操作把宿主系统的C/D/E/F全部挂载：

![挂载本地硬盘][5]

## 寄宿系统映射

右键计算机---映射网络驱动器

![此处输入图片的描述][6]

添加刚刚挂载的分区;

![此处输入图片的描述][7]

保存后即可看到：

![保存后即可看到][8]


  [1]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150831144352.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [2]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150831144426.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [3]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150831154236.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [4]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150831154307.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [5]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150831154343.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [6]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150831141245.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [7]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150831154831.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [8]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150831154905.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5