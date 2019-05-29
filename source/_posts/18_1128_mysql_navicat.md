---
layout: post
title:  MySql and Navicat in MacOS
date:   2018-11-28 08:24:00
category: [SQL]
tags: [Server,MySql,Navicat]
---

<!-- ![MySql and Navicat in MacOS](http://wx3.sinaimg.cn/large/6d184cefly1fxnkwna76bj20oz0460tc.jpg) -->


## Install MySql

### Method one

Download the installation file, choose the dmg file:

<!--more-->
https://dev.mysql.com/downloads/mysql/

Then install the package step by step.

### Method two

Install by command line:

```
brew install mysql
```

## Start MySql

### Add system enviroment

Open terminal, I use zsh, so I edit zsh_profile, if you use bash, edit your bash_profile:

    $ vim ~/.zsh_profile

Add zsh_profile

    $ source ~/.zsh_profile

### Login database

Your can use GUI to start or stop sever in system preference :

![manage][1]

Or use command line.

## Connect to Navicat


New MySQL connection:

![connection][2]

Set a name and add password:

![config][3]

Done:

![success][4]

## Import sql file:

Import sql file:

![Import][5]

Done, I uesd about 30 minutes to import 2kw items, much faster than my classmates, most of them cost several hours :

![Done][6]


> Exchange blogroll： [laker.me]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )


  [1]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18112801.jpg
  [2]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18112802.jpg
  [3]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18112803.jpg
  [4]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18112804.jpg
  [5]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18112805.jpg
  [6]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18112806.jpg