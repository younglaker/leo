---
layout: post
title:  有弹性效果的SVG元素
date:   2015-02-06 08:24:00
category: [翻译,SVG]
---

今天分享一下带有弹性元素的灵感。这个想法是整合SVG元素成为带有弹性动画的组件。使用SVG能使菜单、按钮和其他元素变得更有趣，让交互也更加自然友好。但是不能过度使用弹性效果，只要有微小的变化即可。

> [演示][1] | [代码下载][2]

<!--more-->


为了实现 SVG 动画，我们可以使用 [Snap.svg][3]，这是一个很棒的 JavaScript SVG 库，适合主流现代浏览器。

在一些演示中使用的图标是由大卫·甘迪设计的 [Font Awesome][4]。

[draggable & droppable element][5]的演示用到 David DeSandro 的 [Dragabilly][6]。

> 请注意，这些演示只在新版本的现代浏览器中正常运行。

下面的代码将演示如何使用 SVG 的组件做工具条的动画：

```
<nav id="menu" class="menu">
	<button class="menu__handle"><span>Menu</span></button>
	<div class="menu__inner">
		<ul>
			<li><a href="#"><i class="fa fa-fw fa-home"></i><span>Home<span></a></li>
			<li><a href="#"><i class="fa fa-fw fa-heart"></i><span>Favs<span></a></li>
			<li><a href="#"><i class="fa fa-fw fa-folder"></i><span>Files<span></a></li>
			<li><a href="#"><i class="fa fa-fw fa-tachometer"></i><span>Stats<span></a></li>
		</ul>
	</div>
	<div class="morph-shape" data-morph-open="M300-10c0,0,295,164,295,410c0,232-295,410-295,410" data-morph-close="M300-10C300-10,5,154,5,400c0,232,295,410,295,410">
		<svg width="100%" height="100%" viewBox="0 0 600 800" preserveAspectRatio="none">
			<path fill="none" d="M300-10c0,0,0,164,0,410c0,232,0,410,0,410"/>
		</svg>
	</div>
</nav>
```

SVG插入到菜单到后面，我们用两个 data 属性来存储路径，动画将会使用这个默认的路径。

SVG 在菜单里为绝对位置，并且保证两侧有足够的空间以免弹性动画时元素被截断。SVG设置高宽为100%，而不是按比例，就可以做成自适应的。这对保持特定的形状很重要。包裹SVG的`.morph-shape`要设置固定的宽度：

```
.morph-shape {
	position: absolute;
	width: 240px;
	height: 100%;
	top: 0;
	right: 0;
}

.morph-shape svg path {
	stroke: #5f656f;
	stroke-width: 5px;
}
```

通过 Snap.svg，我们可以很容易的做到变形动画：

```
(function() {

	function SVGMenu( el, options ) {
		this.el = el;
		this.init();
	}

	SVGMenu.prototype.init = function() {
		this.trigger = this.el.querySelector( 'button.menu__handle' );
		this.shapeEl = this.el.querySelector( 'div.morph-shape' );

		var s = Snap( this.shapeEl.querySelector( 'svg' ) );
		this.pathEl = s.select( 'path' );
		this.paths = {
			reset : this.pathEl.attr( 'd' ),
			open : this.shapeEl.getAttribute( 'data-morph-open' ),
			close : this.shapeEl.getAttribute( 'data-morph-close' )
		};

		this.isOpen = false;

		this.initEvents();
	};

	SVGMenu.prototype.initEvents = function() {
		this.trigger.addEventListener( 'click', this.toggle.bind(this) );
	};

	SVGMenu.prototype.toggle = function() {
		var self = this;

		if( this.isOpen ) {
			classie.remove( self.el, 'menu--anim' );
			setTimeout( function() { classie.remove( self.el, 'menu--open' );	}, 250 );
		}
		else {
			classie.add( self.el, 'menu--anim' );
			setTimeout( function() { classie.add( self.el, 'menu--open' );	}, 250 );
		}
		this.pathEl.stop().animate( { 'path' : this.isOpen ? this.paths.close : this.paths.open }, 350, mina.easeout, function() {
			self.pathEl.stop().animate( { 'path' : self.paths.reset }, 800, mina.elastic );
		} );
		
		this.isOpen = !this.isOpen;
	};

	new SVGMenu( document.getElementById( 'menu' ) );

})();
```

通过正确的函数和合适的时间设置，一个略有弹性、有组织的运动效果做好了。但是选项多种多样，并依赖于特定上下文的整体感觉，所以可能性是无穷无尽的:)

希望你喜欢这些小的特效，并做出更多有意思的效果！

> [演示][7] | [代码下载][8]

> 英文原文：[Elastic SVG Elements][9]

> 本文是我为 [SegmentFault][10] 所译

  [1]: http://tympanus.net/Development/ElasticSVGElements/
  [2]: http://tympanus.net/Development/ElasticSVGElements/ElasticSVGElements.zip
  [3]: http://snapsvg.io/
  [4]: http://fortawesome.github.io/Font-Awesome/
  [5]: http://tympanus.net/Development/ElasticSVGElements/drag.html
  [6]: http://draggabilly.desandro.com/
  [7]: http://tympanus.net/Development/ElasticSVGElements/
  [8]: http://tympanus.net/Development/ElasticSVGElements/ElasticSVGElements.zip
  [9]: http://tympanus.net/codrops/2014/12/15/elastic-svg-elements/
  [10]: http://segmentfault.com/blog/news/1190000002541075
