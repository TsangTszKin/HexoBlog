---
title: websocket教程
date: 2018-07-03 10:13:39
tags: [http, 聊天通讯]
categories: '前端'
description: 'websocket教程'

---

# websocket教程
---

![](https://i.imgur.com/k9dbMl5.png)

### HTTP 协议有一个缺陷：通信只能由客户端发起，于是websocket出现了。 websocket实现了浏览器与服务器全双工(full-duplex)通信——允许服务器主动发送信息给客户端。可以和服务端实现实时通讯的功能。

#### 下面是js代码demo和介绍

	<script type="text/javascript">
	    var websocket = null;
	
	    //判断当前浏览器是否支持WebSocket
	    if('WebSocket' in window){
	        websocket = new WebSocket("ws://localhost:7081/websocket/123456");
	    }
	    else{
	        alert('Not support websocket')
	    }
	
	    //连接发生错误的回调方法
	    websocket.onerror = function(event){
	        console.error("WebSocket error observed:", event);
	    };
	
	    //连接成功建立的回调方法
	    websocket.onopen = function(event){
	         console.log("WebSocket connects successful:", event);
	    }
	
	    //接收到消息的回调方法
	    websocket.onmessage = function(event){
			alert(event.data);
	    }
	
	    //连接关闭的回调方法
	    websocket.onclose = function(){
	        
	    }
	
	    //监听窗口关闭事件，当窗口关闭时，主动去关闭websocket连接，防止连接还没断开就关闭窗口，server端会抛异常。
	    window.onbeforeunload = function(){
	        websocket.close();
	    }
	
	    //关闭连接
	     websocket.close();
	
	    //发送消息
	    websocket.send("hellow");
	</script>

---

#### 下面是websocket在各大浏览器的兼容性情况


![](https://i.imgur.com/Np3TCdV.png)

