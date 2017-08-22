---
layout: post
title:  Vue.js 2 高仿饿了么开发及解注一：基础准备
date:   2017-06-20 08:24:00
category: [Vue.js]
tags: [JavaScript,HTML5,Vue.js]
---

![Vue.js 2 高仿饿了么开发及解注一][1]

<!--more-->

> 欢迎交换友链： [Laker's Blog--进击的程序媛]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
> V信: lakerHQ （请注明‘来自博客’）

慕课网早期出了《Vue.js 1 高仿饿了么APP》的课程，本系列文章根据课程，使用 Vue.js 2 版本进行开发，并进行了一步步开发流程记录和详细的代码注解。

[原作者的代码][2]

[我做的含有详细代码注解的版本][3]

## 安装 Vue 模板
安装vue-cli
```
npm install --global vue-cli
```

安装好vue-cli后执行：

```
$ vue init webpack AppName  #建立一个webpack打包的应用，默认使用最新版vue
```

然后按照提示填写信息：

```
? Project name sell
? Project description sell
? Author younglaker <younglaker8@gmail.com>
? Vue build standalone
? Install vue-router? Yes
? Use ESLint to lint your code? Yes
? Pick an ESLint preset Standard  #
? Setup unit tests with Karma + Mocha? No  #单元测试
? Setup e2e tests with Nightwatch? No

   vue-cli · Generated "sell".

   To get started:

     cd sell
     npm install
     npm run dev

```

## 文件目录

-- build ： webpack配置相关
-- config ： webpack配置相关
-- node_modules ： 依赖
-- src ： 开发目录
-- static ： 第三方静态资源
| -- .gitkeep ： 使得如果文件为空也提交到git仓库
-- babelrc ： babel 配置
-- .editorconfig ： 编辑器配置。sublime要安装插件EditorConfig
-- .eslintignore ： 设置忽略语法检查的文件
-- .eslintrc.js ： eslint 配置。
-- index.html ： 项目入口
-- pakage.json ： 配置。`script`设置执行的命令，`npm run dev/start/build`即执行相应的脚本。`dependencies`生产需要的依赖， `devDependencies`编译过程的依赖，版本号前面有个 `^` 表示最低版本

## EsLint 配置

`extends: 'standard'` 是初始化文件时候选的，可以在`'rules'`里添加自己的规则（条件名：0 即为不检测此条件）。

- 默认js不能输入分号，想要分号则添加`'semi': ['error', 'always']`
- 忽略缩进报错`'indent'： 0`
- 不检测 new 实例，在 vue 代码前添加注释 `/* eslint-disable no-new */`

```
/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  render: h => h(App)
});
```

## 组件

查看示例组件`App.vue`，每个组件包括：

```
<template>...</template>

<script>...</script>

<style>...</style>
```

## 新增目录

https://github.com/ustbhuangyi/vue-sell/tree/1.0/src/common

把图标SVG上传到 https://icomoon.io/app/#/select 制作 ico fonts 并下载

- 在 src 文件夹下新建文件夹 common， js
- common 下新建 fonts, js, stylus
- fonts 下把 ico fonts 字体文件放到这
- stylus 下把  ico fonts 的 style.css 改成 ico.styl 放到这，把文字路径的 `fonts/` 改为 `../fonts/`
- 在 static 文件加入 css/reset.css，并在 index.html 里引用`    <link rel="stylesheet" type="text/css" href="static/css/reset.css" />`

安装 stylys：

```
npm[or cnpm] install stylus stylus-loader --save-dev
```

## 模拟数据

添加 `data.json` 到根目录：

https://github.com/ustbhuangyi/vue-sell/blob/1.0/data.json

`dev-server.js`，在`var app = express()` 后面添加（因为用到 express，所以要在起定义后），然后重启服务：
（每次修改 data.json、build文件夹、config文件夹下内容时，都要重启服务）

```
// import data.json
var appData = require('../data.json')
var seller = appData.seller
var goods = appData.goods
var ratings = appData.ratings

var apiRoutes = express.Router()

apiRoutes.get('/seller', function (req, res) {
  res.json({
    status: 1, // 定义状态码
    data: seller
  });
})

apiRoutes.get('/goods', function (req, res) {
  res.json({
    status: 1,
    data: goods
  })
})

apiRoutes.get('/ratings', function (req, res) {
  res.json({
    status: 1,
    data: ratings
  });
})

app.use('/api', apiRoutes)
```

调用的方法见下一篇文章关于 App.vue 菜单导航的写法。

## Header

**index.html**

```
    <meta name="viewport"
        content="width=device-width,initial-scale=1.0,maximum-scale=1.0,minimum-scale=1.0,user-scalable=no">
```

**router/index.js**

把 Hello 的引入删掉，删除 components: Hello。 header 已经在 App.vue 里引入，这里不用再引入。

**App.vue:**

```
<v-header></v-header>

import header from './components/header/header.vue'

export default {
  name: 'app',
  components: {
    'v-header': header
  }
}

<style lang="stylus">
</style>
```

**components/header/header.vue**

```
<template>
  <div class="header">header
  </div>
</template>

<script>
</script>

<style lang="stylus">
</style>
```

## tabs 路由

**App.vue:**

```
<v-header></v-header>
<div class="tab border-1px">
  <div class="tab-item">
    <router-link to="/goods">商品</router-link>
  </div>
  <div class="tab-item">
    <router-link to="/ratings">评论</router-link>
  </div>
  <div class="tab-item">
    <router-link to="/seller">商家</router-link>
  </div>
</div>
```

**build/webpack.base.conf.js** 新增路径别称 （需要重启服务）

```
  resolve: {
    ......
    alias: {
      '@': resolve('src')
      // 就能用 @/ 表示 src/
      // 或改为 'src': path.resolve(__dirname, '../src'),
      'common': path.resolve(__dirname, '../src/common'),
      'components': path.resolve(__dirname, '../src/components')
    }
  }

```

**router/index.js** 修改路由配置

```
// 如果没有上一步配置路径别称，就要用 @/components
import goods from 'components/goods/goods'
import ratings from 'components/ratings/ratings'
import seller from 'components/seller/seller'

export default new Router({
  routes: [{
    path: '/',
    redirect: '/goods'  // 重定向,进入就显示goods信息
  }, {
    path: '/goods',
    component: goods
  }, {
    path: '/ratings',
    component: ratings
  }, {
    path: '/seller',
    component: seller
  }]
})
```

## tabs 选中后高亮

**router/index.js**
全局配置 <router-link> 的默认『激活 class 类名』
http://router.vuejs.org/zh-cn/api/options.html

```
export default new Router({
  linkActiveClass: 'active',

  routes: [{
    path: '/',
    redirect: '/goods'
  }, {....
```

新建 **common/stylus/mixin.styl**
添加 1px border 的样式，通过传颜色使用。

```
border-1px($color)
  position: relative
  &:after
    display: block
    position: absolute
    left: 0
    bottom: 0
    width: 100%
    border-top: 1px solid $color
    content: ' '

border-none()
  &:after
    display: none
```

新建 **common/stylus/base.styl**
对 1px border 的样式在不同dpi相应缩放，避免 iphone6 下 1px BUG。

```
@media (-webkit-min-device-pixel-ratio: 1.5),(min-device-pixel-ratio: 1.5)
  .border-1px
    &::after
      -webkit-transform: scaleY(0.7)
      transform: scaleY(0.7)

@media (-webkit-min-device-pixel-ratio: 2),(min-device-pixel-ratio: 2)
  .border-1px
    &::after
      -webkit-transform: scaleY(0.5)
      transform: scaleY(0.5)
```

新建 **common/stylus/index.styl**
引用所有样式

```
@import "./mixin"
@import "./icon"
@import "./base"
```
**main.js** 里引用

```
import 'common/stylus/index.styl'
```

**App.vue:**
tab基础样式

```
@import "./common/stylus/mixin.styl"

.tab
  display: flex
  width: 100%
  height: 40px
  line-height: 40px
  border-1px(rgba(7, 17, 27, 0.1))
  .tab-item
    flex: 1
    text-align: center
    & > a
      display: block
      font-size: 14px
      color: rgb(77, 85, 93)
      &.active
        color: rgb(240, 20, 20)
```

## 在手机上预览

获取本机ip，例如 192.168.1.2 ， 把 localhost:8080/ 改成 192.168.1.2:8080 ，PC上也可以用这个地址访问。

可以用工具生成二维码，微信扫描访问。确保PC与手机同一局域网下。

## 一些常见报错

| 报错 | 原因 |
| :-------------- | :------------ |
| spaced-commnet | 注释`//`、`/*`后面没有空格，`*/`前面没有空格 |
| unkown custom element | 自定义标签没有正确注册 |
| indent | 缩进问题 |
| space-before-function-paren | 函数名和括号之间没有加空格 |
|  |  |


  [1]: http://77g54f.com1.z0.glb.clouddn.com/bgt-20170620.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [2]: https://github.com/ustbhuangyi/vue-sell
  [3]: https://github.com/younglaker/CometLab/tree/vue-eleme

