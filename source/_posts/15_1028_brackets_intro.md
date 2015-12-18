---
layout: post
title:  为前端而生的编辑器Brackets及配置推荐
date:   2015-10-28 08:24:00
category: [Brackets]
tags: [Brackets,前端工具,开发工具,front-end]
---

##关于
Brackets 号称是懂web设计的开源编辑器。之所以这样说，是因为它是为前端工程师准备的，在前端开发方面做了很多特别设计。比如 可以在HTML里面直接跨文件编辑标签所涉及的CSS、PSD生成web文件、实时预览等。

该项目由Adobe创建和维护，并在[Github上开源][1]。

值得一提的是，该编辑器是用HTML/CSS/JavaScript开发的，所以很多前端工程师可以读懂并进行改进。

早在两年前刚起步时我就开始关注了，但鉴于功能还不完善、社区不够活跃，一直保持观望状态。最近重装电脑，索性把一直用的Sublime放到一边，试着用Brackets。

<!--more-->

## 初体验
用惯Sublime，初次使用Brackets的时候总会不自觉的进行比较。感觉Brackets更像干净的白纸，等着开发者去图画。Brackets要靠插件来完成Sublime很多基本功能。

下面先介绍Brackets特有的功能，再介绍插件和小技巧。

## 特别的功能

### 在HTML里编辑CSS
在HTML文件里，鼠标放到一个要编辑样式的标签上，快捷键`CTL + E`，就可以看到有个下拉编辑框，这里显示了与这个标签有关的样式，直接修改后，相应的样式文件也会改变。

可以看到，这个样式定义在`style.css`文件里，你还可以`new rule`新建样式。

![编辑CSS][2]

### 预览颜色
在样式文件里，鼠标放到一个颜色属性上，就可以预览颜色

![预览颜色][3]

### 用取色器编辑颜色

在颜色值上按`CTRL + E`，调出取色器进行编辑：

![用取色器编辑颜色][4]

### 文件地址提示
![文件地址提示][5]

###图片预览
HTML：

![图片预览][6]

Markdown：

![图片预览][7]

## 主题
###更换主题
在网上找的你喜欢的主题，我用的是一个基于 Sublime Monokai 的主题。GIthub 的地址是 `https://github.com/Brackets-Themes/Monokai`。

有几种方法添加：

- 通过URL
在右边工具栏找到一个望远镜的图标，点击`Install from URL`，粘贴地址上去安装。

![此处输入图片的描述][8]

- 上传压缩包

同样在上图的位置，拖拽zip文件即可

- 在线搜索

Brackets已经被墙，能用的几率很小。完全无法理解为什么编辑器网站都被墙  = =

- 复制到插件文件夹
从菜单`Help > Show Extensions Folder > User`中进入扩展文件夹，把压缩包解压到这里，或者 git clone 主题项目。重启编辑器即可。重启快捷键是 F5。


### 创建新主题

#### 创建主题文件
- 打开编辑器，从菜单`Help > Show Extensions Folder > User`中进入扩展文件夹
- 新建一个文件夹，起一个你喜欢的主题名字
- 在这个文件夹新增文件`package.json`、` theme.less`（CSS也行）

#### 修改package.json
按照以下模板填写，可以参考别人的主题的文件;

    {
        "name": "yourname.my-shiny-theme",
        "title": "My Shiny Theme",
        "description": "This theme is so shiny that you'll need to wear shades!",
        "homepage": "https://github.com/yourname/my-shiny-theme",
        "version": "1.0.0",
        "author": "Your Name <your@email> (http://your.url)",
        "license": "MIT",
        "theme": {
            "file": "theme.less",
            "dark": true,
            "addModeClass": true
        },
        "keywords": ["theme"]
    }

#### 添加主题

- 在编辑器菜单`View > Themes`里添加你的主题
- 编辑你的`theme.less`文件，保存后即可生效，在编辑器里看到效果

#### 开发

前面说到，Brackets是用HTML、CSS、JavaScript开发的，所以前端工程师能很轻易掌握开发这个编辑器的技能。

修改编辑器主题，就行开发网页一样。按F12就能看到Development Tool，是不是Chrome的开发者工具的既视感！是不是一下子就对Brackets有很强烈的归属感~

所以你可以审查元素，获得类名，然后到CSS/LESS文件里进行修改。

比如，我找到JS文件里`for`用到的class是`cm-keyword`，然后就可以在样式文件里修改。

![修改][9]

#### 为不同文件格式设置不同注释样式
在1.1版本之后，在主题` package.json` 文件里开启 `addModeClass` 模式，就可以这样为CSS的注释写样式：

    .cm-m-css.cm-tag {
        color: #6c9ef8;
    }

其他Common modes：

    .cm-m-clike: PHP
    .cm-m-css: CSS, LESS
    .cm-m-javascript: JavaScript
    .cm-m-xml: HTML, XML

#### 修改
比起从0开始，还是站在巨人的肩上比较好。这是我在主题上进行的修改：


    span.cm-builtin {  /*CSS id*/
        color: #FFFD83;
    }
    span.cm-header {  /*MD标题*/
        color: #53C0E0;
    }
    .cm-s-monokai-dark-soda .cm-tag {  /*CSS标签、MD图片标签*/
        color: #F5A14E;
    }
    .cm-s-monokai-dark-soda .cm-comment {  /*注释、MD文件的代码块*/
        color: #c7d4d6;
    }
    span.CodeMirror-matchingbracket {  /* 聚焦的括号 */
        color: #F5C04C !important;
        background-color: none; 
    }


[官方指南][10]

## 小技巧
### 自动补全反括号、引号
Sublime是默认开启这个功能，Brackets需要手动打开，刚开始还比较困惑，差点因为没找到这个小功能而放弃Brackets，因为实在容易出错。

开启菜单 `Edit--Auto Close Brace`

查找解决方案的时候，发现这个功能以前是默认开启的，后来取消了，感觉很不自在。我觉得大多数人都用过Sublime，它的一些好的做法应该保留，这样用户不会产生太大抵触心理。不过ST3也是把很多ST2默认开启的功能改为手动开启，也是烦。

### 修改文件树字体大小
习惯可能大字了。在Sublime是通过 User Setting 里添加 JSON 信息即可。

通过开发者工具，找到定义文件树的标签和样式定义，可以看到是在`style.css`文件里的`#project-files-container a` （注意，我安装的文件树的插件，所以和你所找到的会不一样）：

![样式定义][11]

点击`style.css`，进入开发者工具的 Source 面板，右键`Reveal in navigator`，可以看到文件所在目录。

![文件][12]

找到后打开编辑，保存重启即可。

![修改前][13]

![修改后][14]

## 后记

这仅仅是开始，下篇将介绍非常有用的Brackets插件，装完之后神清气爽~



  [1]: https://github.com/adobe/brackets
  [2]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150916165834.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [3]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150916170646.png
  [4]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150916170741.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [5]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150918090049.png
  [6]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150918090135.png
  [7]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150918090220.png
  [8]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150917144703.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [9]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150917141151.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [10]: https://github.com/adobe/brackets/wiki/Creating-Themes
  [11]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150917142550.png
  [12]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150917142659.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/South/dy/591ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/SouthEast/dx/5/dy/5
  [13]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150917143418.png
  [14]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150917143602.png