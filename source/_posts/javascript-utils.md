---
title: javascript utils
date: 2018-07-03 11:46:16
tags: js,
categories: [前端]
description: 'javascript的常用utils，工具，公共方法，可封装的方法汇集'

---

##格式化时间 时间戳 转 yyyy-MM-dd hh:mm:ss
	function formatTime(time){
		//   格式：yyyy-MM-dd hh:mm:ss
		var date = new Date(time);
		Y = date.getFullYear() + '-';
		M = (date.getMonth()+1 < 10 ? '0'+(date.getMonth()+1) : date.getMonth()+1) + '-';
		D = date.getDate() < 10? '0'+date.getDate()+ ' ': date.getDate() + ' ';
		h = date.getHours()< 10? '0'+date.getHours() + ':': date.getHours() + ':';
		m = date.getMinutes()<10? '0' + date.getMinutes()+':':date.getMinutes()+ ':';
		s = date.getSeconds()< 10? '0'+date.getSeconds():date.getSeconds();
		return Y+M+D+h+m+s;
	}


##js 如何把字符串转化为日期

	var str ='2012-08-12 23:13:15';
	str = str.replace(/-/g,"/");
	var date = newk Date(str );

##获得json对象的键名
	var PersonInfo = {
	    name:'Sigma',
	    age:18
	};
	for( var key in PersonInfo ){
	    alert('Key name is ' + key );
	}


##input file 图片预览（简单实例）
	
	$("input[name=fileimgs]").change(function (){
		var src = getObjectURL(this.files[0]); //获取路径
		$(this).siblings("img").attr("src", src);
	});

	function getObjectURL(file) {
		var url = null;
		if (window.createObjectURL != undefined) {
			url = window.createObjectURL(file)
		} else if (window.URL != undefined) {
			url = window.URL.createObjectURL(file)
		} else if (window.webkitURL != undefined) {
			url = window.webkitURL.createObjectURL(file)
		}
		return url
	};

##获取HTML地址栏的参数

	function getParamByName(paramName){
	     var reg = new RegExp("(^|&)"+ name +"=([^&]*)(&|$)");
	     var r = window.location.search.substr(1).match(reg);
	     if(r!=null)return  unescape(r[2]); return null;
	}

##JS编码解码
	encodeURIComponent()
	decodeURIComponent()

##时间字符串转时间戳 
	var startTime = '2014-07-10 11:21:12';
	var startTimestamp = Date.parse(new Date(startTime));
	startTimestamp = startTimestamp / 1000;
	//2014-07-10 10:21:12的时间戳为：1404958872
	console.log(startTimestamp + "的时间戳为：" + startTimestamp);

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

### 在即将离开当前页面(刷新或关闭)时执行 JavaScript :

	window.onbeforeunload = function () { 
		return ''  //return字符串会系统提醒会否确定离开或者刷新当前页面
	}