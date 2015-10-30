---
layout: post
title:  我是怎么写JavaScript框架的（一）
date:   2015-03-15 08:24:00
category: "JavaScript"
---

![clipboard.png](http://segmentfault.com/img/bVkvoJ)


## 前言
以前大三的时候写的一个小框架，仿jquery链式结构，纯属练手，大牛勿喷。当时还把JQ的源码全部打印下来（因为在电脑上看不方便做笔记），7600+行代码，300+页A4纸，对照着看别人是怎么写的。还好一个长我一届的学长当时比较闲，我说我想读JQ代码，他也没读过，就找来上两届的学长以前练手写的小框架进行学习。可惜只找到了压缩混淆后的代码，对于一个渣渣来说，阅读起来很困难。[在他的指点下][1]，我大致了解了原理，并开始着手自己写。现在陆续有学弟找我要这个代码。虽然现在觉得写得一塌糊涂，但是，可能对于和我当时一样摸不着边的人来说，可能会有帮助。我就打算慢慢解析我是怎么写的，并穿插讲解我对JQ（2.0版）写法的理解。其实源代码里我都写有注释，我也是靠这些注释回忆我当时是怎么想的。可能会有很多不好的地方，轻喷~ 罒ω罒

我给库起名Oct.js，是因为这个是在企鹅实习生应聘失败后为10月校招而写。纪念那个稚嫩的我。

[全部代码，看这里看这里~(￣▽￣)~*　][2]
[配合使用文档看代码更容易理解][3]

<!--more-->

## 闭包结构
为了防止和别的库的冲突，用闭包把整个框架安全地保护好。我们待会的代码都写在里面。这里创建一个全局变量"window.O"，就是在window对象里加个O，它等价于 "Oct"，相当于jquery、Jquery这样的别称，意味着以后用Oct()或O()来进行操作。把window.O写成window.$，那就和JQ的$调用用法一样。window.O返回一个Octobj对象，这很重要。

    (function() {
		// 创建一个全局变量"window.O"
        window.O = Oct = function(selector, root_id, tag) { 
			return new Octobj(selector, root_id, tag); 
		}; 

        // 帅气地定义一个版本
        Oct.version = "1.0"; 

    })();


## 链式结构原理

JQ的流行，我想是因为它很方便吧，一个选择器就可以接着写一连串的方法。链式结构就是在每个方法结束时返回一个对象进行下一个方法的操作。后面会通过代码说明

## 选择器
选择器非常重要。JQ特别把选择器部分剥离出一个库sizzle.js。现在的JQ内部也是调用JQ里面的sizzle。“选择器”三个字写得简单，代码写起来就很有学问，sizzle.js这种高大上的我就不说了。我这里简单实现一些功能：选择class/id/标签。

首先，把上面的Octobj对象骨架搭建起来。包含selector, root_id, tag三个参数。selector就是你想要找的东西，root_id是你想要找的东西的上级的id，tag是你要指定返回某种标签。 

    var Octobj = function(selector, root_id, tag) {

	};

定义一些参数

    // args: 存储root_id的子标签 
    // type: 类型标记，id("#"), class(".") 或者 tag("&。 tag也加标记是为了代码方便
    // eles: 临时的，存储`selector`变量里"# . &"标记后面的字符串
    // selector_exp: 用来匹配标签的正则规则
    var agrs, type, eles; 
    var selector_exp = /^(?:#(\w-_)+|\.(\w-_)+|(\w)+)$/; 
    
    // this.elements: 存储函数结束后返回对象
    this.elements = [];

    // 防止以下情况: $(""), $(null), $(undefined), $(false)
    if (!selector) {
        return this;
    }

接下来处理有没有指定root_id、tag的情况，

    if (root_id) {
        root_id = typeof root_id == "string" ? document.getElementById(root_id) : root_id;
    } else {
        root_id = document.body;
    }
    tag = tag || "*";
    if (tag !== "*") {
        tag = tag.slice(1);
    }

进入核心部分。分两种情况，能支持`querySelector()`方法的“高级”浏览器和不能支持的“低端”浏览器。先是能支持querySelector的，就很简单了：

    if (document.querySelectorAll) {
        // 因为我用'&'符号来标记标签 ，所以要用"replace()"去掉'&' 
        var node_list = document.querySelectorAll(selector.replace("&", ""))
        for (var i in node_list) {
            if (node_list[i].tagName !== undefined) {
                // 把符合要求的元素存入`this.elements`
                this.elements.push(node_list[i]);
            }
        }
    }

不能支持querySelector的，先来设置一些参数：

    // 处理类似JQ $('.a .b')的情况
    selector = selector.replace(/^\s+/, "").split(/\s+/);

    // 如果不指明 "root_id" 和 "tag", "args" 就存储所有的标签
    args = root_id.getElementsByTagName(tag);
    
    // 通过符号标记判断是class/id/tag
    type = selector[0].charAt(0);
    
    // 所要选取的目标的字符串
    eles = selector[0].slice(1);  

处理选择class的情况。有文章指出for in的效率不高，我本来是用for处理的，但是出现问题，因为会把方法一起选进来。JQ用了for in，感觉有了标杆，我就全部改用for in了。

    if (type === ".") {
        // 查找每个标签中有className,提取处理进行匹配
        for (var i in args) {
            if(args[i].className) {

                // className 可能不止一个, 通过空格进行分割
                var r = args[i].className.split(/\s+/);
                for (var j in r) {
                    if (r[j] === eles) {
                        this.elements.push(args[i]);
                    }
                }
            }
        }
    }

处理选择id的情况：

    else if (type === "#") {
        for (var i in args) {
            if(args[i].id) {
                var r = args[i].id.split(/\s+/);
                for (var j in r) {
                    if (r[j] === eles) {
                        this.elements.push(args[i]);
                    }
                }
            }
        }
    }
    
处理选择标签的情况：

    else if (type === "&") {
        for (var i in args) {
            // 你可以"console.log(args[i]);" 可以看到最后一个是"length" ，没有"tagName"，所以要排除这个情况，否则会报错
            if (i !== "length" && typeof args[i] !== "function") {

                // "args[i].tagName" 在浏览器的属性里是用大写的，为了符合我的习惯，改用小写进行判断
                if (args[i].tagName.toLowerCase() === eles.toLowerCase()) {
                    this.elements.push(args[i]);
                }
            }
        }

    }

基础选择器部分完成了，别忘了最后一句，返回找到的元素，给下一个方法进行操作：

    return this;
    
[全部代码][4]

## 用法举例

1.通过 id 选择.

    O("#buddy")

2.通过 class 选择.

    Oct(".buddy")

3.选择所有 div.

    O("&div") // also O("&Div"), O("&DIV")

4.选择 .buddy 里的 `<p>`.

    O(".buddy", null, "&p")

5.选择#dad下的.buddy

    O(".buddy", "#dad")   



  [1]: http://weibo.com/1830309103/zCAmJ7xDY?from=page_1005051830309103_profile&wvr=6&mod=weibotime&type=comment#_rnd1420465493227
  [2]: https://github.com/younglaker/octjs/blob/master/octjs/octjs.js
  [3]: https://github.com/younglaker/octjs/tree/master/doc
  [4]: https://github.com/younglaker/octjs/blob/master/octjs/octjs.js
  [5]: http://segmentfault.com/blog/younglaker/1190000002465399