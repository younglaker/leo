---
layout: post
title:   sublime text 3 注释的快捷键失效
date:   2017-03-09 08:24:00
category: [Sublime]
tags: [Sublime]
---

![title][1]

<!--more-->

> 欢迎交换友链： [Laker's Blog--进击的程序媛](http://laker.me/blog)
> Github：[https://github.com/younglaker](https://github.com/younglaker)
> V信: lakerHQ （请注明‘来自博客’）

---

最近新装了一个ubuntu虚拟机，装了最新的sublime 3，发现注释的快捷键用不了，大大降低了效率，之前在双系统下没有这样的情况，上网搜了一下，根据StackOverflow里的讨论，说这是一个BUG。开发比较急，也没时间用旧版本覆盖在配置，所以找了下解决方案。

## 方法一
检查是否和系统、编辑器内部有快捷键冲突。

安装插件`keymap`，通过菜单`tool->keymap-find a key`，输入`comment`查看当前注释的快捷键是什么。

## 方法二

把如下代码添加到 `Preferences / Key Bindings - User`

```
{ "keys": ["control+keypad_divide"],"command": "toggle_comment", "args": {"block": false} },
{ "keys": ["shift+control+keypad_divide"],"command": "toggle_comment", "args": {"block": true}}
```

## 方法三

德式键盘的`/`在数字7下面，所以把如下代码添加到 `Preferences / Key Bindings - User`

```
{ "keys": ["ctrl+7"], "command": "toggle_comment", "args": { "block": false } },
{ "keys": ["ctrl+shift+7"], "command": "toggle_comment", "args": { "block": true } }
```

## 方法四

更换其他快捷键设置后还不起作用，可能是不识别ctrl键。
我平时习惯右边的 ctrl + / ，上面方法都不起作用，偶然一次发现左边 ctrl + / 才起作用。

## 方法五
用旧一点的版本覆盖，不过可能会丧失某些功能。

[StackOverflow 参考][2]


  [1]: http://77g54f.com1.z0.glb.clouddn.com/bgt-20170309.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [2]: http://stackoverflow.com/questions/17742781/keyboard-shortcut-to-comment-lines-in-sublime-text-3