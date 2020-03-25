---
title: javascript基础
date: 2020-03-24 11:43:12
tags: javascript
categories: 
- 前端面试题
---

## js中有哪些数据类型
int(数值), string(字符串), boolean(布尔), null(空), undefined(未定义), object(对象)

## typeof(typeof()) 和instanceof 的区别?
typeof可以判断变量的数据类型,返回值是字符串;
a instanceof b是判断b是不是在a的原型链上, 也可以实现判断数据类型, 返回值为布尔.

## 怎么判断两个对象相等? 
先判断俩者是不是对象;
再判断俩个对象的所有key值是否相等相同;
最后判断俩个对象的相应的key对应的值是否相同

## js中函数有哪些定义方式
函数声明:function fn(){}
函数表达式:var fn=function(){}
构造函数:var fn=new Function(‘参数1’,’参数2’,’函数体’)

## js中函数有哪些调用形式?
普通函数,对象的方法,事件处理函数,构造函数,回调函数

## "==" 和 "===" 的区别？
==只会对值进行比较,===不仅会对值进行比较,还会对数据类型进行比较.

## js中的常用内置对象有哪些？并列举该对象的常用方法？
Math(数学相关);Date(日期相关);Array;Object

## 列举和数组操作相关的方法
push:将元素添加到数组的末尾, 返回值是数组长度
pop:将数组最后一个元素弹出, 返回值是被弹出的元素
unshift:在数组的开头插入一个元素,返回值是数组的长度
shift:将数组第一个元素弹出,返回值是被弹出的元素
splice(index,len):删除数组中指定元素
concat:连接数组
reverse: 翻转数组

## 列举和字符串操相关的方法
substr(start,len)/substring(start,end): 截取字符串
slice:从数组会字符串中截取一段
indexOf/lastIndexOf:查找某一个字符是否存在于另外一个字符串中, 存在则返回索引, 不存在则返回-1;indexOf是从前向后顺序查找;
lastIndexOf:是从后向前查找
replace:替换字符串特定的字符
toUpperCase:将字符串转成大写
toLowerCase:将字符串转成小写
charAt:获取字符串中指定索引的字符

## document.write和 innerHTML的区别?
document.write是指定在整个页面区域的内容, innerHTML是指定某一个元素的内容.

## 分别阐述split(),slice(),splice(),join()？
split可以使用一个字符串切割另外一个字符串, 返回值是数组;
slice可以从数组中截取一部分(字符串对象也有slice方法);
splice(index,len)可以删除指定的数组元素;
join可以将数组元素使用特定的连接符拼接成字符串

## 例举 3 中强制类型转换和 2 中隐式类型转换？
强制转换:
转化成字符串 toString() String() 转换成数字 Number()、 parseInt()、 parseFloat();
隐式转换:
转换成布尔类型 Boolean() 隐式拼接字符串 
例子 var str = "" + - / % ===

## 如何判断一个变量foo是数组?

foo instanceof Array;
foo.constructor == Array;
Array.isArray(foo) 
Object.prototype.toString.call(foo)=="[object Array]"


Javascript高级
## 什么是原型对象?
每一个构造函数都有一个prototype的属性, 这个属性的值是一个对象, 这个对象就叫做构造函数的原型对象; 一般建议将构造函数的成员属性绑定在原型对象prototype上, 因为原型对象prototype
身上的属性默认可以通过实例对象访问到; 这样做可以保证在每次通过new关键字创建实例对象的时候, 这些方法不会被重复在内存中创建.

## 什么是原型链?
每个构造函数都有一个prototype属性, 即原型对象, 通过实例对象的___proto___属性也可访问原型对象;而原型对象本质也是一个对象, 是对象就有自己的原型对象, 最终形成的链状的结构称为原型链.

## 什么是构造函数?
构造函数本质也是一个函数, 只不过这个函数在定义的时候首字母一般需要大写; 构造函数调用的时候,必须通过一个new关键字来调用; 我们一般不直接使用构造函数, 而是使用构造函数创建出来的实例对象. 构造函数是js面向对象的一个重要组成部分.

