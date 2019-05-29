---
layout: post
title: Django Enviroment in Tencent Cloud Ubuntu
date:   2018-12-28 08:24:00
category: [Python]
tags: [Server,Python,Django,MySql,Tencent Cloud]
---

<!-- ![Django Enviroment in Tencent Cloud Ubuntu][1] -->



## Enviroment:

- MacOS
- Tencent Cloud Ubuntu 18.04
- Python 3.6
- Django 2.0

<!--more-->
## Connect to server


![Connect via SSH][2]

In MacOs, it's very easy to connect to the server. In terminal :

```
ssh -q -l ubuntu -p [port] [ip]
```

Like `ssh -q -l ubuntu -p 20 188.131.***.***`.

Login with password.

## Python

In Ubuntu18.04, there are two versions of Pyhton: 2.7 and 3.6. The default version is 2.7, If you don't want to change, then skip following steps.

Alter to python3.6:

```
$ sudo update-alternatives --install /usr/bin/python python /usr/bin/python2 100
$ sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 150

```

Check whether it successes:

```
$ python --version
Python 3.6.7
```

## Django

Install pip:

```
$ sudo apt install python3-pip
```

Check whether it successes:

```
$ pip --version
pip 9.0.1 from /usr/lib/python3/dist-packages (python 3.6)
```

Install specific Django version :

```
$ sudo pip install Django==2.1.2
```

Create a project

```
cd /data
sudo django-admin startproject helloworld
```

Modify the write permission for everyone :

```
sudo chmod 666 /data/helloworld/helloworld/settings.py
```

Edit the settings:

```
$ cd helloworld/helloworld/
$ vim settings.py
```

Add your IP in `ALLOWED_HOSTS = []` to  `ALLOWED_HOSTS = ["188.131.***.***"]`

Save and quit vim:
```
:wq
```


Open port 8080 in Baota Panel:

![Open port 808](https://raw.githubusercontent.com/aomine-sama/px/master/2018/18122802.jpg)


Or set in Tencent Cloud:

![Open port 808][3]

Run the project :

```
$ cd ../
$ sudo python manage.py runserver 0.0.0.0:8080
```

Visit the website:

![website][4]

Reference:
[ubuntu + nginx + uwsgi + django(python3)][5]
[python3+Django][6]

> Exchange blogroll： [http://laker.me/blog]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )


  [1]: http://wx4.sinaimg.cn/large/6d184cefly1fxvvjn56zij20p004675r.jpg
  [2]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18122801.jpg
  [3]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18122803.jpg
  [4]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18122804.jpg
  [5]: https://www.bt.cn/bbs/thread-8889-1-3.html
  [6]: https://www.cnblogs.com/dalanjing/p/8636338.html