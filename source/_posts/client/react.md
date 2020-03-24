---
title: react
date: 2020-03-24 10:58:53
tags: react
categories: web前端
---

## 169.什么是虚拟DOM, 使用虚拟DOM有什么优势?
虚拟 dom 相当于在 js 和真实 dom 中间加了一个缓存，利用 dom diff 算法避免了没有必要的 dom 操作，从而提高性能。
用 JavaScript 对象结构表示 DOM 树的结构；然后用这个树构建一个真正的 DOM 树，插到文档当中,当状态变更的时候，重新构造一棵新的对象树。然后用新的树和旧的树进行比较，记录两棵树差异把所记录的差异应用到步骤 1 所构建的真正的 DOM 树上，视图就更新了。

## 170.简单介绍下react中的diff算法?
把树形结构按照层级分解，只比较同级元素。
给列表结构的每个单元添加唯一的 key 属性，方便比较。
React 只会匹配相同 class 的 component（这里面的 class 指的是组件的名字）
合并操作，调用 component 的 setState 方法的时候, React 将其标记为 dirty.到每一个事件循环结束, React 检查所有标记 dirty 的 component 重新绘制.
选择性子树渲染。开发人员可以重写 shouldComponentUpdate 提高 diff 的性能。

// 创建对比函数
function updateChildren(vnode, newVnode) { 
var children = vnode.children || []
var newChildren = newVnode.children || []

children.forEach(function (childrenVnode, index) {
// 首先拿到对应新的节点
var newChildVnode = newChildren[index] 
// 判断节点是否相同
if (childrenVnode.tag === newChildVnode.tag) { 
// 如果相同执行递归，深度对比节点
updateChilren(childrenVnode, newChildVnode) 
} else {
// 如果不同则将旧的节点替换成新的节点
repleaseNode(childrenVnode, newChildVnode) 
}
})
}

// 节点替换函数
function repleaseNode(vnode, newVnode) { 
var elem = vnode.elem
var newEle = createElement(newVnode)
}



## 171.什么是Redux?
Redux是一个状态管理工具, 不仅可以在react中使用, 也可在其他框架中使用, 甚至可以脱离框架本身使用. redux中有几个核心的组成部分:
store存储数据的对象,必须通过createStore方法来创建;
action更新数据的规则, 必须有一个属性state, 值必须是字符串;
reducer更新数据的函数, 需要传入state状态数据和action更新规则.
在react中使用redux的时候, 一般会使用react-redux来简化使用步骤. 

## 172.React有哪些常用的组件库?
PC端组件库:
element-ui(饿了么推出的前端组件库), ant-design(阿里巴巴的前端组件库, 几乎覆盖了三大框架); zent(有赞推出的PC端组件库)

## 173.React中如何操作DOM?
在需要进行dom操作的标签上设置一个ref属性, 保证值不要重复, 后期在js部分可以通过”this.refs.属性名”来获取标签的虚拟dom对象.

## 174.什么是高阶组件(HOC)?
函数的返回值是一个函数, 我们称之为高阶函数. 同理一个组件返回值如果还是一个组件, 那么就称之为高阶组件. redux中提供的connect就是一个高阶组件.

## 175.React中调用setState后发生了什么?
在代码中调用 setState 函数之后，React 会将传入的参数对象与组件当前的状态合并，然后触发所谓的调和过程（Reconciliation）。经过调和过程，React 会以相对高效的方式根据新的状态构建 React 元素树并且着手重新渲染整个 UI 界面。在 React 得到元素树之后，React 会自动计算出新的树与老树的节点差异，然后根据差异对界面进行最小化重渲染。在差异计算算法中，React 能够相对精确地知道哪些位置发生了改变以及应该如何改变，这就保证了按需更新，而不是全部重新渲染。

## 176.React中状态state和属性props有什么不同?
state是组件的私有数据, 可读可写, props是只读属性, 一般来自外部(比如父组件)

## 177.React中有几种创建组件的方式?
通过函数的方式创建组件, 此种方式创建的组件为无状态组件(不常用);
React.createClass();
通过class类的方式创建组件(须继承React.Component), 实际开发中使用此种方式.

## 178.React中的组件按照职责不同, 可以分为几种类型?
根据组件的职责通常把组件分为 UI 组件和容器组件;
UI 组件负责 UI 的呈现，容器组件负责管理数据和逻辑;
两者通过 React-Redux 提供 connect 方法联系起来.

## 179.类组件(Class component)和函数式组件(Functional component)之间有何不同?
类组件不仅允许你使用更多额外的功能，如组件自身的状态和生命周期钩子，也能使组件直接访问 store 并维持状态;当组件仅是接收 props，并将组件自身渲染到页面时，该组件就是一个 '无状态组件(stateless component)'，可以使用一个纯函数来创建这样的组件。这种组件也被称为哑组件(dumb components)或展示组件.

