---
layout: post
title:  Vue.js 2 高仿饿了么开发及解注六：goods 商品件组
date:   2017-11-20 08:24:00
category: [Vue.js]
tags: [JavaScript,HTML5,Vue.js]
---

![Vue.js 2 高仿饿了么开发及解注六][1]

<!--more-->

> 欢迎交换友链： [laker.me--进击的程序媛]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
> V信: lakerHQ （请注明‘来自博客’）

慕课网早期出了《Vue.js 1 高仿饿了么APP》的课程，本系列文章根据课程，使用 Vue.js 2 版本进行开发，并进行了一步步开发流程记录和详细的代码注解。

[原作者的代码][2]

[我做的含有详细代码注解的版本][3]

---
# 购物车组件

功能： 点击购物车组件（不只是购物车logo，是整个底部的购物车栏），弹出购物车详情列表，可以删减数量、清空购物车。付款功能

`shopcart.vue` 引入并注册 cartcontrol 组件

```
// “添减食品” 组件
import cartcontrol from 'components/cartcontrol/cartcontrol'

  ...
  components: {
    cartcontrol
  }
```

购物车清单HTML：

```
<!-- 点击购物车logo出来的购物列表 -->
<!-- 折叠动画 fold -->
<transition name="fold">

  <!-- 根据 listShow 的值来显示列表 -->
  <div class="shopcart-list" v-show="listShow">
    <div class="list-header">
      <h1 class="title">购物车</h1>
      <span class="empty" @click="empty">清空</span>
    </div>
    
    <!-- 购物清单 -->
    <!-- 定义了 ref="listContent"，可以传入BS插件，滑动购物清单 -->
    <div class="list-content" ref="listContent">
      <ul>
      
        <!-- 展示加进购物车的食品、数量、价钱 -->
        <!-- goods组件传进来的selectFoods -->
        <li class="food" v-for="food in selectFoods">
          <span class="name">{{food.name}}</span>
          <div class="price">
            <span>￥{{food.price*food.count}}</span>
          </div
          
          <div class="cartcontrol-wrapper">
            <!-- “添减食品” 组件 -->
            <!-- 传入当前 food -->
            <cartcontrol @add="addFood" :food="food"></cartcontrol>
          </div>
        </li>
      </ul>
    </div>
  </div>
</transition>
```

购物车清单JavaScript部分
先定义一个购物车清单的折叠的标记

```
data () {
  return {
    ...
    fold: true 
  }
},
```

通过fold来触发计算listShow()，HTML根据listShow()的返回值来展开、折叠

```
<!-- 根据 listShow 的值来显示列表 -->
<div class="shopcart-list" v-show="listShow">

computed: {
  /* 判断购物车详情列表折叠、打开状态 */
  listShow () {
    // 若购物车里没有东西，则折叠标记fold = true，跳出整个函数
    if (!this.totalCount) {
      this.fold = true
      return false
    }

    // 能运行到这里，说明购物车里有东西，fold=false，所以show=true
    let show = !this.fold
    if (show) {
      // 购物清单超过高度，添加 BScroll 插件，可以滑动清单
      this.$nextTick(() => {
        // 如果this.scroll不存在，则创建
        if (!this.scroll) {
          // 传入DOM <div class="list-content" ref="listContent">，定义了 ref="listContent"
          this.scroll = new BScroll(this.$refs.listContent, {
            click: true
          })
        } else { // 如果this.scroll存在，则更新（插件重新计算内容是否超出固定高度来使用滑动）
          this.scroll.refresh()
        }
      })
    }
    return show
  }
},
```

点击触发的展开、折叠：

```
<!-- 底部购物车 -->
<!-- 点击触发折叠/展开购物车清单 -->
<div class="content" @click="toggleList">

<!-- @click="hideList"：点击阴影遮罩，收起购物车清单 -->
<div class="list-mask" @click="hideList" v-show="listShow"></div>

methods: {
  /* 折叠/展开购物车清单 */
  toggleList () {
    // 如果购物车为空，则退出
    if (!this.totalCount) {
      return
    }

    // 此时购物车不为空，点击购物车组件，设置fold为之前的相反值
    this.fold = !this.fold
  },
  /* 收起购物车清单 */
  hideList () {
    // fold值的变化，会触发listShow()重新计算
    this.fold = true
  },
}
```

清空购物车：

```
<span class="empty" @click="empty">清空</span>

/* 清空购物车 */
empty () {
  this.selectFoods.forEach((food) => {
    food.count = 0
  })
}
```

付款：

```
<!-- 结算按钮 -->
<!-- .stop.prevent 阻止事件冒泡，避免点击付款时，触发整个购物条的点击事件（显示购物清单） -->
<div class="content-right" @click.stop.prevent="pay">
  <div class="pay" :class="payClass">
    {{payDesc}}
  </div>
</div>


computed: {

  /* 付款按钮的字样 */
  payDesc () {
    if (this.totalPrice === 0) {
      // ES6字符串拼接： `字符串${变量}字符串` 等同于'字符串'+变量+'字符串'
      // 注意是反引号 ` ，而不是单引号 '
      return `￥${this.minPrice}元起送`
    } else if (this.totalPrice < this.minPrice) {
      // totalPrice是上面的totalPrice()，minPrice是从goods.vue传进来的
      let diff = this.minPrice - this.totalPrice
      return `还差￥${diff}元起送`
    } else {
      return '去结算'
    }
  },
  
  /* 付款按钮的CSS类 */
  payClass () {
    if (this.totalPrice < this.minPrice) {
      return 'not-enough'
    } else {
      return 'enough'
    }
  }
},

methods: {

  /* 付款 */
  pay () {
    // 如果购买金额不足最低消费要求，则退出函数
    if (this.totalPrice < this.minPrice) {
      return
    }
    window.alert(`支付${this.totalPrice}元`)
  }
}
```



  [1]: http://77g54f.com1.z0.glb.clouddn.com/bgt-20170620.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [2]: https://github.com/ustbhuangyi/vue-sell
  [3]: https://github.com/younglaker/CometLab/tree/vue-eleme

