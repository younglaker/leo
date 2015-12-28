---
layout: post
title:  Hexo3+Github搭建免费博客（四）SEO/统计/RSS
date:   2015-07-16 08:24:00
category: [Hexo]
---

## 提交搜索引擎

### Google
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


### 百度

[百度搜索引擎入口][2]

方法类似谷歌。

> 注意，假设用的是`http://yoursite/blog`，但验证的是`http://yoursite/`，验证主域名

## 统计

因Google Analytics偶尔被墙，故用百度统计。编辑文件`_config.yml`，增加配置选项：

    baidu_tongji: true

注册并登录[百度统计][3]获取你的统计代码。新建文件hexo\themes\**\layout\_partial\baidu_tongji.ejs，内容如下：

    <% if (theme.baidu_tongji){ %>
        #你的百度统计代码
    <% } %>
    

编辑文件`hexo\themes\**\layout\_partial\head.ejs`，在`</head>`之前增加：

    <%- partial('baidu_tongji') %>

## RSS
在根目录下安装`hexo-generator-feed`依赖：

    npm install hexo-generator-feed --save

本主题已经在`head.ejs`里定义了以下代码，使用其他主题的请看主题是如何定义的，或者也这样做：

    <% if (theme.rss){ %>
        <link rel="alternative" href="<%- theme.rss %>" title="<%= config.title %>" type="application/atom+xml">
    <% } %>

部署：
    
    hexo g

部署成功后会在source文件夹里出现`atom.xml`。

在`_config.yml`里：

    rss: true

    menu:
      Home: /blog
      Archives: archives
      Categories: categories
      Blogrolls: blogrolls
      About: about
      RSS: atom.xml #加上这个
      
就会在菜单上出现RSS的链接了。

> 2015-9-9 更新：

今天用freedly订阅博客RSS时，发现地址错误，检查了atom.xml文件，发现博客地址是`http://laker.me/blog/blog//`，而正确的应该是`http://laker.me/blog/`，估计是解析器的问题，因为在config文件里，要求url把子目录写上即`http://laker.me/blog/`，并填写子目录`/blog/`。到插件主页看了，最近有人也遇到这个问题，并进行了更新，但是好像全部换了写法，要升级有点麻烦，我就直接自己改了配置：

在`\node_modules\hexo-generator-feed\atom.ejs`里，把URL的定义（大约第三行：）

    <% var url = config.url + config.root %>

改为：

    <% var url = config.url + '/'%>

把大概第六行

    <link href="<%- encodeURI(feed_url) %>" rel="self"/>

最后的`/`删掉，因为和上面 url 的定义重复了：

    <link href="<%- encodeURI(feed_url) %>" rel="self">

重新编译后即可。

题外话，`feed_url`的定义在`\node_modules\hexo-generator-feed\lib\generator.js`里，有需要可以进行更改：

    var xml = template({
      config: config,
      posts: posts,
      feed_url: config.root + feedConfig.path
    });

  [1]: https://www.google.com/webmasters/tools/home?hl=zh-CN
  [2]: http://www.baidu.com/search/url_submit.htm
  [3]: http://tongji.baidu.com