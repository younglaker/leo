---
layout: post
title:  Hexo3+Github搭建免费博客（四）SEO、统计
date:   2015-07-16 08:24:00
category: [Hexo]
---

##提交搜索引擎

###Google
[Google搜索引擎提交入口][1]

Google提供了详细的说明，推荐的方法是HTML文件上传：

    下载此 HTML 验证文件。 [************.html]
    将该文件上传到 http://yoursite/
    通过在浏览器中访问 http://yoursite/************.html ，确认上传成功。
    点击下面的“验证”。
    为保持已进行过验证的状态，即使成功通过了验证也请不要删除该 HTML 文件。

<!--more-->

hexo会在部署的时候编译这个文件，所以我们要阻止编译，在文件开头添加layout: false来取消hexo对其进行的转换，如下：

    $ ls source/
    404.html    _posts    ************.html
    CNAME    aboutme.md
    $ cat source/************.html
    layout: false
    ---
    google-site-verification: ************.html

也可以使用添加`<meta>`标签的方式，这个比较快捷。

> 注意，假设用的是`http://yoursite/blog`，验证的也是`http://yoursite/blog`


###百度

[百度搜索引擎入口][2]

方法类似谷歌。

> 注意，假设用的是`http://yoursite/blog`，但验证的是`http://yoursite/`，验证主域名

##统计

因Google Analytics偶尔被墙，故用百度统计。编辑文件`_config.yml`，增加配置选项：

    baidu_tongji: true

注册并登录[百度统计][3]获取你的统计代码。新建文件hexo\themes\**\layout\_partial\baidu_tongji.ejs，内容如下：

    <% if (theme.baidu_tongji){ %>
        #你的百度统计代码
    <% } %>
    

编辑文件`hexo\themes\**\layout\_partial\head.ejs`，在`</head>`之前增加：

    <%- partial('baidu_tongji') %>


  [1]: https://www.google.com/webmasters/tools/home?hl=zh-CN
  [2]: http://www.baidu.com/search/url_submit.htm
  [3]: http://tongji.baidu.com