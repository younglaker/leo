---
layout: post
title:  ADF/JDeveloper—两栏布局、折叠菜单
date:   2015-11-16 08:24:00
category: [Java,ADF]
tags: [Java,ADF,JDeveloper]
---

ADF/JDeveloper—两栏布局、折叠菜单

<!--more-->

## 效果

![部门信息][1]



![员工信息][2]

## 准备

我这里的范例用到员工信息表、部门信息表，建立好相应EO、VO、AM、TF、jsff。

![TF][3]


## 主要步骤

在 index.jspx 做好基本布局——左右分栏的splitter，左边放链接。

![基本布局][4]

把部门的TaskFlow拖入 index.jspx ，选择 Dynamic Region：

![把TaskFlow拖入 index.jspx][5]

新建Bean:

![新建Bean][6]

进入个建的Bean，选中 taskFlowId，右键，generate Accessors:

![generate Accessors][7]

就生成下面的方法;

![生成方法][8]

复制这个地址：

![复制][9]

找到 Page Flow 的 adfc-config 文件，把我们刚建的 Bean 的 Scope 属性改为 view：

![adfc-config][10]

在 index.jspx ，给 link 拖一个 Set Property Listener, From 处粘贴刚刚复制的地址：

![Set Property Listener][11]

To 处选择刚刚创建的 Bean 的 taskFlowId

![taskFlowId][12]

Type 选择 Action

![Action][13]

同理给员工的link这样操作，From 处改为员工的 TF 的 name。

即可：

![运行][14]

  [1]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151027171621.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [2]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151027171631.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [3]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151027094228.png
  [4]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151027162918.png
  [5]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151027162717.png
  [6]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151027162818.png
  [7]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151027163026.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [8]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151027163051.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [9]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151027163115.png
  [10]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151027163342.png
  [11]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151027163555.png
  [12]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151027163633.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [13]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151027163651.png
  [14]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151027171621.png