---
layout: post
title:  Vue.js 2 高仿饿了么开发及解注五：购物车组件（上）
date:   2017-11-05 08:24:00
category: [Vue.js]
tags: [JavaScript,HTML5,Vue.js]
---

<!-- ![Vue.js 2 高仿饿了么开发及解注五][1] -->

<!--more-->

> 欢迎交换友链： [laker.me--进击的程序媛]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
> V信: lakerHQ （请注明‘来自博客’）

慕课网早期出了《Vue.js 1 高仿饿了么APP》的课程，本系列文章根据课程，使用 Vue.js 2 版本进行开发，并进行了一步步开发流程记录和详细的代码注解。

[原作者的代码][2]

[我做的含有详细代码注解的版本][3]

---
# 购物车组件

新建组件 shopcart/shopcart.vue

`goods.vue` 里引用，并注册
```
// 购物车组件
import shopcart from 'components/shopcart/shopcart'

export default {
  ...
  components: {
    shopcart
  }
}
```

## 解注： 选择食物

`goods.vue`

```
data.json里goods的结构
"goods": [
  {
    "name": "热销榜",
    "type": -1,
    "foods": [{}, {}...]
  },
  {
    "name": "单人精彩套餐",
    "type": 2,
    "foods": [{}, {}...]
  }
```
放在 computed 里，实时更新
```
computed: {
  selectFoods () {
    let foods = []
    this.goods.forEach((good) => {
      good.foods.forEach((food) => {
        if (food.count) {
          foods.push(food)
        }
      })
    })
    return foods
  }
}
```


## 解注1，接收参数

`goods.vue` 给组件传值selectFoods（选择的食物，最终传的是selectFoods()的返回值foods）、deliveryPrice（配送费）、minPrice（起送价）
```
<shopcart  :selectFoods="selectFoods" :deliveryPrice="seller.deliveryPrice" :minPrice="seller.minPrice"></shopcart>
</div>
```


`shopcart.vue`接收goods组件传进来的deliveryPrice、minPrice，default表示如果没有接收到时的默认值
```
export default {
  props: {
    selectFoods: {
      type: Array,
      default() {
        return [
          {
            price: 10,
            count: 1
          }
        ]
      }
    },
    deliveryPrice: {
      type: Number,
      default: 0
    },
    minPrice: {
      type: Number,
      default: 0
    }
  }
```

配送费直接显示：
```
<div class="desc">另需配送费￥{{deliveryPrice}}元</div>
```

## 解注2： 显示商品总价和总数
计算：
```
computed: {
  /* 计算商品总价 */
  totalPrice() {
    let total = 0
    // 循环累加总价
    this.selectFoods.forEach((food) => {
      total += food.price * food.count
    })
    return total
  },
  /* 计算商品总数 */
  totalCount() {
    let count = 0
    this.selectFoods.forEach((food) => {
      count += food.count
    })
    return count
  },
```

显示：

```
<div class="logo-wrapper">
  <!-- 当 totalCount>0 时，就添加 .highlight 高亮样式 -->
  <!-- totalCount 是一个方法，可以省略‘()’来用 -->
  <div class="logo" :class="{'highlight':totalCount>0}">
    <i class="icon-shopping_cart" :class="{'highlight':totalCount>0}"></i>
  </div>
  <!-- 当 totalCount>0 时，才显示这个标签 -->
  <div class="num" v-show="totalCount>0">{{totalCount}}</div>
</div>
  <!-- 当 totalPrice>0 时，就添加 .highlight 高亮样式 -->
<div class="price" :class="{'highlight':totalPrice>0}">￥{{totalPrice}}</div>
<div class="desc">另需配送费￥{{deliveryPrice}}元</div>
```

## 解注3：付款按钮
付款按钮有三种状态

- 未选择食品时，显示起送价
- 选择食品但未达到起送价，显示差价
- 选择食品但且达到起送价，显示'去结算'

>   ES6字符串拼接： `字符串${变量}字符串` 等同于'字符串'+变量+'字符串'。 注意是反引号 ` ，而不是单引号 '

```
/* 付款按钮的字样 */
payDesc() {
  if (this.totalPrice === 0) {
    return `￥${this.minPrice}元起送`
  } else if (this.totalPrice < this.minPrice) {
    let diff = this.minPrice - this.totalPrice
    return `还差￥${diff}元起送`
  } else {
    return '去结算'
  }
}
```


```
<div class="pay" :class="payClass">
  {{payDesc}}
