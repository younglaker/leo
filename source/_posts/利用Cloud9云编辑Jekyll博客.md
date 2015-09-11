---
layout: post
title:  利用 Cloud9 云编辑 Jekyll 博客
date:   2015-08-28 08:24:00
category: [Jekyll]
---

之前一直使用Jekyll，但是换电脑安装环境觉得很麻烦，尤其是ruby被墙，用 gem 安装Jekyll时候很难安，要换成[淘宝的镜像][1]。后来换成Hexo，但是需要在本地编译上传。试过Koding搭了个在线虚拟机，在线编译后上传。但是感觉还是麻烦，不如Jekyll可以直接上传Markdown文件，由Github直接编译部署的方便。想起以前用过的云编辑器Cloud 9，去看了下文档，支持安装Jekyll，ruby、git环境也已经准备好。试了一下，很快很方便。我的浏览器也有翻墙插件（Shadowsocks + SwitchyOmega），我之前也写过[相关教程][2]（2015-08-31更新：由于SS作者被约喝茶，免费服务网站也被墙，文章时效，已删除）

<!--more-->

##关于 Cloud 9

[管网][3]

Cloud9支持的程序语言有Node.js、HTML5、PHP、Python / Django、Ruby on Rails、C/C++、StrongLoop等，提供FTP、S-S-H和空间托管，有MysqL、MongoDB、SQLite数据库，可以一键安装Wordpress，也可以自己上传程序代码，支持协同编辑合作，另外可以和其它的云空间整合。

Cloud9支持将代码一键发布到Heroku、Windows Azure、Google App Engine、CloudFoundry等云空间上，还可以同步应用到Github空间上。

支持sublime风格，还有常用输入习惯配置“

![编辑器风格][4]

##新建工作空间
这里提供多种开发模板，我们此次选择Custom：

![预览][6]

## 安装Jekyll

打开terminal（快捷键alt+t，或者菜单---window---newterminal），输入：

    gem install jekyll

测试安装是否成功
    
    jekyll

按照官方的教程，这样就安装好了。但是我运行后报错，问题是coffeescript没有安装。

    /usr/local/rvm/gems/ruby-2.2.1@global/gems/bundler-1.8.4/lib/bundler/spec_set.rb:92:in `block in materialize': Could not find coffee-script-source-1.9.1 in any of the sources (Bundler::GemNotFound)

为了以后方便，安装全局的coffee：

    npm install -g coffee-script

测试coffee：

    coffee

coffee安装好之后就可以运行Jekyll了。

新建项目：

    jekyll new my-awesome-site
    cd my-awesome-site
    jekyll serve --host 0.0.0.0 --port 8080

访问地址`https://项目名-用户名.c9.io`，例如我的是` https://blog-younglaker.c9.io`

![预览][5]

##使用博客模板

Cloud 9已结安装好Git，可以直接用。找到你喜欢的博客模板的Github地址，clone下来即可：

    git clone 项目地址

  [1]: http://ruby.taobao.org/
  [2]: http://laker.me/blog/2015/08/24/Shadowsocks%E7%BF%BB%E5%A2%99/
  [3]: https://c9.io
  [4]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150828135504.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [5]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150828140858.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [6]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150828141700.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5