---
title: web前端基础
date: 2020-03-24 10:59:46
tags: 前端基础
categories: 前端面试题
---

# HTML

## Html5新增那些标签?
布局标签:
header,section,footer,article,aside
表单标签: datalist, 
input:type=’week|date|time|datetime|number|search|url|tel|color|email|range’
多媒体标签: audio(音频), video(视频)
其他标签: progress(进度条),meter(度量器)
补充:
Html5新属性:
hidden(隐藏元素),required(必填),minlength(最小长度),maxlength(最大长度),pattern(正则表达式),placeholder(提示文本),autocomplete(自动填充),autofocus(自动获取焦点)

## 行内元素和块级元素的具体区别是什么？
块级元素独占一行页面空间, 不会和其他元素共享一行页面空间;
行内元素可以和其他非块级元素(行内,行内块)共享一行页面空间.

## 列举几个块级标签和行内标签？
块级标签:div,p,h1~h6,section,header,footer
行内标签:span,em(i),strong(b),u,em(i),a

## 行内元素的padding和margin可设置吗？
行内元素设置水平方向的padding和margin是可以生效,但是设置垂直方向的padding和margin虽然看起来对标签起作用,但实际并没有对周围元素产生任何影响, 所以行内元素设置垂直方向的padding和margin是无效的.

## 简述readyonly与disabled的区别
readyonly是设置表单元素为只读状态;
disabled是设置表单元素为禁用状态.

## 哪些标签都存在伪元素?
大部分容器标签(大部分双标签)都有伪元素, iframe没有伪元素;
大部分单标签都没有伪元素, 但是img有伪元素

## 伪元素可以使用js来操作吗?
js不可以操作伪元素

## Html5的网页为什么只需要写<!DOCTYOE HTML>?
HTML ## 01 中的 doctype 需要对 DTD 进行引用，因为 HTML ## 01 基于 SGML。而 HTML 5 不基于 SGML，因此不需要对 DTD 进行引用，但是需要 doctype 来规范浏览器的行为。其中，SGML是标准通用标记语言,简单的说，就是比HTML,XML更老的标准，这两者都是由SGML发展而来的, 而HTML5不是的。


# Css

## px em rem 这三中长度单位的区别？
px是一个绝对单位;em和rem是一个相对单位, em参考的是当前元素的字体(font-size)大小, 参考的是页面根元素html的字体(font-size)大小.

## CSS3新增伪类有那些？
p:first-of-type选择属于其父元素的首个<p>元素。
p:last-of-type选择属于其父元素的最后一个<p>元素。
p:nth-child(2)选择属于其父元素的第二个子元素。
p:nth-type-of(2)选择属于其父元素的第二个子元素p。
:enabled、:disabled 控制表单控件的禁用状态。
:checked，单选框或复选框被选中。

## 谈谈css选择器优先级顺序以及判定标准?
优先级从低到高:
通配符选择器<标签选择器<类选择器(属性选择器)<ID选择器;
行内样式<使用!important修饰的属性优先级最高;
如果两个选择器(属性完全相同)同时命中一个元素, 并且权重一样, 则书写顺序会影响优先级, 后一个选择器的属性会覆盖前一个选择器中相同的属性.

## position 几个属性的作用？
position 的常见四个属性值： relative，absolute，fixed，static。一般都要配合"left"、"top"、"right"以及"bottom" 属性使用。 
1）static：默认位置，（static 元素会忽略任何 top、 bottom、left 或 right 声明）。一般不常用。 
2）relative：位置被设置为 relative 的元素，偏移的 top，right，bottom，left 的值都以它原来的位置为基准偏移。注意 relative 移动后的元素在原来的位置仍占据空间。 
3）absolute：位置设置为 absolute 的元素，可定位于相对于包含它的元素的指定坐标。意思就是如果它的父容器设置了 position 属性，并且 position 的属性值为 absolute 或者 relative，那么就会依据父容器进行偏移。如果其父容器没有设置 position 属性，那么偏移是以 body 为依据。注意设置 absolute 属性的元素在标准流中不占位 置。 
4）fixed：位置被设置为 fixed 的元素，可定位于相对于浏览器窗口的指定坐标。不论窗口滚动与否，元 素都会留在那个位置。它始终是以 body 为依据的。注意设置 fixed 属性的元素在标准流中不占位置。

## position设置为absolue和fixed有什么区别?
absolute是绝对定位, 绝对定位参考的是有明确定位的父元素, 如果直接父元素没有明确定位会一直向上查找,如果父元素都没有明确定位,则参考body标签;
fixed是固定定位, 参考对象是浏览器.

## 在一个页面中给多个元素设置相同的id, 会导致什么问题?
会导致通过js获取dom元素的时候, 只能获取到第一个元素, 后面的元素都无法正常获取.

## 用伪类实现一个上三角?
```
<div class='triangle_border_up'></div>
```

