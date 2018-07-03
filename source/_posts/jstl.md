---
title: jstl
date: 2017-04-26 13:46:12
tags: [jstl, 耶鲁表达式]
categories: [后端]
description: ''

---

### 变量存储
	<fmt:formatNumber var="colNumb" value="${12/fn:length(depts)}">
	</fmt:formatNumber>

	<div id="sliderProgressBar" class="mui-slider-progress-bar mui-col-xs-	${colNumb}">
	</div>
