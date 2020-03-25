---
title: jquery
date: 2020-03-24 11:44:09
tags: jquery
categories: 
- 前端面试题
---

## jquery中的$.each和$(selector).each()有什么不同?

`$.each` 可以循环任何数组, 包括普通数组和jquery对象组成的伪数组; `$(selector).each()` 只能循环遍历jquery对象组成的伪数组.

## Jquery中$.each和原生js中的forEach方法有什么区别?

Jquer中的$.each不仅可以循环遍历普通数组, 还可以循环遍历jquery对象的伪数组, 原生js中的forEach只能循环遍历数组; 其次第二个实参函数的参数顺序不一样, $.each(arr, function(索引, 循环单项, 数组本身){}), arr.forEach(function(循环单项, 索引, 数组本身){})

## 原生JS的 `window.onload` 与 `Jquery的$(document).ready(function() {})，$(function () {})` 有什么不同？

执行时机不一样, window.onload会等待页面元素渲染完毕并且资源文件加载完毕后才会执行; `$(document).ready(function() {})` 是当页面元素渲染完毕后就会执行, 所以执行时机先于window.onload

## Jquery实现连式编程的原理是什么?

jquery的方法中最后都会return一个this, 这个this就是当前元素的jquery对象.

``` 
function $(parma) {
    //如果调用者传入的是一个函数, 则当做入口函数使用
    if (typeof (parma) == 'function') { 
        window.onload = parma
    } else { //如果调用者传入的是一个选择器, 则返回一个对象
        var dom = document.querySelector(parma)
        return {
        0: dom,
        //{color:'red',border:'1px solid red'}
        css: function (obj) { 
            if (typeof (obj) == 'object') {
                for (var key in obj) {
                    dom.style[key] = obj[key];
                }
            }
            return this;
        },
        click: function (fn) {
            // 注册点击事件
            dom.onclick = fn;
            return this;
            },
            hide: function () {
            dom.style.display = 'none';
            return this;
            },
            show: function () {
            dom.style.display = 'block';
            return this;
            },  
            get: function () {
            return dom;
            }
        }
    }
}

```

## Jquery如何多次给同一个标签绑定同一个事件?

使用addEventListener(‘事件名’, function(){})注册的事件, 不会出现事件覆盖, jquery中也是这样做的.

## 如何开发jquery插件?

Jquery提供了两种开发插件的方式:
$.fn: 可以通过任意jquery对象来调用

```
$.fn.green=function(){
    console.log(this, $(this)); 
    $(this).css({background:'green'}); 
}
// 调用以后, div的背景色会被设置成green
$("div").green(); 
```

$.extend: 开发的插件只能通过$顶级对象来调用

```
// 定义
$.extend({
    alert: function (msg) {
    alert(msg); 
}
}); 
// 调用
$.alert('这是提示信息')
```

## Jquery中那些方法不支持链式操作?

`$.trim(); $.each(); $(selector).html(), $(selector).text()`

