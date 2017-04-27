---
layout: post
title:  Git管理多个远程仓库(以Github和Coding为例)
date:   2015-09-17 08:24:00
category: "Git"
tags: [Git]
---


## 两个空代码仓库
如果是两个仓库都是空的，就直接在`.git/config`中添加远端地址

    [remote "origin"]
    	url = https://github.com/younglaker/octjs.git
        url = https://git.coding.net/laker/octjs.git  #添加新地址
    	fetch = +refs/heads/*:refs/remotes/origin/*

地址是配好了，但是还要注意分支一致。我这里都用master，就不会有问题。

<!--more-->

## 非空代码仓库
假设Github中使用了一段时间，想在Coding里备份一个，要想把两边仓库同步到一致的状态。

线到Coding新建仓库，获得地址后，`.git/config`中添加Coding的远端地址，这里我命名为coding：


    [remote "origin"]
    	url = https://github.com/younglaker/octjs.git
    	fetch = +refs/heads/*:refs/remotes/origin/*
    [remote "coding"]   #添加coding远端
    	url = https://git.coding.net/laker/octjs.git  #远端地址
    	fetch = +refs/heads/*:refs/remotes/coding/*  #注意修改远端名

使用Git GUI 获取 Coding上的信息，你也可以使用命令行完成一下操作：

![获取][1]

合并:

![合并][2]

推送，记得选Coding远端：

![推送][3]

然后再修改`.git/config`，吧Coding也用origin远端名，下次就只用`git push`就可以推送到两边了。重启 Git GUI 也只剩一个远端了：

    [remote "origin"]
    	url = https://github.com/younglaker/octjs.git
        url = https://git.coding.net/laker/octjs.git
    	fetch = +refs/heads/*:refs/remotes/origin/*

## Github 不为空，Coding为新建项目

那就在Coding新建项目时导入Github项目，本地git配置改为：

    [remote "origin"]
    	url = https://github.com/younglaker/octjs.git
        url = https://git.coding.net/laker/octjs.git
    	fetch = +refs/heads/*:refs/remotes/origin/*

  [1]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150915165250.png
  [2]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150915165335.png
  [3]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150915165418.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/South/dy/5