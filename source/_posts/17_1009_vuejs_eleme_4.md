---
layout: post
title:  Vue.js 2 高仿饿了么开发及解注四：goods 商品件组
date:   2017-10-09 08:24:00
category: [Vue.js]
tags: [JavaScript,HTML5,Vue.js]
---

<!-- ![Vue.js 2 高仿饿了么开发及解注四][1] -->

<!--more-->

> 欢迎交换友链： [laker.me--进击的程序媛]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
> V信: lakerHQ （请注明‘来自博客’）

慕课网早期出了《Vue.js 1 高仿饿了么APP》的课程，本系列文章根据课程，使用 Vue.js 2 版本进行开发，并进行了一步步开发流程记录和详细的代码注解。

[原作者的代码][2]

[我做的含有详细代码注解的版本][3]


## 评分组件

新建 componet / star / star.vue， 评分星级的图片放入。

评分星级的星星的切图分为无星、半星、全星三种图案，各有2x、3x两种尺寸，通过三种图案组合拼凑成多种评分星数。一个星星用一个 `<span>` 装载，以背景的形式展现。

**star.vue** CSS

```
  @import "../../common/stylus/mixin.styl"

  .star
    font-size: 0
    .star-item
      display: inline-block
      background-repeat: no-repeat
    // star-xx 不同尺寸的星星
    &.star-48
      .star-item
        width: 20px
        height: 20px
        margin-right: 22px
        background-size: 20px 20px
        &:last-child
          margin-right: 0 // 最后 一个星星没有margin-right
        &.on
          // mixin.styl 里定义的 bg-image()
          bg-image('star48_on') // 全星
        &.half
          bg-image('star48_half')  // 半星
        &.off
          bg-image('star48_off')  // 无星
    &.star-36
      .star-item
        width: 15px
        height: 15px
        margin-right: 6px
        background-size: 15px 15px
        &:last-child
          margin-right: 0
        &.on
          bg-image('star36_on')
        &.half
          bg-image('star36_half')
        &.off
          bg-image('star36_off')
    &.star-24
      .star-item
        width: 10px
        height: 10px
        margin-right: 3px
        background-size: 10px 10px
        &:last-child
          margin-right: 0
        &.on
          bg-image('star24_on')
        &.half
          bg-image('star24_half')
        &.off
          bg-image('star24_off')
```
**star.vue** HTML
```
  <!-- 循环填充星星状态的class -->
  <div class="star" :class="starType">
    <!-- v-for：循环获取 itemClasses() 返回的数组 -->
    <!-- :class="itemClass" 把获取的class加给span -->
    <span v-for="(itemClass,index) in itemClasses" :class="itemClass" class="star-item" key="index"></span>
  </div>
```

**star.vue** JavaScript
```
// const 定义常量
const LENGTH = 5   // 星星个数
const CLS_ON = 'on'   // 星星的三种状态
const CLS_HALF = 'half'
const CLS_OFF = 'off'

export default {
  // 使用组件时传入的参数
  props: {
    size: {
      type: Number
    },
    score: {
      type: Number
    }
  },
  // 计算
  computed: {
    starType () {
      return 'star-' + this.size
    },
    itemClasses () {
      let result = []  // 存放最终结果的数组
      let score = Math.floor(this.score * 2) / 2 // 通过分数算星星个数
      // 向下取0.5的公式。floor() 执行向下取整
      // floor(3.3 * 2) / 2 = 3 即 3颗全星+2颗无星
      // floor(3.6 * 2) / 2 = 3.5 即 3颗全星+1颗半星+1颗无星
      let hasDecimal = score % 1 !== 0 // 取余不为0则有半星
      let integer = Math.floor(score) // 整数部分
      for (let i = 0; i < integer; i++) { // 设置全星
        result.push(CLS_ON)
      }
      if (hasDecimal) {
        result.push(CLS_HALF)
      }
      while (result.length < LENGTH) { // 循环，补充无星
        result.push(CLS_OFF)
      }
      return result
    }
  }
}
```

**header.vue** 引用并注册 star 组件
```
import Star from 'components/star/star'

export default {
  ...
  components: {
    Star   // 注册评分组件
  }
}
```

**header.vue** 使用评分组件

```
<div class="star-wrapper">
  <!-- 使用 star 组件时，需传入 size、score -->
  <!-- :size 星星大小，组件定义了48、36、24 -->
  <!-- :score 评分，从data.json里来 -->
  <star :size="48" :score="seller.score"></star>
</div>
```

  [1]: http://77g54f.com1.z0.glb.clouddn.com/bgt-20170620.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [2]: https://github.com/ustbhuangyi/vue-sell
  [3]: https://github.com/younglaker/CometLab/tree/vue-eleme

