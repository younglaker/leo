---
layout: post
title:  在windows(VirtualBox)里安装MacOS
date:   2015-07-23 08:24:00
category: [Mac]
---

我使用的设备、软件的参数：

* win7 64bit (Ubuntu下的安装方式和需要的东西一毛一样)
* virtualbox 5.0

从 链接: http://pan.baidu.com/s/1mix2EpU PWD: haxj 下载以下文件

* HackBoot_Mav.iso
* OSXMavericks2.iso  (解压 OSXMavericks2.part1.rar, OSXMavericks2.part2.rar, OSXMavericks2.part3.rar)

<!--more-->

## 安装

### 配置虚机
![clipboard.png](http://segmentfault.com/img/bVmNKs)

至少2048M

![clipboard.png](http://segmentfault.com/img/bVmNKv)

创建虚拟硬盘

![clipboard.png](http://segmentfault.com/img/bVmNKz)

![clipboard.png](http://segmentfault.com/img/bVmNKB)

![clipboard.png](http://segmentfault.com/img/bVmNKD)

我分配了30G，建议20G以上
![clipboard.png](http://segmentfault.com/img/bVmNKG)

设置虚机取消`启用EFI`

![clipboard.png](http://segmentfault.com/img/bVmNKK)

我分配了2个CPU，大家根据自己情况设置;

![clipboard.png](http://segmentfault.com/img/bVmNKU)

显存128，开启3d渲染

![clipboard.png](http://segmentfault.com/img/bVmNK0)

添加`HackBoot_Mav.iso`

![clipboard.png](http://segmentfault.com/img/bVmNK2)

### 安装
开启虚机

![clipboard.png](http://segmentfault.com/img/bVmNK3)

选择菜单中的设备——分配光驱——OSXMavericks2.iso（没有就选择打开文件寻找），按 F5 

![clipboard.png](http://segmentfault.com/img/bVmNK4)


按 Enter 开始安装，可能停在这里一段时间

![clipboard.png](http://segmentfault.com/img/bVmNkA)

选择系统语言

![clipboard.png](http://segmentfault.com/img/bVmNkE)

看到这个界面

![clipboard.png](http://segmentfault.com/img/bVmNkP)

选择实用工具——磁盘工具

![clipboard.png](http://segmentfault.com/img/bVmNkT)

名称处输入“Mavericks”，点击“抹掉”

![clipboard.png](http://segmentfault.com/img/bVmNkO)

回到这个界面，选择磁盘后安装

![clipboard.png](http://segmentfault.com/img/bVmNlc)

静候佳音

![clipboard.png](http://segmentfault.com/img/bVmNlt)

安装成功后，强制关闭虚机，再把`OSXMavericks2.iso`删了，添加`HackBoot_Mav.iso `

![clipboard.png](http://segmentfault.com/img/bVmNK2)

重新启动，选择菜单中的设备——分配光驱——OSXMavericks2.iso（没有就选择打开文件寻找），按 F5 

![clipboard.png](http://segmentfault.com/img/bVmNLi)

再次进入安装系统，这次选实用工具——终端，输入以下命令：

    umount /Volumes/Mavericks
    hdiutil attach /dev/disk0s2 -mountpoint /Volumes/mnt
    cp -rp /Backup/Kexts/ElliottForceLegacyRTC.kext /Volumes/mnt/System/Library/Extensions
    cp -rp /Backup/Kexts/FakeSMC.kext /Volumes/mnt/System/Library/Extensions
    cp -rp /Backup/Kexts/NullCPUPowerManagement.kext /Volumes/mnt/System/Library/Extensions
    chmod -R 0755 /Volumes/mnt/System/Library/Extensions/ElliottForceLegacyRTC.kext
    chmod -R 0755 /Volumes/mnt/System/Library/Extensions/FakeSMC.kext 
    chmod -R 0755 /Volumes/mnt/System/Library/Extensions/NullCPUPowerManagement.kext
    chown -R root:wheel /Volumes/mnt/System/Library/Extensions/ElliottForceLegacyRTC.kext
    chown -R root:wheel /Volumes/mnt/System/Library/Extensions/FakeSMC.kext 
    chown -R root:wheel /Volumes/mnt/System/Library/Extensions/NullCPUPowerManagement.kext
    hdiutil detach /Volumes/mnt

安装内核扩展后, 退出终端后，关机，关虚机。再把`OSXMavericks2.iso`删了，添加`HackBoot_Mav.iso `

![clipboard.png](http://segmentfault.com/img/bVmNK2)

重新启动，不用再换光驱了，方向键选择 Mavericks，回车


![clipboard.png](http://segmentfault.com/img/bVmNLA)

选择国家
![clipboard.png](http://segmentfault.com/img/bVmNEd)

选择你想要的方式：

![clipboard.png](http://segmentfault.com/img/bVmNEk)

登录Apple ID或者跳过：

![clipboard.png](http://segmentfault.com/img/bVmNEu)

各种设置：

![clipboard.png](http://segmentfault.com/img/bVmNEB)

想想就有点小激动~

![clipboard.png](http://segmentfault.com/img/bVmNEP)

登登登登~

![clipboard.png](http://segmentfault.com/img/bVmNE8)

## 一些必要设置

### 设置输入法中英文切换

我的习惯是把输入法中英文切换设为`ctrl+space`。由于冲突，所以先把spotlight设为`ctrl+f`：

![clipboard.png](http://segmentfault.com/img/bVmNHw)


再把切换输入法设为`ctrl+space`，和Windows一样：

![clipboard.png](http://segmentfault.com/img/bVmNHm)

### 设置可安装非App Store
设置->安全与隐私

![clipboard.png](http://segmentfault.com/img/bVmNHE)

## 免除从 HackBoot_Mav.iso启动
用safati下载 http://pan.baidu.com/s/1hqixcZq 安装：


![clipboard.png](http://segmentfault.com/img/bVmNIK)

![clipboard.png](http://segmentfault.com/img/bVmNIN)

安装成功后关掉mac os和虚拟机

![clipboard.png](http://segmentfault.com/img/bVmNJt)

现在打开设置，原来的`HackBoot_Mav.iso`，如果它还在，可以手动删除，下次开机就可以直接打开mac os了。

如果不行，就把这个勾上：

![clipboard.png](http://segmentfault.com/img/bVmNLE)

> 据说由于虚拟机不支持 Apple Quartz Extreme/Core Image, 需要 Quartz Extreme 的应用软件例如 iBooks Author，Pixelmator，SketchBook 等不能在虚拟机下使用 

参考：[在 Win 7 下使用 VirtualBOX 虚拟机安装 OS X 10.9 Mavericks 及 Xcode 5][1]

  [1]: http://bbs.feng.com/read-htm-tid-7625465.html
