---
layout: post
title: Wechat mini program - start up and homepage
date:   2019-03-06 08:24:00
category: [HTML5]
tags: [HTML5,Front-end,Wechat]
---

<!-- ![Wechat mini program](https://wx2.sinaimg.cn/large/6d184cefly1g0u0mf6a9pj20p00463yw.jpg) -->


## 1. Register an account

Register:
https://mp.weixin.qq.com/cgi-bin/wx

<!--more-->

After register, login in and get AppID to login develop tool.

![AppID](https://wx4.sinaimg.cn/mw690/6d184cefly1fymkjsampgj211g0rwq5v.jpg)

Develop tool:
https://developers.weixin.qq.com/miniprogram/dev/devtools/devtools.html

![Develop tool](https://wx4.sinaimg.cn/mw690/6d184cefly1fymkjx0izpj20ik0qcjsx.jpg)

## 2. app.json

Documents: https://developers.weixin.qq.com/miniprogram/dev/framework/config.html#%E5%85%A8%E5%B1%80%E9%85%8D%E7%BD%AE

### pages
The whole config for mini program.

Add pages url in `pages`, it will add a pakages folders automatically, with `.wxml`, `.wxss`, `.js`,`.json` files:

![pages](https://wx4.sinaimg.cn/mw690/6d184cefly1fymkki4182j20zg0l2afo.jpg)

After saving files, it will refresh and redirect to the first file which means the homepage. We can add a compilation mode to refresh specific page.

![homepage](https://ws3.sinaimg.cn/mw690/6d184cefly1fymkn79brlj20ek0myq4v.jpg)

Generate a QR code to commit remote debug:

![remote debug](https://ws1.sinaimg.cn/mw690/6d184cefly1fymknwkn9yj20h80o6go4.jpg)


### tabBar

![tabBar](https://wx4.sinaimg.cn/mw690/6d184cefly1fymkktawk3j21qa0yqb05.jpg)

```
  "tabBar": {
    "list": [
      {
        "pagePath": "pages/square/square",
        "text": "活动广场",
        "iconPath": "images/icon_square.png",
        "selectedIconPath": "images/icon_square_acted.png"
      },
      {
        "pagePath": "pages/newact/newact",
        "text": "发布活动",
        "iconPath": "images/new_act.png",
        "selectedIconPath": "images/new_act_acted.png"
      },
      {
        "pagePath": "pages/index/index",
        "text": "个人中心",
        "iconPath": "images/icon_my.png",
        "selectedIconPath": "images/icon_my_acted.png"
      }
    ]
  }
```


### windows

![windows](https://ws1.sinaimg.cn/mw690/6d184cefly1fymkn33tr3j21a60egdua.jpg)

```
  "window": {
    "backgroundColor": "#FFFFFF",
    "backgroundTextStyle": "light",
    "navigationBarBackgroundColor": "#F6F6F6",
    "navigationBarTitleText": "WeGo活动行",
    "navigationBarTextStyle": "black"
  }
```


## swiper

https://developers.weixin.qq.com/miniprogram/dev/component/swiper.html

![swiper](https://ws3.sinaimg.cn/mw690/6d184cefly1fymko4ohulj20i20akah7.jpg)

`.wxml`

```

    <!-- Hot activities -->
    <swiper indicator-dots="{{indicatorDots}}"
      autoplay="{{autoplay}}" interval="{{interval}}" duration="{{duration}}">
      <block wx:for="{{hot_list}}" >
        <swiper-item bindtap='goto_details' data-actid="{{item.id}}">
          <!-- Posters -->
          <image src="http://140.143.145.179{{item.post_link}}" class="slide-image" />

          <!-- Titile -->
          <text class="hot_title">{{item.title}}</text>
        </swiper-item>
      </block>
    </swiper>

```

`.js`

Define the data:

```
  data: {
    // show icator dots
    indicatorDots: true,
    // auto play
    autoplay: true,
    // scroll interval
    interval: 3000,
    // stop duration
    duration: 500,
    // hot activities list
    hot_list: []
}
```

Get hot activitis lists by Ajax:

```
onLoad: function (options) {
  var this_obj = this;

  wx.request({
    url: 'xxxx',
    method: "GET",
    header: {
      'Content-Type': 'json'
    },
    data: {
      userID: user_id
    },
    success: function (res) {
      this_obj.setData({
        hot_list: res.data.data.list
      });
    },
    fail: function () {
      console.log("fail");
    }
  });
}
```

## Choose tags

![image](https://ws1.sinaimg.cn/mw690/6d184cefly1fymkoa1e4yj20hm0bywhp.jpg)

`.wxml`

```
<view class='tags_list'>
    <view class='tags_list_title'>标签选择：</view>

    <text class="tags {{current_tag==index?'tags_active':''}}" wx:for="{{tags}}"  data-actname="{{item.name}}" bindtap="selcetTags" data-index ='{{index}}'>{{item.value}}</text>
</view>
```

`.wxss`

```
/* acted tag */
.tags_list .tags_active {
  border: 1px solid #00BF00;
}
```

`.js`

Initial data:

```
  data: {
    // 标签
    tags: [
      { name: 'all', value: '全部' },
      { name: 'party', value: '派对' },
      { name: 'movie', value: '电影' },
      { name: 'sport', value: '健身' },
      { name: 'show', value: '展览' },
      { name: 'exhibition', value: '演出' },
      { name: 'competition', value: '赛事' },
      { name: 'cate', value: '美食' },
      { name: 'others', value: '其他' }
    ],
    // 当前 tag
    current_tag: 0

  }
```

Switch content:

```
selcetTags: function (e) {

  var this_obj = this;

 // Get current tag name
  var current_tagname = e.currentTarget.dataset.actname;

  // Set the tage
  this_obj.setData({
    current_tag: e.currentTarget.dataset.index
  });

  wx.request({
    url: '',
    method: "GET",
    header: {
      'Content-Type': 'json'
    },
    data: {
      userID: app.data.user_id,
      subFilter: current_tagname
    },
    success: function (res) {

      // Rebind act_list
      this_obj.setData({
        act_list: res.data.data.list
      });

    },
    fail: function () {
      console.log("fail");
    }
  });

}
```

## Use wx:for to show lists

![image](https://wx4.sinaimg.cn/mw690/6d184cefly1fymkol36f9j20hc0ge46z.jpg)

```
    <!-- act_list_box -->
    <!-- bindtap='goto_details' to redirect to act detail page -->
    <view class='act_list_box' wx:for='{{act_list}}' bindtap='goto_details' data-actid="{{item.id}}">

      <!-- Poster -->
      <view class='act_img'>
        <image src="http://140.143.145.179{{item.post_link}}" class="act_list_img"/>
      </view>

      <!-- Activities infomation -->
      <view class='act_info'>
        <!-- title -->
        <text>{{item.title}}</text>

        <!-- start_time -->
        <text class="time">{{item.start_time}}</text>

        <!-- join_number/member_limit -->
        <text class='people_number'>{{item.join_number}} / {{item.member_limit}}</text>
      </view>
```
Bind redirect function:

```
  // Redirect to detail page
  goto_details: function(e) {

    var user_id = app.data.user_id;
    var act_id = e.currentTarget.dataset.actid;

    // Convey parameter to detail page
    wx.navigateTo({
      url: '../detail/detail?userID=' + user_id + '&actID=' + act_id
    });
  }
```
> Exchange blogroll： [http://laker.me/blog]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
