---
layout: post
title:  Hexo3+Github搭建免费博客（三）评论/分享/统计
date:   2015-07-15 08:24:00
category: [Hexo]
comments: true
---

## 增加第三方评论工具
### 友言
据说多说问题很多，从hexo2升级到hexo3无法同步评论，界面也不好看，所以选了友言。

在`_config.yml`里添加：

    #友言
    uyan:
      enable: true

<!--more-->

到[友言网站][5]注册账号，获取你的uid。把下面的代码复制粘贴到`themes\*\layout\_partial\article.ejs`

    <% if (config.uyan.enable && page.comments){ %>
    
    <section id="comment">
      <h1 class="title"><%= __('comment') %></h1>
      <div id="disqus_thread">
        <!-- UY BEGIN -->
        <div id="uyan_frame"></div>
        <script type="text/javascript" src="http://v2.uyan.cc/code/uyan.js?uid=你的uid"></script>
        <!-- UY END -->
      </div>
    </section>
    
    <% } %>

本地无法看到，上传到github就可以看了。

![clipboard.png](http://segmentfault.com/img/bVmGA7)

### Disqus

到[官网][5]注册账号。右上角`admin`

![clipboard.png](http://segmentfault.com/img/bVmHlM)

填写信息

![clipboard.png](http://segmentfault.com/img/bVmHlP)

这里就是复制评论脚本的地方：

![clipboard.png](http://segmentfault.com/img/bVmHlR)

hexo已经帮写好Disqus代码，只需要在`_config.yml`填上以下代码。

    # disqus
    disqus_shortname: laker
    
进入profile，这个就是`shortname`

![clipboard.png](http://segmentfault.com/img/bVmHlw)

上传到github就可以看了：

![clipboard.png](http://segmentfault.com/img/bVmHol)

## 加入右上角「fork me on github」
这里有 [github](https://github.com/blog/273-github-ribbons) 给出的各种样式，把代码插入到任意一个全局的模板文件中就行，比如`layout.ejs`的末尾。例如

    <a href="https://github.com/你的github名称"><img style="position: absolute; top: 0; right: 0; border: 0;" src="https://camo.githubusercontent.com/a6677b08c955af8400f44c6298f40e7d19cc5b2d/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f6769746875622f726962626f6e732f666f726b6d655f72696768745f677261795f3664366436642e706e67" alt="Fork me on GitHub" data-canonical-src="https://s3.amazonaws.com/github/ribbons/forkme_right_gray_6d6d6d.png"></a>


![clipboard.png](http://segmentfault.com/img/bVmHmB)


  [5]: https://disqus.com