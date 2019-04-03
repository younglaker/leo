---
layout: post
title:  利用 Github 分支管理一写无关痛痒的项目
date:   2018-02-11 08:24:00
category: [GitHub]
tags: [GitHub]
---

<!-- ![利用 Github 分支管理小项目][1] -->

<!--more-->

> 欢迎交换友链： [laker.me--进击的程序媛]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
> V信: lakerHQ （请注明‘来自博客’）

## 背景

因为经常会写一些小程序，需要备份到 Github 方便管理和分享。随项目增多，Repo 的数目越来越多，但是很多是无关痛痒的，不必要这么多仓库存放。处女座情结表示这样特别乱，而且一眼看上去都是很辣鸡的代码，得想办法整理一下。

## 整理方法

1.建立一个仓库 （例如我的 [CometLab][2]），master分支用来做展示入口，只存放一个 README.md 来作为介绍。起名 Lab，就是意味着这里就是一个实验室。里面都是些实验性的项目。
2.每个小项目用其他分支存放，各分支之间没什么关系。例如现在有的`vue-todo` `vue-eleme` `ng-ionic`。

问题来了，在分支上的提交不计入 contribution，但是我会在这个仓库的分支进行很多开发，导致calendar是空的，不是所有的发布信息都展示出来，管理代码不太方便。


## Contributions未被Github计入的几个常见原因

- 进行Commits的用户没有关联到Github帐号
- 未合并到默认分支或gh-pages的Commit
- Fork的仓库

## 解决

既然要求合并到 master 才能计入 contribution，那么就 merge 一下就可以解决。

分支的小项目在日常进行正常的开发、提交，待基本完成后一次性merge 到 master，以前的 commit 会一次性计入 contribution，展示在 calendar上。

## merge 操作

先切换到默认分支

    git checkout master

合并到 master

    git merge origin/分支名

删除除了mater readme.md 以外的所以文件，并修改readme的冲突，保持 master 为空。提交更改到本地：

    git add -A
    git commit -m'merge'

再提交到 master

    git push origin master

在分支里曾经提交过的 commit 就会一次性计入 contribution，展示在 calendar上。

## 升级用法

为了方便开发，每个分支在本地用一个文件夹。

下载指定分支的代码：

    git clone -b 分支 git@github.com:younglaker/CometLab.git

修改本地文件夹名字成分支名字，方便管理。

再 clone 一个完整的仓库，需要 merge 的时候再 pull、merge、push。

## 常见问题

提交代码找不到远端分支。很可能是本地所在分支不是AAA，很可能目前是在master，误以为在AAA分支。

```
$ git push origin AAA
error: src refspec AAA does not match any.
error: failed to push some refs to 'git@github.com:younglaker/BBB.git'

```






  [1]: http://77g54f.com1.z0.glb.clouddn.com/bgt-20180211.jpg?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [2]: https://github.com/younglaker/CometLab

