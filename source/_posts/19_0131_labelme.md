---
layout: post
title: Use labelme to annotate image for machine learning
date:   2019-01-31 08:24:00
category: [AI]
tags: [AI, ML]
---

<!-- ![labelme](https://wx4.sinaimg.cn/large/6d184cefgy1fzoyeywzqxj20p0046q3i.jpg) -->


Labelme is a graphical image annotation tool. It is written in Python and uses Qt for its graphical interface. It is open source in Github at [https://github.com/wkentaro/labelme][1]

<!--more-->
## Installation

It can be used in both Python 2 and Python 3. Now, let's use Python 3.

I use Anaconda for machin learning. So in Anaconda :


1. Install conda

![Install conda](https://raw.githubusercontent.com/aomine-sama/px/master/common/19013101.jpg)

If conda is not working in terminal, activate your terminal profile:

```
$ source ~/.zsh_profile
```

![image](https://raw.githubusercontent.com/aomine-sama/px/master/common/19013102.jpg)

2. Create a new environment

Choose a Python version you want.

```
conda create -n labelme python=3.6
```

Then we get a new clean environment for labelme:

![a new clean environment](https://raw.githubusercontent.com/aomine-sama/px/master/common/19013103.jpg)

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

![environment](https://raw.githubusercontent.com/aomine-sama/px/master/common/19013104.jpg))

Python will be the version we chosen:

![Python](https://raw.githubusercontent.com/aomine-sama/px/master/common/19013105.jpg))

The pip also is the labelme version :

![pip](https://raw.githubusercontent.com/aomine-sama/px/master/common/19013106.jpg))

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

![labelme](https://raw.githubusercontent.com/aomine-sama/px/master/common/19013107.jpg))

> Exchange blogroll： [http://laker.me/blog]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )


  [1]: https://github.com/wkentaro/labelme
