---
layout: post
title:  跟着阿大学CodeIgniter （二）—— 文件上传
date:   2014-01-24 08:24:00
category: "PHP"
---

<!-- ![请输入图片描述][1] -->
<!-- Ubuntu下的PS太难用了，为做一张配图，还要切回winows，好苦13 ╮(╯-╰)╭ -->


## 原生php上传
在使用CI之前，我们来看看用原生代码是如何上传的，做个对比，就知道CI有多么方便～

首先创建一个视图ci/application/views/uploader1.php

<!--more-->

- 表单的 action 填写调用的控制器的上传方法'upload1/up'，这个将在下一步代码中完成控制器具体内容
- 填写method，get或post
- 当表单需要上传时，应填写'enctype="multipart/form-data"'

    	<form action="upload/up" method="post" enctype="multipart/form-data">
    		<input type="file" name="upfile">
    		<input type="submit" name="sub" value="submit">
    	</form>

然后写控制器ci/application/controllers/upload1.php

- move_uploaded_file() 是PHP的一个内置方法，把上传好的文件从缓存处移到你想要的位置

        <?php if ( ! defined('BASEPATH')) exit('No direct script access allowed');

        class Upload1 extends CI_Controller {
        	function index()
        	{
        		$this -> load -> view('uploader1.php'); //调用视图
        	}

        	function up() //这个就是视图里action调用的上传接口
        	{
        		if (!empty($_POST['sub'])) { //当提交的时候
        			// var_dump($_FILES['upfile']); 可以打印看看上传文件的信息
        			$f = $_FILES['upfile']; //把文件信息赋给一个变量，方便调用
        			if ($f['size'] > 102400) { //限制文件大小
        				echo "too large";
        			} else {
        				if ($f['type'] == 'image/png') { //限制文件类型为png
        					$t = time(); // 时间戳
        					$s = '.png';
        					move_uploaded_file($f['tmp_name'], move_uploaded_file($f['tmp_name'], './uploads/'.$t.$s);
        					//$f['tmp_name']是上传好的文件从缓存文件，'/uploads/$t$s'是我们要移动到的文件夹，在根目录下自己创建的uploads文件夹。'./uploads/'.$t.$s 是变量的值进行字符串拼接，把文件以时间戳命名
        				}
        			}
        		}
        	}
        }
        ?>

现在可以访问localhost/ci/index.php/upload进行上传文件了

## CI文件上传
CI有一个丰富的上传类[upload](http://codeigniter.org.cn/user_guide/libraries/file_uploading.html)，它的源码放在system/libraries/upload.php。我们可以轻松的调用它完成一系列操作。

- 定义一个数组，存放设置
- 引用CI 的 upload类，使用do_upload('上传框的name')方法进行上传。若上传文件的input的name是userfile，则此方法不用带参数。可以看到upload类的源码里此处有个默认值就是userfile。
- 接收成功或出错信息。
> 成功：$this -> upload -> data()
> 错误：$this -> upload -> display_errors()

首先创建一个视图ci/application/views/uploader2.php

- 注意此处 action 改为 'upload2/up'，其他不变

    	<form action="upload2/up" method="post" enctype="multipart/form-data">
    		<input type="file" name="upfile">
    		<input type="submit" name="sub" value="submit">
    	</form>

然后写控制器ci/application/controllers/upload2.php

- 设置参数[更多](http://codeigniter.org.cn/user_guide/libraries/file_uploading.html)：

| 名称 | 介绍 |
| ----- | ----- | ------ |
|upload_path|文件上传路径。该路径必须是可写的，相对路径和绝对路径均可以。|
|allowed_types|允许上传文件的MIME类型；通常文件扩展名可以做为MIME类型. 允许多个类型用竖线分开|
|file_name|想要使用的文件名,如果设置了这个参数，CodeIgniter 将根据这里设置的文件名来对上传的文件进行重命名。文件名中的扩展名也必须是允许的文件类型。|
|max_size|允许上传文件大小的最大值（以K为单位）。该参数为0则不限制。注意：通常PHP也有这项限制，可以在php.ini文件中指定。通常默认为2MB。|
|max_width|上传文件的宽度最大值（像素为单位）。0为不限制。|
|max_height|上传文件的高度最大值（像素为单位）。0为不限制。|



    <?php if ( ! defined('BASEPATH')) exit('No direct script access allowed');

    class Upload2 extends CI_Controller {
    	function index()
    	{
    		$this -> load -> view('uploader2.php');
    	}

    	function up()
    	{
    	    // 把需要的配置放入config数组
    		$config['upload_path'] = './uploads';
    		$config['allowed_types'] = 'gif|jpg|png';
    		$config['max_size'] = '102400';
    		$this -> load -> library('upload', $config); //调用CI的upload类
    		$this -> upload -> do_upload('upfile'); //使用do_upload('上传框的name')方法进行上传

    		// 以下代码为拓展的，非必要
    		if ($this -> upload -> do_upload('upfile')) { //上传成功
    			$data = array('upload_data' => $this -> upload -> data()); //将文件信息存入数组
    			var_dump($data); //打印文件信息
    		} else { //上传失败
    			$error = array('error' => $this -> upload -> display_errors());//将错误信息存入数组
    			var_dump($error); //打印错误信息
    		}
    	}
    }
    ?>

现在可以访问localhost/ci/index.php/upload2进行上传文件了

## 小结
CI的上传类是我们上传更方便，代码量少，并且很整洁

## 本系列文章
[跟着阿大学CodeIgniter （一）——了解MVC](http://blog.segmentfault.com/younglaker/1190000000392848)
[跟着阿大学CodeIgniter （二）—— 文件上传](http://blog.segmentfault.com/younglaker/1190000000396029)
[跟着阿大学CodeIgniter （三）—— 操作数据库](http://blog.segmentfault.com/younglaker/1190000000402287)


  [1]: http://segmentfault.com/img/bVbPbI
