---
title: 微信小程序
date: 2020-03-24 11:00:34
tags: minapp
categories: 
- 前端面试题
---

## 微信小程序目前有几种主流的开发模式?
微信官方:
原生方式; 
wepy(微信官方推出的开发框架, 为了迎合目前主流前端框架的语法和提高开发效率); 
第三方公司:
mpvue(使用vue的语法开发小程序, 是一个阉割版的vue)
uni-app(使用vue的语法进行开发, 是一个阉割版的vue, 据说一套代码可以编译出运行在多个平台的应用)

## 简单介绍微信小程序的开发过程
首先得注册以为微信小程序, 因为小程序开发过程中需要一个appid;
其次下载腾讯官方的开发者工具(开发者工具必须使用个人微信登录), 小程序只能运行在开发这工具或者微信应用内部;
创建应用, 填入申请的appid, 即可快速生成小程序的项目结构.

## 微信小程序中的tabbar导航如何制作
小程序中的tabbar底部导航是配置出来的, 只需要在应用配置文件中添加一个tabbar配置阶段, 按照官方文档配置即可, tabbar数量至少2个, 最多5个.

## 微信小程序中如何实现页面跳转?
小程序页面跳转:
使用组件<navigator url=”../home/home”>目标页面</navigator>
使用api: wx.navigateTo({url:’../home/home’})
Tabbar页面跳转:
wx.switchTabbar({url:’../index/index’})
使用组件<navigator url=”../home/home” open-type=”switchTab”>目标页面</navigator>

## 简单描述微信小程序的生命周期?
小程序的生命周期分为应用生命周期和页面生命周期.
应用生命周期: 
onLaunch: 应用启动, 只执行一次;
onShow: 应用切换到前台;
onHide: 应用切换到后台模式;
noError: 运行阶段出现错误;
onPageNotFound: 找不到页面
页面生命周期:
onLoad: 页面开始加载;
onReady: 页面加载完毕;
onShow: 页面进入焦点状态;
onHide: 页面进入后台状态

## 微信小程序中如何请求数据接口?
通过wx.request

wx.request({
url: 'test.php', //仅为示例，并非真实的接口地址
data: {
x: '',
y: ''
},
header: {
'content-type': 'application/json' // 默认值
},
success(res) {
console.log(res.data)
}
})



## 如何优化小程序代码包的体积?
分包加载,使用分包加载可以让小程序代码包体积达到8M(最多四个分包,每个分包最大2M);将资源文件尽量放在远程服务器端.

## 你了解到微信小程序有哪些组件库?
Vant Weapp, iview Weapp, minui, WeUI, iview-mpvue
