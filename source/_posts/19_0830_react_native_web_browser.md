---
layout: post
title: React native web browser
date: 2019-08-30 08:24:00
category: [React]
tags: [React, React Native]
---

## Method 1: react-native-web

[https://github.com/necolas/react-native-web](https://github.com/necolas/react-native-web)

Android emulator lists:

<!--more-->

```
emulator -list-avds
```

Run emulator

```
emulator -avd [name]
```

Installation:

```
npm install react-web-cli -g
```

---

## Method 2: expo (recommanded)

[https://docs.expo.io/versions/latest/introduction/running-in-the-browser/](https://docs.expo.io/versions/latest/introduction/running-in-the-browser/)

Ensure your project has at least expo@^33.0.0 installed.

```
$ npm i -g expo-cli

//Add web dependencies:
$ yarn add react-native-web react-dom

$ expo start --web
```

Running the expo and copy the homepage url:

![expo](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19093001.png)

Or find the url in terminal:

![terminal](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19093003.png)

Visit the url :

![Visit](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19093002.png)

> Exchange blogroll： [http://laker.me/blog](http://laker.me/blog)
> Github：[https://github.com/younglaker](https://github.com/younglaker)
