---
layout: post
title:  Ubuntu/Debian 里 npm 安装包报错解决方案
date:   2015-10-12 08:24:00
category: [Nodejs]
tags: [Nodejs,npm,Ubuntu]
---

## 问题
在下Debian/Ubuntu 里 npm 安装包时：

    sudo npm install

可能会遇到如下报错：

<!--more-->

    /bin/sh: 1: node: not found
    gyp: Call to 'node -e "require('nan')"' returned exit status 127. while trying to load binding.gyp
    gyp ERR! configure error 
    gyp ERR! stack Error: `gyp` failed with exit code: 1
    gyp ERR! stack     at ChildProcess.onCpExit (/usr/share/node-gyp/lib/configure.js:344:16)
    gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
    gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:797:12)
    gyp ERR! System Linux 3.16.0-23-generic
    gyp ERR! command "nodejs" "/usr/bin/node-gyp" "rebuild"
    gyp ERR! cwd /home/laker/project/node-china/node_modules/bcrypt
    gyp ERR! node -v v0.10.25
    gyp ERR! node-gyp -v v0.12.2
    gyp ERR! not ok 
    npm WARN This failure might be due to the use of legacy binary "node"

提取报错的关键词：

    node: not found
    npm WARN This failure might be due to the use of legacy binary  "node"

或者有时候是：

    /usr/bin/env: node: No such file or directory

也就是没有找到node。这是因为Ubuntu/Debia安装的 Nodejs 在 `/usr/bin/nodejs` 里，而大多数包是用 `/usr/bin/node`路径。 

## 解决方案一：

使用symbolic link （符号链接，又称软链接）：

    sudo ln -s /usr/bin/nodejs /usr/bin/node

## 解决方案二

安装legacy：

    sudo apt-get install nodejs-legacy

## 解决方案三：

项目目录里：
修改package.json 文件中的

    "start": "node ./bin/"

改为

    "start": "nodejs ./bin/www"  

bin/www文件中的：

    #!/usr/bin/env node 
    
改为
    
    #!/usr/bin/env nodejs  


更多相关讨论参考这条 [Github issue][1]

## 拓展 

系统中的链接是一个已经存在的文件的另一个名字。

Linux链接分两种，一种被称为硬链接（Hard Link），另一种被称为符号链接（Symbolic Link）。

默认情况下，`ln`命令产生硬链接。`-s`相当于建立快捷方式，删掉不影响源文件

硬连接指通过索引节点来进行连接，相当于另一个文件别名入口，删掉任何一个都物理删除了。

软链接文件有类似于Windows的快捷方式。它实际上是一个特殊的文件。在符号连接中，文件实际上是一个文本文件，其中包含的有另一文件的位置信息。只要删掉了源链接文件，软链接也就失效了。


  [1]: https://github.com/nodejs/node-v0.x-archive/issues/3911