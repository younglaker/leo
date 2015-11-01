---
layout: post
title:  Github push 常见报错解决方案
date:   2015-09-18 08:24:00
category: [Git]
tags: [Git]
---

> 本文可供git的其他托管应用如coding，gitcafe参考，解决方案的思路一致。

<!--more-->

## fatal: could not read Username for 'https://github.com': Invalid argument

无法识别设置的github用户名。

### 原因
根据[StackOverflow][1]上的讨论，据说是1.8.5的BUG，但是我现在用到2.5.2了还是会出现这样问题。不过解决方案是可用的。

其他参考： 
[Error when push commits with Github: fatal: could not read Username][2]
[Github configuration question / problem][3]
[sublime-text-git，fatal: could not read Username for 'https://github.com': Device not configured ][4]
[Git push requires username and password][5]

### 方案一

检查是否进行的Git设置，[详情][6]

    git config --global user.name "YOUR NAME"
    git config --global user.email "YOUR EMAIL ADDRESS"


### 方案二
确保用户名正确的情况还是报错，就把HTTPS改为SSH方式连接，例如：

    [branch "gh-pages"]
    	remote = git@github.com:younglaker/blog.git
    	merge = refs/heads/gh-pages

## fatal: Could not read from remote repository.


    fatal: Could not read from remote repository.
    
    Please make sure you have the correct access rights
    and the repository exists.

### 原因
因为使用 SSH 连接，安全问题，要把Github添加到信任列表里。

### 方案


根据[Github的文档][7]，执行以下命令:

     ssh -T git@github.com
     
输入yes回车：

    Are you sure you want to continue connecting (yes/no)? yes

看到下面的返回信息，就是把Github添加到信任列表里了：

    Hi username! You've successfully authenticated, but GitHub does not
    # provide shell access.


  [1]: http://stackoverflow.com/questions/20871549/error-when-push-commits-with-github-fatal-could-not-read-username/20884273#20884273
  [2]: http://stackoverflow.com/questions/20871549/error-when-push-commits-with-github-fatal-could-not-read-username
  [3]: https://github.com/hexojs/hexo/issues/857
  [4]: https://github.com/kemayo/sublime-text-git/issues/176
  [5]: http://stackoverflow.com/questions/6565357/git-push-requires-username-and-password
  [6]: https://help.github.com/articles/set-up-git/
  [7]: https://help.github.com/articles/generating-ssh-keys/