## js中实现继承的方式?
ES6之前官方并没有提供一种实现继承的语法, 所以大部分继承方式都是程序员通过代码在模拟.常见的继承方式有以下几种:
原型继承;
借用构造函数继承;
组合继承;

function Person(name,age,gender){
this.name=name||'';
this.age=age||'';
this.gender=gender||'';
}
Person.prototype.sayHi=function(){
console.log('I am '+this.name);
}
var p1=new Person('zs',30,'男');
function Student(name,age,gender,score){
// 通过构造继承属性
Person.call(this,name,age,gender);
}

// 通过原型继承,继承方法
Student.prototype=new Person();
// 修改constructor的指向
Student.prototype.constructor=Student;
// 动态添加成员方法
Student.prototype.printScore=function(){
console.log('my score is '+this.score);
}
// 创建Student实例对象
var s1=new Student('zs',30,'男',90);
ssayHi();
sprintScore();

ES6之后使用extends关键字实现继承(class Student extends Person{})

## 什么是闭包, 有什么作用, 使用的时候需要注意什么?
闭包是一个跟函数相关的概念,表现形式是一个父函数内部,嵌套了一个子函数, 子函数直接或间接的被返回给外部作用域, 并且子函数中会使用到父函数局部作用域中的变量.当我们在外部调用这个子函数的时候, 就会发生闭包现象.
闭包的作用:闭包可以延展一个函数的作用域
注意事项:不能滥用闭包, 会导致内存泄漏

function fn(){
var a=100;
return function(){
return a;
}
}
var fn1=fn();
fn1();


## 什么是内存泄漏, 那些操作会引起内存泄漏?
内存泄漏是指本应该被垃圾回收机制回收的内存空间由于某种特殊原因没有及时被回收, 称之为内存泄漏. 滥用全局变量和滥用闭包都会导致内存泄漏.

## 什么是预解析?
JS代码在执行之前,解析引擎会对代码进行一个预先的检查, 主要会对变量和函数的声明进行提升, 将变量和函数的声明提到代码的最前面.变量只提升声明, 不提升赋值.

## 说说你对this关键字的理解
this在不同的场景下指向不太一样, 主要分为一下几种情况:
普通函数中指向全局window;
对象的成员方法中指向该方法的宿主对象;
构造函数中指向new出来的实例对象;
事件处理函数中指向事件源;
回调函数中指向全局window

## call/apply/bind的区别
这三个方法都是函数这个特殊对象的方法,通过这三个方法都可以改变函数内部this的指向.
不同点:
call和apply会调用一次函数, 而bind不会调用函数, 只会在内存中创建一个函数的副本(修改过this指向的函数).
call从第二个参数开始需要一个参数列表,
apply第二个参数需要是一个数组

## caller和callee的区别是什么?
函数fun.caller返回调用fun的函数对象，即fun的执行环境，如果fun的执行环境为window则返回null; 
Callee是函数的arguments这个特殊对象的一个属性, 指向函数本身.

## new操作符具体干了什么呢?
第一步创建一个空对象;
第二步将this指向空对象;
第三步动态给刚创建的对象添加成员属性;
第四步隐式返回this
代码分析
## 下面代码的执行结果是什么?

var hellword=(function(){
console.log('hello one');
setTimeout(function(){
console.log('hello two');
},100);
setTimeout(function(){
console.log('hello three');
},0);
console.log('hello four');
}());

依次输出: hello one,hello four,hello three,hello two

## 下面代码执行结果是什么?

var a={
id:10
}
b=a;
b.id=1;
b.name='test';
console.log(a);

执行结果: 
输出 {id: 1, name: "test"}
分析过程: 
对象是一种引用数据类型, 简单的b=a只是把a在内存中的地址赋值给了b, 所以修改b会影响a.

## 下面代码执行结果是什么?

