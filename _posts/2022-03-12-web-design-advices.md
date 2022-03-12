---
layout: post
title: Web Design Advices
author: Kujisa
categories: Design
tags: Web CSS HTML Design
---

## Scroll Bar

```css
::-webkit-scrollbar {
	width: 3px;
	height: 3px;
}

::-webkit-scrollbar-thumb {
	background-color: lightseagreen;
	min-height: 100px
}

::-webkit-scrollbar-thumb:hover {
	background-color: seagreen
}
```

## Progress Bar

```css
#progressBar {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	z-index: 998;
#top-progress-bar {
	position: relative;
	top: 0px;
	left: 0px;
	right: 0px;
	background-color: lightseagreen;
	height: 2px;
	width: 100%;
	transition: width 0.2s ease 0s, opacity 0.6s ease 0s;
	opacity: 1;
}
```
```html
<div id="progressBar">
<div id="top-progress-bar"></div>
</div>
```
```javascript
// 页面总高
var totalH = document.body.scrollHeight || document.documentElement.scrollHeight;
// 可视高
var clientH = window.innerHeight || document.documentElement.clientHeight;
window.onscroll = function() {
	// 计算有效高
	var validH = totalH - clientH;
	// 滚动条卷去高度
	var scrollH = document.body.scrollTop || document.documentElement.scrollTop;
	// 百分比
	var result = ((scrollH / validH) * 100).toFixed();
	document.getElementById("top-progress-bar").style.width = result + "%";
}
```