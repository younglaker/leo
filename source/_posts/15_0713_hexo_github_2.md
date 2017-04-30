---
layout: post
title:  Hexo3+Github搭建免费博客（二）自定义主题
date:   2015-07-13 08:24:00
category: [Hexo]
tags: [Hexo]
---

## 更换主题

找一个你喜欢的主题，`clone`到`theme`文件夹，例如[官网推荐的一些][1]。

执行如下命令

    git clone https://<git/repository> themes/<themename>

将`_config.yml`文件中的`theme`字段设置为与` <themename>`一致

    # Extensions
    theme: [themename]

很简单地就替换了。但是不同主题会有不同的差异，还要手动修改。例如默认主题没有`categories`、`tags`、`about`页面，要自己建立。具体可以看你所用的的主题的指南。

如果主题没有这些页面，自己又需要，可以自己写一个。

<!--more-->

## 自定义页面

例如做一个tags页面：

    hexo new page tags

这样就会在`source`文件夹下面建一个`tags`文件夹，里面有个`index.md`，就是要显示的模板。你还得在主题的`layout`文件夹里加一个`tags.ejs`布局。

在文章头部加上category、tags：

    ---
    layout: post
    title:  
    date:   
    category: HTML5
    ---

如果有多个标签的话，可以用下面两种办法来设置：

    tages: [标签1,标签2,...标签n]

或

     tages: 
    - 标签1
    - 标签2
    ...
    - 标签n

从`category`和`tages`单词单复数就可以看出，一篇文章不支持多个一级分类。如果你这样写：

    category: [CSS3,HTML5]

就会变成CSS3是一级分类，HTML5是它的二级分类。为什么不能支持多个一级分类，[作者是这样解释的][2]。对于不用标签的我，这个真不好用。


[问一个关于categories和tags的问题][3]

## 首页文章列表显示摘要

hexo2可以在配置文件里设置`archive: 2`，但是我试了不起作用。[作者是这么说的][4]，让大家自行在文章里添加`<!-- more -->`，这个标记上面的就是摘要。

## 导航菜单

默认的导航菜单只有Home和Archives两项，那么我们怎么来增加其他的导航菜单进去呢？
首先打开主题的配置文件_config.yml：

    menu:
      Home: /
      Archives: /archives
      About: /about

`menu:`部分是设置菜单的，在下面加了一项设置About: /about
想上面说的标签页、分类页一样，前面部分是名称，后面部分是访问路径，名称的可以用中文,访问路径也可以直接设置到其他站点的任何页面。

下面我们来建立这个about，运行命令：

    hexo n page 'about'

会在source目录里生成一个对应的about目录，该目录下的index.md，就是你访问About时的页面。可以自行修改内容。





  [1]: https://hexo.io/themes/
  [2]: https://github.com/hexojs/hexo/issues/419#issuecomment-31712933
  [3]: https://github.com/iissnan/hexo-theme-next/issues/51
  [4]: https://github.com/litten/hexo-theme-yilia/issues/44#issuecomment-88369280
