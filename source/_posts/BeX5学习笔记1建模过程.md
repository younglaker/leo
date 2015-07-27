---
layout: post
title:  BeX5学习笔记（一）建模过程
date:   2015-07-27 08:24:00
category: [ERP,BeX5]
---

最近公司要开发ERP系统，看中这个开发工具，所以学习一下。

## 关于

[BeX5][1] – 专业、强大的企业快速开发平台

* 定位：开发面向企业和政务的信息化系统和管理软件系统
* 适用：OA/HR/CRM等各类管理软件，电子政务及各行业管理软件
* 前端：安卓app/苹果app/微信服务号/PC web app
* 后端：工作流、报表、组织机构、业务逻辑等能力，j2ee框架
* 费用：按企业用户数收费，20用户免费，商业版收费

<!--more-->

##前期准备
[下载后][2]，打开这三个工具并保持窗口打开：

![clipboard.png](http://segmentfault.com/img/bVmQq2)


## 文件结构

* BIZ：建模所用
* UIZ：界面
* Native：本地应用

##开始
###新建一个ERP应用

右键BIZ，新建应用，一个文件夹就是一个应用：

![clipboard.png](http://segmentfault.com/img/bVmOJq)

![clipboard.png](http://segmentfault.com/img/bVmOJB)

###建业务模块
右键应用，新建业务模块

![clipboard.png](http://segmentfault.com/img/bVmOJv)

![clipboard.png](http://segmentfault.com/img/bVmOJw)

###数据建模
右键ontology文件夹，新建ontology

![clipboard.png](http://segmentfault.com/img/bVmOJL)

![clipboard.png](http://segmentfault.com/img/bVmOKa)

####添加概念和关系
这里概念就是数据表，关系就是字段。
添加一个“物品信息”概念和4个关系：

![clipboard.png](http://segmentfault.com/img/bVmOJZ)

####生成数据库表

保存刚刚的设置后，点击“生成数据库表”tab下的添加，生成3个标准动作，一直下一步。

![clipboard.png](http://segmentfault.com/img/bVmOKq)

###流程建模

![clipboard.png](http://segmentfault.com/img/bVmOL2)

###给流程添加权限
这里process就是流程，acivity就是环节。
选中动作设置，添加上面添加的那3个动作;

![clipboard.png](http://segmentfault.com/img/bVmOM5)

##做界面

###新建W文件
在`UIZ > erp > buy > process > goods`右键文件夹，新建W文件：

![clipboard.png](http://segmentfault.com/img/bVmOMW)

###配置W文件
如图选择：
![clipboard.png](http://segmentfault.com/img/bVmONt)

在主数据tab的概念里，添加我们刚做的物品信息表（ER_WPXX）其他选项就自动带出:

![clipboard.png](http://segmentfault.com/img/bVmONw)

列表视图添加version以外的字段：

![clipboard.png](http://segmentfault.com/img/bVmONB)

详细视图添加version以外的字段：

![clipboard.png](http://segmentfault.com/img/bVmONC)

添加好后点击完成得到这样的界面：

![clipboard.png](http://segmentfault.com/img/bVmONP)

生成的W文件，和对应流程的环节名相同

![clipboard.png](http://segmentfault.com/img/bVmQpB)

##把功能挂出来

`UIZ/erp/config/erp.function.xml`

* “添加顶层菜单目录” erp
* “添加功能菜单选项”，选择goods，改名为“物品信息维护”

![clipboard.png](http://segmentfault.com/img/bVmQqr)

##在网站上开放功能

访问 http://127.0.0.1:8080/ （之前开启`启动BeX5运行平台.bat`、`启动MySQL数据库.bat`），管理员用户名：system， 密码：123456

###新增角色
进入后，到`组织权限/角色管理`新增功能角色“ERP管理员”，并给这个角色新增`/ERP/物品信息维护`

![clipboard.png](http://segmentfault.com/img/bVmQrP)

###授权
`按组织授权->起步软件->system->分配角色->ERP管理员`

![clipboard.png](http://segmentfault.com/img/bVmQsA)

重新登录网站

就可以看到刚制作的功能：

![clipboard.png](http://segmentfault.com/img/bVmQsN)

##小结

框架采用Bootstrap，在现有的企业级应用里算是蛮前卫了，趁着这个机会，推动公司员工浏览器升级换代。建站也很方便快捷。值得继续探索~


  [1]: http://wex5.com/cn/
  [2]: http://wex5.com/cn/downloads/