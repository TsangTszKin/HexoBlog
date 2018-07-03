---
title: 把es6编译成es5
date: 2018-07-03 09:55:16
tags: '架构'
categories: '前端'
description: 'vue2.0编译打包后的语法版本兼容性问题处理'
---


##1,  当初解决过程第一步
IE浏览器报Promise未定义的错误
背景： 一个vue-cli构建的vue项目，一个使用angular的项目，两个项目在其他浏览器一切正常，但是ie中会报Promise未定义的错误
 
解决办法： 

####vue的项目：

- 1. 　npm install babel-polyfill --save
- 2. 　在main.ts中 import "babel-polyfill"
- 3.    如果使用了vuex，则在vuex的index.ts文件中也要  import "babel-polyfill"，最好放在 import Vuex from 'vuex' 的前面
 
####angular的项目：
这个项目比较老，都是采用文件引入的方式，所以用import的方式会报错，这里解决办法：

- 1.    npm install babel-polyfill --save
- 2.    从  node_modules  文件夹下找到 _babel-polyfill@6.26.0@babel-polyfill  (名字根据版本号改变)下的  dist  中  polyfill.min.js ，  将其拷贝到一个文件夹中，我这里是babel-polyfill
- 3.    在引入文件的index.html中引入即可,  <script src="/babel-polyfill/polyfill.min.js" type="text/javascript"></script>

##2,  当初解决过程第二步
https://www.jianshu.com/p/2b373b0910ed

安装babel-cli 

	npm install --save-dev babel-cli
装Babel的preset以正确识别ES6代码  

	npm install --save-dev babel-preset-es2015
然后再在项目根目录下面新建一个名为 .babelrc 文件，内容如下：

	{
	  "presets": [
	    "es2015"
	  ]
	}