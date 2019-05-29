---
layout: post
title:  AI 学习1	：Anaconda 配置
date:   2018-10-04 08:24:00
category: [AI]
tags: [Algorithm,人工智能,AI,ML,DL]
---

<!-- ![AI 学习：Anaconda 配置][1] -->


## 安装

本文环境是 Mac OS。

目前Anaconda 出了 Python3.7 版本，但 TensorFlow 只支持3.5、3.6、2.7。有两种解决方案。

<!--more-->
- 方案一：

安装3.7版，再根据官方推荐的方法安装3.5、3.6。

http://docs.anaconda.com/anaconda/faq/#how-do-i-get-anaconda-with-python-3-5-or-3-6

> We recommend that you download the latest version of Anaconda and then [make a Python 3.5 (or 3.6) environment][2].
> Or download the latest version of Anaconda and run the following command to install Python 3.5 (or 3.6) in the root environment: conda install python=3.5
or

> `conda install python=3.6`

> Or download the most recent Anaconda installer that included Python 3.5 (Anaconda 4.2.0) or Python 3.6 (Anaconda 5.2.0). You can download either of these from our [archive][3]. Scroll down the page until you find the version you need for your platform.

命令行执行：

```
$ conda install python=3.6

```

命令：

> 开启环境
> $ source activate py36

> 关闭环境
> $ source deactivate

开启环境

```
$ source activate py36
(py36)

$ conda info --envs
# conda environments:
#
base                     /Users/laker/anaconda3
Laker                    /Users/laker/anaconda3/envs/Laker
py36                  *  /Users/laker/anaconda3/envs/py36

(py36)
```
我尝试了这个方法，最后3.6是安装成功了，但是客户端打不开了，尝试了网上解决闪退的办法未果，貌似这是个通病。折腾了一上午也没搞好，折腾到崩溃，之后卸载采取第二种方案

- 方案二：

到清华镜像下载以往版本，官网也有，但是慢。

https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/

安装好后，Anaconda 自带 Python 环境，与 Mac 自身的不相干。
## 换源

安装后尝试如下命令

     conda --version


如果出现

    $ conda --version
    conda 4.3.30


表示安装成功，如果没有，则需配置环境变量
修改`.bash_profile` 或 `zsh_profile`，我用的 zsh

    vi ~/.zsh_profile

添加以下命令

    export PATH="/Users/nick(你自己的安装路径)/anaconda3/bin:$PATH"


vim使用`:wq`命令保存退出
保存文件后如要立即生效，输入以下命令，

    source $HOME/.zsh_profile

> 注意：重启机子后也可能要执行这个

再次测试`conda --version`命令是否安装成功.

如果成功，我们继续用以下命令修改conda的镜像源，这里用清华的源。输入以下两条命令来添加源：

    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
    conda config --set show_channel_urls yes

此时~/下会生成.condarc文件。

用`vi ~/.condarc`命令进入vim编辑器，删除其中的第三、第四行，即删除了默认的源，然后`:wq`保存：

    channels:
      - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
      - defaults #删除
    ssl_verify: true #删除
    show_channel_urls: true

`conda info` 查看当前配置信息，channel URLs只剩下清华的源

```
channel URLs : https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/osx-64
    https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/noarch
```

## 安装 TensorFlow

注意，这里是用 Anaconda 的 pip，不是本机的 pip，所以 pip 前加上路径

更新 pip
```
$ ~/anaconda3/bin/pip install --upgrade pip
```

更新 TensorFlow

```
$ ~/anaconda3/bin/pip install --upgrade --ignore-installed tensorflow
```

可能会有一段黄色警告，再多等会，或者开代理

```
# laker @ Laker in ~ [13:11:43]
$ ~/anaconda3/bin/pip install --upgrade --ignore-installed tensorflow
Collecting tensorflow
  Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'NewConnectionError('<pip._vendor.urllib3.connection.VerifiedHTTPSConnection object at 0x11021c828>: Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known',)': /simple/tensorflow/
  Retrying (Retry(total=3, connect=None, read=None, redirect=None, status=None)) after connection broken by 'NewConnectionError('<pip._vendor.urllib3.connection.VerifiedHTTPSConnection object at 0x110067a58>: Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known',)': /simple/tensorflow/
  Retrying (Retry(total=2, connect=None, read=None, redirect=None, status=None)) after connection broken by 'NewConnectionError('<pip._vendor.urllib3.connection.VerifiedHTTPSConnection object at 0x110067ac8>: Failed to establish a new connection: [Errno 65] No route to host',)': /simple/tensorflow/
  Downloading https://files.pythonhosted.org/packages/70/78/cd74769027b6249e45807637c1aa3ef212b9492349cca4b87e5de1a10548/tensorflow-1.11.0-cp36-cp36m-macosx_10_11_x86_64.whl (59.3MB)
    9% |███                             | 5.4MB 96kB/s eta 0:09:20
```



## 安装Jupyter, Spyder

![Jupyter,spyder][4]

## 测试环境

下载测试文件
链接:https://pan.baidu.com/s/1U_P1VsJyJ3Zn8SAprz9Sxw 提取码: vtaf

安装测试文件的依赖库 pygame

    $ ~/anaconda3/bin/pip install pygame

运行Jupyter，点击面板的 Launch，

![Jupyter][5]

或者输入命令

    ipython notebook

找到文件所在位置

![Jupyter界面][6]

进入`homework0.ipynb`，运行

![homework0.ipynb][7]

效果是两个特效的窗口

![效果][8]

参考：
[Anaconda之Python环境配置][9]
[Add PATH][10]


> 欢迎交换友链： [laker.me--进击的程序媛]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
> V信: lakerHQ （请注明‘来自博客’）

  [1]:https://raw.githubusercontent.com/aomine-sama/px/master/2018/18100401.jpg
  [2]: https://conda.io/docs/py2or3.html
  [3]: https://repo.anaconda.com/archive/
  [4]:https://raw.githubusercontent.com/aomine-sama/px/master/2018/18100402.jpg
  [5]:https://raw.githubusercontent.com/aomine-sama/px/master/2018/18100403.jpg
  [6]:https://raw.githubusercontent.com/aomine-sama/px/master/2018/18100404.jpg
  [7]:https://raw.githubusercontent.com/aomine-sama/px/master/2018/18100405.jpg
  [8]:https://raw.githubusercontent.com/aomine-sama/px/master/2018/18100406.jpg
  [9]: https://www.jianshu.com/p/b9eac8419c8d
  [10]: http://docs.anaconda.com/anaconda/faq/#should-i-add-anaconda-to-the-macos-or-linux-path