---
layout: post
title: HTML entity to String
author: Kujisa
categories: JavaScript
tags: JavaScript HTML
---

# 一般方法：
```JavaScript
function entityToString(entity) {
    var div = document.createElement('div');
    div.innerHTML = entity;
    var res = div.innerText || div.textContent;
    return res;
}
```

# 在不支持原生dom的情况下（cheerio下的方法）：
```JavaScript
function entityToString(entity) {
    $('#ets').remove();
    $('body').append('<div id="ets"></div>');
    $('#ets').html(entity);
    var res = $('#ets').text();
    return res;
}
```