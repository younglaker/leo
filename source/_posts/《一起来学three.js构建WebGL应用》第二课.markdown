---
layout: post
title:  《一起来学three.js构建WebGL应用》第二课
date:   2015-01-13 08:24:00
category: [翻译,HTML5]
---

上一篇：[《一起来学three.js构建WebGL应用》第一课](http://segmentfault.com/blog/news/1190000002421007)

----

继续来学习 WebGL 的 three.js 库。

今天做些不一样的东西（如 MeshBasicMaterial，MeshLambertMaterial 和 MeshPhongMaterial），尽量使用各种参数（color，opacity，ambient，emissive，specular），讲解如何制作纹理和凹凸映射的使用。

![clipboard.png](http://segmentfault.com/img/bVkwm1)

**[Live Demo](http://www.script-tutorials.com/demos/385/index.html "WebGL With Three.js - Lesson 2 - demo")**

<!-- more -->

## HTML

如果你已经完成了[第一课](http://segmentfault.com/blog/news/1190000002421007)，那这里没什么新的内容。

这是要使用的 HTML 代码：

```
<!DOCTYPE html>
<html lang="en" >
    <head>
        <meta charset="utf-8" />
        <meta name="author" content="Script Tutorials" />
        <title>WebGL With Three.js - Lesson 2 | Script Tutorials</title>
        <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
        <link href="css/main.css" rel="stylesheet" type="text/css" />
    </head>
    <body>
        <script src="js/three.min.js"></script>
        <script src="js/THREEx.WindowResize.js"></script>
        <script src="js/OrbitControls.js"></script>
        <script src="js/stats.min.js"></script>
        <script src="js/script.js"></script>
    </body>
</html>
```

## Javascript

### 主要场景

我们借用以前教程的主体代码

```
var particleLight;

var lesson2 = {
    scene: null,
    camera: null,
    renderer: null,
    container: null,
    controls: null,
    clock: null,
    stats: null,

    init: function() { // Initialization

        // 创建主场景
        this.scene = new THREE.Scene();

        var SCREEN_WIDTH = window.innerWidth,
            SCREEN_HEIGHT = window.innerHeight;

        // 准备照相机
        var VIEW_ANGLE = 45, ASPECT = SCREEN_WIDTH / SCREEN_HEIGHT, NEAR = 1, FAR = 5000;
        this.camera = new THREE.PerspectiveCamera( VIEW_ANGLE, ASPECT, NEAR, FAR);
        this.scene.add(this.camera);
        this.camera.position.set(100, 1000, 1000);
        this.camera.lookAt(new THREE.Vector3(0,0,0));

        // 准备渲染器
        this.renderer = new THREE.WebGLRenderer({antialias:true, alpha: false});
        this.renderer.setSize(SCREEN_WIDTH, SCREEN_HEIGHT);
        this.renderer.setClearColor(0xffffff);

        this.renderer.shadowMapEnabled = true;
        this.renderer.shadowMapSoft = true;

        // 容器
        this.container = document.createElement('div');
        document.body.appendChild(this.container);
        this.container.appendChild(this.renderer.domElement);

        // 事件
        THREEx.WindowResize(this.renderer, this.camera);

        // 轨道控制器 (OrbitControls)
        this.controls = new THREE.OrbitControls(this.camera, this.renderer.domElement);
        this.controls.target = new THREE.Vector3(0, 0, 0);

        // 时钟
        this.clock = new THREE.Clock();

        // 统计
        this.stats = new Stats();
        this.stats.domElement.style.position = 'absolute';
        this.stats.domElement.style.bottom = '0px';
        this.stats.domElement.style.zIndex = 10;
        this.container.appendChild( this.stats.domElement );

        // 直线光照
        var dLight = new THREE.DirectionalLight(0xffffff);
        dLight.position.set(1, 300, 1);
        dLight.castShadow = true;
        // dLight.shadowCameraVisible = true;
        dLight.shadowDarkness = 0.2;
        dLight.shadowMapWidth = dLight.shadowMapHeight = 1000;
        this.scene.add(dLight);

        // 特定光照
        particleLight = new THREE.Mesh( new THREE.SphereGeometry(10, 10, 10), new THREE.MeshBasicMaterial({ color: 0xffffaa }));
        particleLight.position = dLight.position;
        this.scene.add(particleLight);

        // 背景
        var groundGeometry = new THREE.PlaneGeometry(1200, 1200, 1, 1);
        ground = new THREE.Mesh(groundGeometry, new THREE.MeshLambertMaterial({
            color: 0xFF62B0
        }));
        ground.position.y = 0;
        ground.rotation.x = - Math.PI / 2;
        ground.receiveShadow = true;
        this.scene.add(ground);
    }
};

// 给场景加动画
function animate() {
    requestAnimationFrame(animate);
    render();
    update();
}

// 更新控制器和统计
function update() {
    lesson2.controls.update(lesson2.clock.getDelta());
    lesson2.stats.update();

    // smoothly move the particleLight
    var timer = Date.now() * 0.000025;
    particleLight.position.x = Math.sin(timer * 5) * 300;
    particleLight.position.z = Math.cos(timer * 5) * 300;
}

// 渲染场景
function render() {
    if (lesson2.renderer) {
        lesson2.renderer.render(lesson2.scene, lesson2.camera);
    }
}

// 初始化页面
function initializeLesson() {
    lesson2.init();
    animate();
}

if (window.addEventListener)
    window.addEventListener('load', initializeLesson, false);
else if (window.attachEvent)
    window.attachEvent('onload', initializeLesson);
else window.onload = initializeLesson;
```

### 颜色

和第一课一样，添加一个函数来生成一个随机的颜色（当然这个随机颜色是从预定义的颜色阵列里随机选择）：

```
var colors = [
    0xFF62B0,
    0x9A03FE,
    0x62D0FF,
    0x48FB0D,
    0xDFA800,
    0xC27E3A,
    0x990099,
    0x9669FE,
    0x23819C,
    0x01F33E,
    0xB6BA18,
    0xFF800D,
    0xB96F6F,
    0x4A9586
];

function getRandColor() {
    return colors[Math.floor(Math.random() * colors.length)];
}

```

创建并使用 SphereGeometry 网格来画一个球体：

```
drawSphere: function(x, z, material) {
    var cube = new THREE.Mesh(new THREE.SphereGeometry(70, 70, 20), material);
    cube.rotation.x = cube.rotation.z = Math.PI * Math.random();
    cube.position.x = x;
    cube.position.y = 100;
    cube.position.z = z;
    cube.castShadow = cube.receiveShadow = true;
    this.scene.add(cube);
}
```

### 材料

如果你已经观看了[Demo][1]，很容易就会发现从简单到复杂整个被分成了好几个部分：

- 从左到右开始结束的三个球是最简单的：使用了MeshBasicMaterial，MeshLambertMaterial 和MeshPhongMaterial，且仅使用了 `color`
- 接下来的三个球几乎是相同的，但设置为半透明（透明度为0.5），第二行使用以下属性进行不同的组合：环境（ambient）、发射（emissive）、反射（specular）、光泽（shininess）
- 最后的三排，使用纹理和凹凸组合：

```
var mlib = {
  '1':   new THREE.MeshBasicMaterial({ color: getRandColor() }),
  '2':   new THREE.MeshLambertMaterial({ color: getRandColor() }),
  '3':   new THREE.MeshPhongMaterial({ color: getRandColor() }),

  '4':   new THREE.MeshBasicMaterial({ color: getRandColor(), opacity: 0.5, transparent: true }),
  '5':   new THREE.MeshLambertMaterial({ color: getRandColor(), opacity: 0.5, transparent: true }),
  '6':   new THREE.MeshPhongMaterial({ color: getRandColor(), opacity: 0.5, transparent: true }),

  '7':   new THREE.MeshLambertMaterial({ color: 0xff0000, ambient: 0xffffff }),
  '8':   new THREE.MeshLambertMaterial({ color: 0xff0000, emissive: 0x000088 }),

  '9':   new THREE.MeshPhongMaterial({ color: 0xff0000, ambient: 0x3ffc33 }),
  '10':  new THREE.MeshPhongMaterial({ color: 0xff0000, emissive: 0x000088 }),
  '11':  new THREE.MeshPhongMaterial({ color: 0xff0000, emissive: 0x004000, specular: 0x0022ff }),
  '12':  new THREE.MeshPhongMaterial({ color: 0xff0000, specular: 0x0022ff, shininess: 3 }),

  '13':  new THREE.MeshLambertMaterial({ map: texture, color: 0xff0000, ambient: 0x3ffc33 }),
  '14':  new THREE.MeshLambertMaterial({ map: texture, color: 0xff0000, emissive: 0x000088 }),
  '15':  new THREE.MeshLambertMaterial({ map: texture, color: 0xff0000, emissive: 0x004000, specular: 0x0022ff }),
  '16':  new THREE.MeshLambertMaterial({ map: texture, color: 0xff0000, specular: 0x0022ff, shininess: 3 }),

  '17':  new THREE.MeshPhongMaterial({ map: texture, color: 0xff0000, ambient: 0x3ffc33 }),
  '18':  new THREE.MeshPhongMaterial({ map: texture, color: 0xff0000, emissive: 0x000088 }),
  '19':  new THREE.MeshPhongMaterial({ map: texture, color: 0xff0000, emissive: 0x004000, specular: 0x0022ff }),
  '20':  new THREE.MeshPhongMaterial({ map: texture, color: 0xff0000, specular: 0x0022ff, shininess: 3 }),

  '21':  new THREE.MeshPhongMaterial({ map: texture, bumpMap: textureBump, color: 0xff0000, ambient: 0x3ffc33 }),
  '22':  new THREE.MeshPhongMaterial({ map: texture, bumpMap: textureBump, color: 0xff0000, emissive: 0x000088 }),
  '23':  new THREE.MeshPhongMaterial({ map: texture, bumpMap: textureBump, color: 0xff0000, emissive: 0x004000, specular: 0x0022ff }),
  '24':  new THREE.MeshPhongMaterial({ map: texture, bumpMap: textureBump, color: 0xff0000, specular: 0x0022ff, shininess: 3 }),
}
```

把这些材料加入数组方便待会儿的使用。注意这里使用了两个纹理，一是“映射”，其次是“凹凸映射”。代码如下：

```
var texture = THREE.ImageUtils.loadTexture('texture.png');
texture.repeat.set(10, 10);
texture.wrapS = texture.wrapT = THREE.RepeatWrapping;
texture.anisotropy = 16;
texture.needsUpdate = true;

var textureBump = THREE.ImageUtils.loadTexture('bump.png');
textureBump.repeat.set(10, 10);
textureBump.wrapS = textureBump.wrapT = THREE.RepeatWrapping;
textureBump.anisotropy = 16;
textureBump.needsUpdate = true;
```

现在只需要把不同位置的球用上不同的材料：

```
// add spheres with different materials
this.drawSphere(-550, 400, mlib['1']);
this.drawSphere(-350, 400, mlib['2']);
this.drawSphere(-150, 400, mlib['3']);

this.drawSphere( 150, 400, mlib['4']);
this.drawSphere( 350, 400, mlib['5']);
this.drawSphere( 550, 400, mlib['6']);

this.drawSphere(-550, 200, mlib['7']);
this.drawSphere(-350, 200, mlib['8']);

this.drawSphere( -50, 200, mlib['9']);
this.drawSphere( 150, 200, mlib['10']);
this.drawSphere( 350, 200, mlib['11']);
this.drawSphere( 550, 200, mlib['12']);

this.drawSphere(-250, 0, mlib['13']);
this.drawSphere( -90, 0, mlib['14']);
this.drawSphere(  90, 0, mlib['15']);
this.drawSphere( 250, 0, mlib['16']);

this.drawSphere(-250, -200, mlib['17']);
this.drawSphere( -90, -200, mlib['18']);
this.drawSphere(  90, -200, mlib['19']);
this.drawSphere( 250, -200, mlib['20']);

this.drawSphere(-250, -400, mlib['21']);
this.drawSphere( -90, -400, mlib['22']);
this.drawSphere(  90, -400, mlib['23']);
this.drawSphere( 250, -400, mlib['24']);
```

**[Live Demo](http://www.script-tutorials.com/demos/385/index.html "WebGL With Three.js - Lesson 2 - demo")**

好啦，今天的教程就到这里。

---

> 原文 [WebGL With Three.js – Lesson 2](http://www.script-tutorials.com/webgl-with-three-js-lesson-2/)

> 本文是我为 [SegmentFault][2] 所译

  [1]: http://www.script-tutorials.com/demos/385/index.html "WebGL With Three.js - Lesson 2 - demo"
  [2]: http://segmentfault.com/blog/news/1190000002482866
