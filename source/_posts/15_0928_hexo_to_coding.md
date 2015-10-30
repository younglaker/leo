---
layout: post
title:  把 Hexo 托管到 Coding
date:   2015-09-28 08:24:00
category: [Hexo]
tags: [Hexo,Coding,静态博客]
---

本文基于Hexo已经开发好，只是修改托管地址。关于Hexo其他文章详见[这里][1]。

## 新建Coding项目

新建Coding项目，并导入Github项目。

<!--more-->

## 修改Deploy地址

在config文件，设置远端地址：

    deploy:
      type: git
      repo: git@git.coding.net:laker/blog.git
      branch: gh-pages

然后编译、部署。

部署时我遇到这个报错;

    fatal: Could not read from remote repository.
    
    Please make sure you have the correct access rights
    and the repository exists.

根据[Coding的文档][2]，执行以下命令:

     ssh -T git@git.coding.
     
输入yes回车：

    Are you sure you want to continue connecting (yes/no)? yes
    Warning: Permanently added 'git.coding.net,111.12.46.121' (RSA) to the list of known hosts.
    Coding.net Tips : [Hello laker! You've connected to Coding.net by SSH successfully! ]

这就把Coding添加到信任列表里。这个和Github一样 `ssh -T git@github.com`。

## 开启Coding演示
按提示一步步点就行了：

![开启Coding演示][3]

提示：这样部署博客，并不能获得码币。而且经测试，Hexo不支持同时多个托管仓库，所以我还是放在Github上 = =

  [1]: http://laker.me/blog/categories/Hexo/
  [2]: https://coding.net/help/about_git/about_ssh_host_key
  [3]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150918140237.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/South/dy/5