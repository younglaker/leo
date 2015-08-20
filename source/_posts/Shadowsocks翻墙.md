---
layout: post
title:  Shadowsocks 翻墙利器 科学上网
date:   2015-08-04 08:24:00
category: [科学上网]
---

[shadowsocks-windows][1] shadowsocks-windows github的下载地址。但由于是存储在AWS，所以还是要翻墙下不了。这里在百度云[备份了一个Windows版本][2]可供使用。

朋友黑帝做了个网站[艹墙爱好者协会][3]，提供免费代理服务。请勿滥用。在网站找个邀请码，注册登录。

个人中心 -> 节点列表 -> 找到节点二维码

![找到节点二维码][4]

<!-- more -->

右键shadowsocks -> 服务器 -> 扫描屏幕二维码

![扫描屏幕二维码][5]

shadowsocks会自动获取代理信息

![获取代理信息][6]

开启服务，并选用PAC模式

![此处输入图片的描述][7]

chrome安装插件SwitchyOmega，填写代理服务器如下

![插件SwitchyOmega][8]

更新规则

![更新规则][9]


规则地址是 https://autoproxy-gfwlist.googlecode.com/svn/trunk/gfwlist.txt

![规则地址][10]

如果在线更新不成功，下载这个[OmegaOptions.bak][11]提交

![本地上传][12]

插件选择自动切换模式即可

![成功][13]


  [1]: https://github.com/shadowsocks/shadowsocks-windows/releasesps://github.com/shadowsocks/shadowsocks-windows/releases
  [2]: http://pan.baidu.com/s/1mgkYHmw
  [3]: http://bilibilo.in/
  [4]: http://77g54f.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20150819155234.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [5]: http://77g54f.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20150819163548.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [6]: http://77g54f.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20150819155359.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [7]: http://77g54f.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20150819164122.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10
  [8]: http://77g54f.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20150819153102.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [9]: http://77g54f.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20150819152243.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [10]: http://77g54f.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20150819153024.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [11]: http://pan.baidu.com/s/1mgkYHmw
  [12]: http://77g54f.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20150819154907.png
  [13]: http://77g54f.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20150819155040.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10