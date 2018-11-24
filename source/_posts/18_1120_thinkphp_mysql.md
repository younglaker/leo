---
layout: post
title:  Install ThinkPHP in Tencent Cloud
date:   2018-11-20 08:24:00
category: [Server]
tags: [Server,PHP,ThinkPHP,MySql,Tencent Cloud]
---

![Tencent Cloud and Baota Panel](http://wx4.sinaimg.cn/large/6d184cefly1fx7m4l3l8sj20p0046wf0.jpg)

<!--more-->

> Exchange blogroll： [laker.me]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )

## Installation 

Install ThinkPHP 5 in Baota Panel:

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


  [1]: http://wx1.sinaimg.cn/mw690/6d184cefly1fxev3h4cgsj20vp0nu78l.jpg
  [2]: http://wx2.sinaimg.cn/mw690/6d184cefly1fxetszitejj21k40muag8.jpg
  [3]: http://wx2.sinaimg.cn/mw690/6d184cefly1fxettd9s42j20tw0pc76n.jpg
  [4]: http://wx4.sinaimg.cn/mw690/6d184cefly1fxettjiz72j20oo0bgmyu.jpg
  [5]: http://wx2.sinaimg.cn/mw690/6d184cefly1fxettow4m5j20xk0m241h.jpg
  [6]: http://wx2.sinaimg.cn/mw690/6d184cefly1fxetubwd72j216o0hs40u.jpg
  [7]: http://wx2.sinaimg.cn/large/6d184cefly1fxetup3k4pj21sa0daad4.jpg
  [8]: http://wx2.sinaimg.cn/mw690/6d184cefly1fxetuyfimpj21560gun16.jpg
  [9]: http://wx2.sinaimg.cn/mw690/6d184cefly1fxetv7rxffj20pl0el41v.jpg
  [10]: http://wx2.sinaimg.cn/mw690/6d184cefly1fxetvu2j4ej20te0lk78l.jpg
  [11]: http://wx4.sinaimg.cn/mw690/6d184cefly1fxetwn4el5j20v40jkwhw.jpg
  [12]: http://wx2.sinaimg.cn/mw690/6d184cefly1fxetwdrbq2j20le0ewq4d.jpg
  [13]: http://wx3.sinaimg.cn/mw690/6d184cefly1fxetxc6oiyj20w00ek40g.jpg