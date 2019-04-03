---
layout: post
title:  跟着阿大学CodeIgniter （四）——登录验证
date:   2014-02-15 08:24:00
category: "PHP"
---

<!-- ## 镇文图 -->
<!-- ![镇文图][1] -->

## 什么是Session
Session是用于保持状态的基于Web服务器的方法。可以简单理解为服务器给用户生成了一个通行证。

<!--more-->

## 登录的过程

1.提交用户输入的用户名和密码
2.检查是否存在此用户名
3.如果存在，检查密码是否正确
4.如果正确，生成session

## 将要用到的几个关键语句

1.加载session类

    $this -> load -> library('sesion');

2.创建session

    $this -> session -> set_userdata($array);

3.查看session

    $this -> session -> userdata(session名);

4.删除session

    $this -> session -> unset_userdata(session名);

## Here we go

1.先修改配置
找到application/config/config.php，把$config['encryption_key']赋与一个密钥值，随意起。
2.建立views/login.php文件

	<form action="login/check" method="post">
	<!-- login/check意味着我们待会要用到控制器Login的check函数 -->
		name: <input type="text" name="u_name">
		password: <input type="password" name="u_pw">
		<input type="submit" name="submit" value="submit">
	</form>

	<a href="login/logout">退出</a>
	<!-- 调用控制器Login的logout函数 -->

3.编写控制器类

    <?php if ( ! defined('BASEPATH')) exit('No direct script access allowed');

    class Login extends CI_Controller {

        public function index() {
            $this -> load -> view('login');
        }
    }

4.接下来，我们要一步步往这个类里面加功能。首先是检验用户提交的信息正误／创建session

    function check() {
        $this -> load -> model('user_test');
        //user_test 是上一篇文章（链接见文末）中创建的User_test模型
        $user = $this -> user_test -> u_select($_POST['u_name']);
        //调用User_test模型的u_select方法查询提交的用户名的信息
        if ($user) {
        // 如果此用户存在
            if ($user[0] -> upw == $_POST['u_pw']) {
            // 如果提交的密码与正确密码一致，则创建session
                echo 'pw right';
                $this -> load -> library('session');
                // 载入CI的session库
                $arr = array('s_id' => $user[0] -> uid);
                // 把用户ID存入数组
                $this -> session -> set_userdata($arr);
                设置session
            } else {
                echo 'pw wrong';
            }
        } else {
            echo 'name wrong';
        }
    }

5.判断是否登录

    function is_login() {
        $this -> load -> library('session');
        // 载入CI的session库
        if ($this -> session -> userdata('s_id')) {
        // 如果能取得这个ID的session，就意味着处于登录状态
            echo "logined";
        } else {
            echo "no login";
        }
    }

6.退出登录

    function logout() {
        $this -> load -> library('session');
        // 载入CI的session库
        $this -> session -> unset_userdata('s_id');
        // 删除此ID是session
    }

7.控制器最终代码

    <?php if ( ! defined('BASEPATH')) exit('No direct script access allowed');

    class Login extends CI_Controller {

        public function index() {
            $this -> load -> view('login');
        }

        function check() {
            $this -> load -> model('user_test');
            $user = $this -> user_test -> u_select($_POST['u_name']);
            // var_dump($user);
            // $user[0] -> upw
            if ($user) {
                if ($user[0] -> upw == $_POST['u_pw']) {
                    echo 'pw right';
                    $this -> load -> library('session');
                    $arr = array('s_id' => $user[0] -> uid);
                    $this -> session -> set_userdata($arr);
                } else {
                    echo 'pw wrong';
                }
            } else {
                echo 'name wrong';
            }
        }

        function is_login() {
            $this -> load -> library('session');
            if ($this -> session -> userdata('s_id')) {
                echo "logined";
            } else {
                echo "no login";
            }
        }

        function logout() {
            $this -> load -> library('session');
            $this -> session -> unset_userdata('s_id');
        }
    }

8.测试
现在可以访问localhost/ci/index.php/login 进行测试了

## 本系列文章
[跟着阿大学CodeIgniter （一）——了解MVC](http://blog.segmentfault.com/younglaker/1190000000392848)
[跟着阿大学CodeIgniter （二）—— 文件上传](http://blog.segmentfault.com/younglaker/1190000000396029)
[跟着阿大学CodeIgniter （三）—— 操作数据库](http://blog.segmentfault.com/younglaker/1190000000402287)


  [1]: http://segmentfault.com/img/bVbSFL