```
.triangle_border_up{
    border:20px solid red;
    border-top:0;
    border-left:20px solid transparent;
    border-right:20px solid transparent; 
    width:0px;
}
```


## 怎么让一个不定宽高的 div，垂直水平居中？
方案一:transform

```
.parent{
    background: #DDD;
    width: 400px;
    height: 400px;
}
.son{
    position: relative;
    background: pink;
    width: 200px;
    height: 200px;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
} 
```

方案二:flex弹性布局

```
.parent{
    display: flex;
    justify-content: center;
    align-items: center;
    background: #DDD;
    width: 400px;
    height: 400px;
}
.son{
    background: pink;
    width: 200px;
    height: 200px;
} 

```
方案三:绝对定位

```
.parent{
    position: relative;
    background: #DDD;
    width: 400px;
    height: 400px;
}
.son{
    position: absolute;
    top:0;
    bottom:0;
    left:0;
    right:0;
    background: pink;
    width: 200px;
    height: 200px;
    margin: auto;
}

```

## 清除浮动有哪些常用的方式?
额外标签法: 在浮动元素的最后添加一个块级标签, 给其设置一个clear:both的属性 (缺点:会在页面上产生很多空白标签);
给浮动元素的父元素设置高度:(缺点:不太灵活);
给浮动元素的父元素设置overflow:hidden;
使用伪元素法:(推荐使用)
```
.clear:after{
    content:'';
    display:block;
    overflow:hidden;
    visibility:hidden;
    clear:both;
}
```


## 让两个块级元素在一行显示有哪些做法?
设置显示模式:`display:inline|inline-block;`
flex布局: 给父元素设置display:flex;
使用浮动;

## 如何设置一个元素在垂直方向居中?
首先不考虑代码的灵活性, 可以使用margin外边距或者padding内边距来实现元素在垂直方向居中显示.具体可以给父元素设置一个垂直方向的padding内边距; 也可以给需要垂直居中的子元素设置垂直方向的外边距.其次如果这个需要垂直居中的元素是一个单行文本, 则可以使用行高等于标签高度的方式来实现.也可以使用css3中的flex布局, 使用align-items:center设置元素在侧轴(垂直方向)居中对齐.也可以使用绝对定位的方式, 设置元素在相对定位的父元素中垂直对齐.

## 说说图片懒加载的原理?实际开发中用过哪些图片懒加载的插件?
img标签在加载图片的时候, 是通过请求src属性所指向的文件来加载图片的, 那如果img标签本身没有src属性的话, 那么img标签在渲染的时候, 就不会加载图片.所以图片懒加载的原理就是将img标签的src属性给暂时先改成一个自定义的属性, 这样页面已加载就会不去加载图片, 当img标签所在区域进入屏幕可视区域后, 从存放图片路径的自定义属性中获取图片地址,并动态的设置给对应img标签的src属性, 这样浏览器就会自动帮助我们去请求对应的图片资源, 也就实现了所谓的图片懒加载.图片懒加载的插件有很多, 大部分是基于jquery的, 比如jquery.lazyload. 当然vue的中也有实现了图片懒加载的插件, 比如vue-lazyload, vue的组件库中也有图片懒加载的组件.

## css3新增了那些新特性?
媒体查询(@media);
transfrom系列:translate平移, scale缩放,rotate旋转
动画(animate);
过渡效果(transition);
flex弹性(伸缩)布局;
盒模型计算方式box-sizing:border-box;
线性渐变(linear-gradient),径向渐变;
伪元素,文字阴影(text-shadow), 边框阴影(box-shadow),圆角(border-radius)

## display:none和visibility:hidden的区别?
display:none隐藏元素后,不占位;
visibility:hidden隐藏元素后占位.

## Less是什么?
Less是一种css预处理语言, 在less中可以定义一些变量和表达式以及使用嵌套语法; less中使用@定义变量(@baseColor:pink); 后期可以通过一些编译工具(less)将less编译成浏览器能直接识别的css样式. 所以less只是在开发阶段使用的一种中间语言, 使用less的目的是提高开发效率以及提高代码的可维护性.

## Scss是什么?(sass)
scss是一种css预处理语言, 在less中可以定义一些变量和表达式以及使用嵌套语法; scss中使用$定义变量($baseColor:pink); 后期可以通过一些编译工具(node-sass)将less编译成浏览器能直接识别的css样式. 所以scss只是在开发阶段使用的一种中间语言, 使用scss的目的是提高开发效率以及提高代码的可维护性.

## Stylus是什么?(.styl)
stylus是一种css预处理语言, 在stylus中可以定义一些变量和表达式以及使用嵌套语法(stylus中是使用缩进的语法表示嵌套关系); 后期可以通过一些编译工具(stylus)将stylus编译成浏览器能直接识别的css样式. 所以stylus只是在开发阶段使用的一种中间语言, 使用stylus的目的是提高开发效率以及提高代码的可维护性.

