---
layout: post
title:  Web开发利器推荐（一）
date:   2015-03-11 08:24:00
category: [翻译,工具]
---

看到一个很棒的系列，介绍了很多对web开发很有帮助的利器，解决了很多开发中遇到的繁琐事，翻译来分享一下：

---

##[Prepros][1]

![clipboard.png](http://segmentfault.com/img/bVk15L)

这是很赞的预处理程序。 Prepros能编译很多种语言 (LESS, Sass, SCSS, Stylus, Jade, Slim, Coffeescript, LiveScript, Haml, Markdown)，实时压缩和连接JS，优化图片，当CSS或HTML变化时自动刷新浏览器，多设备测试。

所以你不用购买[Liverload][2] 和 [Ghostlab][3]，Prepros是[开源][4]、免费的。 类似的功能只能通过[Grunt][5]实现，但Prepros让事情变得简单。

<!--more-->

付费版本提供了 1-Click FTP/SFTP 部署、远程设备的检查和调试、其他有用的解决方案。

##[Brackets][6]

![clipboard.png](http://segmentfault.com/img/bVk15M)

Adobe团队用NodeJS为web程序员开发的开源编辑器。 它的界面有点像 Sublime Text，它有实时自动加载工具、插件系统、HTML/CSS/JS自动补全。 Brackets允许在HTML文档里编辑CSS，按下CMD/CTRL + E后，找到相应选择器。 里面还很多像CSS过渡编辑器这样的智能工具。

##[VerbalExpressions][7]

谁不爱写正则表达式？ 如果用VerbalExpressions写JavaScript进行URL检查的正则表达式可能会像这样：

    // Create an example of how to test for         correctly formed URLs
    var tester = VerEx()
            .startOfLine()
            .then( "http" )
            .maybe( "s" )
            .then( "://" )
            .maybe( "www." )
            .anythingBut( " " )
            .endOfLine();
    
    // Create an example URL
    var testMe = "https://www.google.com";
    
    // Use RegExp object's native test() function
    if( tester.test( testMe ) ) alert( "We have a correct URL "); // This output will fire
    else alert( "The URL is incorrect" );

VerbalExpressions也能操作 Ruby, C#, Python, Java, Groovy, PHP, Haskell, C++, Objective-C的正则。

## [HTML.js][8]

这个是 fork 自 Voyeur.js 的库，压缩后才2KB，语法良好，用于遍历和操作DOM。

###查找元素

    HTML.div.h1; // body>div>h1, return H1 elent
    HTML.div.h1.innerHTML = "Ilya Pestov"; 
    HTML.div.ul.li; // return array of li elements
    
    HTML.find("#example"); // return one node
    HTML.find(".example"); // return array of nodes
    HTML.find("#example").h1.em; 
    
###回调函数

HTML.tag...use( callback(element) ) Root HTMLElement


    HTML.div.ul.li.use(); // return div element
    HTML.div.ul.li.use(function(li, i) {
            // loop in list 
            li.innerHTML = "List item #" + i;
    });
    
    HTML.div.ul.use(function(ul) {
            ul.style.background = "blue";
            ul.li; //..
    });


###创建元素

HTML.create.tag...mult( factor ) Array

    HTML.create.div; // return div element
    HTML.create.div.h1; // return H1 with div parent
    HTML.create.div.h1.em;
    
    HTML.create.ul.li.mult(10).use(function(li, i) { // create 10 li elements 
         li.innerHTML = "Created list items!"; // 
    });
    
    //HTML.tag...eq( begin , end ) HTMLElement|Array
    HTML.create.ul.li.mult(10).eq(7).innerHTML = "The 8th item.";
    
    HTML.ul.li.eq(2, 6).use(function(li, i) {
         li.create.em.innerText = "Hello World";
    });


 HTML.js还提供了操作DOM的好方法： .each(), remove(), ify(), ._other(), _fn()等。详情请看文档。

##[LiveScript][9]

LiveScript是一种编译为JavaScript的语言。 它能直接映射到JavaScript，能避免重复的样板。

    take = (n, [x, ...xs]:list) -->
      | n <= 0     => []
      | empty list => []
      | otherwise  => [x] ++ take n - 1, xs
    
    take 2, [1 2 3 4 5] #=> [1, 2]
    
    take-three = take 3
    take-three [3 to 8] #=> [3, 4, 5]
    
    # Function composition, 'reverse' from prelude.ls
    last-three = reverse >> take-three >> reverse
    last-three [1 to 8] #
    
###写成JS


    var take, takeThree, lastThree, slice$ = [].slice;
    take = curry$(function(n, list){
      var x, xs;
      x = list[0], xs = slice$.call(list, 1);
      switch (false) {
      case !(n <= 0):
        return [];
      case !empty(list):
        return [];
      default:
        return [x].concat(take(n - 1, xs));
      }
    });
    take(2, [1, 2, 3, 4, 5]);
    takeThree = take(3);
    takeThree([3, 4, 5, 6, 7, 8]);
    
    
    lastThree = function(){
      return reverse(takeThree(reverse.apply(this, arguments)));
    };
    lastThree([1, 2, 3, 4, 5, 6, 7, 8]);
    function curry$(f, bound){
      var context,
      _curry = function(args) {
        return f.length > 1 ? function(){
          var params = args ? args.concat() : [];
          context = bound ? context || this : this;
          return params.push.apply(params, arguments) <
              f.length && arguments.length ?
            _curry.call(context, params) : f.apply(context, params);
        } : f;
      };
      return _curry();
    }


##[git-html5.js][10]

Git在JavaScript下的应用。 类似Brackets的插件，我很肯定这是geek们的好帮手。


##众筹: Ghost - 一个博客平台

据我所知这是第一次众筹合作的CMS。 作者John O'Nolan的项目在[Kickstarter][11]获得了400000美金，是他所需金额的785%。 Ghost 是开源项目，设计美观，可以理解的和自适应的管理界面。


##[Infogr.am][12]

Infographics 不仅能够管理大量的信息，也更生动地把数据显示在时间和空间上，还能统计趋势。 Infogram 是非常简单的创建图表的工具。 它能把图表，地图，照片，视频和数据导入XLS，XLSX或CSV。 据我所知，这是唯一交互式的图表生成器。 这还是个社交网络。 能与朋友分享信息和嵌入到您的网站。


> 英文原文：[Awesomeness & Usefulness for Web Developers][13]

> 本文是我为 [SegmentFault][14] 所译

  [1]: http://alphapixels.com/prepros/
  [2]: http://livereload.com/
  [3]: http://vanamco.com/ghostlab/
  [4]: https://github.com/Subash/Prepros
  [5]: http://gruntjs.com/
  [6]: http://brackets.io/
  [7]: https://github.com/VerbalExpressions/JSVerbalExpressions
  [8]: https://github.com/nbubna/HTML
  [9]: http://livescript.net/
  [10]: https://github.com/ryanackley/git-html5.js
  [11]: http://www.kickstarter.com/projects/johnonolan/ghost-just-a-blogging-platform
  [12]: https://infogr.am/
  [13]: http://ipestov.com/awesomeness-and-usefulness-for-web-developers/
  [14]: http://segmentfault.net/blog/news/1190000002590594