</div>
```

# “添加食物”组件

新建 `components/cartcontrol/cartcontrol.vue`
在`shopcart.vue`引入并注册

```
import cartcontrol from 'components/cartcontrol/cartcontrol'

components: {
  cartcontrol
}

<li class="food" v-for="food in selectFoods">
  ...
  <div class="cartcontrol-wrapper">
    <!-- 传入 food -->
    <cartcontrol :food="food"></cartcontrol>
  </div>
</li>
```

## 解注1：减号滚动出现、数字渐变的动画

vue.js 的 transition 的使用可以参考 header.vue 里的注释

添加 transition 标签，name 里写上动画名 move

```
<transition name="move">
  <!-- 当food.count>0时显示删除按钮 -->
  <div class="cart-decrease" v-show="food.count>0" >
    <span class="inner icon-remove_circle_outline"></span>
  </div>
</transition>
```

name="xx",这里就是 xxe-enter-active，xxe-leave-active

```
.cart-decrease
  ...
  opacity: 1
  transform: translate3d(0, 0, 0)
  &.move-enter-active, &.move-leave-active
    transition: all 0.4s linear
  &.move-enter, &.move-leave-active
    opacity: 0
    transform: translate3d(24px, 0, 0)
    .inner
      transform: rotate(180deg)
