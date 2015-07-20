---
layout: post
title:  HTML5 Web Speech API，让网站更有趣
date:   2015-02-05 08:24:00
category: [翻译,HTML5]
---

![clipboard.png](http://segmentfault.com/img/bVkOoy)

Web API 变得越来越丰富，其中一个值得注意的是`Web Speech` API。传统的网站只能“说”，这个API的出现，让网站能“倾听”用户。这个功能已经开放了一系列的用法，非常棒。

在这篇文章中，我们将看一下这项技术和建议的用法，以及如何用它来增强用户体验的一些好例子。

<!--more-->

> 声明：本技术比较前沿，目前该规范是W3C的“非官方编辑器的征求意见稿”（截至2014年6月6日）。它的使用方法可能和本文中的代码片有所不同。查看代码规范和发布前的测试是很有必要的。

##语音合成 Speech Synthesis
该API分为两部分。首先，让我们来看看语音的合成部分——说话。如果你的网站有一些文字内容——文章主体、表单、输入框、标签等——你可以运行一些有趣的功能，设备就会把文字读给用户听。

来看看做到这一点所需要的代码。首先创建`SpeechSynthesisUtterance`接口的新实例。然后指定要阅读的文本。再把这个实例添加到队列中，告诉浏览器什么时候说话。

下面的speak函数里完成了上面所述的功能 ，把想要朗读的内容作为参数。

```
function speak(textToSpeak) {
   //创建一个 SpeechSynthesisUtterance的实例
   var newUtterance = new SpeechSynthesisUtterance();

   // 设置文本
   newUtterance.text = textToSpeak;

   // 添加到队列
   window.speechSynthesis.speak(newUtterance);
}
```

现在我们需要做的就是调用这个函数，并传入我们想要朗读的内容：

    speak('Welcome to Smashing Magazine');

`SpeechSynthesisUtterance`还有开始、暂停、停止功能，还能设置语言、速度、声音。停止、启动或暂停都触发一个事件，开发者可以编写这个事件来完成很多有趣的事情。

目前，语音合成只有Chrome和Safari（包括桌面和移动设备版）支持。此外，通过API提供给用户的声音在很大程度上取决于操作系统。谷歌有自己的一套给Chrome的默认声音，可以在Mac OS X，Windows和Ubuntu上使用。Mac OS X的声音也可用，所以和OSX的Safari的声音一样。你可以通过开发者工具的控制台看有哪种声音可用。

    window.speechSynthesis.getVoices();
    
**如果你使用OS X，可以用“Zarvox”声音**

##语音识别 Speech Recognition
Web Speech API另一部分是语音识别，它能够识别用过从麦克风或网站应用获取的语音。

让我们通过一些代码运行。这一次，我们将创建`SpeechRecognition`的新实例。因为这部分只得到了Chrome的支持，所以要添加WebKit的前缀。

    var newRecognition = webkitSpeechRecognition();

`peechRecognition`有相当多的属性。比如状态是可连续的，浏览器在没有接收到声音的一段时间后默认把状态设为`false`，如果你想继续听，可以设为`true`。

    newRecognition.continuous = true;

开启和停止语音识别，使用`start()` 、 `stop()`：

    // 开始
    newRecognition.start();
    
    // 停止
    newRecognition.stop();
    
还可以绑定很多事件，例如：`soundstart`、`speechstart`、`result` 、 `error`。[看看这个demo][1]。

##使用场景举例
### 听写

目前，Speech API最常见的用法是听写和读取。也就是用户通过麦克风说话，设备把语音翻译成文字（看看[Chrome开发团队做的demo][2]），或者设备读取文字转化成语音。

设备能说话这是非常有用的功能。设想一下，当你早上起床的时候，镜子告诉你今天的天气，这多么神奇。

很多汽车都有语音系统，在你开车的时候给你导航。设想一下，当你在开车的时候，浏览器把你想要的内容读给你听，多么方便。

###声音控制
听写可以很容易地变成语音控制。正如上面的例子，我们可以通过语音导航。如果把这个功能加入到网络电视的浏览器中，将会有更多有意思的实现。

我的同事做了个网球应用，在他打球的时候，它的应用会把他的分数读出来。

###翻译
未来翻译会变得很不一样。一个人说了一段话，设备就翻译成对方的语言并读出。

##限制
离线是需要注意的问题。目前API的实现是浏览器把数据发送到远端服务器，再把处理好的数据返回。没有网络就无法实现功能。

---

> 英文原文： [Enhancing User Experience With The Web Speech API][3]

> 本文是我为 [SegmentFault](http://segmentfault.com/a/1190000002538321/) 所译

  [1]: http://codepen.io/Rumyra/pen/bCphe
  [2]: https://www.google.com/intl/en/chrome/demos/speech.html
  [3]: http://www.smashingmagazine.com/2014/12/05/enhancing-ux-with-the-web-speech-api/
