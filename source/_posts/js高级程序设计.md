---
title: js高级程序设计笔记
date: 2018-06-20 21:46:09
tags: [js, 继承, 闭包, vue双向绑定原理]
categories: '前端'
description: 'js高级程序设计笔记'

---

# js高级程序设计笔记
## 一，基本类型和引用类型的值
- ECMAScript 变量可能包含两种不同数据类型的值：基本类型值和引用类型值。基本类型值指的是
简单的数据段，而引用类型值指那些可能由多个值构成的对象。
- 在将一个值赋给变量时，解析器必须确定这个值是基本类型值还是引用类型值。第 3 章讨论了 5 种
基本数据类型：
 - Undefined
 - Null
 - Boolean
 - Number
 - String
 
这 5 种基本数据类型是按值访问的，因为可以操作保存在变量中的实际的值。
引用类型的值是保存在内存中的对象。与其他语言不同，JavaScript 不允许直接访问内存中的位置，
也就是说不能直接操作对象的内存空间。在操作对象时，实际上是在操作对象的引用而不是实际的对象。
为此，引用类型的值是按引用访问的

- 在 ECMAScript 中，引用类型是一种数据结构，
用于将数据和功能组织在一起。它也常被称为类，但这种称呼并不妥当。尽管 ECMAScript
从技术上讲是一门面向对象的语言，但它不具备传统的面向对象语言所支持的类和接口等基本结构。引
用类型有时候也被称为对象定义，因为它们描述的是一类对象所具有的属性和方法。

- 引用类型
 - Object 类型
 - Array 类型
 - Function 类型
 - Date 类型
 - RegExp 类型

## 二，call apply this blind的应用

### 1, 示例1
	function sum (num1, num2) {
		return num1 + num2;
	}
	
	alert(sum.apply(this, [1, 2])); 			//3
	alert(sum.call(this, 1, 2)); 				//3

### 2， 示例2

	window.name = 'test1';
	var obj = new Object();
	obj.name = 'test2';
	
	fuunction getName() {
		alert(this.name);
	}
	
	getName();									//test1
	getName.apply(this);						//test1
	getName.apply(window);						//test1
	getName.apply(obj);							//test2
	getName.call(obj);							//test2
	getName.blind(obj);							//test2

## 三，创建对象

### 1，工厂模式

- 传入属性值到函数中新创建一个对象，封装好新对象属性再返回对象
- 缺点：工厂模式虽然解决了创建多个相似对象的问题，但却没有解决对象识别的问题（即怎样知道一个对象的类型）

### 2，构造函数模式

- 传入属性值到函数中，封装给this，没有return，调用的时候直接var a =  new A('test');
- 缺点：创建多个完成同样任务的 Function 实例的确没有必要；但是函数转移到了构造函数外部就丝毫没有封装性可言了

### 3，原型模式

- 将要封装的信息直接添加到原型对象中，让所有对象实例共享它所包含的属性和方法
- 缺点：引用类型值（如数组）的属性来说，引用类型值的属性值存在于prototype中而非实例中，所有实例的对这个引用类型的属性值都是同一个引用，一旦修改会影响所有实例


### 4， 组合使用构造函数模式和原型模式

- 构造函数模式用于定义实例属性，而原型模式用于定义方法和共享的属性。这是创建自定义类型的最常见方式
	
## 四，继承
#### 其实现继承主要是依靠 原型链 来实现的
	function SuperTest() {
		this.name = 'superTest';
	}
	
	SuperTest.prototype.getSuperTestName = function () {
		return this.name;
	}
	
	function Test () {
		this.name = 'test';
	}
	
	//继承了SuperTest
	Test.prototype = new SuperTest();
	
	
	Test.prototype.getTestName = function () {
		return this.name;
	}
	
	var superTest = new SuperTest();
	var test = new Test();
	
	alert(superTest.getSuperTestName());			//superTest
	alert(test.getTestName());						//test
	alert(test.getSuperTestName());					//superTest

## 五，闭包
### 有权访问另一个函数作用域内变量的函数都是闭包。
### 闭包就是一个函数引用另外一个函数的变量，因为变量被引用着所以不会被回收，因此可以用来封装一个私有变量。这是优点也是缺点，不必要的闭包只会徒增内存消耗！

	function a(){
	  var n = 0;
	  function inc() {
		n++;
		console.log(n);
	  }
	  inc(); 
	  inc(); 
	}
	a(); //控制台输出1，再输出2
	
	匿名函数的执行环境具有全局性，因此其 this 对象通常指向 window
	var name = "The Window";
	var object = {
	 name : "My Object",
	 getNameFunc : function(){
		 return function(){
			return this.name;
		 };
	 }
	};
	alert(object.getNameFunc()()); //"The Window"（在非严格模式下）
	
	改良
	var name = "The Window";
	var object = {
	 name : "My Object",
	 getNameFunc : function(){
		var that = this; 
		 return function(){
			return that.name;
		 };
	 }
	};
	alert(object.getNameFunc()()); //"My Object"

## 六，vue双向绑定的实现原理
### Vue.js 最核心的功能有两个，一是响应式的数据绑定系统，二是组件系统。

### 访问器属性是对象中的一种特殊属性，它不能直接在对象中设置，而必须通过 defineProperty() 方法单独定义。

       var obj = { };

       // 为obj定义一个名为 hello 的访问器属性

       Object.defineProperty(obj, "hello", {

         get: function () {return sth},

         set: function (val) {/* do sth */}

       })

       obj.hello // 可以像普通属性一样读取访问器属性，访问器属性的"值"比较特殊，读取或设置访问器属性的值，实际上是调用其内部特性：get和set函数。

       obj.hello // 读取属性，就是调用get函数并返回get函数的返回值

       obj.hello = "abc" // 为属性赋值，就是调用set函数，赋值其实是传参 