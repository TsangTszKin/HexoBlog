---
title: css3
date: 2016-05-09 23:02:16
description: '一下关于css3的效果汇集'
tags: 'css'
categories: '前端'

---

### 鼠标移上去有动画变化，放大等

	.img {
	    -webkit-transform: scale(1.0);
	    -moz-transform: scale(1.0);
	    -o-transform: scale(1.0);
	    -ms-transform: scale(1.0);
	    transform: scale(1.0);
	    -webkit-transition: all .5s eas;
	    -moz-transition: all .5s ease;
	    -o-transition: all .5s ease;
	    -ms-transition: all .5s ease;
	    transition: all .5s ease;
	}
	
	.img : hover {
	    -webkit-transform: scale(1.1);
	    -moz-transform: scale(1.1);
	    -o-transform: scale(1.1);
	    -ms-transform: scale(1.1);
	    transform: scale(1.1);
	    -webkit-transition: all .5s ease;
	    -moz-transition: all .5s ease;
	    -o-transition: all .5s ease;
	    -ms-transition: all .5s ease;
	    transition: all .5s ease;
	}

---

### 淡入淡出

	{
		-webkit-animation-name: fadeIn; /*动画名称*/
		-webkit-animation-duration: 1s; /*动画持续时间*/
		-webkit-animation-iteration-count: 1; /*动画次数*/
		-webkit-animation-delay: 0s; /*延迟时间*/
	}