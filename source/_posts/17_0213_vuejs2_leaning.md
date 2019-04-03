---
layout: post
title:   Vue.js 2.0 学习
date:   2017-02-13 08:24:00
category: [Vue.js]
tags: [Vue.js,JavaScript]
---

<!-- ![title][1] -->

<!--more-->

## 前期

- Ubutu
- npm

## 安装

    npm install vue -g

或用Bower：

    bower install vue

或安装命令行工具：
```
# 全局安装 vue-cli
$ npm install --global vue-cli
# 创建一个基于 webpack 模板的新项目
$ vue init webpack my-project
# 安装依赖，走你
$ cd my-project
$ npm install
$ npm run dev
```

## 调试工具

Chrome 应用商场搜 `Vue.js devtools`， 并在浏览器拓展程序管理里开启“允许访问文件网址”

## Sublime 插件

- Vue Syntax highlight
- Vuejs Snippets
- HTML/CSS/JS Prettify（格式化）， 安装后 tools->HTML/CSS/JS Prettify->set prettify preference 在"allowed_file_extensions": ["htm", "html", "xhtml", "shtml", "xml", "svg","vue"] 加上vue

## 安装 Vue 模板
安装好vue-cli后执行：

```
$ vue init webpack AppName  #建立一个webpack打包的应用，默认使用最新版vue
```

用 Vue 1.x ：

```
vue init webpack#1.0 AppName
```

进入应用后安装依赖，包含node/webpack等
```
$ cd AppName
$ npm install # 或用cnpm
```

运行服务，才能访问index， http://localhost:8080/
```
$ npm run dev
```

发布：
```
npm run build
```
或
```
webpack build
```
生成文件在`dist/stastic/`

![发布][2]

webpack+vue能很好的完成单页面应用的开发，官方也提供了很多例子和教程。但使用webpack能不能用到多页面项目中，同时又能使用vue进行模块组件化开发呢？参考：https://github.com/laoxubuer/Webpack-Vue-MultiplePage

插件、依赖

安装：

    npm i vue-resource vue-router vuex --save

main.js 加入:

    import VueRouter from 'vue-router'
    import VueResource from 'vue-resource'

## jQuery

安装：


在 `build/webpack.dev.conf.js` 和 ` build/webpack.prod.conf.js` 里添加一个新的 `new webpack.ProvidePlugin`

```
plugins: [

  // ...

  new webpack.ProvidePlugin({
    $: 'jquery',
    jquery: 'jquery',
    'window.jQuery': 'jquery',
    jQuery: 'jquery'
  })
]
```

[参考1][3], [参考2][4]

## BootStrap

安装：

    npm i bootstrap --save

main.js 加入:

    import 'bootstrap/dist/css/bootstrap.css'
    import 'bootstrap/dist/js/bootstrap.js'

## Sass

- node-sass
- sass-loader： webpack自动打包

    npm i node-sass sass-loader --save

把文件引用放入 App.vue 顶部

    <style src="./assets/sass/main.sass" lang="sass"></style>

用 webpack 的时候，尽量把资源看做模块依赖，不需要额外编译这些 sass 了，而且生产构建时自动会合并到一个 css 文件里。
https://segmentfault.com/q/1010000004479605

## JS插件

https://segmentfault.com/q/1010000005169531?_ea=806312
http://blog.csdn.net/ansu2009/article/details/53305134


## Ajax

除了用jQuery的Ajax，还有这个插件[vue-resource][5]，跟jquery不同的是它没有async选项，也就是说所有请求都是异步的。


  [1]: http://77g54f.com1.z0.glb.clouddn.com/bgt-20170213.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [2]: http://77g54f.com1.z0.glb.clouddn.com/QQ20170122172023.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [3]: http://stackoverflow.com/questions/37928998/how-to-use-a-jquery-plugin-inside-vue
  [4]: https://segmentfault.com/a/1190000007020623#articleHeader2
  [5]: https://github.com/pagekit/vue-resource
