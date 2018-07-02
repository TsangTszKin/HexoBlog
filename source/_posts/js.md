---
title: js
date: 2018-07-02 11:16:34
tags: 'js'
categories: '前端'
description: 'javascript常用积累'
---

### 回车键监听

	document.onkeydown = function(event) {
		var e = event || window.event || arguments.callee.caller.arguments[0];
		if(e && e.keyCode == 13) { // enter 键
						
		}
	};


###  设置    checkkbox 全选全不选 选中不选中

	this.checked = true;
	this.checked = false;

### 四舍五入保留N位小数

	NumberObject.toFixed(num) 

toFixed() 方法可把 Number 四舍五入为指定小数位数的数字。

num必需。规定小数的位数，是 0 ~ 20 之间的值，包括 0 和 20，有些实现可以支持更大的数值范围。如果省略了该参数，将用 0 代替。


### 获取浏览器的类型
	
	 function getBrowserType () {
			var userAgent = navigator.userAgent; //取得浏览器的userAgent字符串
			var isOpera = userAgent.indexOf("Opera") > -1;
			if(isOpera) {
				return "Opera"
			}; //判断是否Opera浏览器
			if(userAgent.indexOf("Firefox") > -1) {
				return "FF";
			} //判断是否Firefox浏览器
			if(userAgent.indexOf("Chrome") > -1) {
				return "Chrome";
			}
			if(userAgent.indexOf("Safari") > -1) {
				return "Safari";
			} //判断是否Safari浏览器
			if(userAgent.indexOf("compatible") > -1 && userAgent.indexOf("MSIE") > -1 && !isOpera) {
				return "IE";
			}; //判断是否IE浏览器
		}

###  获取窗口的高度 

	 	let winWidth = 0;
	    if (window.innerWidth) winWidth = window.innerWidth;
	    else if (document.body && document.body.clientWidth)     //IE 
	        winWidth = document.body.clientWidth;
	    return winWidth;