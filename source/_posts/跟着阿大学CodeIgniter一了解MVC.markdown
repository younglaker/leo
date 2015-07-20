---
layout: post
title:  跟着阿大学CodeIgniter（一）——了解MVC
date:   2014-01-23 08:24:00
category: "PHP"
---

## 有的没的
![青峰大辉][1]
[阿大](http://baike.baidu.com/link?url=e1_jXEDQnhyDOoG5YCg9_-EU2HZD5_2kpGIz4MgVe7U5HQ19v0IssPJDYnt2gTI2v-DnAQs52mWbi4fiJdo_Na)镇文(-_-メ)～  
阿大你太黑了，回去洗把脸看看有没有救～

## 学习背景 
CI是一个比较流行的PHP MVC框架，CI的文档完善和资源丰富，适合初学～
按照我觉得比较高效的学习方法：了解基本语法 -> 学会使用一个流行的框架 -> 反过来在用原生语言自己实现一个框架

<!--more-->


## 关于CodeIgniter 
[codeigniter](http://codeigniter.org.cn/)是一套给 PHP 网站开发者使用的应用程序开发框架和工具包。它提供一套丰富的标准库以及简单的接口和逻辑结构，其目的是使开发人员更快速地进行项目开发。使用 CodeIgniter 可以减少代码的编写量，并将你的精力投入到项目的创造性开发上。

## 什么MVC

- M：Model，模型，通常包括对数据库的操作
- V：View，视图，给用户看的页面，模板
- C：Controller，控制器，接收用户请求，让M和V执行操作，生成页面返回到用户端

## 准备工作

- [下载](http://codeigniter.org.cn/user_guide/installation/downloads.html)CI框架
- 解压放置开发目录
- 开启本地服务器（这里我使用的是apache和mysql）

## 控制器

- 一个控制器就是一个类文件，用户通过URL访问的就是某个Controller的类的某个成员方法。
- 文件放在application/controllers里
- 类名首字母必须大写，并继承CI的类CI_Controller
- 访问的路径为：localhost/项目名/入口/控制器名/控制器的方法[/参数]。
- 若需要传参，访问时在地址后加'/参数值'

例如，把下面文件保存为ci/application/controllers/hello.php

    <?php if ( ! defined('BASEPATH')) exit('No direct script access allowed'); //防止直接通过文件路径访问
    
    class Hello extends CI_Controller {
    
    	public function sayhello($n) {
    		echo $n  ;
    	}
    }

访问http://localhost/ci/index.php/hello/sayhello/segmentfault， 就可以在页面上看到'segmentfault'。

## 视图

- 文件放在application/views里
- 通过控制器可以合成页面
- 在控制器中的调用方法：$this -> load -> view(视图名, 参数数组);

例如：用一个控制器，调用几个视图，显示点文字  
    
ci/application/controllers/hello.php

    <?php if ( ! defined('BASEPATH')) exit('No direct script access allowed');
    
    class Hello extends CI_Controller {
    
    	public function index() { // 如果访问index方法，url可省略此方法名
    		$name = 'Da';
    		$word = 'SegmentFault';
            $data = array('v_name' => $name, 'v_word' => $word); 
    		// 把变量合成一个数组，以便传入视图。带'v'前缀的是在视图里引用的变量名，我故意做得带区别一些。
    		$this -> load -> view('welcome.php', $data);
    		$this -> load -> view('foot.php');
    		// 可以同时调用多个视图。如果是调用php文件，可省略后缀
    	}
    }

ci/application/views/welcome.php

    <p><?= $v_name;?> recommends <?= $v_word;?> to you.</p>


ci/application/views/foot.php

    <p>I'm footer.</p>
    
访问http://localhost/ci/index.php/hello， 就可以在页面上看到
> Da recommends SegmentFault to you.
> I'm footer.

## 小练习——文件操作
功能：每刷新一次页面，页面上的数字加一  
ci/application/controllers/counter.php

    <?php if ( ! defined('BASEPATH')) exit('No direct script access allowed');
    
    class Counter extends CI_Controller {
    
    	public function index() {
    		$c = file_get_contents('./num.txt'); 
    		$c = $c ? $c : 0; //如果文件不存在，则设初始值0
    		$data = array('v_c' => $c);
    		$c++;
    		$re_f = fopen('./num.txt', 'w');
    		fwrite($re_f, $c);
    		fclose($re_f);
    		$this -> load -> view('count.php', $data);
    	}
    }

ci/application/views/count.php
    
    <p><?= $v_c;?></p>

访问http://localhost/ci/index.php/counter 刷新看看吧～

## 本系列文章
[跟着阿大学CodeIgniter （一）——了解MVC](http://blog.segmentfault.com/younglaker/1190000000392848)
[跟着阿大学CodeIgniter （二）—— 文件上传](http://blog.segmentfault.com/younglaker/1190000000396029)  
[跟着阿大学CodeIgniter （三）—— 操作数据库](http://blog.segmentfault.com/younglaker/1190000000402287)

## 注
本系列文章前五章根据[php100 2012](http://www.php100.com/html/shipinjiaocheng/newz/) 15到20课的视频学习整理并加入自己的内容而成

  [1]: http://segmentfault.com/img/bVbOml