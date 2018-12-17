---
title: vue踩坑
date: 2018-07-03 10:13:39
tags: 框架
categories: '前端'
description: '一些关于我在开发vue框架开发过程中积累一些比较巧妙的地方的知识点，不断累计，持续更新~'

---



##多个单页面应用 

![](https://i.imgur.com/b7y8Yuq.png)

---

##路由命名
在 import 路由文件后，我将它命名为Router，就会出现报错，最终发现原因是：
router 才是Vue实例化的配置字段名称，写个其他的它当然不认识了。真是低级错误。
给自己一个红牌警告！

---

