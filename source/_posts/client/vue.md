---
title: vue
date: 2020-03-24 10:59:46
tags: vue
categories: web前端
---
## vue中如何封装一个组件
首先定义一个后缀名为.vue的文件.文件内部还是三部分组成, template模板部分, script逻辑部分, style样式部分. 这三部分是组件的核心部分, 组件需要哪些结构, 在模板部分书写, 需要什么样的外观样式, 通过style部分书写, 有哪些行为在script部分书写.一定要在script部分使用es6模块化的导出语法(export default{}), 进行导出. 然后在需要调用组件的地方使用es6模块化导入语法导入即可, 组件需要哪些参数, 直接在调用的部分进行传递即可.主要逻辑还是在组件中完成.

## Vue中computed和watch的区别?
computed是计算属性, 可以根据data中的数据成员,动态计算出一个新的数据成员(这个数据成员在data中并不存在), 计算属性的函数必须有返回值; watch是监视器, 可以监视data中某一个数据成员的改变或路由中的某些属性的改变, 可以根据这个改变, 做一些其他操作(不仅仅局限于更新其他相关数据).
Watch监听器:
var vm = new Vue({
el: '#demo',
data: {
firstName: 'Foo',
lastName: 'Bar',
fullName: 'Foo Bar'
},
watch: {
firstName: function (val) {
this.fullName = val + ' ' + this.lastName
},
lastName: function (val) {
this.fullName = this.firstName + ' ' + val
}
}
})
计算属性:
var vm = new Vue({
el: '#demo',
data: {
firstName: 'Foo',
lastName: 'Bar'
},
computed: {
fullName: function () {
return this.firstName + ' ' + this.lastName
}
}
})

## 谈谈对vue中插槽的理解?
Vue中的插槽分为三种, 匿名插槽, 具名插槽, 作用域插槽.
通过插槽可以动态指定某一个组件模板部分的渲染, 我们在调用组件的时候, 在组件的调用标签中间传递了什么样的标签结构, 那么该组件就会把我们传递的标签结构放在他的模板部分进行渲染.

## v-show 和 v-if在隐藏一个元素的时候有什么不同, 应该如何来选择?
v-show是通过css的方式来隐藏元素, 而v-if是根据条件是否成立决定是否要创建元素. 如果某个元素需要频繁切换显示状态的话, 建议是使用v-show, 因为频繁创建销毁DOM需要性能开销.

## 什么是Vuex, 在那种场景下使用?
Vuex是针对vue的一个状态管理工具. 有几个核心的部分:
state存储状态数据;
mutations: 更新数据的方法, 
actions: 调用mutations中的方法, 更新state数据;
getters: 对state中的数据进行预处理
当组件的关系比较复杂的时候, 可以使用vuex简化组件间的传值.

## 说说Vue路由的使用步骤?
第一步:下载路由模块vue-router;
第二步:创建路由对象;
第三步:配置路由规则;
第四步:将路由对象注册为vue实例对象的成员属性

## 你所了解到的常见Vue组件库有哪些?
PC端组件库: element-ui, ant-design, iview
移动端: mint-ui, vant, vux

## 谈谈对于MVVM的理解?
MVVM由三部分组成M(model数据层), V(view视图层),VM(view-model)视图模型层. 是一种框架的设计思想, vue就是基于mvvm来设计的.
其中M(model)层是负责初始化数据,V(view)只负责页面展示,VM(view-model)用来连接view层和model层, 将数据层的数据传递一个视图层进行展示, 将视图层的操作传递到数据层进行持久化.

## Vue的生命周期?
创建阶段: 只执行一次
beforeCreate(开始进行一些数据和方法的初始化的操作, data中的数据和methods中的方法还不能用),
 created(已经完成数据和方法的初始化, data中的数据和methods中的方法可以使用了),
 beforeMount(开始渲染虚拟DOM),
mounted(已经完成了虚拟DOM 的渲染, 可以操作DOM 了, 只执行一次)
运行阶段: 执行多次
beforeUpdate(data中的数据即将被更新, 会执行多次)
updated(data中的数据已经更新完毕, 会执行多次)
销毁阶段: 只执行一次
beforeDestroy(vue实例即将销毁, 此时data中的数据和methods中的方法依然处于可用状态)
destroyed(vue实例已经销毁, 此时data中的数据和methods中的方法已经不可用)

## Vue实现数据双向绑定的原理?
Vue是使用数据劫持, 结合发布者订阅者模式实现双向数据绑定的