var length=10;
function fn(){
console.log(this.length);
}
var obj={
length:5,
method:function(fn){
fn();
arguments[0]();
}
}
obj.method(fn,1);

执行结果: 
在控制台输出10,2
分析过程:
fn(); 此时this指向window, 所以this.length=10; 
arguments[0]()中的this永远指向arguments, 而arguments本身有一个length属性, 就是参数的个数.

## 下面代码执行完毕, 浏览器依次弹出什么?

(function test(){
var a=b=5;
alert(typeof a); 
alert(typeof b); 
})()
alert(typeof a); 
alert(typeof b); 

执行结果: 
依次弹出: number; number,undefined,number
分析过程:
自调用函数会开辟一个局部作用域, var a=b=5这句代码var只会修饰a, 所以a是一个局部变量, b是全局变量

## 下面代码输出结果是什么?
[1,2,3].map(parseInt);
输出结果:[1,NaN,NaN];
分析过程:

[1,2,3].map(function(item,index){
// console.log(item,index);
//parseInt(数值,进制)
parseInt(1,0);
parseInt(2,1);
parseInt(3,2);
});


## 下面代码执行结果是什么?

console.log(square(5));
var square=function(n){
return n*n;
}

执行结果: 
报错(Uncaught TypeError: square is not a function)
分析过程: 
函数表达式方式声明的函数只提升声明, 不提升赋值, 所以不能再声明之前调用.

## 下面代码执行结果是什么?

console.log(0=='2'==new Boolean(true)=='1');

执行结果: 输出true
分析过程: 0==’2’返回true; true==new Boolean(true)返回true; true==’1’返回true; 所以最终结果是true.

## 下面的代码会输出什么?怎么改动下面代码, 使其依次输出1,2,3,4,5

for(var i=1;i<=5;i++){
setTimeout(function(){
console.log(i);
},1000);
}

执行结果:
在控制台输出:6,6,6,6,6
改造后的代码:

for (var i = 1; i <= 5; i++) {
(function (i) {
setTimeout(function () {
console.log(i);
}, 1000*i)
})(i)
}


## 下面代码执行结果是什么?

var a=10;
function Foo(){
if(true){
let a=4;
}
alert(a);
}
Foo();

执行结果: 弹出10
分析过程: let声明的变量有块级作用域, 所以let 声明的a只在if条件的花括号中生效, 所以会向上级作用域查找.
编码题
## 使用js封装一个冒泡排序
// 冒泡排序
function sortBubble(arr){
for(var i=0;i<arr.length;i++){
for(var j=0;j<arr.length-i;j++){
if(arr[j]>arr[j+1]){
var temp=arr[j];
arr[j]=arr[j+1];
arr[j+1]=temp;
}
}
}
return arr;
}

## 封装一个方法实现去除数组中的重复元素
方案一:

// 数组去重
function unique(arr){
var newArr=[];
for(var i=0;i<arr.length;i++){
if(newArr.indexOf(arr[i])==-1){
newArr.push(arr[i]);
}
}
return newArr;
}

方案二:

var arr=[1,2,2,3,3,4] 
Array.from(new Set(arr))

分析过程:
Set是es6中新增的一种数据类型, 和数组很类似, 但是元素不能重复; Array.from也是es6新增的方法, 可以将类数组对象(伪数组, set), 转换成数组.

## 已知数组var arr=[‘This’, ’is’, ‘Woqu’, ‘Company’], alert出”This is Woqu Company”.

alert(arr.join(' '));


## 编写一个js函数parseQueryString, 它的用途是把url中的参数解析为一个对象, 如
var url=”http://www.demo.cn/index.html?key1=val1&key2-val2”

function parseQueryString(argu) {
var str = argu.split('?')[1];
var result = {};
var temp = str.split('&');
for (var i = 0; i < temp.length; i++) {
var temp2 = temp[i].split('=');
result[temp2[0]] = temp2[1];
}
return result;
}


