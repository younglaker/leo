---
layout: post
title:   HTML5+Ajax上传文件
date:   2016-01-05 08:24:00
category: [Ajax上传文件]
tags: [HTML5,Ajax]
---
![HTML5+Ajax上传文件][1]

<!--more-->

## HTML

`input`类型设为`file`：

```
<label for="img_input"></label>
<input id="img_input" type="file"/>
```

如果想上传多文件，可添加`multiple`

```
<input type="file" name="img" multiple="multiple" />
```

用`accept="MIME_type"`限制提交的文件类型，用逗号隔开的 [MIME 类型][2]列表（服务器端也要最好类型检测双保险），如：

```
<input type="file" accept="image/gif, image/jpeg" />
<input type="file" accept="image/*"/>
```

## 获取文件内容

JavaScript：

```
var file = document.getElementById('fileToUpload').files[0];
```

jQuery：

```
var file = $("#img_input").prop("files")[0];
```

## 上传

XMLHttpRequest Level 2添加了一个新的接口`FormData`。利用FormData对象，我们可以通过JavaScript用一些键值对来模拟一系列表单控件。比起普通的Ajax，使用FormData的最大优点就是我们可以异步上传一个二进制文件。

```
// 创建
var form_data = new FormData();

// 获取文件
var file_data = $("#img_input").prop("files")[0];

// 把所以表单信息
form_data.append("id", "001");
form_data.append("name", "test");
form_data.append("img", file_data);

$.ajax({
    type: "POST",
    url: "....",
    dataType : "json",
    processData: false,  // 注意：让jQuery不要处理数据
    contentType: false,  // 注意：让jQuery不要设置contentType
    data: form_data
}).success(function(msg) {
    console.log(msg);
}).fail(function(msg) {
    console.log(msg);
});
```

## 多文件上传

**方法一 ：一次性上传多个文件**

如果后台接口允许多文件上传，就把文件存到一个变量后上传。

**方法二 ：一次性上传多个文件**

如果后台接口要求单个文件，就循环获取文件信息提交，Ajax使用同步上传`async: false`。

## 跨域

JSONP是使用GET方法，无法发送文件。可以让后台开启CORS，Ajax也使用跨域`crossDomain: true`即可。

```
$.ajax({
    type: "POST",
    url: "....",
    dataType : "json",
    crossDomain: true,
    processData: false,  // 注意：让jQuery不要处理数据
    contentType: false,  // 注意：让jQuery不要设置contentType
    data: form_data
}).success(function(msg) {
    console.log(msg);
}).fail(function(msg) {
    console.log(msg);
});
```


  [1]: http://77g54f.com1.z0.glb.clouddn.com/bgt-523586.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/South/dy/5
  [2]: https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input