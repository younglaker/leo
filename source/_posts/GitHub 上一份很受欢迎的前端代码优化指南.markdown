---
layout: post
title:  GitHub 上一份很受欢迎的前端代码优化指南
date:   2015-03-09 08:24:00
category: [翻译,技术]
---
看到一份很受欢迎的[前端代码指南][1]，根据自己的理解进行了翻译，但能力有限，对一些JS代码理解不了，如有错误，望斧正。

<!--more-->

##HTML
###语义化标签
HTML5 提供了很多语义化元素，更好地帮助描述内容。希望你能从这些丰富的标签库中受益。

    <!-- bad -->
    <div id="main">
      <div class="article">
        <div class="header">
          <h1>Blog post</h1>
          <p>Published: <span>21st Feb, 2015</span></p>
        </div>
        <p>…</p>
      </div>
    </div>
    
    <!-- good -->
    <main>
      <article>
        <header>
          <h1>Blog post</h1>
          <p>Published: <time datetime="2015-02-21">21st Feb, 2015</time></p>
        </header>
        <p>…</p>
      </article>
    </main>

请确保正确使用语义化的标签，错误的用法甚至不如保守的用法。

    <!-- bad -->
    <h1>
      <figure>
        <img alt=Company src=logo.png>
      </figure>
    </h1>
    
    <!-- good -->
    <h1>
      <img alt=Company src=logo.png>
    </h1>

###简洁

确保代码简洁性，不要再采用XHTML的旧做法。

    <!-- bad -->
    <!doctype html>
    <html lang=en>
      <head>
        <meta http-equiv=Content-Type content="text/html; charset=utf-8" />
        <title>Contact</title>
        <link rel=stylesheet href=style.css type=text/css />
      </head>
      <body>
        <h1>Contact me</h1>
        <label>
          Email address:
          <input type=email placeholder=you@email.com required=required />
        </label>
        <script src=main.js type=text/javascript></script>
      </body>
    </html>
    
    <!-- good -->
    <!doctype html>
    <html lang=en>
      <meta charset=utf-8>
      <title>Contact</title>
      <link rel=stylesheet href=style.css>
    
      <h1>Contact me</h1>
      <label>
        Email address:
        <input type=email placeholder=you@email.com required>
      </label>
      <script src=main.js></script>
    </html>



###可用性
可用性不应该是事后才考虑的事情。你不必成为WCAG专家来改进网站，你可以通过简单的修改做出不错的效果，例如；

* 正确使用`alt`属性
* 确保链接和按钮正确使用（不要用`<div class=button> `这种粗暴的做法）
* 不依赖于颜色来传达信息
* 给表单做好lable标记


```
   <!-- bad -->
    <h1><img alt="Logo" src="logo.png"></h1>
    
    <!-- good -->
    <h1><img alt="My Company, Inc." src="logo.png"></h1>
```
###语言

定义语言和字符编码是可选项，建议在文档级别处定义。使用UTF-8编码。

    <!-- bad -->
    <!doctype html>
    <title>Hello, world.</title>
    
    <!-- good -->
    <!doctype html>
    <html lang=en>
      <meta charset=utf-8>
      <title>Hello, world.</title>
    </html>



###性能
除非有非要在加载内容前加载脚本的必要性由，不然别这样做，这样会阻碍网页渲染。如果你的样式表很大，必须独立放到一个文件里。两次HTTP 请求不会显著降低性能。

    <!-- bad -->
    <!doctype html>
    <meta charset=utf-8>
    <script src=analytics.js></script>
    <title>Hello, world.</title>
    <p>...</p>
    
    <!-- good -->
    <!doctype html>
    <meta charset=utf-8>
    <title>Hello, world.</title>
    <p>...</p>
    <script src=analytics.js></script>

##CSS
###分号
不能漏写分号

    /* bad */
    div {
      color: red
    }
    
    /* good */
    div {
      color: red;
    }


###盒模型

整个文档的盒模型应该要相同，最好使用`global * { box-sizing: border-box; } `定义。不要修改某个元素的盒模型。

    /* bad */
    div {
      width: 100%;
      padding: 10px;
      box-sizing: border-box;
    }
    
    /* good */
    div {
      padding: 10px;
    }



