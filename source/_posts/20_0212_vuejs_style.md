---
layout: post
title: Vuejs style 计算属性 样式绑定 动态属性
date:   2020-02-12 08:24:00
category: [Vue.js]
tags: [Vue.js,Web]
---


## 目标

动态设置进度条宽度

<!--more-->

![进度条](https://raw.githubusercontent.com/aomine-sama/px/master/2019/20021201.png)


文档
 [[https://cn.vuejs.org/v2/guide/class-and-style.html#绑定内联样式](https://cn.vuejs.org/v2/guide/class-and-style.html#%E7%BB%91%E5%AE%9A%E5%86%85%E8%81%94%E6%A0%B7%E5%BC%8F)
](https://cn.vuejs.org/v2/guide/class-and-style.html#%E7%BB%91%E5%AE%9A%E5%86%85%E8%81%94%E6%A0%B7%E5%BC%8F)
[https://cn.vuejs.org/v2/guide/computed.html](https://cn.vuejs.org/v2/guide/computed.html)



## 方法一

绑定样式`:style`

read_page、total_page是两个参数
```
<view class="filled" :style="{ width: read_page / total_page * 100 + '%'}"></view>
```

## 方法二

注意

- :style= 的方法countWidth后不能加()
- 使用 computed ，不是methods
- return 'width: 20%; height: 30px'，不是return {width: 20%; height: 30px  }

```
<view class="filled" :style="countWidth"></view>

  computed: {
    countWidth: function () {
      return 'width: 20%; height: 30px'
    }
  }
```

参考
[https://juejin.im/post/5d5b87bc6fb9a06b1417e651](https://juejin.im/post/5d5b87bc6fb9a06b1417e651)
[https://blog.csdn.net/freedomVenly/article/details/80752215](https://blog.csdn.net/freedomVenly/article/details/80752215)
[https://segmentfault.com/q/1010000008835283](https://segmentfault.com/q/1010000008835283)


> Exchange blogroll： [http://laker.me/blog]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )

