---
title: 'HTML input 标签的 accept 属性 常用的例子'
date: 2018-07-02 10:45:58
description: 'input[file]标签的accept属性可用于指定上传文件的 MIME类型 。
例如，想要实现默认上传图片文件的代码，代码可如下：
 accept="image/*" 但是！
这段代码在Chrome和Safari等Webkit浏览器下却出现了响应滞慢的问题，可能要等 6~10s 才能弹出文件选择对话框。简直不能忍呀。'
tags: [DOM, MIME]
categories: '前端'

---

在IE和Firefox中使用 accept=”image/*” 属性则没有发现响应延迟的问题。
于是几经尝试后，发现是 accept=”image/*” 属性的问题，删掉它或者将 * 通配符修改为指定的MIME类型，就可以解决Webkit浏览器下的对话框显示滞慢的问题。
解决办法如下：
accept="image/gif,image/jpeg,image/jpg,image/png,image/svg"
accept=”image/*”属性会对每一个文件都遍历一次所有的”image/*”文件类型，当文件较多时，文件的检验时间较长，这可能是Webkit的底层实现的bug。
另外，
accept=”audio/*”和 accept=”video/*” 属性 在 Webkit浏览器下也会有同样的响应延迟的问题。同理，通过将 * 通配符 修改成指定的MIME类型就可解决。

	
	switch (this.accept) {
	case "pic":
	        this.MIME = "image/jpg, image/png, image/jpeg, image/gif, image/svg";
	        break;
	case "doc":
	        this.MIME = "application/msword, application/vnd.openxmlformats-officedocument.wordprocessingml.document";
	        break;
	case "ppt":
	        this.MIME = "application/vnd.ms-powerpoint, application/vnd.openxmlformats-officedocument.presentationml.presentation";
	        break;
	case "xls":
	        this.MIME = "application/vnd.ms-excel, application/vnd.openxmlformats-officedocument.spreadsheetml.sheet";
	        break;
	case "txt":
	        this.MIME = "text/plain";
	        break;
	case "pdf":
	        this.MIME = "application/pdf";
	        break;
	case "html":
	        this.MIME = "text/html";
	        break;
	case "mp3":
	        this.MIME = "audio/mpeg";
	        break;
	case "mp4":
	        this.MIME = "audio/mp4, video/mp4";
	        break;
	default:
	        break;
	}
