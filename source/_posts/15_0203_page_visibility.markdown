---
layout: post
title:  使用 Page Visibility API ，让网站更友好
date:   2015-02-03 08:24:00
category: [翻译,HTML5]
---
我们可能都有这样的经历：打开一个浏览器，加载之前打开的所有标签页，听到几个页面发出的混合在一起的声音。虽然浏览器通过标签的声音图标、插件等方法告知用户发声的页面，但这种体验还是很糟糕。作为开发者和设计者，我们有责任让网站更受欢迎。

网站是不是应该在被激活使用时才能发出声音？为什么我们要浪费资源和进程在我们看不到的动画上？

幸运的是，现在有一个解决方案：HTML5 有个页面可见（Page Visibility）的API。你可以看到[Active Theory](http://activetheory.net/)已经在新项目里使用了这个API。例如[Under Armor][3] 和 [A Spacecraft For All][4]：点击其他标签页，刚才还在运行的多媒体就会暂停。我喜欢把这样的网站成为“有礼貌的网站（polite web）”：网站考虑了用户的注意力、带宽等。


<!--more-->

开发者曾经用绑定`onblur()`和`onfocus()`事件来尝试完成这样的效果。他们这样比什么都不做的好，但是这样的做法不能分辨窗口是否是真的隐藏。比如：有两个左右并排的窗口，用户都能看到他们的内容，但是在两个窗口之间切换时还是或激发`onblur()`或`onfocus()`事件。

## 使用Page Visibility

有很多使用Page Visibility API的情况，最常见的情况是——页面有一个视频，但用户看不到它，那就没有必要继续播放它。

    <video autoplay controls id="videoElement">
    	<source src="rar.mp4">
    	<source src="rar.webm">
    </video>
    
    <script>
    var videoElement = document.getElementById("videoElement");
    
    document.addEventListener("visibilitychange", function() {
        if (document.hidden) {     
            videoElement.pause();  
        } else {
            videoElement.play();   
        } 
    });
    </script>

但是这样有个问题，让用户觉得有点突然：用户切换标签时突然打开或停止视频的声音。可以把效果改为切换标签时渐渐显示或隐藏声音。这个可以借助jQuery的动画方法完成。

    <script>
    var videoElement = document.getElementById("videoElement");
    
    document.addEventListener("visibilitychange", function() {
        if (document.hidden) {     
            $("#videoElement").animate({volume: 0}, 1000, "linear", function() {
                videoElement.pause();
            });
        } else {
            videoElement.play();  
            $("#videoElement").animate({volume: 1}, 1000, "linear");
        } 
    });
    </script>

## 规范

Page Visibility API的规范很简单，只有两个方法：`document.hidden` 根据浏览器窗口的状态返回 `true` 或 `false`。具体的状态存储在`document.visibilityState`（`hidden` 、 `visible`、`prerender`、`unloaded`）里。`visibilitychange`可以作为一个事件。`document.visibilityState`可以检测为什么document不可见。但是`document.hidden`已经能满足大部分的需求。

## 注意事项和浏览器支持

Page Visibility API采用保守的方式来报告document的隐藏：如果用户在同一浏览器窗口里切换就会报告，但如果是用别的窗口遮住当前页面，就不会报告。这个API不是万无一失的，在某些情况下会误报，使用的时候要小心。

[浏览器对Page Visibility API的支持是比较好的][5]：所有的现代浏览器（除了Opera Mini）都支持这个API，包括IE10+。供应商前缀也慢慢取消：目前需要`-webkit`前缀是Android和黑莓的浏览器。我在上面的代码中为了简化操作，没有加前缀。但是添加前缀和测试也很方便。

Page Visibility API是Progressive Enhancement（渐进增强）的一个好例子。如果浏览器不支持这个API，该脚本将被忽略，用户将像平时一样被不受控制的声音打扰。

## 其他用法

Page Visibility API不仅可以用于声音和视频，还可以用于slider 、 PPT。

使用这个API可以使网站更友好、更绿色、更有责任感。建议广大开发者和设计师考虑把它整合到自己的项目中。

---

> 英文原文：[Creating Well-Behaved Sites With The Page Visibility API][6]

> 本文是我为 [SegmentFault][7] 所译

  [1]: http://gisele.underarmour.com/
  [2]: http://spacecraftforall.com/
  [3]: http://gisele.underarmour.com/
  [4]: http://spacecraftforall.com/
  [5]: http://caniuse.com/#feat=pagevisibility
  [6]: http://www.smashingmagazine.com/2015/01/20/creating-sites-with-the-page-visibility-api/
  [7]: http://segmentfault.com/blog/news/1190000002531702
