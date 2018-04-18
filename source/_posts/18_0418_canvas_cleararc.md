---
layout: post
title:  HTML5 Canvas 清除圆形、不规则区域
date:   2018-04-18 08:24:00
category: [HTML5]
tags: [JavaScript,HTML5,Canvas]
---

![Canvas 清除不规则区域][1]

<!--more-->

> 欢迎交换友链： [laker.me--进击的程序媛]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
> V信: lakerHQ （请注明‘来自博客’）


 默认 Canvas Api 只提供了清除矩形区域的接口 `clearRect()`，但有时候需要清除圆形或其他特殊形状的区域。比如我在开发 [pixeler](https://github.com/younglaker/pixeler) 擦除绘制的圆形，刚开始是用 `clearRect()`， 设置大于圆形直径的正方形来擦除，后来想，能不能直接擦除圆形区域。
 
 根据 [Stack Overflow][2] 的回答和 [Mozilla 的文档][3]，`ctx.globalCompositeOperation` 提供了多种色彩合成模式，其中 `destination-out` 能够完成清除效果：
 
 ![destination-out][4]
 
 可以拓展 Canvas 接口：
 
```
CanvasRenderingContext2D.prototype.clearArc = function(x, y, radius, startAngle, endAngle, anticlockwise) {
    this.beginPath();
    this.globalCompositeOperation = 'destination-out';
    this.fillStyle = 'black';
    this.arc(x, y, radius, startAngle, endAngle, anticlockwise);
    // 参数分别是：圆心横坐标、纵坐标、半径、开始的角度、结束的角度、是否逆时针
    this.fill();
    this.closePath();
};
```

 进一步，可以自定义各种路径：
 
```
CanvasRenderingContext2D.prototype.clear = function() {
    this.save();
    this.globalCompositeOperation = 'destination-out';
    this.fillStyle = 'black';
    this.fill();
    this.restore();
};

CanvasRenderingContext2D.prototype.clearArc = function(x, y, radius, startAngle, endAngle, anticlockwise) {
    this.beginPath();
    this.arc(x, y, radius, startAngle, endAngle, anticlockwise);
    this.clear();
};

CanvasRenderingContext2D.prototype.clearShape = function(x, y, radius, startAngle, endAngle, anticlockwise) {
    this.beginPath();
    // 定义各种不规则图形，如三角形、五角星...
    this.clear();
};

```

调用：
```
var canvas = document.getElementById('canvas');
var context = canvas.getContext('2d');

context.clearArc(50, 100, 10, 0, Math.PI * 2, false);
context.clearArc(80, 100, 20, 0, Math.PI, false);

```

[效果参考][5]


  [1]: http://77g54f.com1.z0.glb.clouddn.com/bgt-20180411.jpg?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [2]: https://stackoverflow.com/questions/3564717/how-can-i-clear-an-arc-or-circle-in-html5-canvas
  [3]: https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/globalCompositeOperation
  [4]: http://77g54f.com1.z0.glb.clouddn.com/QQ20180522-180816@2x.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [5]: http://jsdo.it/akm2/e8CK