## 180.说说react的生命周期函数?
初始化阶段：
getDefaultProps:获取实例的默认属性
getInitialState:获取每个实例的初始化状态
componentWillMount：组件即将被装载、渲染到页面上
render:组件在这里生成虚拟的 DOM 节点
componentDidMount:组件真正在被装载之后
运行中状态：
componentWillReceiveProps:组件将要接收到属性的时候调用
shouldComponentUpdate:组件接受到新属性或者新状态的时候（可以返回 false，接收数据后不更新，阻止 render 调用，后面的函数不会被继续执行了）
componentWillUpdate:组件即将更新不能修改属性和状态
render:组件重新描绘
componentDidUpdate:组件已经更新
销毁阶段：
componentWillUnmount:组件即将销毁

## 181.react 性能优化可以使用哪个生命周期函数？
shouldComponentUpdate 这个方法用来判断是否需要调用 render 方法重新描绘 dom。因为 dom 的描绘非常消耗性能，如果我们能在 shouldComponentUpdate 方法中能够写出更优化的 dom diff 算法，可以极大的提高性能。

## 182.应该在 React 组件的何处发起 Ajax 请求?
在 React 组件中，应该在 componentDidMount 中发起网络请求。这个方法会在组件第一次“挂载”(被添加到 DOM)时执行，在组件的生命周期中仅会执行一次。更重要的是，你不能保证在组件挂载之前 Ajax 请求已经完成，如果是这样，也就意味着你将尝试在一个未挂载的组件上调用 setState，这将不起作用。在 componentDidMount 中发起网络请求将保证这有一个组件可以更新了。

## 183.React如何实现服务端渲染?
Next.js 是一个轻量级的 React 服务端渲染应用框架.

## 184.自定义的react组件首字母为什必须要大写?
Babel在对jsx代码进行编译的时候, 如果首字母大写, 就把其当做react组件编译, 编译成js对象; 如果首字母小写,则认为是一个普通的html标签, 会解析成普通字符串.
## 185.setState 什么时候是同步,什么时候是异步?
这里的“异步”不是说异步代码实现. 而是说 react 会先收集变更,然后再进行统一的更新. setState 在原生事件和 setTimeout 中都是同步的. 在合成事件和钩子函数中是异步的. 在 setState 中, 会根据一个 isBatchingUpdates 判断是直接更新还是稍后更新, 它的默认值是 false. 但是 React 在调用事件处理函数之前会先调用 batchedUpdates 这个函数, batchedUpdates 函数 会将 isBatchingUpdates 设置为 true. 因此, 由 react 控制的事件处理过程, 就变成了异步(批量更新).

## 186.React 事件机制跟原生事件有什么区别?
React 的事件使用驼峰命名, 跟原生的全部小写做区分.不能通过 return false 来阻止默认行为, 必须明确调用 preventDefault 去阻止浏览器的默认响应.

## 187.React 事件中为什么要绑定 this 或者要用箭头函数?
事实上, 这并不算是 react 的问题, 而是 this 的问题. 但是也是 react 中经常出现的问题. 因此也讲一下<button type="button" onClick={this.handleClick}>Click Me</button>这里的this是当事件被触发时进行绑定的.  this的值会回退到默认绑定，即值为 undefined，这是因为类声明和原型方法是以严格模式运行。我们可以使用 bind 绑定到组件实例上. 而不用担心它的上下文.因为箭头函数中的 this 指向的是定义时的 this，而不是执行时的 this. 所以箭头函数同样也可以解决.
## 188.谈谈react中的事件机制
在组件挂载的阶段, 根据组件生命的 react 事件, 给 document 添加事件 addEventListener, 并添加统一的事件处理函数 dispatchEvent.
将所有的事件和事件类型以及 react 组件进行关联, 将这个关系保存在一个 map 里. 当事件触发的时候, 首先生成合成事件, 根据组件 id 和事件类型找到对应的事件函数, 模拟捕获流程, 然后依次触发对应的函数.
## 189.谈谈 jsx 的原理
<div>Hello ConardLi</div>
实际上, babel 帮我们将这个语法转换成
React.createElement('div', null, `Hello ConardLi`)

## 190.Jsx在书写的时候和html有什么不同?
必须有一个根标签在最外层包裹(因为这里的标签需要babel编译, 编译成React.createElement(‘标签名’,’属性对象’, ’内容’) )
双标签和单标签(<br/>,<hr/>)都必须闭合, 否则无法通过编译

## 191.在jsx中如果非要创建多个平行标签, 该如何处理?
在jsx的最外层使用<></>进行包裹;
或者使用<React.Fragment></React.Fragment>标签进行包裹;
两种方式本质是一样的, 底层都是通过
document.createDocumentFragment()创建了一个虚拟dom标签.

