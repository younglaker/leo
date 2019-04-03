---
layout: post
title:   HTML5上传图片文件（含拖拽、预览、上传、美化）
date:   2016-03-04 08:24:00
category: [Ajax]
tags: [HTML5,Ajax]
---

<!-- ![HTML5上传图片文件][1] -->

[上篇文章讲到如何上传文件][2]。本文讲细分讲述图片上传、预览。

<!--more-->

## 关于接口

[File API][3]

- File - 独立文件；提供只读信息，例如名称、文件大小、mimetype 和对文件句柄的引用。
- FileList - File 对象的类数组序列（考虑多文件上传或者从桌面拖动目录或文件）。
- Blob - 可将文件分割为字节范围。
- FileReader - 读取File或Blob
- URL scheme


## 检测浏览器是否支持

```
// 检测是否支持File API
if (window.File && window.FileReader && window.FileList && window.Blob) {
  //  支持
} else {
  alert('不支持');
}
```

## 基本代码

选取一张图片，并预览：
[Demo1][4]

```
<input id="img_input" type="file" accept="image/*"/>
<label for="img_input"></label>
<div class="preview_box"></div>

.preview_box img {
  width: 200px;
}

$("#img_input").on("change", function(e){

  var file = e.target.files[0]; //获取图片资源

  // 只选择图片文件
  if (!file.type.match('image.*')) {
    return false;
  }

  var reader = new FileReader();

  reader.readAsDataURL(file); // 读取文件

  // 渲染文件
  reader.onload = function(arg) {

    var img = '<img class="preview" src="' + arg.target.result + '" alt="preview"/>';
    $(".preview_box").empty().append(img);
  }
});

```

上传到服务器

```
var form_data = new FormData();
var file_data = $("#img_input").prop("files")[0];

// 把上传的数据放入form_data
form_data.append("user", "Mike");
form_data.append("img", file_data);

$.ajax({
    type: "POST", // 上传文件要用POST
    url: "",
    dataType : "json",
    crossDomain: true, // 如果用到跨域，需要后台开启CORS
  processData: false,  // 注意：不要 process data
  contentType: false,  // 注意：不设置 contentType
    data: form_data
}).success(function(msg) {
    console.log(msg);
}).fail(function(msg) {
    console.log(msg);
});

```

## 拖拽上传

三个相关事件：

- dragenter
- dragover
- drop

原生JavaScript：

[Demo2][5]

```
<div id="drop_zone">Drop files here</div>
<ul id="list"></ul>


// 必须阻止dragenter和dragover事件的默认行为，这样才能触发 drop 事件
function fileSelect(evt) {

  evt.stopPropagation();
  evt.preventDefault();

  var files = evt.dataTransfer.files; // 文件对象
  var output = [];

  // 处理多文件
  for (var i = 0, f; f = files[i]; i++) {
    output.push('<li><strong>', escape(f.name), '</strong> (', f.type || 'n/a', ') - ',
                f.size, ' bytes, last modified: ',
                f.lastModifiedDate.toLocaleDateString(), '</li>');
  }
  // 显示文件信息
  document.getElementById('list').innerHTML = output.join('');
}

function dragOver(evt) {
  evt.stopPropagation();
  evt.preventDefault();
  evt.dataTransfer.dropEffect = 'copy';
}

// 监听器
var dropZone = document.getElementById('drop_zone');
dropZone.addEventListener('dragover', dragOver, false);
dropZone.addEventListener('drop', fileSelect, false);
```

jQuery：

其他代码可以不变，注意监听事件的时候的，由于jQuery的封装，数据存放的字段有变，传参是`e.originalEvent`而不是`e`：

```
$("#drop_zone").on('dragover', function(e){
  e.stopPropagation();
  e.preventDefault();
  handleDragOver(e.originalEvent);
});

$("#drop_zone").on('drop', function(e){
  e.stopPropagation();
  e.preventDefault();
  handleFileSelect(e.originalEvent);
});
```

## 美化上传框

###方法一： 在隐藏的文件输入框上调用click()方法

隐藏掉默认的的文件输入框`<input>`元素，使用自定义的界面来充当打开文件选择对话框的按钮。要使用样式`display:none`把原本的文件输入框隐藏掉，然后在需要的时候调用它的click()方法就行了。

```
<input type="file" id="fileElem" multiple accept="image/*" style="display：none" onchange="handleFiles(this.files)">
<a href="#" id="fileSelect">选择文件</a>

var fileSelect = document.getElementById("fileSelect"),
  fileElem = document.getElementById("fileElem");

fileSelect.addEventListener("click", function (e) {
  if (fileElem) {
    fileElem.click();  // jQuery可以使用 trigger()
  }
  e.preventDefault(); // prevent navigation to "#"
}, false);
```

###方法二：用label

隐藏input，把样式写到label上，点击label就是对input进行操作。

[Demo3][6]

```
<input id="img_input2" type="file" accept="image/*"/>
<label for="img_input2" id="img_label2">选择文件
    <i class="fa fa-plus fa-lg"></i>
</label>
<div id="preview_box2"></div>


#img_input2 {
  display: none;
}
#img_label2 {
  background-color: #f2d547;
  border-radius: 5px;
  display: inline-block;
  padding: 10px;
}
#preview_box2 img {
  width: 200px;
}
```


  [1]: http://77g54f.com1.z0.glb.clouddn.com/bgt-718552.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjIucG5n/dissolve/100/gravity/South/dy/5
  [2]: http://laker.me/blog/2016/03/04/16_0304_ajax_file_upload/
  [3]: http://www.w3.org/TR/file-upload/
  [4]: https://codepen.io/younglaker/pen/vGmaYr
  [5]: https://codepen.io/younglaker/pen/vGmaYr
  [6]: https://codepen.io/younglaker/pen/vGmaYr