```

## 解注：添加食物，小球跳进购物车的动画

`cartcontrll.vue` 里获取点击的食物加号的DOM

https://cn.vuejs.org/v2/api/#vm-emit

`vm.$emit()`：触发当前实例上的事件。附加参数都会传给监听器回调。

侦听事件使用 `$on(eventName)`
定义和触发事件使用 `$emit(eventName)`

（vue.js 1.0 中的 `$dispatch` 和 `$broadcast` 已经被移除）

```
methods: {
  /* 添加食物到购物车 */
  addCart (event) {
    ...

    // 定义并触发 add 事件，event.target（点击的目标，即食品对应的加号） 作为参数
    this.$emit('add', event.target)
  }
```

`goods.vue` 里添加食物的组件里使用
触发在cartcontroll.vue里定义的add事件，事件发生时触发addFood()
@add 等同于 v-on:add
```
<cartcontrol @add="addFood"></cartcontrol>

```

`goods.vue`  addFood()调用_drop(), 调用_drop()再调用shopcart组件的drop方法

```
<shopcart ref="shopcart" ...></shopcart>

addFood (target) {
  this._drop(target)
},
_drop (target) {
  // 体验优化,异步执行下落动画
  this.$nextTick(() => {
    // 先在 <shopcart> 标签里添加 ref="shopcart" 属性，goods组件就能访问子组件shopcart里的方法
    this.$refs.shopcart.drop(target)
  })
}
```

`shopcart.vue`
这里的transition用 [JavaScript 钩子][4]的用法。

- @before-enter="方法"
- @enter="方法"
- @after-enter="方法"
- @enter-cancelled="方法"
- @before-leave="方法"
- @leave="方法"
- @after-leave="方法"
- @leave-cancelled="方法"

```
<transition name="drop" @before-enter="beforeDrop" @enter="dropping" @after-enter="afterDrop">
  <div class="ball" v-show="ball.show">
  </div>
</transition>

methods: {
  // --------
  // 进入中
  // --------
  beforeDrop: function (el) {},
  // 此回调函数是可选项的设置
  // 与 CSS 结合时使用
  dropping: function (el, done) {},
  afterDrop: function (el) {}
}

```

`shopcart.vue` 里的动画的具体实现。HTML部分：

```
<!-- 点击添加食物时，跳到购物车的动画小球 -->
<div class="ball-container">
  <!-- 循环显示小球 -->
  <div v-for="ball in balls">
    <!-- 小球下落的动画 -->
    <!-- https://cn.vuejs.org/v2/guide/transitions.html#JavaScript-钩子 -->
    <!-- 这里使用了Vue transition 的 avaScript-钩子。@before-enter、@enter、@after-enter、@enter-cancelled、@before-leave、@leave、@after-leave、@leave-cancelled -->
    <!-- methods: {
      beforeDrop: function (el) {},
      // 此回调函数是可选项的设置
      // 与 CSS 结合时使用
      dropping: function (el, done) {},
      afterDrop: function (el) {}
    } -->
    <!-- 推荐对于仅使用 JavaScript 过渡的元素添加 v-bind:css="false"，Vue 会跳过 CSS 的检测。这也可以避免过渡过程中 CSS 的影响 -->
    <transition name="drop" @before-enter="beforeDrop" @enter="dropping" @after-enter="afterDrop">
      <!-- 通过 ball.show 来判断是否显示 -->
      <div class="ball" v-show="ball.show">
        <div class="inner inner-hook"></div>
      </div>
    </transition>
  </div>
</div>
```

JavaScript 里写动画的方法

```
/* 找到可用的小球，将其push到dropBalls[] */
drop (el) {
  // 传入的 el 是点击的加号的DOM
  // balls，自定义的变量
  for (let i = 0; i < this.balls.length; i++) {
    let ball = this.balls[i]
    if (!ball.show) {
      ball.show = true
      ball.el = el
      // dropBalls[]，自定义的变量，下落的小球
      this.dropBalls.push(ball)
      // 找到一个可用的ball，push到dropBalls[]后就可以退出了
      return
    }
  }
},
/* ‘下落动画’前 */
beforeDrop (el) {
  let count = this.balls.length
  while (count--) {
    let ball = this.balls[count]
    if (ball.show) {
      // drop() 里 给 ball添加的el属性（存放点击的加号的DOM）
      // getBoundingClientRect() 浏览器接口，获取【加号】相对于视窗的距离
      let rect = ball.el.getBoundingClientRect()
      // 购物车与加号的水平距离 = 购物车横坐标 - 小球.ball的left大小
      let x = rect.left - 32
      // y 是负数
      // 购物车与加号的垂直距离 = -(窗口高度 - 购物纵坐标 - 小球.ball的bottom大小)
      let y = -(window.innerHeight - rect.top - 22)
      // 先不显示
      el.style.display = ''
      // 外面纵向偏移，内部横向偏移，最终达到整体抛物线的动画
      // 外面的DOM做纵向动画
      // 注意：字符串拼接，有变量的时候不用单引号，用`
      el.style.webkitTransform = `translate3d(0,${y}px,0)`
      el.style.transform = `translate3d(0,${y}px,0)`
      // 内部的DOM做横向动画
      let inner = el.getElementsByClassName('inner-hook')[0]
      inner.style.webkitTransform = `translate3d(${x}px,0,0)`
      inner.style.transform = `translate3d(${x}px,0,0)`
    }
  }
},
/* ‘下落动画’时 */
dropping (el, done) {
  // el.offsetHeight 触发浏览器重绘(当获取一些属性时，浏览器为取得 正确的值会触发重绘重排，如offsetTop、offsetLeft、 offsetWidth、offsetHeight、scrollTop、scrollLeft、scrollWidth、scrollHeight、 clientTop、clientLeft、clientWidth、clientHeight、getComputedStyle() (currentStyle in IE))
  // 触发重绘，下面
  // 但是变量rf不用，所以加个eslint的注释不做变量是否使用的检查
  /* eslint-disable no-unused-vars */
  let rf = el.offsetHeight
  // 重置属性
  this.$nextTick(() => {
    el.style.webkitTransform = 'translate3d(0,0,0)'
    el.style.transform = 'translate3d(0,0,0)'
    let inner = el.getElementsByClassName('inner-hook')[0]
    inner.style.webkitTransform = 'translate3d(0,0,0)'
    inner.style.transform = 'translate3d(0,0,0)'
    el.addEventListener('transitionend', done)
  })
},
/* ‘下落动画’后 */
afterDrop (el) {
  // 把dropBalls的这个元素删除
  let ball = this.dropBalls.shift()
  // 重置小球属性
  if (ball) {
    ball.show = false
    el.style.display = 'none'
  }
}
```

还要在 CSS 里定义 transition 的属性

- transition: 过渡效果的属性 耗时 速度 延迟开始

```
.ball-container
  .ball
    // 配合js写的小球下落的transition，这里定义了完成时间、弧度用贝塞尔曲线速度，来使效果出现抛物线效果
    transition: all 0.4s cubic-bezier(0.49, -0.29, 0.75, 0.41)
    .inner
      // 配合js写的小球下落的transition
      transition: all 0.4s linear
```

  [1]: http://77g54f.com1.z0.glb.clouddn.com/bgt-20170620.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [2]: https://github.com/ustbhuangyi/vue-sell
  [3]: https://github.com/younglaker/CometLab/tree/vue-eleme
  [4]: https://cn.vuejs.org/v2/guide/transitions.html#JavaScript-%E9%92%A9%E5%AD%90