###流
尽量不要改变元素默认行为。保持默认的文本流。比如，移出一个图片下面的一个白块，不影响原本的显示：

    /* bad */
    img {
      display: block;
    }
    
    /* good */
    img {
      vertical-align: middle;
    }


类似的，尽量不要改变浮动方式。

    /* bad */
    div {
      width: 100px;
      position: absolute;
      right: 0;
    }
    
    /* good */
    div {
      width: 100px;
      margin-left: auto;
    }


#定位
有很多CSS定位方法，尽量避免使用以下方法，根据性能排序：

    display: block;
    display: flex;
    position: relative;
    position: sticky;
    position: absolute;
    position: fixed;


###选择器

紧密耦合DOM选择器，三个层级以上建议加class：

    /* bad */
    div:first-of-type :last-child > p ~ *
    
    /* good */
    div:first-of-type .info

避免不必要的写法：

    /* bad */
    img[src$=svg], ul > li:first-child {
      opacity: 0;
    }
    
    /* good */
    [src$=svg], ul > :first-child {
      opacity: 0;
    }

###指明
不要让代码难于重写，让选择器更精确，减少ID、避免使用`!important`

    /* bad */
    .bar {
      color: green !important;
    }
    .foo {
      color: red;
    }
    
    /* good */
    .foo.bar {
      color: green;
    }
    .foo {
      color: red;
    }

###覆盖
覆盖样式会使维护和调试更困难，所以要尽量避免。

    /* bad */
    li {
      visibility: hidden;
    }
    li:first-child {
      visibility: visible;
    }
    
    /* good */
    li + li {
      visibility: hidden;
    }

###继承
不要把可继承的样式重复声明：

    /* bad */
    div h1, div p {
      text-shadow: 0 1px 0 #fff;
    }
    
    /* good */
    div {
      text-shadow: 0 1px 0 #fff;
    }

###简洁
保持代码的简洁。使用属性缩写。不必要的值不用写。

    /* bad */
    div {
      transition: all 1s;
      top: 50%;
      margin-top: -10px;
      padding-top: 5px;
      padding-right: 10px;
      padding-bottom: 20px;
      padding-left: 10px;
    }
    
    /* good */
    div {
      transition: 1s;
      top: calc(50% - 10px);
      padding: 5px 10px 20px;
    }

###语言
能用英文的时候不用数字。

    /* bad */
    :nth-child(2n + 1) {
      transform: rotate(360deg);
    }
    
    /* good */
    :nth-child(odd) {
      transform: rotate(1turn);
    }


###供应商的前缀
砍掉过时的供应商前缀。必须使用时，需要放在标准属性前：

    /* bad */
    div {
      transform: scale(2);
      -webkit-transform: scale(2);
      -moz-transform: scale(2);
      -ms-transform: scale(2);
      transition: 1s;
      -webkit-transition: 1s;
      -moz-transition: 1s;
      -ms-transition: 1s;
    }
    
    /* good */
    div {
      -webkit-transform: scale(2);
      transform: scale(2);
      transition: 1s;
    }

###动画

除了变形和改变透明度用`animation`，其他尽量使用`transition`。

    /* bad */
    div:hover {
      animation: move 1s forwards;
    }
    @keyframes move {
      100% {
        margin-left: 100px;
      }
    }
    
    /* good */
    div:hover {
      transition: 1s;
      transform: translateX(100px);
    }

###单位

可以不用单位时就不用。建议用`rem`。时间单位用`s`比`ms`好。

    /* bad */
    div {
      margin: 0px;
      font-size: .9em;
      line-height: 22px;
      transition: 500ms;
    }
    
    /* good */
    div {
      margin: 0;
      font-size: .9rem;
      line-height: 1.5;
      transition: .5s;
    }

###颜色
需要做透明效果是用`rgba`，否则都用16进制表示：

    /* bad */
    div {
      color: hsl(103, 54%, 43%);
    }
    
    /* good */
    div {
      color: #5a3;
    }

###绘图
减少HTTPS请求，尽量用CSS绘图替代图片：

    /* bad */
    div::before {
      content: url(white-circle.svg);
    }
    
    /* good */
    div::before {
      content: "";
      display: block;
      width: 20px;
      height: 20px;
      border-radius: 50%;
      background: #fff;
    }

