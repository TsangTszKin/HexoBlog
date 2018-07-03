---
title: css
date: 2018-07-03 10:56:37
tags: css
categories: '前端'
description: 'css样式的积累'

---

##chrome   冲掉它自带的表单样式

	input:-webkit-autofill {
	-webkit-box-shadow: 0 0 0px 1000px white inset;
	-webkit-text-fill-color: black;
	}

## 长文本自动换行 样式
	｛ 
		word-wrap: break-word;
		word-break: break-all;
	｝

##长文本不换行

	white-space: nowrap;

##div等没有disabled属性的标签元素 禁止点击事件 直接样式  

	pointer-events:none;

##text-overflow:ellipsis的巧妙运用

注意：overflow: hidden; text-overflow:ellipsis;white-space:nowrap;一定要一起用    max-width: 100px;

- 1.一定要给容器定义宽度.
- 2.如果少了overflow: hidden;文字会横向撑到容易的外面
- 3.如果少了white-space:nowrap;文字会把容器的高度往下撑；即使你定义了高度，省略号也不会出现，多余的文字会被裁切掉
- 4.如果少了text-overflow:ellipsis;多余的文字会被裁切掉，就相当于你这样定义text-overflow:clip.

如果容器是table，当文字内容过多时，不换行，而是出现...

##placeholder的样式修改
	
	   /*placeholder字体颜色*/  
	   ::-webkit-input-placeholder { /* WebKit browsers */  
	       color:#ccc;  
	   }  
	   :-moz-placeholder { /* Mozilla Firefox 4 to 18 */  
	       color:#ccc;  
	   }  
	   ::-moz-placeholder { /* Mozilla Firefox 19+ */  
	       color:#ccc;opacity:1;  
	   }  
	   :-ms-input-placeholder { /* Internet Explorer 10+ */  
	       color:#ccc !important;  
	   }  

##动画，从下到上出现
	div{
	        /*动画*/
	       display: block;
	       height: 0px;
	       animation: myfirst 0.25s;
	       -webkit-animation: myfirst 0.25s;
	       animation-fill-mode: forwards;
	  }
	 @-webkit-keyframes myfirst
	 /* Safari and Chrome */
	1%{height:0px;}
	2%{height:1px;}
	4%{height:2px;}
	6%{height:3px;}
	8%{height:4px;}
	10%{height:5px;}
	12%{height:6px;}
	14%{height:7px;}
	16%{height:8px;}
	18%{height:9px;}
	20%{height:10px;}
	22%{height:11px;}
	24%{height:12px;}
	26%{height:13px;}
	28%{height:14px;}
	30%{height:15px;}
	32%{height:16px;}
	34%{height:17px;}
	36%{height:18px;}
	38%{height:19px;}
	40%{height:20px;}
	42%{height:21px;}
	44%{height:22px;}
	46%{height:23px;}
	48%{height:24px;}
	50%{height:25px;}
	52%{height:26px;}
	54%{height:27px;}
	56%{height:28px;}
	58%{height:29px;}
	60%{height:30px;}
	62%{height:31px;}
	64%{height:32px;}
	66%{height:33px;}
	68%{height:34px;}
	70%{height:35px;}
	72%{height:36px;}
	74%{height:37px;}
	76%{height:38px;}
	78%{height:39px;}
	80%{height:40px;}
	82%{height:41px;}
	84%{height:42px;}
	86%{height:43px;}
	88%{height:44px;}
	90%{height:45px;}
	92%{height:46px;}
	94%{height:47px;}
	96%{height:48px;}
	98%{height:49px;}
	100%{height:50px;}
	 }

## 图片居中显示
	div {
		max-height: 180px;
		display: -webkit-flex;
		display: flex;
		justify-content: center;
		overflow: hidden;
		align-items: center;
	}
	img{
	    width: 100%;
	}
	
	<div>
	    <img src="...">
	</div>

##图片自适应居中显示不变形
	.ui-img-div {
		display: webkit-flex;
		display: flex;
		justify-content: center;
		overflow: hidden;
		align-items: center;
	}
	.ui-img-div img {
	    width:100%;
	}
	<div class="ui-img-div" style="height: 100%;">
	    <img src="">
	</div>

##定义行数多余省略 

	word-break: break-all;
	display: -webkit-box;   
	-webkit-line-clamp: 4;//四行
	-webkit-box-orient: vertical;
	overflow: hidden;