## 统计str=”jhadfgskjfajhdewqe”字符串中出现最多的字母?
function countStr(str){
var json = {};
// 循环完毕后会得到一个对象,如{a:0,b:1,c:2,d:3,e:4}
for (var i = 0; i < str.length; i++) {
if (!json[str.charAt(i)]) {
json[str.charAt(i)] = 1;
} else {
json[str.charAt(i)]++;
}
};
var iMax = 0;
var iIndex = '';
// 查找出现次数做多的字符,和出现次数
for (var i in json) {
if (json[i] > iMax) {
iMax = json[i];
iIndex = i;
}
}
return {
count:iMax, //出现的最多次数
char:iIndex // 出现次数做多的字符
}
}

## 编码实现对象深拷贝

function deepClone(obj) {
if (obj instanceof Obejct) {
let isArray = Array.isArray(obj)
let cloneObj = isArray ? [] : {}
for (let key in obj) {
cloneObj[key] = isObject(obj[key]) ? deepClone(obj[key]) : obj[key]
}
}else{
throw new Error('obj 不是一个对象！')
}
return cloneObj
}


## 有Student和Person两个类, Person类有name属性和sayName方法, Student类继承自Person类. 分别使用ES5和ES6的语法实现.
ES6实现:

class Person{
constructor(props){
this.name=props.name;
}
sayName(){
console.log(`My name is ${this.name}`);
}
}

class Student extends Person{
constructor(props){
super(props);
this.name=props.name;
}
}

ES5实现
function Person(name=''){
this.name=name;
}
Person.prototype.sayName=function(){
console.log(`My name is ${this.name}`);
}

function Student(name){
Person.call(this,name)
}
Student.prototype=new Person();
Student.prototype.constructor=Student;


## 写一个左中右布局占满屏幕, 其中左右两块固定宽度200,中间自适应,要求先加载中间块, 请写出结构和样式
Css样式

*{
padding: 0;
margin: 0;
}
html,body{
height: 100%;
}
.center{
height: 100%;
background: #1FA363;
margin:0 200px;
}
.left{
position: absolute;
width: 200px;
height: 100%;
left: 0;
top: 0;
background: #DC4C3F;
}
.right{
position: absolute;
width: 200px;
height: 100%;
right: 0;
top: 0;
background: #FFCE44;
}
html结构: 

<div class="center">center</div> 
<div class="left">left</div>
<div class="right">right</div>

思路分析: html标签的加载顺序是自上而下, 所以要想让中间部分先加载, 只需要把中间部分的标签写在最前面即可.

## 如何扩展jquery的静态方法, 如$.getName();

$.extend({
getName: function () { 
// do something
}
});


## 使用js求10000以内的所有质数的和.

function getZs(num) {
var sum=0;
for (var i = 2; i <= num; i++) {//4
//假设所有的数都是质数
var flag = true;
//通过嵌套循环找到 i 除了1 和本身以外所有可能出现的因子
for (var j = 2; j < i; j++) {
//判断 i 是否为质数
if (i % j == 0) {//能进到当前的分支 说明不是质数
flag = false;
}
}
if (flag == true) {
console.log(i);
sum+=i;
}
}
return sum;
}


## 使用js打印出1-10000之间的所有对称数(如121, 1331)

function isSymNum(start, end) {
start = (start <= 11 ? 11 : start);
for (var i = start; i <= end; i++) {
var strI = +(i.toString().split('').reverse().join(''));
if (strI == i) {
console.log(i);
}
}
}


## 二维数组根据num的值进行升序排序:
var list = [
{
id: 32, num: 5
},
{
id: 28, num: 12
},
{
id: 23, num: 9
}]
实现过程:

list.sort(function(a,b){
return a.num-b.num;
})


## Js中eval的功能是什么? 缺点是什么?
eval函数的作用: 可以将一个字符串当做js代码执行.
缺点: 执行效率比较低, 不安全.

## 有一个数列(0,1,1,2,3,5,8,13,..),定义函数求数列第n项

