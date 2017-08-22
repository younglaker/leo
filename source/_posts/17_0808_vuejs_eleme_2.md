---
layout: post
title:  Vue.js 2 高仿饿了么开发及解注二：header 组件
date:   2017-08-08 08:24:00
category: [Vue.js]
tags: [JavaScript,HTML5,Vue.js]
---

![Vue.js 2 高仿饿了么开发及解注二][1]

<!--more-->

> 欢迎交换友链： [Laker's Blog--进击的程序媛]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
> V信: lakerHQ （请注明‘来自博客’）

慕课网早期出了《Vue.js 1 高仿饿了么APP》的课程，本系列文章根据课程，使用 Vue.js 2 版本进行开发，并进行了一步步开发流程记录和详细的代码注解。

[原作者的代码][2]

[我做的含有详细代码注解的版本][3]



# vue-resource

处理HTTP请求，https://github.com/pagekit/vue-resource

## 安装

    cnpm install vue-resource --save

## 引用

在 **routers/index.js** :

```
// 注入
import Resource from 'vue-resource'

// 注册
Vue.use(Resource)
```

# 编写header内容
## App.vue
发起ajax请求
```
// 定义一个常量，表示请求返回正常
const RESP_OK = 1

export default {
  name: 'app',
  data() {
    return {
      seller: {}
    }
  },
  created () {
    this.$http.get('/api/seller').then((response) => {
      // .body 获取 json 数据
      response = response.body

      // 判断请求是否正常
      if (response.status === RESP_OK) {
        this.seller = response.data

        // 测试
        console.log(this.seller)
      }
    })
  },
  ...
}
```

接口 `/api/seller` 在之前写的 `build/dev-server.js` 里定义了状态码和返回的数据

```
apiRoutes.get('/seller', function (req, res) {
  res.json({
    status: 1,
    data: seller
  });
})
```
**App.vue :**
把 Ajax 请求获取的 seller 对象传给 v-header 标签。
:seller="seller" 等同于 v-bind:seller="seller"
```
<v-header :seller="seller"></v-header>
```
##  header.vue

获取 seller 对象
```
  export default {
    props: {
      seller: {
        type: Object
      }
    },
    ...
```
写好一系列HTML、CSS。
注意几个地方：
1、在 **common/mixin.styl** 添加根据设备 dpi 使用不同像素的图片作为背景的代码。

> 组件使用的图片都放在组件的文件夹里。

```
bg-image($url)
  background-image: url($url + "@2x.png")
  @media (-webkit-min-device-pixel-ratio: 3),(min-device-pixel-ratio: 3)
    background-image: url($url + "@3x.png")
```

使用方法 `bg-image('图片名')`

```
bg-image('bulletin')
```

2、**header.vue** 里引用 mixin.styl
```
@import "../../common/stylus/mixin"
```

3、异步插入的图片地址，要用 vue 的指令 `:src`。如果用 `src` 就会在编译的时候渲染，但异步获取图片地址会有延时，导致找不到图片。

```
<img width="64" height="64" :src="seller.avatar">
```

4、多class的处理

在 data.json 里，定义有商家支持的活动

```
"supports": [
  {
    "type": 0,
    "description": "在线支付满28减5"
  },
  {
    "type": 1,
    "description": "VC无限橙果汁全场8折"
  },
  {
    "type": 2,
    "description": "单人精彩套餐"
  },
  {
    "type": 3,
    "description": "该商家支持发票,请下单写好发票抬头"
  },
  {
    "type": 4,
    "description": "已加入“外卖保”计划,食品安全保障"
  }
]
```
header.vue  CSS 添加每个活动 icon 的样式
```
  .icon
    ...
    &.decrease
      bg-image('decrease_2')
    &.discount
      bg-image('discount_2')
    &.invoice
      bg-image('invoice_2')
    &.special
      bg-image('special_2')
    &.guarantee
      bg-image('guarantee_2')
```
header.vue 创建classMap数组，依次写下对应data.json的supports数字的class
```
  export default {
    ...
    created() {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    }
```
icon 标签通过 :class 动态绑定class
```
<span class="icon" :class="classMap[seller.supports[0].type]"></span>
```

5、用 v-if 判断异步请求完成后再渲染，不使用则会在请求完成前竞选人导致报错，如：

```
<div v-if="seller.supports" class="support">
```

6、详细活动弹出层

HTML：

整个详情弹出层，通过指令 v-show 来控制显示隐藏
```
<div v-show="detailShow" class="detail">

```
显示按钮
```
<div v-if="seller.supports" class="support-count" @click="showDetail">
```
关闭按钮
```
<div class="detail-close" @click="hideDetail">
  <i class="icon-close"></i>
</div>
```

JavaScript：

```
  export default {
    ...
    data () {
      return {
        detailShow: false // 初始化 detailShow
      }
    },
    methods: {
      // 显示、隐藏的方法
      showDetail () {
        this.detailShow = true
      },
      hideDetail () {
        this.detailShow = false
      }
    }
```



  [1]: http://77g54f.com1.z0.glb.clouddn.com/bgt-20170620.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [2]: https://github.com/ustbhuangyi/vue-sell
  [3]: https://github.com/younglaker/CometLab/tree/vue-eleme

