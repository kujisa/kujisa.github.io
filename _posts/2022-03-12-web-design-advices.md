---
layout: post
title: Web Design Advices
author: Kujisa
categories: Design
tags: Web CSS HTML Design
---

## Scroll bar

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

## Progress bar

```html
<div id="progressBar">
<div id="top-progress-bar"></div>
</div>
```

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

## Animations

### Time

comfortable: 0.8s

fast: 0.6s

```css
transition: all 0.8s;
```

### Slide up

```css
.post-list-anim-slideup{
  animation: post-list-anim-slideup 0.6s;
}

@keyframes post-list-anim-slideup { 
  0% {
    opacity: 0.25;
    -webkit-transform: translateY(20px);
    -ms-transform: translateY(20px);
    transform: translateY(20px);
  }
  100%{}			
}
```

```javascript
window.onload = function () {
  let postLists = document.querySelectorAll(".post-list > li");
  
  let postListObserver = new IntersectionObserver((entries, observer) => {
    entries.forEach((entry, index) => {
      if (entry.isIntersecting) {
        if(!entry.target.classList.contains("post-list-anim-slideup")){
          entry.target.className="post-list-anim-slideup"
        }
      }
    })
  })

  postLists.forEach(function (postList) {
    postListObserver.observe(postList);
  })
}
```

## Font family

Raleway and Roboto
```scss
@import url('https://fonts.googleapis.com/css2?family=Raleway:wght@100;200;300;400;500;600;700;800;900&family=Roboto:wght@300;700&display=swap');
$base-font-family: Raleway,Roboto,sans-serif;
```

## Box shadow

```css
box-shadow: 0px 12px 8px -12px #c0bebe;
```

## Color

{:color-style: style="background: black;" }
{:color-style: style="color: white;" }
{:font-style: style="font-weight: 900; text-decoration: underline;" }

|:Example   :|:CSS:|
| -| - | 
|   MS Pink  {: style="background: radial-gradient(100% 193.51% at 100% 0%, #EDF4F8 0%, #EFF2FA 16.92%, #FAEFF6 34.8%, #FAE6F2 48.8%, #FAF0F7 63.79%, #F1F1FB 81.34%, #F0F4F8 100%);" }                |`background: radial-gradient(100% 193.51% at 100% 0%, #EDF4F8 0%, #EFF2FA 16.92%, #FAEFF6 34.8%, #FAE6F2 48.8%, #FAF0F7 63.79%, #F1F1FB 81.34%, #F0F4F8 100%);`|
|   Github Cyan  {: style="background: linear-gradient(120deg, #155799, #159957);" }    |`background: linear-gradient(120deg, #155799, #159957);`
|   MDN eg.   {: style="background: linear-gradient(#e66465, #9198e5);" }         |`background: linear-gradient(#e66465, #9198e5);`

## Hyperlink

### External icon
```css
a[href^="https://"] {
  background: url(/assets/images/external.svg) center right no-repeat;
  padding-right: 13px;
}
a[href^="http://"] {
  background: url(/assets/images/external.svg) center right no-repeat;
  padding-right: 13px;
}
a[href^="https://miraihere.com"] {
  background: none;
  padding-right: 0;
}
```

## Translator Voice

### Chinese

Bing translator

### English

Baidu translator