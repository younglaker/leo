---
layout: post
title:  First step in Tencent Cloud and Baota Panel
date:   2018-11-13 08:24:00
category: [Server]
tags: [Server,PHP,Tencent Cloud]
---

![Tencent Cloud and Baota Panel](http://wx4.sinaimg.cn/large/6d184cefly1fx7m4l3l8sj20p0046wf0.jpg)

<!--more-->

> Exchange blogroll： [laker.me]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )

## Install Baota Panel in Tencent Cloud

Visit [https://www.bt.cn/][1]:

![bt website][2]

Find the installation command, now we use V5.9 for CentOS. Also you can use other systems you want.

![installation command][3]
```
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install.sh && sh install.sh
```

Open your sever in Tencent Cloud:

![Tencent Cloud][4]

Install Baota Panel:

![Install Baota Panel][5]

Then we get your Baota Panel accout for the server, and login your panel. Here is my serve address, yours is different.

![Baota Panel accout][6]

## New a website in Tencent Cloud

After login your server panel, setup a new website in the server:

![New a website][7]

Add your domain name:

![Add domain name][8]

All done, you can visit it now:

![visit][9]

You can edit files in Tencent Cloud, use cd into the file:

![edit files][10]

```
vi index.html
```

![vi index.html][11]

Save and visit:

![visit][12]


  [1]: https://www.bt.cn/
  [2]: http://wx3.sinaimg.cn/mw690/6d184cefly1fx6o8b5ehnj21ac0ngagg.jpg
  [3]: http://wx2.sinaimg.cn/mw690/6d184cefly1fx6o8jm2wlj21ds0bqn0t.jpg
  [4]: http://wx2.sinaimg.cn/mw690/6d184cefly1fx7k4mtsmvj21k40ncdp9.jpg
  [5]: http://wx4.sinaimg.cn/large/6d184cefly1fx6o938vr1j21go086wgg.jpg
  [6]: http://wx2.sinaimg.cn/mw690/6d184cefly1fx6o9h3n7vj20n608sq46.jpg
  [7]: http://wx1.sinaimg.cn/mw690/6d184cefly1fx6o9z91xpj212g0gmgok.jpg
  [8]: http://wx1.sinaimg.cn/mw690/6d184cefly1fx6oai0mvzj21100i2n01.jpg
  [9]: http://wx1.sinaimg.cn/mw690/6d184cefly1fx6oape3hej215g0uq78v.jpg
  [10]: http://wx1.sinaimg.cn/mw690/6d184cefly1fx6oayqr3fj20ru01ugly.jpg
  [11]: http://wx1.sinaimg.cn/mw690/6d184cefly1fx6ob3u08qj20z00l843a.jpg
  [12]: http://wx4.sinaimg.cn/mw690/6d184cefly1fx6ocgwlzij20ue0ky419.jpg