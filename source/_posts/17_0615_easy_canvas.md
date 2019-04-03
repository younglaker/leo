---
layout: post
title:   EasyCanvas：连续画图的一些总结
date:   2017-06-15 08:24:00
category: [HTML5]
tags: [JavaScript,HTML5,Canvas]
---

<!-- ![Easy Canvas][1] -->

<!--more-->

> 欢迎交换友链： [Laker's Blog--进击的程序媛]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
> V信: lakerHQ （请注明‘来自博客’）

---

自己造轮子，写一个 Canvas 绘图库 [EasyCanvas][2] ，master 分支上已完成基本图形的绘制。我开始思考如何让这个框架更高效地绘制，接口的设计比实现头痛多了。

> 欢迎有兴趣的朋友加入本框架的编写中，或者提供修改建议。V信：lakerHQ

## 最初的设计

目前 master 分支上的版本的配置里的 points 传入坐标，不同的画图功能，points 是不同含义。

例如画线，第一组数组是起始点，后面依次是下一个绘制点，就可以连续画线：

```
b.line({
    points: [[10, 100], [200, 100], [10, 200]]
});
```

例如画二次贝塞尔曲线，三组坐标分别是开始点、控制点、结束点：

```
b.bezier({
    points: [[20, 20],  [200, 100], [200, 20]]
});
```

例如画矩形，points是矩形左上角坐标，矩形长宽另写：

```
b.rect({
    points: [10, 50],
    rectWidth: 300,
    rectHeight: 200
});
```

## 问题

- 按目前的设计，除了画直线，连续画图要多次调用同一个方法，如：

```
b.bezier({
    points: [[20, 20],  [200, 100], [200, 20]]，
    color: "#00f",
    shadowColor: "#000"
}).bezier({
    points: [[10, 10],  [100, 100], [100, 10]]，
    color: "#00f",
    shadowColor: "#000"
});
```

上述代码想画两条同样样式的曲线，但是写法过于累赘，并且两条曲线是不相连接。

- 必要的属性分开写，增加代码量。例如画矩形必须提供起始坐标和长宽，把基本值分开书写徒增代码量：

```
b.rect({
    points: [10, 50],
    rectWidth: 300,
    rectHeight: 200
});
```


## 改进方案：

目标：

- 只写一次方法就能连续画图
- 缩减不必要的代码

所以把配置的 points 去掉，所有基本配置由 basic 传入。

例如画一条连续的二次贝塞尔曲线，坐标两两成一组，曲线第一笔画的最后一组坐标（200, 10）是二笔画的起始点，这样既节省代码，又避免修改的时候出错：

```
b.bezier({
    shadow: [1, 1, 7, "#0f0"],
    color: "#0000ff",
    shadowColor: "#000",
    basic: [
            [20, 20, 20, 100, 200, 10], //曲线第一笔画
            [30, 100, 300, 10] //曲线第二笔画
           ]
});
```

例如画多条的二次贝塞尔曲线：

```
b.bezier({
    shadow: [1, 1, 7, "#0f0"],
    color: "#0000ff",
    shadowColor: "#000",
    basic: [    //第一条曲线
            [20, 20, 20, 100, 200, 10],
            [30, 100, 300, 10]
           ],
    basic1: [    //第二条曲线
            [10, 10, 10, 100, 100, 10],
            [40, 100, 400, 10],
            [50, 120, 200, 60]
           ],
    .....
    basicN: []
});
```

例如画矩形， basic 的参数依此代码起始点横纵坐标、长宽：

```
b.rect({
    color: "#0000ff",
    basic: [10, 10, 50, 100]
});

b.rect({
    color: "#0000ff",

    basic: [10, 10, 50, 100],
    basic1: [20, 30, 550, 120]
});
```

最开始设计的时候，为了表意明确，把坐标、长宽都独立成一个设置值，但是这几个值都是画图最基本的参数，并且参考 CSS 样式、Canva s画图的参数设置方式，也就决定把基本值合并在一个 basic 设置里。

## 代码实现

画曲线部分下一笔画的开始时上一笔画的结束，代码实现方案有两种：

- 把上一笔画的结束点 unshift 到下一笔画的数值最开始
- 绘制时判断是否第一笔画，进行相应操作

我选择了第二种方案，代码如下：

```
/*
 *  Draw quadratic curve
 */
bezier: function(settings) {
	var opt = _extendDefaults(this.defaults, settings);
	var bs = {};

	_setOpt(this.ctx, opt);

	// 遍历所有设置
	for (var i in opt) {
		// 把 basic 设置放入 bs
		if (!!i.match(/basic/))
			// 给 “baisc” 填充成 “baisc0”，方便后续遍历
			bs[!!i.match(/basic\d+/) ? i : i + "0"] = opt[i];
	}

	for (var i = 0; i < Object.keys(bs).length; i++) {
		var basic = bs["basic" + i];

		for (var j = 0; j < basic.length; j++) {

			if (j === 0) {	// basic0
				this.ctx.moveTo(basic[j][0], basic[j][3]);
				this.ctx.quadraticCurveTo(basic[j][2], basic[j][3], basic[j][4], basic[j][5]);

			} else {	// 其他basic使用上一笔画的结束点作为此笔画的起始点
				this.ctx.moveTo(basic[j - 1][4], basic[j - 1][5]);
				this.ctx.quadraticCurveTo(basic[j][0], basic[j][4], basic[j][2], basic[j][3]);
			}
		}
	}

	this.ctx.fill();
	this.ctx.stroke();
	this.ctx.closePath();

	this._renewDefaults();

	return this;
},
```

  [1]: http://77g54f.com1.z0.glb.clouddn.com/bgt-20170615.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [2]: https://github.com/younglaker/EasyCanvas