// 初始值
var data = {
msg: 'hello',
title: '标题'
}
for (var key in data) {
Object.defineProperty(window, key, {
get: function () {
// console.log('get被触发了');
return data[key];
},
set: function (input) {
// do something: 如通知界面层更新 
console.log(input, '假装在通知界面');
}
});
}
title = 'title初始值';
console.log(title);


执行过程分析:
读取title或者msg的时候get方法会自动触发; 重新给title或msg赋值的时候,set方法会被自动触发(可以在此处通知界面层更新)

## Vue创建组件的时候,data为什么要使用匿名函数return一个对象?
因为对象是一种引用数据类型,在内存中只有一份. 如果data的值直接是一个对象的话, 那么后期组件在不同的地方多次调用的时候, 会相互产生影响, 因为每一次调用操作的data对象是一样的. 使用函数的方式返回对象, 可以保证组件的每一次调用都会创建一个新对象, 这样组件的每一次调用不会相互产生影响.

## Vue中实现父组件向子组件传递数据?
第一步: 在子组件的调用标签上声明一个自定义属性, 属性值来自父组件的data
第二步: 在子组件的定义部分声明一个属性props, 值是一个数组, 将自定义属性的名字在props中进行声明; 在子组件的模板部分可以使用props中声明过的数据.

// 父组件
Vue.component('parent',{
template:`
<div> 
<child :msgFromParent="msg"></child> 
<div>`,
data:function(){
return {
title:'父组件的标题',
msg:'这是传给子组件的值'
}
},
// 子组件
components:{
child:{
// 模板
template:`
<div>
<h1>{{msgFromParent}}</h1> 
</div>`,
// 数据模型
data:function(){
return {
title:'子组件标题'
}
},
//获取父组件中传过来的值
props:['msgFromParent']
}
}
});


## Vue中如何实现子组件向父组件传递数据?
第一步: 在子组件的调用标签只上通过v-on动态绑定一个自定义事件, 自定义事件的处理函数必须在父组件的methods中提前声明, 这个函数需要一个形参, 来接收子组件传递过来的数据.
第二步: 在子组件中通过this.$emit(自定义事件,数据)触发自定义事件的执行, 此动作可以放在子组件的created/mounted生命周期中, 可以放在某个事件处理函数中.

## Vue中实现兄弟组件间的传递数据?
第一步: 声明一个空的Vue实例对象comm, 作为事件中心的角色
第二步: 在acom组件中通过comm.$emit(自定义事件,数据)的方式触发事件(此操作可放在某个事件处理函数或者acom组件的生命周期函数created/mounted中)
第三步: 在bcom组件中通过comm.$on(自定义事件,function(data){})监听自定义事件的执行(操作可放在bcom组件的声明周期函数created/mounted中)

// 公共组件
var comm=new Vue();
// 兄弟组件1

Vue.component('coma',{
template:`
<div>
<h1>{{title}}</h1>
<button @click="sendMsg">发送</button>
</div>
`,
data:function(){
return {
title:'组件A',
msg:'传给兄弟组件的值'
}
},
methods:{
sendMsg:function(){
comm.$emit('myevent',this.msg)
}
},
created:function(){
// 注册自定义事件
comm.$emit('myevent',this.msg);
console.log('注册事件OK');
}
});
// 兄弟组件2
Vue.component('comb',{
template:`
<div>
<h1>{{title}}</h1>
<h1>{{msg}}</h1>
</div>
`,
data:function(){
return {
title:'组件B',
msg:''
}
},
mounted:function(){
comm.$on('myevent',(data)=>{
this.msg=data 
console.log(data);
});
}
});


## Vue中有几种路由模式?
Vue中的路由模式有两种:hash,history; 默认是hash模式; 可以在创建路由对象的时候, 使用mode属性来切换路由模式.
const router=new Router({mode:’history’})

## Vue路由导航守卫是什么, 以及应用场景
路由守卫是在页面进行路由跳转的时候做一些处理, 比如拦截.
vue-router中提供了下面几种路由导航守卫:
全局前置守卫

const router = new VueRouter({ ... })

router.beforeEach((to, from, next) => {
// from从里来
// to到哪里去
// next是否要放行
})

全局后置钩子

router.afterEach((to, from) => {
// ...
})


路由独享守卫: 在声明路由的时候, 针对特定路由的钩子函数

const router = new VueRouter({
routes: [
{
path: '/foo',
component: Foo,
beforeEnter: (to, from, next) => {
// ...
}
}
]
})


## Vue如何自定义一个过滤器？
定义全局过滤器:
Vue.filter(‘过虑器名称’,function(input){ return input });
定义局部过滤器:

