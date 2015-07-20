---
layout: post
title:  征服命令行
date:   2015-01-22 08:24:00
category: [翻译,Terminal]
---

![help.png][1]

命令行（command line），也称为 CLI, Terminal, bash, shell……我们中有很多人很怕使用它，但其实只要你知道一些基本的命令和概念，就没什么好怕的了。（文中接下来的内容，命令行统一用 CLI 称呼）


<!--more-->

## 什么时候需要用到 CLI？

80 年代那种只能用命令行来控制电脑运行的时代早已成为历史，现在的操作系统基本都已图形界面化，虽然有些地方还是不可避免的要用到它。那我们今天就来看一下，有哪些地方需要用到命令行呢？

- 远程服务（不止于 FTP 文件上传下载）
- 现代编程框架（如 Ruby on Rails）
- 像 Git/Subversion 一类的版本控制系统（在没有一个优秀的 GUI 解决方案的情况下）

这些是最常用到的。不过今天的重点是初步学习。

## 开始

Mac 下可以使用 `Terminal.app`

![clipboard.png](/img/bVkAYc)

Windows 下可以按 <kbd>win</kbd> + <kbd>R</kbd>，输入 cmd 打开命令行工具，或者使用 Git Bash

![clipboard.png](/img/bVkAYg)

## 基本的认知

CLI 无非几个步骤：

1. 输入一个命令
2. 添加一些参数
3. 按回车键确认

大多数命令只对你当前的目录（location）有效，因此，第一个要知道的命令就是帮助我们找到“现在在哪里”：

![clipboard.png](/img/bVkBpB)

`pwd` 代表 `__p__rint __w__orking __d__irectory`：返回结果为“显示当前正在进行工作的目录”。

`cd` 代表 `__c__hange __d__irectory`：返回结果为“改变当前工作目录”。下图是进入当前目录下的一个子目录：

![clipboard.png](/img/bVkBpW)

`..`：返回上一级目录（当前目录的父目录）

![clipboard.png](/img/bVkBpY)


`~` 是一种特殊的路径符号，代表着当前用户的“home”文件夹，故此有两种方法可以到你的 home 文件夹：

 1. 提供完整的路径：

    ```
    $ cd /Users/<your-username>/projects/
    ```
   
    或用：
   
    ```
    $ cd ~/projects/
    ```

    2. 另一个重要的命令 `ls`，用于列出当前目录或指定目录的内容：
   
        ```
        $ ls path/to/folder
        ```
   
    这个命令的两个重要的可选参数：

    * `-l`：输出一个附加信息的列表。
    * `-a` 标志：把隐藏的文件（夹）也显示出来，这个在如使用版本控制等很多情况下都很有用。  

结合一下，你可以在当前目录下这样使用：

![clipboard.png](/img/bVkBqo)

或者在别的路径下调用：

    $ ls -la path/to/folder

## 文件（夹）相关的命令

### 删除

删除文件：

```
$ rm path/to/file.ext
```

删除文件夹要加上`-r`（recursive），这样就会把目录里的所有内容都删除：

```
$ rm -r path/to/folder
```

### 移动

例子：

```
$ mv path/to/file.ext different/path/file.ext
```

这个命令也能用来给文件重命名：

```
$ mv old-filename.ext new-filename.ext
```

### 复制

使用 `cp` 命令，用法同 `mv`

### 新建

使用 `mkdir`（make directory）：

```
$ mkdir new-folder
```

## 输出

命令行还可以用来显示文件的内容。虽然使用编辑器来执行这一任务会更优雅，但有在有些情况下使用命令行反倒会方便一些。比如，当你只是想快速浏览一下，或因为是远程服务（这样图形界面操作的方式行不通），使用命令行就会变得很便捷：

使用 `cat` 命令会输出一个完整的文件内容

![clipboard.png](/img/bVkBsy)

`head` 和 `tail` 命令非常相似，分别是只显示前 10 行、后 10 行内容。


需要注意的是，`less` 命令有所不同：它虽然也用于显示输出，但它可以控制页面流程本身，也就是它只显示一个页面的内容，然后只能等待下一步指示。屏幕的最后一行显示的是当前文件名或只是一个等待接收命令的冒号 `:`，这时候按空格键将向前翻一页，按 <kbd>b</kbd> 键将后退一页，按 <kbd>q</kbd> 将退出 `less` 命令。

## <kbd>CTRL</kbd> 键的使用

* <kbd>CTRL</kbd> + <kbd>A</kbd>：光标移到行首
* <kbd>CTRL</kbd> + <kbd>E</kbd>：光标移到行末
* <kbd>CTRL</kbd> + <kbd>C</kbd>：终止当前运行的命令

## 用 <kbd>TAB</kbd> 键完成内容自动补充

输入文件名和路径的时候很容易出错，这时候就需要 <kbd>TAB</kbd> 键来帮你自动完成所写的内容。

例如当你想切换到一个别的目录，你可以手动输入每一个部分的路径：

```
$ cd ~/design/favorite-customer/mockups/
```

或者使用 <kbd>TAB</kbd> 键快速完成：

![clipboard.png](/img/bVkBuy)

你输入的字符不是每次都是明确的——因为“de”也可以是文件夹中“development”或“dentist”，在这种情况下 TAB 键不能自动补充你的输入，但它会有一个可能选项的列表，然后自动补全一些文字让你输入地更明确些。

## 用方向键查看历史命令

CLI 会像浏览器一样记录你最近的命令历史，所以：

* 向上键 <kbd>↑</kbd> 翻向更早的记录
* 向下键 <kbd>↓</kbd> 翻向更近期的记录

![clipboard.png](/img/bVkBuU)

## CLI 的替代品

现在有很多图形界面工具可以让你脱离 CLI，如 FTP 的客户端 [Transmit][2] ，版本控制器客户端 [Tower][3]。但不可否认，CLI 在某些情况下仍然是最好的选择。


> 原文 [Lose Fear of the Command Line][4]

> 本文是我为 [SegmentFault][5] 所译

  [1]: /img/bVkFgM
  [2]: http://panic.com/transmit/
  [3]: http://www.git-tower.com/
  [4]: http://designmodo.com/command-line/#
  [5]: http://segmentfault.com/blog/news/1190000002505102
