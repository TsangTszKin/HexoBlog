---
title: prototype、_ _proto_ _ 与constructor
date: 2018-06-20 10:27:12
description: '讲解JS中的prototype、_ _proto_ _ 与constructor'
tags: [js, 原型]
categories: '前端'

---

# 讲解JS中的prototype、_ _proto_ _ 与constructor
---
![](https://i.imgur.com/spnZ8Hr.png)
--- 

### 首先，我们需要牢记两点：①__proto__和constructor属性是对象所独有的；② prototype属性是函数所独有的。但是由于JS中函数也是一种对象，所以函数也拥有__proto__和constructor属性，这点是致使我们产生困惑的很大原因之一

## 一，_ _proto_ _

  _ _proto_ _ 它是对象所独有的，可以看到__proto__属性都是由一个对象指向一个对象，即指向它们的原型对象（也可以理解为父对象），那么这个属性的作用是什么呢？它的作用就是当访问一个对象的属性时，如果该对象内部不存在这个属性，那么就会去它的__proto__属性所指向的那个对象（可以理解为父对象）里找，如果父对象也不存在这个属性，则继续往父对象的__proto__属性所指向的那个对象（可以理解为爷爷对象）里找，如果还没找到，则继续往上找….直到原型链顶端null（可以理解为原始人。。。），此时若还没找到，则返回undefined（可以理解为，再往上就已经不是“人”的范畴了，找不到了，到此为止），由以上这种通过__proto__属性来连接对象直到null的一条链即为我们所谓的原型链。

## 二，prototype

prototype属性，别忘了一点，就是我们前面提到要牢记的两点中的第二点，它是函数所独有的，它是从一个函数指向一个对象。它的含义是函数的原型对象，也就是这个函数（其实所有函数都可以作为构造函数）所创建的实例的原型对象，由此可知：f1.__proto__ === Foo.prototype，它们两个完全一样。那prototype属性的作用又是什么呢？它的作用就是包含可以由特定类型的所有实例共享的属性和方法，也就是让该函数所实例化的对象们都可以找到公用的属性和方法。

## constructor
constructor属性也是对象才拥有的，它是从一个对象指向一个函数，含义就是指向该对象的构造函数，每个对象都有构造函数，从图中可以看出Function这个对象比较特殊，它的构造函数就是它自己（因为Function可以看成是一个函数，也可以是一个对象），所有函数最终都是由Function()构造函数得来，所以constructor属性的终点就是Function()。

---

#总结一下： 
1. 我们需要牢记两点：①__proto__和constructor属性是对象所独有的；② prototype属性是函数所独有的，因为函数也是一种对象，所以函数也拥有__proto__和constructor属性。

2. __proto__属性的作用就是当访问一个对象的属性时，如果该对象内部不存在这个属性，那么就会去它的__proto__属性所指向的那个对象（父对象）里找，一直找，直到__proto__属性的终点null，然后返回undefined，通过__proto__属性将对象连接起来的这条链路即我们所谓的原型链。

3. prototype属性的作用就是让该函数所实例化的对象们都可以找到公用的属性和方法，即f1.__proto__ === Foo.prototype。

4. constructor属性的含义就是指向该对象的构造函数，所有函数（此时看成对象了）最终的构造函数都指向Function()。

![](https://i.imgur.com/nDwLg2Y.jpg)