new Vue({
filters:{
dateFmt:function(input){
return 'yyyy-mm-dd';
}
} 
})


## Vue如何自定义一个vue指令？
定义全局指令:
Vue.directive(‘指令名’,function(el,binding){});
定义私有指令:
new Vue({
directives:{
focus:function(el,binding){
}
}
});

## 怎么定义 vue-router 的动态路由? 怎么获取通过路由传过来的参数?

const router=new VueRouter({
routes:[
{path:'/product/:id',component:Product}
]
});
// 获取参数:
this.$route.params.id


## Vue路由模块中$route和$router的区别?
$route中存储的是跟路由相关的属性(如$route.params,$route.query) ;  $router中存储的是和路由相关的方法(如$router.push(),$router.go()), 

## vue中v-for指令循环遍历中key属性的作用？
Key属性的作用是在数据层和视图层之间建立一一对应关系, 方便后期对页面进行局部更新. 如果某一条数据发生改变, 只更新当前数据对应的DOM元素.

## Vue和react有哪些不同的地方?
Vue实现了双向数据绑定(数据<=>界面);react仅仅实现了单项数据流(数据层=>界面层); vue中提供了指令, react中没有指令的概念. vue中使用插值表达式在进行数据渲染, react中使用jsx进行数据的渲染.

## Vue有哪些常用的事件修饰符?
.prevent: 阻止默认事件;
.stop: 阻止冒泡;
.once: 事件执行一次;
.self: 只当在 event.target 是当前元素自身时触发处理函数

## 列举Vue中常用的指令
v-model:实现双向数据绑定;
v-bind: 绑定属性;
v-on:注册事件;
v-html: 设置标签内容(允许内容html)
v-text: 设置标签的内容(不允许包含html)
v-clack: 解决插值表达式闪烁问题
V-for: 循环遍历数组或对象

## Vue中如何解决插值表达式闪烁问题?
使用v-html或v-text替代插值表达式;
使用v-clack解决插值表达式闪烁, 
第一步:声明属性选择器[v-clack]{display:none}
第二步:在插值表达式所在标签添加属性v-clack

## Vue路由中如何实现通过锚点值的改变切换组件?
通过监听hashchange事件, 具体如下:

window.addEventListener('hashchange',function(){
console.log('hash change');
});
 

## vue中如何实现给样式添加作用域?说明其实现原理
vue中要给样式添加作用域, 只需要给style标签添加scoped属性即可.
实现原理:
添加了scoped属性的style标签内的样式会被改写成一个交集选择器, 会在原来类名的基础上添加一个随机属性(如.container[v-abcde]), 同时引用该类名的标签也会添加一个相同的属性(如<div class=”container”  v-abcde></div>) , 这样的话, 这个类名就可以对引用它的标签生效, 同时不会影响其他同类名的标签.

## Vue中如何动态添加一个路由规则?
使用router.addRoutes([{path:’’,component:’’}])

## Vue中有何优化页面的加载效率?
使用路由懒加载和组件懒加载; 
不要打包一些公共的依赖(vue, 组件库);
使用CDN加载这些依赖文件

## 什么是路由懒加载? 路由懒加载有什么好处? 如何实现路由懒加载?
路由懒加载是指通过异步的方式来加载对应的路由组件(默认情况是将所有的组件全部加载并打包).
路由懒加载的好处: 可以提高页面的加载速度, 尤其是首页的加载速度(因为使用了懒加载后, 加载首页的时候, 就不需要加载其他页面对应的组件, 在需要的时候再加载)
具体实现:

import Vue from 'vue';
import Router from 'vue-router'; 
// 异步导入组件 
// 异步加载方式一
const List = resolve => require(['@/components/list'], resolve);
// 异步加载方式二
const Detail = () => import(/* webpackChunkName: "group-master" */ '@/components/detail')

Vue.use(Router); 
export default new Router({
// 路由规则
routes:[
{path:'/list',component:List},
{path:'/detail',component:Detail}
],
// 路由模式: 默认hash, 可选值hash(如#/index)|history(/index)
mode:'history'
});


## Vue中如何触发一个自定义事件?
通过this.$emit(event, ’数据’) 可以触发自定义事件的执行.

## Vue中如何监听自定义事件的执行?
通过this.$on(event,callback)可以监听自定义事件的执行

## Vue中如何移除自定义事件?
通过this.$off(event,callback)可以移除一个自定义事件; 如果某些特殊场景下,一个事件被触发一次后就需要将其移除, 可以使用this.$once(event,callback)进行事件注册

## vm.$mount(selector)方法的作用是什么?
手动将一个vue实例挂载到页面上

