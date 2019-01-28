---
layout: post
title: Use labelme to annotate image for machine learning
date:   2019-01-31 08:24:00
category: [AI]
tags: [AI, ML]
---

![labelme](https://wx4.sinaimg.cn/large/6d184cefgy1fzoyeywzqxj20p0046q3i.jpg)

<!--more-->

> Exchange blogroll： [http://laker.me/blog]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )

Labelme is a graphical image annotation tool. It is written in Python and uses Qt for its graphical interface. It is open source in Github at [https://github.com/wkentaro/labelme][1]

## Installation

It can be used in both Python 2 and Python 3. Now, let's use Python 3.

I use Anaconda for machin learning. So in Anaconda :


1. Install conda

![Install conda](https://ws1.sinaimg.cn/mw690/6d184cefgy1fzoxcwooe8j21gi118tf0.jpg)

If conda is not working in terminal, activate your terminal profile:

```
$ source ~/.zsh_profile
```

![image](https://wx4.sinaimg.cn/mw690/6d184cefgy1fzoxl24g3xj20u00hsn1u.jpg)

2. Create a new environment

Choose a Python version you want.

```
conda create -n labelme python=3.6
```

Then we get a new clean environment for labelme:

![a new clean environment](https://wx2.sinaimg.cn/mw690/6d184cefgy1fzoxfcd0ixj20qu0em0u3.jpg)

3. Install labelme

Active the environment :

```
activate labelme
```

If not worked and show `zsh: command not found: activate`, add `source` like this:

```
source activate labelme
```

We will in the labeme environment.

![environment](https://ws4.sinaimg.cn/mw690/6d184cefgy1fzoxip1hzrj20ka03y74r.jpg)

Python will be the version we chosen:

![Python](https://ws1.sinaimg.cn/mw690/6d184cefgy1fzoxon8x00j20ni050mxv.jpg)

The pip also is the labelme version :

![pip](https://ws2.sinaimg.cn/mw690/6d184cefgy1fzoxowgvazj219k0500tv.jpg)

Install labelme:

```
$ pip install labelme
```

## Use labelme

Input:

```
$ labelme
```

or:

```
$ labelme # Open GUI
```

![labelme](https://wx3.sinaimg.cn/mw690/6d184cefgy1fzoy0my8ghj21no136hdt.jpg)


  [1]: https://github.com/wkentaro/labelme
