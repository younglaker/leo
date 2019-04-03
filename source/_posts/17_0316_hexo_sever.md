---
layout: post
title:   Hexo server not working；Hexo 无法访问页面
date:   2017-03-16 08:24:00
category: [Hexo]
tags: [Hexo]
---

<!-- ![Hexo server not working][1] -->

<!--more-->

> 欢迎交换友链： [Laker's Blog--进击的程序媛](http://laker.me/blog)
> Github：[https://github.com/younglaker](https://github.com/younglaker)
> V信: lakerHQ （请注明‘来自博客’）

---
If you can run `hexo s` perfectly, but can't vist the local page at `http://localhost:4000/blog/`. May you can try another port like 5000:

```
$ hexo server -p 5000
INFO  Start processing
INFO  Hexo is running at http://0.0.0.0:5000/blog/. Press Ctrl+C to stop.
```

Then visit `http://localhost:5000/blog/` or `http://127.0.0.1:4000/blog/`. If it works, congratulations.

You can add this configuration to the file `_config.yml` at root:

```
server:
  port: 5000 # or anohter number
  log: false
  ip: 0.0.0.0
  compress: false
  header: true
```

Run, then ok：
```
$ hexo s
INFO  Start processing
INFO  Hexo is running at http://0.0.0.0:5000/blog/. Press Ctrl+C to stop.
```

---

早在15年建了这个Hexo的blog，不知从什么时候起，Hexo server 就不能运行了，当时因为样式已经稳定，直接写好文章、编译、就发布了，就没有处理这个问题。最近升级了 Nodejs，有些依赖报错，只能从新安装。又由于代码库出现问题，发布的 blog 布局出错，要调整样式必须在本地调。

我重新 init 了一个 blog，`hexo s` 能正常运行没有报错，但是无法访问 `http://localhost:4000/blog/` 。

经过查找资料发现，是因为 4000 端口被福昕阅读器占用，换个端口就好了。

```
$ hexo server -p 5000
INFO  Start processing
INFO  Hexo is running at http://0.0.0.0:5000/blog/. Press Ctrl+C to stop.
```

此时就可以通过 `http://localhost:5000/blog/` 或 `http://127.0.0.1:4000/blog/` 访问。

> 如果直接复制官网的命令，会报错
```
$ hexo s -p 5000
bash: $'\302\226hexo': command not found
```
> 因为空格符编码问题，手动输入一遍是没有问题的
> [参考][2]

但是以上命令只能一次性使用，下次还会恢复成4000，要在根目录下`_config.yml`里配置一下：
[hexo-server][3]
```
server:
  port: 5000
  log: false
  ip: 0.0.0.0
  compress: false
  header: true
```

运行即可：

```
$ hexo s
INFO  Start processing
INFO  Hexo is running at http://0.0.0.0:5000/blog/. Press Ctrl+C to stop.
```

## 127.0.0.1, 0.0.0.0, localhost 的区别

- 127.0.0.1是一个回送地址，指本地机，一般用来测试使用。
- localhost 是 127.0.0.1 的别名，可以改成别的。win7下可以到
`C:\Windows\System32\drivers\etc\hosts`里修改。
- 0.0.0.0 表示无路由目标，主机可能有多个ip地址， 0.0.0.0 指向本机所有ip地址

[参考][4]

  [1]: http://77g54f.com1.z0.glb.clouddn.com/bgt-20170316.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [2]: http://superuser.com/questions/670867/why-do-i-sometimes-get-sh-302-211-command-not-found-in-xterm-sh/1123368#1123368
  [3]: https://github.com/hexojs/hexo-server
  [4]: https://www.howtogeek.com/225487/what-is-the-difference-between-127.0.0.1-and-0.0.0.0/


