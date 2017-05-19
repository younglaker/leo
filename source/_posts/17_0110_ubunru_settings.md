---
layout: post
title:    我的 Ubuntu 配置记录
date:   2017-01-10 08:24:00
category: [Ubutntu]
tags: [Ubutntu]
---

![The cover][1]
重新装了系统，又得花老大劲配置环境，好多东西不记得了，只能看笔记和Google，但是比较琐碎，效率还是比较低。索性记录一下我的配置过程，以便今后再配环境时能快速一些。

<!--more-->

## Ubuntu更换源
更换网易或阿里源
![更换网易或阿里源][2]

## Ubuntu安装Python
自带

## Chrome
由于需要翻墙，先在windows下载好linux版本，上传到百度云或U盘，再到Ubuntu系统里安装。

**下载安装包方式**

到这个地址下载 https://www.google.com/intl/zh-CN/chrome/browser/?standalone=1 下载deb文件

## Ubuntu科学上网

### 浏览器插件
上传omega及其配置到百度云或U盘，再到Ubuntu系统里安装。

### Ubuntu安装ss
安装的命令：

然后安装 PIP

    apt-get install python-gevent python-pip

安装 ss

    pip install shadowsocks

为了支持加密方式，需要安装

    apt-get install python-m2crypto

运行：

    sslocal -s 地址 -p 端口 -k 密码 -m 加密方式

## Sublime

安装插件前按Ctrl+` 调出console输入

```
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
```

## Ubuntu安装Git
安装

    apt-get install git

配置Github：
```
$ git config --global user.name "用户名"
$ git config --global user.email 邮箱
$ ssh-keygen -t rsa -b 4096 -C "邮箱"
$ ssh-add ~/.ssh/id_rsa
```
把在~/.ssh（根目录下按 ctrl + H 显示隐藏文件）ssh-key 添加到 Github 设置里

## Ubuntu安装Nodejs

安装NVM，重启terminal:

    wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash

安装Nodejs 6.10.3，含npm，可换其他版本

    nvm install 6.10.3
    node -v

切换Nodejs版本

    nvm use 6.10.3（版本号）

## Ubuntu安装cnpm

https://npm.taobao.org

    npm install -g cnpm --registry=https://registry.npm.taobao.org
    cnpm install [name]

## Ubuntu安装Bower

    npm install bower -g
    bower -v

## Ubuntu安装Ruby
含gem

    sudo apt-get install ruby 2.4 （最新版本号可在官网查）

移除默认的https://rubygems.org源：

    gem source --remove https://rubygems.org/

然后添加淘宝的源https://ruby.taobao.org/:

    gem source -a https://ruby.taobao.org/

确保只有 ruby.taobao.org

    gem sources -l
	*** CURRENT SOURCES ***
	https://ruby.taobao.org

## Ubuntu安装Sass

    gem install sass

## Ubuntu安装CoffeeScript


## Ubuntu安装Gulp

    npm install --global gulp

## Ubuntu安装Vim

    sudo apt-get install vim

## Ubuntu安装Vue.js

    npm install vue -g

或用Bower：

    bower install vue

或安装命令行工具：

    # 全局安装 vue-cli
    $ npm install --global vue-cli
    # 创建一个基于 webpack 模板的新项目
    $ vue init webpack my-project
    # 安装依赖，走你
    $ cd my-project
    $ npm install
    $ npm run dev


## bootstrap

    bower init
    bower install bootstrap#3.3.7 --save

  [1]: http://77g54f.com1.z0.glb.clouddn.com/bgt-20170110.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/South/dy/5
  [2]: http://77g54f.com1.z0.glb.clouddn.com/QQ20170105162824.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/South/dy/5