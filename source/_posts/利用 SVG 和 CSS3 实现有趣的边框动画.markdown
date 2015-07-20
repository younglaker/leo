---
layout: post
title:  利用 SVG 和 CSS3 实现有趣的边框动画
date:   2015-02-12 08:24:00
category: [翻译,CSS3]
---

> [演示](http://tympanus.net/Tutorials/BorderAnimationSVG/) | [下载](http://tympanus.net/Tutorials/BorderAnimationSVG/BorderAnimationSVG.zip)

今天我们来探索一下[Carl Philipe Brenner的网站][1]上一个微妙而有趣的动画效果。当鼠标经过网格元素时，会有一个微妙的动画发生——网格元素变得透明，每条边有个顺时针的动画，创造了非常好的效果。这种效果是通过JS给`span`标签的宽或者高做了动画。我们待会会用SVG和CSS渐变来完成。注意，这个技术还是实验性的。


<!--more-->

首先，让我们来看看基本的概念，然后我们会朝着这个方向努力。

**请注意，我们将在SVG上使用CSS过渡，可能无法得到所有浏览器的支持。**

乍眼一看可能不明白这个效果是怎么完成的。我们先仔细看看上面的边就会发现，白色的边的宽度不断从右边往左边延伸，而一条稍微延时的边紧跟着一起移动。每条边都有这样的做法。看起来就像上面的边经过拐角移动到了左边，并以此类推。

不用SVG也能完成这样的效果，甚至只用伪元素。但是我们想探索一下怎样用CSS而不是JavaScript来控制SVG。

现在，来思考一下要怎么创建出这样的效果。我们可以改变矩形的`troke-dashoffset`或者直接画线。我们尝试不用JavaScript的解决方案。我们发现，CSS过渡`stroke-dashoffset` 和 `stroke-dasharray`的值会触发很多BUG。所以我们要尝试不同的解决方案，利用线条和它们的动画，这在CSS里很容易理解和实现。这也给我们更多机会去探索不同的动画效果。

我们将要使用的线的特别之处是，它们在这个动画里将有三种状态。它们是方盒边长的三倍，其中中间一截是与边等长的间隙。我们将通过设置`stroke-dashoffset`的值来实现与方盒的边等长。现在，这个动画实现的关键在于线的位置转换：



![bordereffect_01.gif][2]

SVG与方盒大小一致，就不会看到超出虚线的部分。

我们先完成第一条线：

    <div>
    	<svg width="200" height="200">
    		<line x1="0" y1="0" x2="600" y2="0" />
    	</svg>
    </div>

这个`div`长宽20px，和SVG一样。把SVG位置设为`absolute`，线宽度为10，`stroke-dasharray`为200。

    div {
    	width: 200px;
    	height: 200px;
    	position: relative;
    	overflow: hidden;
    	background: #ddd;
    }
    
    svg {
    	position: absolute;
    	top: 0;
    	left: 0;
    }
    
    svg line {
    	stroke-width: 10;
    	stroke: #000;
    	fill: none;
    	stroke-dasharray: 200;
    	-webkit-transition: -webkit-transform .6s ease-out;
    	transition: transform .6s ease-out;
    }
    
    div:hover svg line {
    	-webkit-transform: translateX(-400px);
    	transform: translateX(-400px);
    }

当数鼠标悬浮在div上时，线也有一个过渡。我们要把线移动到它的三分之二处，所以要在x轴上移动到-400px处，你可以[看看这个效果][3]。因为[translation][4]不能在这里用百分比做单位，所以用px。

接着添加其余三条线，gif效果：

![bordereffect_02.gif][5]

我们需要实现以下效果：线的第一部分移出方盒后，旁边的线的最后一部分移动进来，，这将传进直线在转角处转弯的假象，

来看看坐标系的定义：

![clipboard.png](http://segmentfault.com/img/bVkSro)

左边的线的坐标是(0,200) 到 (0,-400)，底部的是(200,200) 到 (-400,200)，右边的是right one (200,0) 到 (200,600)：

    <div>
    	<svg width="200" height="200">
    		<line class="top" x1="0" y1="0" x2="600" y2="0"/>
    		<line class="left" x1="0" y1="200" x2="0" y2="-400"/>
    		<line class="bottom" x1="200" y1="200" x2="-400" y2="200"/>
    		<line class="right" x1="200" y1="0" x2="200" y2="600"/>
    	</svg>
    </div>
    
给每条线加上不同的`hover`效果：

    div:hover svg line.top {
      -webkit-transform: translateX(-400px);
      transform: translateX(-400px);
    }
    
    div:hover svg line.bottom {
      -webkit-transform: translateX(400px);
      transform: translateX(400px);
    }
    
    div:hover svg line.left {
      -webkit-transform: translateY(400px);
      transform: translateY(400px);
    }
    
    div:hover svg line.right {
      -webkit-transform: translateY(-400px);
      transform: translateY(-400px);
    }

[看看现在的效果][6]。

现在方盒大小改为300 x 460，再给它添加一些内容：

    <div class="box">
    	<svg xmlns="http://www.w3.org/2000/svg" width="100%" height="100%">
    		<line class="top" x1="0" y1="0" x2="900" y2="0"/>
    		<line class="left" x1="0" y1="460" x2="0" y2="-920"/>
    		<line class="bottom" x1="300" y1="460" x2="-600" y2="460"/>
    		<line class="right" x1="300" y1="0" x2="300" y2="1380"/>
    	</svg>
    	<h3>D</h3>
    	<span>2012</span>
    	<span>Broccoli, Asparagus, Curry</span>
    </div>

为了实现Carl Philipe Brenner的网站上的效果，我们还要添加颜色过渡效果、盒子阴影等：

    .box {
    	width: 300px;
    	height: 460px;
    	position: relative;
    	background: rgba(255,255,255,1);
    	display: inline-block;
    	margin: 0 10px;
    	cursor: pointer;
    	color: #2c3e50;
    	box-shadow: inset 0 0 0 3px #2c3e50;
    	-webkit-transition: background 0.4s 0.5s;
    	transition: background 0.4s 0.5s;
    }
    
    .box:hover {
    	background: rgba(255,255,255,0);
    	-webkit-transition-delay: 0s;
    	transition-delay: 0s;
    }
    
    
给文字加上样式：

    .box h3 {
    	font-family: "Ruthie", cursive;
    	font-size: 180px;
    	line-height: 370px;
    	margin: 0;
    	font-weight: 400;
    	width: 100%;
    }
    
    .box span {
    	display: block;
    	font-weight: 400;
    	text-transform: uppercase;
    	letter-spacing: 1px;
    	font-size: 13px;
    	padding: 5px;
    }
    
    .box h3,
    .box span {
    	-webkit-transition: color 0.4s 0.5s;
    	transition: color 0.4s 0.5s;
    }
    
    .box:hover h3,
    .box:hover span {
    	color: #fff;
    	-webkit-transition-delay: 0s;
    	transition-delay: 0s;
    }

给SVG和线条添加样式：

    .box svg {
    	position: absolute;
    	top: 0;
    	left: 0;
    }
    
    .box svg line {
    	stroke-width: 3;
    	stroke: #ecf0f1;
    	fill: none;
    	-webkit-transition: all .8s ease-in-out;
    	transition: all .8s ease-in-out;
    }

给线的过渡加上延时：

    .box:hover svg line {
    	-webkit-transition-delay: 0.1s;
    	transition-delay: 0.1s;
    }

之前我们定义的`stroke-dasharray`只有一个值，但是现在要因尺寸变化而修改

    .box svg line.top,
    .box svg line.bottom {
    	stroke-dasharray: 330 240; 
    }
    
    .box svg line.left,
    .box svg line.right {
    	stroke-dasharray: 490 400;
    }

如果你尝试这些值，你就能看到这些线条不同的显示效果。

最后，我们要个hover过渡设置相应的值。因为现在元素是300px宽，所以水平线条改为900px，竖线同理改变:

    .box:hover svg line.top {
    	-webkit-transform: translateX(-600px);
    	transform: translateX(-600px);
    }
    
    .box:hover svg line.bottom {
    	-webkit-transform: translateX(600px);
    	transform: translateX(600px);
    }
    
    .box:hover svg line.left {
    	-webkit-transform: translateY(920px);
    	transform: translateY(920px);
    }
    
    .box:hover svg line.right {
    	-webkit-transform: translateY(-920px);
    	transform: translateY(-920px);
    }

大功告成。希望能通过这些效果激发你的创意，实现更多的效果~

> [演示](http://tympanus.net/Tutorials/BorderAnimationSVG/) | [下载](http://tympanus.net/Tutorials/BorderAnimationSVG/BorderAnimationSVG.zip)


> 英文原文：[Creating a Border Animation Effect with SVG and CSS][7]

> 本文是我为 [SegmentFault][8] 所译

  [1]: http://carlphilippebrenner.com/
  [2]: http://segmentfault.com/img/bVkSqN
  [3]: http://jsbin.com/lajigoxa/4/edit?html,css,output
  [4]: http://www.w3.org/TR/SVG/coords.html#TransformAttribute
  [5]: http://segmentfault.com/img/bVkSrl
  [6]: http://jsbin.com/kutewana/3/edit?html,css,output
  [7]: http://tympanus.net/codrops/2014/02/26/creating-a-border-animation-effect-with-svg-and-css/
  [8]: http://segmentfault.com/blog/news/1190000002553605
