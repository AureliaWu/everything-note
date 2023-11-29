---
layout: "post"
title: "uni-app"
date: "2019-8-25 10:06:05"
categories: [web,vue, uni-app]
tags: [Computer Language, web,vue, uni-app]
---

# uni-app笔记

## uni-app介绍

`uni-app` 是一个使用 Vue.js 开发所有前端应用的框架，开发者编写一套代码，可发布到iOS、Android、H5、以及各种小程序（微信/支付宝/百度/头条/QQ/钉钉）等多个平台。

## 快速上手

### 下载编辑器HBuilderX

HBuilderX，以下简称HX， HX是轻量编辑器和强大IDE的完美结合体。敏捷的性能，清爽的界面，强大的功能和于一身。HX是通用的前端开发工具，但为uni-app做了特别强化。
下载App开发版，可开箱即用；如下载标准版，在运行或发行uni-app时，会提示安装uni-app插件，插件下载完成后方可使用。因此，直接下载APP版比较方便。

下载地址： https://www.dcloud.io/hbuilderx.html

### 运行


## 页面样式与布局

flex布局？

尺寸和单位： H5适配，宽度使用百分比，高度使用px
uniapp 基准宽度为750px，设计稿1px与框架样式1px转换公式： 设计稿 1px / 设计稿基准宽度 = 框架样式 1px / 750px

内联样式，直接在页面使用style,写在app.vue会应用于所有页面

## 配置文件

### pages.json

#### 默认配置

```json
{
	"pages": [ //pages数组中第一项表示应用启动页，参考：https://uniapp.dcloud.io/collocation/pages
		{
			"path": "pages/index/index",
			"style": {
				"navigationBarTitleText": "uni-app"
			}
		}
	],
	"globalStyle": {
		"navigationBarTextStyle": "black",// 导航栏文字颜色
		"navigationBarTitleText": "uni-app",
		"navigationBarBackgroundColor": "#F8F8F8",
		"backgroundColor": "#F8F8F8"
	}
}

```

`pages`每新建一个页面需要配置一次，放在第一个表示入口页面
`pages.styles` 每个页面个性化背景颜色等配置

#### tabBar

color: 文字颜色
selectedColor: 选中颜色
list: 配置文件路径、图标、名称等

最多只能放五个小图标

#### condition

启动模式配置，仅开发期间生效，用户检查传值？

## 生命周期

### 应用生命周期

`App.vue`文件中的`onLaunch` `onShow` `onHide` 表示的是整个应用的生命周期，进入应用-->显示应用-->关闭应用

`onLaunch`全局只触发一次，可在此处获取用户操作的场景值，如进入主程序、扫码进入程序...

### 页面生命周期

每个页面自己的生命周期：  `onLoad` `onReady` `onShow` `onHide` 等

`onLoad`： 页面初始化，执行一次

`onShow`: 页面进入执行，进入多次，执行多次

`onReady`: 页面加载完毕，执行一次

`onHide`: 页面离开执行，离开多次，执行多次

`onPullDownRefresh`: 监听用户下拉动作

	- 需要在 `pages.json` 里，找到的当前页面的`pages`节点，并在 `style` 选项中开启 `enablePullDownRefresh`。

	- 当处理完数据刷新后，`uni.stopPullDownRefresh` 可以停止当前页面的下拉刷新。

`onShareAppMessage`: 用户点击右上角分享

### 组件生命周期

写在组件中。

`beforeMount`: 在挂载开始之前被调用

`mounted`: 挂载到实例上之后调用

## 路由跳转

### 跳转至tabbar中配置的页面

`uni.switchTab(OBJECT)`

`OBJECT`参数: 

- `url` 

	需要跳转的 tabBar 页面的路径（需在 pages.json 的 tabBar 字段定义的页面），路径后不能带参数

- `success`  

	接口调用成功的回调函数

- `fail` 

	接口调用失败的回调函数

- `complete`

	接口调用结束的回调函数（调用成功、失败都会执行）

### 跳转至非tabbar中配置的页面

#### navigateTo

`uni.navigateTo(OBJECT)`

不关闭当前页，跳转至新页面。如列表页跳到详情页

`OBJECT`参数： 

- `url`	

	需要跳转的应用内非`tabBar`的页面的路径 , 路径后可以带参数。
	参数与路径之间使用?分隔，参数键与参数值用=相连，不同参数用&分隔；

- `animationType`	

	默认值为`pop-in`，表示窗口显示的动画效果

- `animationDuration`

	窗口动画持续时间，单位为ms

- `success`	

	接口调用成功的回调函数	

- `fail`

	接口调用失败的回调函数	
- `complete`

	接口调用结束的回调函数（调用成功、失败都会执行）

#### redirectTo

`uni.redirectTo(OBJECT)`

关闭当前页面，跳转新页面

## 模板语法和数据绑定

声明在data中的数据是响应式绑定

### 列表渲染

使用 `v-for`属性

### 条件渲染

使用 `v-if` 或 `v-hidden`属性

`v-if` 根据条件进行渲染
`v-hidden` 根据条件进行展示，类似于`v-show`

## class 和 style 的绑定

### 动态绑定

class支持的语法 `:class` 
style支持的语法 `:style`

## 事件处理

事件映射表：

```json

```

uni-app中没有什么默认事件，比如submit不会自动提交

## 基础组件

`view` : 视图区域
`scroll-view` : 滚动区域
`swiper` : 轮播区域

## uni-app中的请求


---

官方地址： https://uniapp.dcloud.io/README

参考视频: https://www.bilibili.com/video/av48272338?from=search&seid=7223491785740158297
