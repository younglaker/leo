---
layout: post
title:  Hexo3+Github搭建免费博客（五）七牛图床
date:   2015-07-27 08:24:00
category: [Hexo]
comments: true
---

业内比较有名的有又拍和七牛。SegmentFault用又拍，感觉经常无法显示。认识七牛的朋友，有问题可以直接找他，感觉比较靠谱。

[七牛][1]的免费额度挺高的：

* 10GB永久免费存储空间   
* 每月10GB下载流量
* 每月10万次Put请求
* 每月100万次Get请求

<!--more-->

##开通空间
注册账号后开通**公开**空间，这个空间名就是以后常提到的Bucket name。

关闭图片保护

下载同步工具[qrsbox][2]

[登录七牛开发者自助平台，查看 Access Key 和 Secret Key][3]

![找密钥][4]

进行配置同步工具：

![配置同步工具][5]

工具就会自动监测文件夹并上传，很快就能到七牛的内容管理里获取外链地址。

![外链][6]

##问题解决
###同步工具无法使用？
我刚开始用的时候，上传失败，问了七牛小伙伴，ping了七牛地址，返回IP不是他们的，所以怀疑被运营商劫持，修改hosts就好了。

`C:\Windows\System32\drivers\etc\hosts`添加:

    115.231.182.136 up.qiniu.com
    183.136.139.10 up.qiniu.com

###上传的图片没有看到水印？
水印是实时生成的，不是生成好放在那里的

###本地删除文件后，远端是否也删除了？
不是。qrsbox不同于dropbox，属于单向同步，本地文件删除不影响远端。

  [1]: https://portal.qiniu.com/signup?code=3l89z2x4en0wi
  [2]: http://devtools.qiniu.io/qiniu-devtools-windows_386-current.zip
  [3]: https://portal.qiniu.com/setting/key
  [4]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150727143821.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjMucG5n/dissolve/100/gravity/SouthWest/dx/5/dy/5
  [5]: http://77g54f.com1.z0.glb.clouddn.com/ikbear_1437976339441_56.jpg?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjMucG5n/dissolve/100/gravity/SouthWest/dx/5/dy/5
  [6]: http://77g54f.com1.z0.glb.clouddn.com/QQ20150727153031.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjMucG5n/dissolve/100/gravity/SouthWest/dx/5/dy/5