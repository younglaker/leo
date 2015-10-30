---
layout: post
title:  巧用CSS3 text-shadow ，做出PS效果的文字
date:   2015-01-12 08:24:00
category: [翻译,CSS3]
---

## CSS3 Shadows浏览器支持情况
text-shadow 和 box-shadow 这两个属性在主流现代浏览器上得到了很好的支持( > Chrome 4.0, > Firefox 3.5, > Safari 4.0, > Opera 9.6, > IE10)。

## text-shadow 和 box-shadow 的不同之处：

![clipboard.png](http://segmentfault.com/img/bVkzqv)

<!--more-->

box-shadow语法：

    box-shadow: none|h-shadow v-shadow blur spread color |inset|initial|inherit;

text-shadow语法：

    text-shadow: h-shadow v-shadow blur color|none|initial|inherit;


这里只有几个不同点：

* 不能为文本创建一个内阴影
* 有文字阴影没有扩散距离

但是可以创建多个阴影（显示在彼此的顶部）。

## text-shadow学习

### color 和 offsets
在下面的例子中，我们定义了水平和垂直偏移和自定义颜色

![clipboard.png](http://segmentfault.com/img/bVkzqI)

```
text-shadow:10px 10px;

text-shadow:-5px -5px; color:blue;

text-shadow:-1px -1px white; color:blue; background:#888;

text-shadow:1px 1px rgba(255,255,255, 0.5); color:blue; background:#eee;
```


注意，正值使阴影往右/下移动，负值往左/上移动

阴影的颜色是可选的，如果颜色没填，就使用从父级继承的颜色。然而，在不同的浏览器下可能会有所不同，所以我建议定义颜色项（RGB或RGBA和HSLA等）。

### blur
在下面的例子中，我们定义了各种模糊：

![clipboard.png](http://segmentfault.com/img/bVkzqT)

模糊是可选的参数，它定义了距离模糊。它应该是一个正数（因为0意味着没有模糊）。下面的图片，说明它是如何工作的：

![clipboard.png](http://segmentfault.com/img/bVkzqU)
```
element {
  text-shadow:5px 5px 3px darkred; color:red;
}

element {
  text-shadow:4px -4px 10px red; 
  color:azure;
  background:#333;
}

element {
  text-shadow:0px 0px 4px ;
}
parent {
  color:red;
}

element {
  text-shadow:0px 0px 4px ;
}
parent {
  color:lightgray; 
background:#333;
}

```

第一个例子使用不同的模糊距离，最后两个例子我们不设置颜色，但采用不同的颜色和背景色的父级。

##Expansion 和 contraction

与box-shadow类似，spread 属性将要在css4中要添加。目前，它得到了ie10（可能是更现代的浏览器）的支持。这是text-shadow的第四个参数。你可以使用这个参数的扩大、缩小阴影。

![clipboard.png](http://segmentfault.com/img/bVkzrc)
```
text-shadow:5px 5px 0px 3px lightgreen; color:green;

text-shadow:8px 8px 2px -3px darkgreen; color:green; font-weight:900;

text-shadow:0 0 0 3px rgba(128, 255, 0, 0.75); color:green;  background:#333;
```

正值扩大阴影，负值缩小阴影。零的值可用于给文本加边（第三例）。

### 多阴影
正如我们之前说的，你可以给文字加多个阴影：

![clipboard.png](http://segmentfault.com/img/bVkzrk)

简单的加边例子：
```
text-shadow: 0 0 0 3px white, 0 0 0 4px gray; color:magenta; /* example 1: basic outlining */

text-shadow: 3px 3px 4px 2px rgba(255,255,255,0.35),   /* example 2 */
             6px -6px 4px 2px rgba(255,255,255,0.25),  
             -3px -3px 4px 6px rgba(255,0,255,0.15);

text-shadow: 0 0 0 3px white,   /* example 3: neon - 1 */
             0 0 2px 6px magenta, 
             0 0 1px 9px white, 
             0 0 6px 12px magenta;
color:magenta;

text-shadow: 0 0 2px #fff,    /* example 4: neon 2 */
             0 0 4px 2px rgba(255,255,255,0.5), 
             0 0 6px 6px #f0f, 
             0 0 4px 7px #fff, 
             0 0 3px 15px #222, 
             -4px 0 2px 9px #f0f, 
             4px 0 2px 9px #f0f, 
             0 -4px 2px 9px #f0f, 
             0 4px 2px 9px #f0f;
color:white;

text-shadow: 0 -3px 3px 15px white, 0 1px 2px 9px; /* example 5: text underlining */
color:magenta;
```

运行效果：

![clipboard.png](http://segmentfault.com/img/bVkztL)


已经说过“spread”是css4的属性），但是你仍然用CSS3模拟：

```
text-shadow: 0px 0px 0px 4px magenta;

/* is similar to: */

text-shadow: magenta 0px 2px,  
             magenta 2px 0px,  
             magenta -2px 0px,  
             magenta 0px -2px,  
             magenta -1.4px -1.4px,  
             magenta 1.4px 1.4px,  
             magenta 1.4px -1.4px,  
             magenta -1.4px 1.4px;
```

## 例子：

##Twin shadow

![clipboard.png](http://segmentfault.com/img/bVkzt8)
```
text-shadow: 0 0 2px 2px white, 
             2px 0 2px 5px #222, 
             3px 0 3px 6px #933, 
             5px 0 2px 14px #222, 
             6px 0 5px 16px #533;
background-color:#222;
color:white;
```

##Letter-press


![clipboard.png](http://segmentfault.com/img/bVkzue)
```
text-shadow: 0px 2px 3px #555;
background-color:#333;
```

##Rainbow

![clipboard.png](http://segmentfault.com/img/bVkzuj)
```
text-shadow: 0 0 2px 3px yellow, 
             0 0 2px 6px orange, 
             0 0 2px 9px red, 
             0 0 2px 12px lime, 
             0 0 2px 15px blue, 
             0 0 2px 18px violet;
```
##3D

![clipboard.png](http://segmentfault.com/img/bVkzur)
```
text-shadow: 0 0 1px #999, 
             1px 1px 1px #888, 
             2px 2px 1px #777, 
             3px 3px 1px #666, 
             4px 4px 1px #555, 
             5px 5px 1px #444;
background-color:#333;
color:white;
```

##Retro / Vintage 

![clipboard.png](http://segmentfault.com/img/bVkzuw)
```
text-shadow: 2px 2px #fff, 
             3px 3px #666;
```
##First-letter-only shadow

![clipboard.png](http://segmentfault.com/img/bVkzuy)
```
.text { 
    text-shadow:0 0 5px; 
} 

.text::first-letter { 
    color:azure; 
    text-shadow:0 0 5px, 0 0px 6px 3px blue, 0 -2px 6px 6px cyan, 0 -4px 9px 9px lightblue ; 
}
```

#作业

一起试试，要怎样才能完成下面的效果吧~

![clipboard.png](http://segmentfault.com/img/bVkzuG)

---

> [英文原文][1]

> 本文是我为 [SegmentFault](http://segmentfault.com/a/1190000002480757/) 所译

  [1]: http://www.script-tutorials.com/practice-with-text-shadows/
