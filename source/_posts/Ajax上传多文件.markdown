---
layout: post
title:  Ajax上传多文件
date:   2014-12-16 08:24:00
category: [翻译,Ajax]
---

AJAX的采用标志着的Web历史上的一个巨大飞跃。与Web服务器通信而不需要重新加载页面的能力已改变了Web应用程序构建。动态网站的概念形成以后，AJAX(XMLHttpRequests) 技术发展迅速。

近年来XMLHttpRequests增加了一个很好的功能来处理文件上传。传统上，许多开发者用其他技术如Flash上传文件到服务器。这种方法的问题是，用户需要安装第三方浏览器插件的。

在这篇文章中你会学到如何用JavaScript技术将文件上传到服务器。我们将教你一个请求上传多文件的例子。然而，你可以用同样的办法上传单个文件。
让我们开始吧！

<!--more-->

## 选择要上传的文件
你需要做的第一件事就是建立你的HTML表单让用户选择文件。让事情简单，我们用标准的`<input>`元素并设为`file`类型。

	<form id="file-form" action="handler.php" method="POST">
	  <input type="file" id="file-select" name="photos[]" multiple/>
	  <button type="submit" id="upload-button">Upload</button>
	</form>

请注意，`<input>`元素有个`multiple`属性。这将允许用户通过浏览器文件选择器选择多个文件。如果你不指定此属性的用户只能选择一个文件。
现在你的HTML表格建好了，我们再看看处理文件上传的JavaScript代码。

## 上传文件到服务器
首先你需要创建三个变量来获取HTML里的`<form>`，`<input>`，`<button>`元素。

	var form = document.getElementById('file-form');
	var fileSelect = document.getElementById('file-select');
	var uploadButton = document.getElementById('upload-button');

下一步你需要绑定一个事件监听器到表单的`onsubmit`事件。

	form.onsubmit = function(event) {
	  event.preventDefault();

	  // 更新按钮里的文字
	  uploadButton.innerHTML = 'Uploading...';

	  // 其余的代码将在这里...
	}

在事件监听器里，首先调用`event`对象的`preventDefault()`。这将阻止浏览器提交的表单，使我们能够继续处理Ajax文件上传。
下一步，更新的`uploadButton`的`innerHTML`属性为`Uploading...`，这告诉用户文件上传中。
接下来，从`<input>`元素中获取`[FileList](https://developer.mozilla.org/en-US/docs/Web/API/FileList)`内容并存储到变量里。你可以通过访问`files`属性来做到这点。

	// 获取选择的文件
	var files = fileSelect.files;

然后创建一个新的`[FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData)`对象。这是用来接收Ajax请求获取的键/值对数据。

	// 创建一个FormData对象
	var formData = new FormData();

然后，通过循环获取`files`数组的每一个文件内容，并将它们添加到你刚才创建的`formData`对象里。你也许还想检查用户选的文件是否是你规定的文件类型。

	// 对每个文件进行循环处理
	for (var i = 0; i < files.length; i++) {
	  var file = files[i];

	  // 检查文件类型
	  if (!file.type.match('image.*')) {
	    continue;
	  }

	  // 添加文件到formData
	  formData.append('photos[]', file, file.name);
	}

在这里，你先读取当`files`数组里的所有文件，然后检查以确保它是图像。该文件的`type`属性将返回一个字符串的文件类型。你可以使用JavaScript的 `match()`方法来确保这个字符串匹配所需的类型。如果文件类型不匹配，通过调用`continue`跳过后面的语句结束本轮循环。
然后使用`append()`方法把文件添加到`formData`对象里。

---
注：

`FormData.append()`方法用于处理[`Files`](https://developer.mozilla.org/en-US/docs/Web/API/File)，[`Blobs`](https://developer.mozilla.org/en-US/docs/Web/API/Blob)，或`Strings`。

	// Files
	formData.append(name, file, filename);

	// Blobs
	formData.append(name, blob, filename);

	// Strings
	formData.append(name, value);    

第一个参数指定数据项的`name `。这将形成数据的`key `。第二个参数指定一个`File`、 `Blob`或者 `String`作为数据数据的`value `。当添加一个`File`或 `Blob`，可以指定一个`filename`文件名，但这不是必需的。

---

下一步你需要设置`XMLHttpRequest`与服务器通信。你首先需要创建一个新的`XMLHttpRequest`对象。

	// 设置请求。
	var xhr = new XMLHttpRequest();

现在您需要创建一个新连接到服务器。你使用`open`方法。该方法带三个参数。HTTP的请求方式、url和一个布尔值(确定是否应处理异步请求)。

	// 打开连接。
	xhr.open('POST', 'handler.php', true);

下一步你需要建立一个事件侦听器，`onLoad`事件完成后就会触发时。`xhr`对象的`status`属性会告诉你请求是否成功完成。

	// 请求完成时建立一个处理程序。
	xhr.onload = function () {
	  if (xhr.status === 200) {
	    // File(s) uploaded.
	    uploadButton.innerHTML = 'Upload';
	  } else {
	    alert('An error occurred!');
	  }
	};

剩下要做的是发送请求。用`xhr`的`send`方法发送`formData`。

	// 发送数据。
	xhr.send(formData);

这就是开始使用Ajax文件上传的内容。您的服务器端代码需要提取文件并处理。

## 浏览器的支持
浏览器支持总体上是好的。Internet Explorer是唯一的例外。IE 10及以上的版本支持，但早期版本的IE不支持本文提到的一些XMLHttpRequest功能。

| IE    | FIREFOX | CHROME | SAFARI | OPERA |
| :-----| ------: | ------:| ----:  | :---: |
| 10.0+ | 4.0+    |  7.0+  |   5+   |  12+  |

## 总结
在这篇文章中你学到了如何上传文件使用本地JavaScript技术，Web服务器。在功能方面的进步，消除XMLHttpRequests供开发者使用第三方浏览器插件来处理文件上传的需要。这是很好的为本地的浏览器功能往往是更快和更比一个插件提供的安全。
你计划在你的项目中使用Ajax上传的文件？请在下面的评论中分享你的想法。

---

> [英文原文](http://blog.teamtreehouse.com/uploading-files-ajax#)

