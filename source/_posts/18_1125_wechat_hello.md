---
layout: post
title:  Develope WeChat Official Account's Hello Message
date:   2018-11-25 08:24:00
category: [Server]
tags: [Server,PHP,ThinkPHP,MySql,Tencent Cloud,Wechat]
---

![Develope WeChat Official Account's Hello Message](http://wx2.sinaimg.cn/large/6d184cefly1fxnkwi98vuj20p0046dg6.jpg)

<!--more-->

> Exchange blogroll： [laker.me]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )


## Apply test account

Apply for Wechat testing account:

https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1421137524

![Application][1]

## Connect WeChat server with

Enter your testing account, and set your server address and the director `wx` for WeChat server. Set a token name what ever you like: 

![token name][2]

Enter your Baota Panel, new a file `wx` in `application/public/`

![Baota Panel][3]

Add a new file  `index.php` in `wx`

Function:

- Connect to WeChat server
- When someone subscribes, reply a hello message
- When get user text messge, reply what he sent

```
<?php
    /*
    * Connect to WeChat server
    */
    // Get signature nonce token timestamp echostr
    $nonce     = $_GET['nonce'];
    $token     = 'YOUR_TOKEN';
    $timestamp = $_GET['timestamp'];
    $echostr   = $_GET['echostr'];
    $signature = $_GET['signature'];
    // Set it as array, and sort
    $array = array();
    $array = array($nonce, $timestamp, $token);
    sort($array);
    // Join them as a string, use sha1 to encrypt, and check with signature
    $str = sha1( implode( $array ) );
    
    //The first time weixin api
    if( $str == $signature && $echostr ){
        echo  $echostr;
        exit;
    }

    else{

        /*
        * When someone subscribes, reply a hello message
        */
        // 1. Get the posted xml data from Weixin
        $postArr = $GLOBALS['HTTP_RAW_POST_DATA'];
        // 2. Deal with message type and set reply type and content
        $postObj = simplexml_load_string( $postArr );
        // Check if the data is subscription event
        if( strtolower( $postObj->MsgType) == 'event'){
            // If it'is subscribe event
            if( strtolower($postObj->Event == 'subscribe') ){
                // Reply text message 
                $toUser   = $postObj->FromUserName;
                $fromUser = $postObj->ToUserName;
                $time     = time();
                $msgType  =  'text';
                $content  = 'Hello, welcome~ '.$postObj->FromUserName.'-'.$postObj->ToUserName;;
                $template = "<xml>
                                <ToUserName><![CDATA[%s]]></ToUserName>
                                <FromUserName><![CDATA[%s]]></FromUserName>
                                <CreateTime>%s</CreateTime>
                                <MsgType><![CDATA[%s]]></MsgType>
                                <Content><![CDATA[%s]]></Content>
                                </xml>";
                $info     = sprintf($template, $toUser, $fromUser, $time, $msgType, $content);
                echo $info;
            }
        }

        /*
        * When get user text messge, reply what he sent
        */
        // Check if the data is text
        if( strtolower( $postObj->MsgType) == 'text'){
             // Get text message
        $content = $postObj->Content;
                // Reply text message 
                $toUser   = $postObj->FromUserName;
                $fromUser = $postObj->ToUserName;
                $time     = time();
                $msgType  =  'text';
                $content  = 'The content you sent is '.$content;
                $template = "<xml>
                                <ToUserName><![CDATA[%s]]></ToUserName>
                                <FromUserName><![CDATA[%s]]></FromUserName>
                                <CreateTime>%s</CreateTime>
                                <MsgType><![CDATA[%s]]></MsgType>
                                <Content><![CDATA[%s]]></Content>
                                </xml>";
                $info     = sprintf($template, $toUser, $fromUser, $time, $msgType, $content);
                echo $info;
        }
    }
```

In  Official Accounts，when you subscibe, it will say hello to you . When you send a text, it will send what you sent:

![Done][4]


  [1]: http://wx4.sinaimg.cn/mw690/6d184cefly1fxetxsngt1j20x40hqdif.jpg
  [2]: http://wx4.sinaimg.cn/mw690/6d184cefly1fxev12r26ej20jq0boq3p.jpg
  [3]: http://wx2.sinaimg.cn/mw690/6d184cefly1fxeycapacwj20q00faabs.jpg
  [4]: http://wx4.sinaimg.cn/mw690/6d184cefly1fxnj4rdnwbj20u00w1jvy.jpg