function getFibo(n){
if(n==1) return 0;
if(n==2) return 1;
return getFibo(n-1)+getFibo(n-2);
}


## 使用什么办法能让如下条件判断成立?

if(a==1&&a==2&&a==3){
console.log('ok')
}

方案一:
var a={
value:1,
toString:function(){
return this.value++;
}
}
方案二:

var a = [1,2,3];
a.join = a.shift;

思路分析:
数组本身有一个join方法, 在把数组当做简单数据类型调用的时候,会自动调用join; 而shift也是一个数组的方法, shift是将数组的开头元素删除, 返回值就是删除的元素, a.join=a.shift相当于在每一次调用a的时候都会调用shift方法.
方案三:
var init=1;
Object.defineProperty(window, 'a', {
get: function () {
return init++;
}
});

## 下面代码输出结果是什么?

function changeObjectProperty(o){
// 输出的是这个结果
o.siteUrl = "http://www.csser.com/";
o = new Object();
o.siteUrl = "http://www.popcg.com/";
}
var CSSer = new Object();
changeObjectProperty( CSSer );


console.log( CSSer.siteUrl );

输出结果:  http://www.csser.com/
WebAPI
## 列举DOM元素增删改查的API
创建DOM: document.createElement();
查找DOM:
document.getElementById();
document.getElementsByClassName();
document.getElementsByName();
document.querySelectorAll();
document.querySelector();
追加DOM: parentDom.appendChild();
移除DOM: parentDom.removeChild()

## BOM中有哪些常用的对象?
location: 
location.href; 页面url地址
location.hash; url中#后的部分
location.search; url中?后的部分(查询字符串)
location.reload(); 刷新页面;
navigator:
navigator.userAgent: 浏览器的userAgent信息
history:
history.go(1);前进1步
history.go(-1);后退1步;
history.forward();前进
history.back(); 后退
screen: 
screen.availWidth: 屏幕有效宽度 
screen.availHeight: 屏幕有效高度

## 列举几个常见的浏览器兼容问题?
主流浏览器发送ajax使用XMLHttpRequest创建异步对象,
IE浏览器时候用XActive创建异步对象;
主流浏览器注册事件
addEventListener("eventType","handler","true|false"); removeEventListner("eventType","handler","true|false");
IE浏览器:
注册事件:attachEvent( "eventType"，"handler") 
移除事件:detachEvent("eventType"，"handler" )
阻止事件冒泡:
主流浏览器:event.stopPropagation()
IE浏览器:event.cancleBubble=true;
获取事件源:
主流浏览器: event.target
IE浏览器:event.srcElement

## 什么是事件委托?
本应该注册给子元素的事件, 注册给父元素

## 事件委托的原理是什么?
事件冒泡, 因为有事件冒泡的存在, 所以子元素的事件会向外冒泡, 触发父元素的相同事件, 根据事件对象可以找到真正触发事件的事件源.

## Javscript中有几种定时器, 有什么区别?
setInterval: 间歇定时器, 间隔一定的事件就执行, 执行多次;
setTimeout: 延时定时器, 只执行一次

## 如何实现多个标签页的通信?
localStorage可以实现同一浏览器多个标签页之间通信的原理;
localStorage是Storage对象的实例。对Storage对象进行任何修改，都会在文档上触发storage事件。当通过属性或者setItem()方法保存数据，使用delete操作符或removeItem()删除数据，或者调用clear()方法时，都会发生该事件。
A.html

<input type="text">
<button id="btn">Click</button>
<script>
window.οnlοad=function(){
var oBtn=document.getElementById("btn");
var oInput=document.getElementsByTagName("input")[0];
oBtn.οnclick=function(){
var val=oInput.value;
localStorage.setItem("value",val);
}
}
</script>

B.html

<script>
window.addEventListener("storage",function(event){
console.log("value is"+localStorage.getItem("value"));
console.log("key is"+event.newValue);
},false); 
</script>