###注释

    /* bad */
    div {
      // position: relative;
      transform: translateZ(0);
    }
    
    /* good */
    div {
      /* position: relative; */
      will-change: transform;
    }

##JavaScript
###性能
有可读性、正确性和好的表达比性能更重要。JavaScript基本上不会是你的性能瓶颈。有些可优化细节例如：图片压缩、网络接入、DOM文本流。如果你只能记住本指南的一条规则，那就记住这条吧。

    // bad (albeit way faster)
    const arr = [1, 2, 3, 4];
    const len = arr.length;
    var i = -1;
    var result = [];
    while (++i < len) {
      var n = arr[i];
      if (n % 2 > 0) continue;
      result.push(n * n);
    }
    
    // good
    const arr = [1, 2, 3, 4];
    const isEven = n => n % 2 == 0;
    const square = n => n * n;
    
    const result = arr.filter(isEven).map(square);

###Statelessness

尽量保持代码功能简单化，每个方法都对其他其他代码没有负影响。不使用外部数据。返回一个新对象而不是覆盖原有的对象。

    // bad
    const merge = (target, ...sources) => Object.assign(target, ...sources);
    merge({ foo: "foo" }, { bar: "bar" }); // => { foo: "foo", bar: "bar" }
    
    // good
    const merge = (...sources) => Object.assign({}, ...sources);
    merge({ foo: "foo" }, { bar: "bar" }); // => { foo: "foo", bar: "bar" }

###尽量使用内置方法

    // bad
    const toArray = obj => [].slice.call(obj);
    
    // good
    const toArray = (() =>
      Array.from ? Array.from : obj => [].slice.call(obj)
    )();

###严格条件
在非必要严格条件的情况不要使用。

    // bad
    if (x === undefined || x === null) { ... }
    
    // good
    if (x == undefined) { ... }

###对象
不要在循环里强制改变对象的值，，可以利用`array.prototype`方法。

    // bad
    const sum = arr => {
      var sum = 0;
      var i = -1;
      for (;arr[++i];) {
        sum += arr[i];
      }
      return sum;
    };
    
    sum([1, 2, 3]); // => 6
    
    // good
    const sum = arr =>
      arr.reduce((x, y) => x + y);
    
    sum([1, 2, 3]); // => 6
    If you can't, or if using array.prototype methods is arguably abusive, use recursion.
    
    // bad
    const createDivs = howMany => {
      while (howMany--) {
        document.body.insertAdjacentHTML("beforeend", "<div></div>");
      }
    };
    createDivs(5);
    
    // bad
    const createDivs = howMany =>
      [...Array(howMany)].forEach(() =>
        document.body.insertAdjacentHTML("beforeend", "<div></div>")
      );
    createDivs(5);
    
    // good
    const createDivs = howMany => {
      if (!howMany) return;
      document.body.insertAdjacentHTML("beforeend", "<div></div>");
      return createDivs(howMany - 1);
    };
    createDivs(5);

###Arguments
忘记`arguments `对象吧，其他参数是更好的选择，因为：
    
* 它已经被定义
* 它是一个真的数组，很方便使用

        // bad
        const sortNumbers = () =>
          Array.prototype.slice.call(arguments).sort();
        
        // good
        const sortNumbers = (...numbers) => numbers.sort();

###Apply
忘记`apply()`，改用运算操作。

    const greet = (first, last) => `Hi ${first} ${last}`;
    const person = ["John", "Doe"];
    
    // bad
    greet.apply(null, person);
    
    // good
    greet(...person);

###Bind
不用`bind()`方法，这有更好的选择：

    // bad
    ["foo", "bar"].forEach(func.bind(this));
    
    // good
    ["foo", "bar"].forEach(func, this);
    // bad
    const person = {
      first: "John",
      last: "Doe",
      greet() {
        const full = function() {
          return `${this.first} ${this.last}`;
        }.bind(this);
        return `Hello ${full()}`;
      }
    }
    
    // good
    const person = {
      first: "John",
      last: "Doe",
      greet() {
        const full = () => `${this.first} ${this.last}`;
        return `Hello ${full()}`;
      }
    }

###更好的排序
避免多重嵌套：

    // bad
    [1, 2, 3].map(num => String(num));
    
    // good
    [1, 2, 3].map(String);