var MyComponent = Vue.extend({
template: '<div>Hello!</div>'
})
// 创建并挂载到 #app (会替换 #app)
new MyComponent().$mount('#app')
// 同上
new MyComponent({ el: '#app' })


## Vue中keep-alive组件的作用是什么?
keep-alive可以将被包裹的组件暂存在内存当中, 当页面切换的时候, 组件不会被重复的销毁和创建, 从而可以提高整体性能, 同时也可以保存组件的一些状态. 

## Vue中如何手动销毁一个vue实例?
调用vm.$destroy()可销毁一个vue实例(清理它与其它实例的连接，解绑它的全部指令及事件监听器)

## Vue中有哪些内置的组件?
component, slot, transition, transition-group, keep-alive

<!-- 动态组件由 vm 实例的属性值 `componentId` 控制 -->
<component :is="componentId"></component>

<!--tansition动画组件的使用-->
<transition>
<div v-if="ok">toggled content</div>
</transition>


## vue实例中有哪些属性?
vm.$data可以获取vm实例对象data中的数据;
vm.$props可以获取vm组件接收到的 props 对象数据;
vm.$el可以获取vm实例对象的根dom元素;

var MyComponent = Vue.extend({
template: '<div>Hello!</div>'
})
// 在文档之外渲染并且随后挂载
var vm = new MyComponent().$mount()
document.getElementById('app').appendChild(vm.$el)

vm.$refs可以获取vm实例中注册过 ref 特性的所有dom元素和组件实例.

## Vue.use(plugin)的作用是什么, 使用的时候需要注意什么问题?
Vue.use的作用是安装一个Vue插件, 该方法需要在调用 new Vue() 之前被调用.

## vm.$nextTick(fn)的作用是什么?
延迟某个操作的执行, 直到dom更新以后在执行.
<body>
<div id="app"><h1 ref="h1">{{title}}</h1></div>
</body>
<script>
var vm = new Vue({
el: '#app',
data: {
title: '这是一个标题'
}
created: function () {
this.$nextTick(() => {
             // 在created里直接操作ref会报错
this.$refs.hinnerHTML = '这是更新以后的标题';
});
}
});
</script>


## vue中的混入(mixin)有什么作用?
混入 (mixin) 提供了一种非常灵活的方式，来分发 Vue 组件中的可复用功能。一个混入对象可以包含任意组件选项。当组件使用混入对象时，所有混入对象的选项将被“混合”进入该组件本身的选项。
当组件和混入对象含有同名选项时，这些选项将以恰当的方式进行“合并”。比如，数据对象在内部会进行递归合并，并在发生冲突时以组件数据优先。同名钩子函数将合并为一个数组，因此都将被调用。另外，混入对象的钩子将在组件自身钩子之前调用。

## 如何开发一个vue插件?
Vue.js 的插件应该暴露一个 install 方法。这个方法的第一个参数是 Vue 构造器，第二个参数是一个可选的选项对象

// 定义插件
const myPlugin={
    install:(Vue,options)=>{
         //  添加全局方法或属性
        Vue.myGlobalMethod = function () {
            // 逻辑...
        }
        //  添加全局指令
        Vue.directive('my-directive', {
            bind (el, binding, vnode, oldVnode) {
            // 逻辑...
            }
        })
        //  添加实例方法
        Vue.prototype.$myMethod = function (methodOptions) {
            // 逻辑...
        }
        //  注入组件选项(混入)
        Vue.mixin({
            created: function () {
            // 逻辑...
            }
        })
        //  注册全局组件
        Vue.component('myCompent',{
            template:'<h1>loading...</h1>'
        });

    }
}
export default myPlugin;
// 调用插件
Vue.use(myPlugin,{})


## 什么是ssr? 如何实现ssr?
ssr是全拼(server side rendering) ,中文意思, 服务端渲染, 让页面的渲染在服务端完成, 生产环境必须部署nodeJS的环境, 因为服务端渲染必须借助nodeJS来完成. vue中可以使用nuxt框架实现服务端渲染.

## 什么是SPA?
SPA(Single Page Application), 单页面应用程序, 使用vue, react, angular创建的项目都属于SPA. 因为整个项目只有一个页面, 其他页面都是在该页面的基础上局部刷新而来的.
传统方式创建的项目都是MPA(Mutilple Page Application)多页面应用程序.

## 使用vue,react,angular开发的SPA单页面应用有什么优缺点?
单页面应用虽然性能方面得到了提升, 但是有一个致命的缺点就是不利于seo, 搜索引擎几乎不会抓取单页面应用.