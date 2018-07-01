---
title: "jQuery动画效果animate滚动到指定页面ID的位置"
date: 2016-05-06
description: '要实现animate滚动到页面指定id的位置，就要获取ID的数字值，也就是距离顶部的距离，再通过animate的scrollTop滚动 
点击ID为comt的元素，回到ID为comments的位置；点击ID为xia的元素，回到id为footer的位置'
tags: "js"
categories: "前端"
---


	$(document).ready(function($){
		$('#comt').click(function(){
		    $('html,body').animate({scrollTop:$('#comments').offset().top}, 800);
		});
		$('#xia').click(function(){
		    $('html,body').animate({scrollTop:$('#footer').offset().top}, 800);
		});
	});


