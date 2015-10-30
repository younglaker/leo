---
layout: post
title:  Web开发利器推荐（五）
date:   2015-03-20 12:55:11
category: [翻译,工具]
---

##StackEdit

它是一款很棒的`Markdown`编辑器。 基于`PageDown`开发而来，已经被 `Stack Overflow` 和其他 `Stack Exchange` 站点使用。 

StackEdit 能实时预览文档，保存到云端或本地的local storage，导出 Markdown、HTML 或 PDF 格式，与GitHub、Gist、Google Drive、 Dropbox 或者任何 SSH 服务器。 

![clipboard.png](http://segmentfault.com/img/bVk69a)

还有其他功能： 支持`LaTeX`、所见即所得、在线/离线模式、`Prettify/Highlight.js`语法高亮、支持扩展。

<!--more-->

##App.io - 在浏览器中运行移动app

![clipboard.png](http://segmentfault.com/img/bVk69c)

##IM Creator

![clipboard.png](http://segmentfault.com/img/bVk69d)

在之前的文章中介绍了 Webflow。 现在我想介绍另一个创建响应式网站的GUI工具。 主要的区别是它有更多的主题。

##Autoprefixer

解析CSS和并根据 [Can I Use][1] 添加CSS厂商前缀。

这样你写CSS的时候就可以不用考虑CSS厂商前缀（完全忘记了它们吧）：

    :fullscreen a {
        transition: transform 1s;
    }

Autoprefixer 将根据当前浏览器的流行度和支持度提供合适的前缀。 来尝试一下 Autoprefixer 的[演示][2]。

    :-webkit-full-screen a {
        -webkit-transition: -webkit-transform 1s;
                transition: transform 1s;
    }
    :-moz-full-screen a {
        transition: transform 1s;
    }
    :-ms-fullscreen a {
        transition: transform 1s;
    }
    :fullscreen a {
        -webkit-transition: -webkit-transform 1s;
                transition: transform 1s;
    }

##Keypress.js

![clipboard.png](http://segmentfault.com/img/bVk69i)

这是最佳的捕捉键盘输入的解决方案：

    keypress.combo("shift s", function() {  
        console.log("You pressed shift and s");
    });
    
    // There are also a few other shortcut methods:
    
    // If we want to register a counting combo
    keypress.counting_combo("tab space", function(e, count) {  
        console.log("You've pressed this " + count + " times.");
    });

它有许多事件和组合的变化：

    keypress.register_combo({  
        "keys"              : null,
        "on_keydown"        : null,
        "on_keyup"          : null,
        "on_release"        : null,
        "this"              : window,
        "prevent_default"   : false,
        "prevent_repeat"    : false,
        "is_ordered"        : false,
        "is_counting"       : false,
        "is_sequence"       : false,
        "is_exclusive"      : false
        "is_solitary"       : false
    });

##Dropzone.js

![clipboard.png](http://segmentfault.com/img/bVk69l)

这是个很好的拖拽上传文件的脚本。 支持Chrome 7+、Firefox 4+、IE 10+、Opera 12+、 Safari 6+。它的使用很简单：

插入脚本（还提供一个Requirejs AMD 模块）：

    <script src="./path/to/dropzone.js"></script>  
    <form id="my-awesome-dropzone" action="/target" class="dropzone"></form>  
    
这样就好了。 真的！ 你也可以用JS代码：

    // Dropzone class:
    var myDropzone = new Dropzone("div#myId", { url: "/file/post"});
    
    // jQuery plugin
    $("div#myId").dropzone({ url: "/file/post" });

##其他

[花10美元你就可以在 Sublime 里用 Git][3]  ：


![clipboard.png](http://segmentfault.com/img/bVk69p)

[Odometr][4] —— 创建优雅的计数器

![clipboard.png](http://segmentfault.com/img/bVk68T)

[PreRender][5] —— 把JavaScript生成的页面渲染为有更好SEO的HTML。

![clipboard.png](http://segmentfault.com/img/bVk68U)

[Source][6]  —— 前端文档引擎。

![clipboard.png](http://segmentfault.com/img/bVk68V)


CSS Tricks 的一个创新 —— [Conical Gradients in CSS][7]。

![clipboard.png](http://segmentfault.com/img/bVk68W)

欧洲核子研究中心展示了原始的上网浪形式，创建了 [Line Mode Browser][8]。

![clipboard.png](http://segmentfault.com/img/bVk680)

一个不同寻常的网站 —— [Fontwalk][9]，全站应用了视差效果。

![clipboard.png](http://segmentfault.com/img/bVk68Y)

> 英文原文：[Awesomeness & Usefulness for Web Developers #5][10]

> 本文是我为[SegmentFault][11]所译


  [1]: http://caniuse.com/
  [2]: http://simevidas.jsbin.com/gufoko/quiet
  [3]: https://sublimegit.net/
  [4]: http://github.hubspot.com/odometer/
  [5]: https://github.com/prerender/prerender
  [6]: http://sourcejs.com/
  [7]: http://css-tricks.com/conical-gradients-css/
  [8]: http://line-mode.cern.ch/
  [9]: http://www.fontwalk.de/
  [10]: http://ipestov.com/awesomeness-and-usefulness-for-web-developers-5/
  [11]: http://segmentfault.com/blog/news/1190000002610048