###Composition
避免方法嵌套调用，改用`composition `：

    const plus1 = a => a + 1;
    const mult2 = a => a * 2;
    
    // bad
    mult2(plus1(5)); // => 12
    
    // good
    const pipeline = (...funcs) => val => funcs.reduce((a, b) => b(a), val);
    const addThenMult = pipeline(plus1, mult2);
    addThenMult(5); // => 12

###缓存

缓存性能测试，大数据结构和任何高代价的操作。

    // bad
    const contains = (arr, value) =>
      Array.prototype.includes
        ? arr.includes(value)
        : arr.some(el => el === value);
    contains(["foo", "bar"], "baz"); // => false
    
    // good
    const contains = (() =>
      Array.prototype.includes
        ? (arr, value) => arr.includes(value)
        : (arr, value) => arr.some(el => el === value)
    )();
    contains(["foo", "bar"], "baz"); // => false

###变量
`const` 优于 `let`， `let` 优于 ` var`。

    // bad
    var obj = {};
    obj["foo" + "bar"] = "baz";
    
    // good
    const obj = {
      ["foo" + "bar"]: "baz"
    };

###条件判断
用多个`if`，优于 `if` 、`else if`、`else` 和`switch`。

    // bad
    var grade;
    if (result < 50)
      grade = "bad";
    else if (result < 90)
      grade = "good";
    else
      grade = "excellent";
    
    // good
    const grade = (() => {
      if (result < 50)
        return "bad";
      if (result < 90)
        return "good";
      return "excellent";
    })();

###对象的操作
避免使用`for...in`。

    const shared = { foo: "foo" };
    const obj = Object.create(shared, {
      bar: {
        value: "bar",
        enumerable: true
      }
    });
    
    // bad
    for (var prop in obj) {
      if (obj.hasOwnProperty(prop))
        console.log(prop);
    }
    
    // good
    Object.keys(obj).forEach(prop => console.log(prop));

###使用map
合理使用的情况下，map更强大：

    // bad
    const me = {
      name: "Ben",
      age: 30
    };
    var meSize = Object.keys(me).length;
    meSize; // => 2
    me.country = "Belgium";
    meSize++;
    meSize; // => 3
    
    // good
    const me = Map();
    me.set("name", "Ben");
    me.set("age", 30);
    me.size; // => 2
    me.set("country", "Belgium");
    me.size; // => 3

###Curry
在别的语言里有Curry的一席之地，但在JS里避免使用。不然会是代码阅读困难。

    // bad
    const sum = a => b => a + b;
    sum(5)(3); // => 8
    
    // good
    const sum = (a, b) => a + b;
    sum(5, 3); // => 8

###可读性
不要使用自以为是的技巧：

    // bad
    foo || doSomething();
    
    // good
    if (!foo) doSomething();
    
    // bad
    void function() { /* IIFE */ }();
    
    // good
    (function() { /* IIFE */ }());
    
    // bad
    const n = ~~3.14;
    
    // good
    const n = Math.floor(3.14);

###代码重用
对写些小型、组件化、可重用的方法。

    // bad
    arr[arr.length - 1];
    
    // good
    const first = arr => arr[0];
    const last = arr => first(arr.slice(-1));
    last(arr);
    
    // bad
    const product = (a, b) => a * b;
    const triple = n => n * 3;
    
    // good
    const product = (a, b) => a * b;
    const triple = product.bind(null, 3);

###依赖
减少第三方库的使用。当你无法完成某项工作时可以使用，但不要为了一些能自己实现的小功能就加载一个很大的库。
    
    // bad
    var _ = require("underscore");
    _.compact(["foo", 0]));
    _.unique(["foo", "foo"]);
    _.union(["foo"], ["bar"], ["foo"]);
    
    // good
    const compact = arr => arr.filter(el => el);
    const unique = arr => [...Set(arr)];
    const union = (...arr) => unique([].concat(...arr));
    
    compact(["foo", 0]);
    unique(["foo", "foo"]);
    union(["foo"], ["bar"], ["foo"]);


--------

> 英文原文 [Frontend Guidelines](https://github.com/bendc/frontend-guidelines)

> 本文是我为 [SegmentFault][2]  所译

  [1]: https://github.com/bendc/frontend-guidelines#semicolons
  [2]: http://segmentfault.net/blog/news/1190000002587334

