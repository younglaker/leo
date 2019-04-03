---
layout: post
title:  Chome插件+JavaScript实现自动抢红包
date:   2015-12-10 08:24:00
category: [JavaScript]
tags: [JavaScript,自动抢红包]
---
双十一红包没在意，听朋友说抢到上百的红包，双十二弹出广告随便点了一下，心血来潮想写了个脚本。

<!-- ![双十二红包][1] -->

<!--more-->

道理都一样，这里以页面  http://market.m.taobao.com/markets/20151212/home/main-wf?mode=wow&refpid=mm_24258358_2367760_29508556&eh=9MANEb1txpZNUyfOh2k%2BHnlAZJ8kDjl4H2AndNdwGaudqXxjHuKwGLMXXejB4P7LX9iCfKlIJzkveuFnQMBXxMkbLKg8nWNj&ali_trackid=2:mm_24258358_2367760_29508556:1449540117_270_505160058  为例，使用Chrome插件的方法（还有很多其他实现方式，我这里想尝试Chrome插件的编写）。只是做了模拟点击。

## 配置Chrome插件

本地新建一个目录 click ，新建文件manifest.json，里面定义了插件的配置。

```
{
  "name": "click",
  "version": "1.0",
  "manifest_version":2,
  "description": "Red packet",
  "permissions": ["http://*/*"],
  "content_scripts":[
  {
      "matches":["https://www.taobao.com/markets/20151212/home/main-wf?mode=wow&refpid=mm_14428609_3290185_40982810&eh=fPCHhJ44zFBNUyfOh2k%2BHiZfdLHx8kQ31QInGOP2KCpZ4u2OgYu3W%2FmbDHCJJEP7X9iCfKlIJzkveuFnQMBXxMkbLKg8nWNj&ali_trackid=2:mm_14428609_3290185_40982810:1449725091_258_1788766137"],
      "js":["jquery-2.1.4.min.js","main.js"]
  }
  ]
}
```

- name： 插件名
- manifest_version： 固定值2
- content_scripts： 匹配的网站
- js： 需要加载的脚本，目前manifest.json、jquery-2.1.4.min.js、main.js都放在同一目录下。
- 其他配置如ico之类都省略了，有需要请自行查找资料

## 写脚本

先找到抢红包的按钮。这里是这个图片，没有id、class等任何方便查询的标记，所以采用XPath：

![抢红包的按钮][2]

同理找到再次抢红包的按钮的XPath：

![再次抢红包的按钮][3]

把以下代码粘贴到 main.js:
```
$(document).ready(function() {

    var a = setInterval(function () {
      console.log("开始");

      // 点击抢红包
        $(document).xpathEvaluate('/html/body/div[11]/div[2]/img').click();

        // 点击再来一次
        var b = setInterval(function () {
          $(document).xpathEvaluate('/html/body/div[11]/div[4]/div[2]/div[1]').click();
      }, 2000);
    }, 2000);
});

// 处理XPath
$.fn.xpathEvaluate = function (xpathExpression) {
   $this = this.first();

   xpathResult = this[0].evaluate(xpathExpression, this[0], null, XPathResult.ORDERED_NODE_ITERATOR_TYPE, null);

   result = [];
   while (elem = xpathResult.iterateNext()) {
      result.push(elem);
   }

   $result = jQuery([]).pushStack( result );
   return $result;
}

```

上面的代码已经可以正常运行了，但是淘宝有反作弊机制，我的脚本刷了几百下就被封了。为了降低被封的风险，应改进代码把间隔时间设为随机数，此处我就不再写出具体代码了。

## 添加插件

Chrome开启开发者模式，加载自己建的插件目录即可

![添加插件][4]

## 测试

现在到抢红包的页面刷新后就可以看到效果了，建议不要刷太频繁，我的已经被封了。

反正我刷了几百下也没有出一个红包，就当做练习了~


  [1]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151210162024.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/South/dy/5
  [2]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151210162236.png
  [3]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151210162319.png
  [4]: http://77g54f.com1.z0.glb.clouddn.com/QQ20151210170453.png