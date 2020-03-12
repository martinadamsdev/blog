---
title: "CSS布局之水平居中布局"
date: 2020-02-25T02:16:07+08:00
draft: false
tags: ["CSS", "布局", "居中", "水平居中"]
categories: ["前端"]
author: "<a href=\"https://w3cfed.com\" target=\"_blank\">w3cfed</a>"
---

### 概念：
水平居中布局 指的是**当前元素在父级元素容器中，水平方向是居中显示的**。

### 方案一： inline-block + text-align

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>水平居中布局</title>
	<style>
		#parent {
			width: 100%;
			height: 200px;
			background-color: #ccc;

			text-align: center;
		}
		#child {
			width: 200px;
			height: 200px;
			background: orangered;

			display: inline-block;
		}
	</style>
</head>
<body>
<div id="parent">
	<div id="child"></div>
</div>
</body>
</html>
```
<!--more-->

#### 优缺点
**优点**：浏览器兼容性好。代码中使用的均是  CSS 2 中的属性，浏览器兼容性良好。
**缺点**：`text-align` 具有继承性。子元素中的文本会继承父元素的 `text-align` 属性。若子元素中的文本不是居中显示时，则需要重新设置 `text-align` 属性将其覆盖。

### 方案二：table + margin

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>水平居中布局</title>
<style>
	#parent {
		background-color: #ccc;
	}

	#child {
		width: 200px;
		height: 200px;
		/* display 的值为 block 和 table */
		display: table;
		/*
		 margin 属性:外边距
		 * 一个值 - 上右下左
		 * 二个值 - 第一个值表示上下，第二个值表示左右
		   * auto 浏览器自动计算(等分)
		 * 三个值 - 第一个值表示上，第二个值表示左右，第三个值表示下
		 * 四个值 - 上右下左
		*/
		margin: 0 auto;
		background: orangered;
	}
</style>
</head>
<body>
	<!--定位父级元素-->
	<div id="parent">
		<!--定位子级元素-->
		<div id="child"></div>
	</div>
</body>
</html>
```
#### 优缺点
**优点**：只需要对子元素设置就可以显示水平居中布局效果。
**缺点**：如果子元素脱离文档流，导致 `margin` 属性的值失效。

### 方案三：absolute + transform
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>水平居中布局</title>
	<style>
		#parent {
			width: 100%;
			height: 200px;
			background-color: #ccc;

			/* 开启定位 */
			position: relative;
		}

		#child {
			width: 200px;
			height: 200px;
			background: orangered;
			/*
			  当把当前元素设置为绝对定位后:
			 *如果父级元素没有开启定位，当前元素相对于页面定位，
			 *如果父级元素开启了定位的话，当前元素相对于父级元素定位
			*/

			position: absolute;
			left: 50%; /* 子级元素相对于父级元素的左边 50% */
			transform: translateX(-50%);
		}
	</style>
</head>
<body>
	<!--定位父级元素-->
	<div id="parent">
		<!--定位子级元素-->
		<div id="child"></div>
	</div>
</body>
</html>
```
#### 优缺点
**优点**：父级元素是否脱离文档流，不影响子级元素居中显示效果。
**缺点**：`transform` 属性是 CSS 3 中新增的属性，浏览器支持情况不好。


