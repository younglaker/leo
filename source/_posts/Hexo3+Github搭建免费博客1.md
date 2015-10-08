---
layout: post
title:  Hexo3+Github搭建免费博客（一）基本安装
date:   2015-07-10 08:24:00
category: [Hexo]
comments: true
---
前两天有朋友要和我交换博客友情链接，原本博客使用jekyll，换了电脑，要重新配置，有些依赖被墙，各种问题，折腾了一天才弄好。昨天想给博客换皮肤，看到Hexo和jekyll的比较，都说jekyll太重，hexo轻巧很多，所以决定尝试一下。虽然用了很久的jekyll，想自己做主题，但文件太多，搞不清楚哪跟哪。现在换了hexo，简洁明了，真的很容易上手。而且是台湾同胞写的，遇到问题交流起来没那么困难。现在项目还在不断更新中。

> 网络上很多老文章是hexo2的教程，与hexo3有所差异。本文记录hexo3的。

<!--more-->

## 了解Hexo
[官网][1] | [Github][2]
A fast, simple & powerful blog framework。
快速、简洁且高效的博客框架。

* 超快速度
Node.js 所带来的超快生成速度，让上百个页面在几秒内瞬间完成渲染。

* 支持 Markdown
Hexo 支持 GitHub Flavored Markdown 的所有功能，甚至可以整合 Octopress 的大多数插件。

* 一键部署
只需一条指令即可部署到 GitHub Pages, Heroku 或其他网站。

* 丰富的插件
Hexo 拥有强大的插件系统，安装插件可以让 Hexo 支持 Jade, CoffeeScript。

## 安装Hexo
别看官网就几句简单命令，它省略了很多步骤。因为Hexo3把很多依赖独立出来了，所以要手动安装。

### 先安装Nodejs

到[官网][3]下载安装适合你电脑的版本，我现在用的iwn7 64bit。

也可以用nvm下载。

cURL:

    $ curl https://raw.github.com/creationix/nvm/master/install.sh | sh
    
Wget:

    $ wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh

安装完成后，重启终端并执行下列命令即可安装 Node.js。

    $ nvm install 0.10

###安装git

Windows：下载并安装 [git][4].
Mac：使用 [Homebrew][5], [MacPorts][6] 或下载 [安装程序][7] 安装。
Linux (Ubuntu, Debian)：sudo apt-get install git-core
Linux (Fedora, Red Hat, CentOS)：sudo yum install git-core

###安装 hexo-cli
这是最基本的hexo

    npm install hexo-cli -g

>Mac 用户在编译时可能会遇到问题，请先到 App Store 安装 Xcode，Xcode 完成后，启动并进入 Preferences -> Download -> Command Line Tools -> Install 安装命令行工具。

### 安装各种依赖
**切换到项目目录安装依赖**（我第一次尝试的时候没有切换的项目文件夹，所以一直运行不了，切记！这使得项目多了就很麻烦），复制下面命令安装吧。不懂为什么要独立这几个出来，都是必须的。

###安装生成器
这些用于生成博客目录，hexo文件很多，但是有个叫public的，这才是要上传到github的，也就是generator生成的。

	npm install hexo-generator-index --save
	npm install hexo-generator-archive --save
	npm install hexo-generator-category --save
	npm install hexo-generator-tag --save

###安装hexo-server
本地运行必须

	npm install hexo-server --save

###安装发布器
发布到远程服务要用的，如果只要托管到github，所以必须装git，其他可以不装。

	npm install hexo-deployer-git --save
	npm install hexo-deployer-heroku --save
	npm install hexo-deployer-rsync --save
	npm install hexo-deployer-openshift --save

###安装依赖

    npm install

> 注意：之后带有--save选项和npm install命令必须在之前初始化的博客目录下运行

##建立github项目
>我看很多教程没有这一步，不知道是不是必须的，因为我觉得这样是开启pages服务，github才给出一个访问地址，为了保险就做了

先到github建一个项目，假设项目名`blog`，地址`https://github.com/younglaker/blog.git`

到setting里开启github pages

