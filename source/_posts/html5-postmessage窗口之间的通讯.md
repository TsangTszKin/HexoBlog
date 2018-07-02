---
title: H5 postmessage通讯
date: 2017-08-14 11:20:12
tags: 'html5'
categories: '前端'
description: 'html5 postmessage窗口之间的通讯'
---

父窗口监听
IE:

	window.attachEvent('message', function(e) {
		var msg = e.data;					
	}, false);

其它：

	window.addEventListener('message', function(e) {
		var msg = e.data;					
	}, false);

子窗口发送消息：

	window.parent.postMessage("hello word:", "*");
