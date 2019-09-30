---
layout: post
title: React native 加 android安卓模拟器
date: 2019-09-03 08:24:00
category: [React]
tags: [React, React Native]
---

[https://expo.io/learn](https://expo.io/learn)

```
npm install -g expo-cli
expo init my-new-project
```

<!--more-->

下载网易 mumu 安卓模拟器
[https://mumu.163.com/](https://mumu.163.com/)

[http://mumu.163.com/2017/12/19/25241_730476.html?type=notice](http://mumu.163.com/2017/12/19/25241_730476.html?type=notice)
添加 adb，执行

```
$ adb kill-server && adb server && adb shell
```

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090301.png)

查看

```
$ adb devices
```

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090302.png)

开启模拟器 USB 调试模式

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090303.png)

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090304.png)

开启项目

```
cd my-new-project
expo start
```

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090305.png)

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090306.png)

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090307.png)

> Exchange blogroll： [http://laker.me/blog](http://laker.me/blog)
> Github：[https://github.com/younglaker](https://github.com/younglaker)