![clipboard.png](http://segmentfault.com/img/bVmD55)

一直下一步就建好了。设置`gh-pages`为默认分支：


![clipboard.png](http://segmentfault.com/img/bVmD6x)


克隆到本地一个文件夹：

     git clone https://github.com/younglaker/blog.git

把里面的内容都删掉，待会创建hexo博客

##本地部署

cd到项目文件夹

    hexo init


###目录介绍


    ├── .deploy_git 执行hexo deploy命令部署到GitHub上的内容目录
    ├── public 执行hexo generate命令，输出的静态网页内容目录
    ├── scaffolds 模板
    ├── scripts 扩展hexo功能的js
    ├── source 存放博客内容，正文、404、favicon.ico，CNAME、tags等都应该放这里，该目录下可新建页面目录。
    |   ├── _drafts 草稿箱
    |   └── _posts 文件箱，写的md文章就放这里
    ├── themes 存放皮肤，要换皮肤都下载到这里
    ├── _config.yml 全局的配置文件，后面会讲到如何配置
    └── db.json 静态常量


### 配置`_config.yml`

大多数使用默认配置，有些可选，有些必改。

**博客信息：**

    # Site
    title: Laker's blog
    subtitle: 进击的程序媛
    description: 前端
    author: John Doe
    email: younglaker8@gmail.com
    language: zh-CN
    timezone:

**博客和文章地址：**

    # URL
    ## 如果网站是放在二级目录，URL设为 'http://yoursite.com/child'，根目录设为 '/child/'
    url: http://laker.me/blog
    root: /blog/ # 二级目录
    permalink: :year/:month/:day/:title/ # 文章地址的形式

**博客每页显示文章数：**

    # Pagination
    per_page: 10
    pagination_dir: page

**部署的地址：**

执行`hexo d`时候上传的远端地址

    # Deployment
    deploy:
      type: git #不要写github,写git
      repo: https://github.com/younglaker/blog.git
      branch: gh-pages

注意：  
1、
> [升级到hexo 3.0后deploy type: github选项无效][8]

2、
> deploy 报错 ：fatal: could not read Username for 'https://github.com': Invalid argument

如果按照github设置username没有问题，那就把部署地址改为SSH形式：

    deploy:
      type: git
      repo: git@github.com:younglaker/blog.git
      branch: gh-pages

参考： 
[Error when push commits with Github: fatal: could not read Username][9]
[Github configuration question / problem][10]
[sublime-text-git，fatal: could not read Username for 'https://github.com': Device not configured ][11]
[Git push requires username and password][12]

###生成静态页面

    hexo generate
    
或
    
    hexo g

就会根据`source`文件夹的内容生成`public`文件夹，把md文章转换成html。`public`文件夹也就是要上传到github的东西，其他都会被ignore，所以在Github上看是很简洁的，这点比 jekyll 好。

###打开服务

    hexo server
    
或

    hexo s

浏览器访问 http://localhost:4000 就可以看到效果。

![图片描述][13]

###上传到github

    hexo deploy

或

    hexo d


hexo就会帮你完成上传工作，不用自己执行add、commit、push等一系列繁琐的工作。但是也有不好的地方，就是不能给提交进行注释，默认是上传时间。

![clipboard.png](http://segmentfault.com/img/bVmEPz)

可以到配置修改，增添`message`，但不能做到在命令行里自定义。如果每次提交都到这里修改，也挺麻烦的：

    deploy:
      type: git
      repo: <repository url>
      branch: [branch]
      message: [message]

这篇介绍了基本的使用，下篇介绍自定义~(*^__^*) 


  [1]: https://hexo.io/
  [2]: https://github.com/hexojs/hexo
  [3]: https://nodejs.org/
  [4]: https://git-scm.com/download/win
  [5]: http://mxcl.github.com/homebrew/
  [6]: http://www.macports.org/
  [7]: http://sourceforge.net/projects/git-osx-installer/
  [8]: https://github.com/hexojs/hexo/issues/1013
  [9]: http://stackoverflow.com/questions/20871549/error-when-push-commits-with-github-fatal-could-not-read-username
  [10]: https://github.com/hexojs/hexo/issues/857
  [11]: https://github.com/kemayo/sublime-text-git/issues/176
  [12]: http://stackoverflow.com/questions/6565357/git-push-requires-username-and-password
  [13]: http://segmentfault.com/img/bVmEEP