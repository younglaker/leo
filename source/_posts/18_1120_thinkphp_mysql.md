---
layout: post
title:  Install ThinkPHP in Tencent Cloud
date:   2018-11-20 08:24:00
category: [Server]
tags: [Server,PHP,ThinkPHP,MySql,Tencent Cloud]
---

<!-- ![Tencent Cloud and Baota Panel](http://wx4.sinaimg.cn/large/6d184cefly1fx7m4l3l8sj20p0046wf0.jpg) -->


## Installation

Install ThinkPHP 5 in Baota Panel:

<!--more-->
![ThinkPHP][1]

Choose ThinkPHP

![ThinkPHP][2]

Add your server infomation:

![server infomation][3]

Finish installation

![Finish][4]

You can visit your website now:

![visit][5]

You can edit the welcome message:

![edit][6]

## Create a database table

Manage your database:

![database][7]

Enter phpMyadmin:

![phpMyadmin][8]

Create a user table:

![user table][9]

Insert  a data for admin user:

- name: admin
- pwd: 21232f297a57a5a743894a0e4a801c3 (admin)

## Create a login page

Connect ThinkPHP to database:

![Connect][10]

Edit config file for debug pattern:

![config][11]

Add a view file:

![view][12]

`application/index/view/login/index.html`

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login system</title>
    <link href="/static/bootstrap/css/bootstrap.min.css" rel="stylesheet">
</head>

<body class="gray-bg">
<div class="container">
  <div class="row">
      <div class="col-sm-7">
          <div class="ibox float-e-margins">
              <div class="ibox-content">
                  <div class="row">
                      <div class="col-sm-6 b-r">
                          <h3 class="m-t-none m-b">Login</h3>
                          <p>Welcome (⊙o⊙)</p>
                          <form role="form" action="{:url('login/dologin')}" method="post">
                              <div class="form-group">
                                  <label>Useranme</label>
                                  <input type="text" placeholder="Input your name" class="form-control" name="user_name">
                              </div>
                              <div class="form-group">
                                  <label>Password</label>
                                  <input type="password" placeholder="Input your password" class="form-control" name="user_pwd">
                              </div>
                              <div>
                                  <button class="btn btn-sm btn-primary pull-right m-t-n-xs" type="submit"><strong>Login</strong>
                                  </button>
                              </div>
                          </form>
                      </div>
                  </div>
              </div>
          </div>
      </div>
  </div>
</div>
<script src="/static/js/jquery.min.js?v=2.1.4"></script>
<script src="/static/bootstrap/js/bootstrap.min.js"></script>
</body>
</html>
```

Add controller Login:
`application/index/controller/Login.php`

```
<?php
namespace app\index\controller;

use think\Controller;

class Login extends Controller
{
    public function index()
    {
    // Deal with login
      return $this->fetch();

    }
    public function doLogin()
    {
      $param = input('post.');
      if(empty($param['user_name'])){

        $this->error('Username can't be null');
      }

      if(empty($param['user_pwd'])){

        $this->error('Password can't be null');
      }

      // Check username
      $has = db('users')->where('user_name', $param['user_name'])->find();
      if(empty($has)){

        $this->error('Usename or password is wrong');
      }

      // Check password
      if($has['user_pwd'] != md5($param['user_pwd'])){

        $this->error('Usename or password is wrong');
      }

      // Remember the user infomation
      cookie('user_id', $has['id'], 3600);  // One month's validity period
      cookie('user_name', $has['user_name'], 3600);

      $this->redirect(url('index/index'));
    }
}

```
Visit：

![Success][13]

> Exchange blogroll： [laker.me]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )


  [1]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18112001.jpg
  [2]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18112002.jpg
  [3]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18112003.jpg
  [4]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18112004.jpg
  [5]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18112005.jpg
  [6]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18112006.jpg
  [7]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18112007.jpg
  [8]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18112008.jpg
  [9]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18112009.jpg
  [10]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18112010.jpg
  [11]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18112011.jpg
  [12]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18112012.jpg
  [13]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18112013.jpg