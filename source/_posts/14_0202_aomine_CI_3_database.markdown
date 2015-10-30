---
layout: post
title:  跟着阿大学CodeIgniter （三）—— 操作数据库
date:   2014-02-02 08:24:00
category: "PHP"
---

![请输入图片描述][1]

## 碎碎念
过年还来SegmentFault学习的都是好少年～  

## 知识重点
涉及到数据库，就是比较复杂的内容了，所以本文略长，但是CI还是为我们省了很多麻烦事。CI提供了强大的数据库函数类——Active Record，源码是/system/database/DB_active_rec.php文件。

<!--more-->


- 使用
 
    > $this -> db -> 方法名()

- 连接数据库
 
    > $this -> load -> database();

- 插入
 
    > $this -> db -> insert(表名, 数据);

- 更新

    > $this -> db -> where(字段名, 字段值);  
	> $this -> db -> update(表名, 修改值的数组);

- 查找

    > $this -> db -> where(字段名, 字段值);  
	> $this -> db -> select(查找的字段名);  
	> $query = $this -> db -> get(表名);  
	> return $query -> result();  

- 删除

    > $this -> db -> where(字段名, 字段值);
	> $this -> db -> delete(表名);

## 创数据库
本例中，创建数据库ci，用户表user，user表里的字段为编号uid, 用户名uname, 密码upw。

## 配置数据库文件
到/application/config/database.php进行必要的配置，把数据库名／密码／编码等填写好。

## 编写模型
由本CI系列博客第一章可知，这些对数据库的操作要写在模型里。所以在model里创建一个user_test.php的文件。

- 构造函数

    	class User_test extends CI_Model { // 类名首字母大写，继承CI_Model类
    		
    		function __construct() {
    			parent::__construct(); // 继承父类的构造函数
    			$this -> load -> database(); // 连接数据库
    		}
    	}

- 插入
 
		function u_insert($arr) {
            $this -> db -> insert('user', $arr);
            //把传来的数据数组插到user表里
		}

- 更新

		function u_update($id, $arr) {
			$this -> db -> where('uid', $id); //查找到此id的用户信息
			$this -> db -> update('user', $arr);//更新
		}


- 查找

		 function u_select($name) { // 这里是通过用户名来查找，可以自定义其他字段
			$this -> db -> where('uname', $name);
			$this -> db -> select('*'); //选取全部信息
			$query = $this -> db -> get('user');
			return $query -> result(); //返回值
		}


- 删除

		 function u_del($id) {
			$this -> db -> where('uid', $id);//查找到此id的用户信息
			$this -> db -> delete('user');//删除此id所有信息
		}

- 整个代码

        <?php
        	class User_test extends CI_Model
        	{
        		
        		function __construct()
        		{
        			parent::__construct();
        			$this -> load -> database();
        		}
        
        		function u_insert($arr) {
        			$this -> db -> insert('user', $arr);
        		}
        
        		function u_update($id, $arr) {
        			$this -> db -> where('uid', $id);
        			$this -> db -> update('user', $arr);
        		}
        
        		function u_del($id) {
        			$this -> db -> where('uid', $id);
        			$this -> db -> delete('user');
        		}
        
    		    function u_select($name) {
    		    	$this -> db -> where('uname', $name);
        			$this -> db -> select('*');
        			$query = $this -> db -> get('user');
        			return $query -> result();
        		}
        	}
        ?>
        
## 调用此模型
这里写一个注册功能来示范如何使用我们刚刚创建的模型。创建controller/signin.php和views/signin.php文件

- 编写views/signin.php
 
    	<form action="signin/regist" method="post"> 
        <!-- 当提交时触发signin/regist控制器 -->
    		name: <input type="text" name="u_name">
    		password: <input type="password" name="u_pw">
    		<input type="submit" name="submit" value="submit">
    	</form>

- 编写controller/signin.php

        <?php if ( ! defined('BASEPATH')) exit('No direct script access allowed'); //防止直接通过文件路径访问
        
        class Signin extends CI_Controller {// 类名首字母大写，继承CI_Controller类
        
            public function index() {
                $this -> load -> view('signin'); //载入signin视图
            }
        
            function regist() {
                $this -> load -> model('user_test'); //载入我们之前创建的User_test模型，首字母不用大小
                $arr = array('uname' => $_POST['u_name'], 'upw' => $_POST['u_pw']); 
                //获取提交的表单内容，=>左边是数据表里面的键名，=>右边是通过name获取的表单值
                $this -> user_test -> u_insert($arr); //调用user_test的u_insert方法插入数据
            }
        }

- 使用  
访问localhost/ci/index.php/signin，填写表单即可注册，进入数据库看看就有内容插入了。

## 本系列文章
[跟着阿大学CodeIgniter （一）——了解MVC](http://blog.segmentfault.com/younglaker/1190000000392848)
[跟着阿大学CodeIgniter （二）—— 文件上传](http://blog.segmentfault.com/younglaker/1190000000396029)  
[跟着阿大学CodeIgniter （三）—— 操作数据库](http://blog.segmentfault.com/younglaker/1190000000402287)


  [1]: http://segmentfault.com/img/bVbQOE