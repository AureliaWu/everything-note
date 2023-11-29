---
layout: "post"
title: "微信小程序"
date: "2020-2-4 11:30"
categories: miniProgram
tags: [Computer Language, miniProgram]
---

# 开发环境

参考微信小程序官方文档： https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/getstart.html

1. 注册账号

- 每个邮箱仅能申请一个小程序

- 邮箱必须未被微信公众号注册且未被微信用户绑定

2. 获取APPID

3. 下载微信小程序开发工具，下载地址： https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html

# 小程序Demo

启动微信小程序开发工具，使用测试appid新建项目。

## 小程序结构目录

结构|传统web|微信小程序
-|-|-
结构|HTML|WXML
样式|CSS|WXSS
逻辑|JavaScript|JavaScript
配置|无|JSON

**传统web是三层结构，微信小程序是四层结构，多了一层配置.json**

## 初始化demo结构分析

- pages 用于存放页面

- utils 存放工具类

- app.js 小程序入口文件

- app.json 公共配置文件，配置小程序大体结构(默认标题等)

- app.wxss 全局样式

- project.config.json 对应小程序开发工具详情中的内容

## 配置文件介绍

一个小程序应用包括最基本的两种配置文件： 全局设置的app.json和页面自己的page.json

**配置文件中不能出现注释**

### 全局配置文件app.json

全局配置文件可配置小程序的所有页面路径、界面表现、网络超时时间、底部tab等。

https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/app.html

Demo中的默认配置如下： 

```json
{
  "pages": [
    "pages/index/index",
    "pages/logs/logs"
  ],
  "window": {
    "backgroundTextStyle": "light",
    "navigationBarBackgroundColor": "#fff",
    "navigationBarTitleText": "WeChat",
    "navigationBarTextStyle": "black"
  },
  "style": "v2",
  "sitemapLocation": "sitemap.json"
}

```

- pages 整个小程序中拥有的页面路径

    一般新增页面时需要进行两步操作： 1. 在指定位置新增页面 2. 将新增页面路径填入app.json的pages中

    使用小程序开发工具，直接在app.json中添加pages路径，编译后会自动新增文件和文件夹

    小程序加载顺序是根据页面路径的配置而来

- window

    设置小程序的状态栏、导航条、标题、窗口背景色等

    https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/app.html#window

- tabBar 

    配置底部导航栏

    - `list`: tab的列表，最少 2 个、最多 5 个 tab
        tab 按数组的顺序排序，每个项都是一个对象，其属性值只有四个：
        `pagePath`、`text`、`iconPath`、`selectedIconPath`

    - `color`: tab 上的文字默认颜色，仅支持十六进制颜色

    示例： 

    ```json
        {
        "pages": ["pages/index/index", "pages/logs/index"],
        "window": {
            "navigationBarTitleText": "Demo"
        },
        "tabBar": {
            "list": [
            {
                "pagePath": "pages/index/index",
                "text": "首页"
            },
            {
                "pagePath": "pages/logs/logs",
                "text": "日志"
            }
            ]
        },
        "networkTimeout": {
            "request": 10000,
            "downloadFile": 10000
        },
        "debug": true,
        "navigateToMiniProgramAppIdList": ["wxe5f52902cf4de896"]
    }

    ```

    ### 页面配置文件

    用来表示页面目录下的`page.json`和小程序页面相关的配置，可以在此独立定义每个页面的一些属性，如顶部颜色、是否允许下拉刷新等。

    页面的配置只能设置app.json中部分`window`配置项的内容，页面中的配置项会覆盖`app.json`的`window`中相同的配置项

    ## 视图层

    `WXML(WeiXin Markup Language)`是框架设计的一套语言，集合基础组件、事件系统可以构建出页面的结构

    ### 基础组件

    https://developers.weixin.qq.com/miniprogram/dev/component/view.html

    名称|	功能说明
    -|-
    `cover-image`|	覆盖在原生组件之上的图片视图
    `cover-view`|	覆盖在原生组件之上的文本视图
    `movable-area`|	movable-view的可移动区域
    `movable-view`|	可移动的视图容器，在页面中可以拖拽滑动
    `scroll-view`|	可滚动视图区域
    `swiper`|	滑块视图容器
    `swiper-item`	|仅可放置在swiper组件中，宽高自动设置为100%
    `view`|	视图容器

    - `view` 标签

        类似于`div`，但有自己的属性

        如`hover-class`表示 指定按下去的样式类

    - `text`标签

        显示普通的文本，只能嵌套text

        `selectable` 表示文本是否可选，默认为否

        `decode` 表示是否解码，默认为否

    - `image`图片标签

        默认宽度为320px,高度240px

        **此标签其实是web中的图片标签和背景图片的结合，并且不支持web中的背景图片的写法**

        属性名| 类型 | 默认值 | 说明
        -|-|-|-
        src|string| |图片地址
        mode|String|'scaleToFill'|图片裁剪、缩放的模式
        lazy-load|Boolean|false|图片懒加载，只针对page与scroll-view下的image起作用
    
    - `swiper`标签

        轮播图组件，默认宽度100%,高度150%
        
        子元素必须有`swiper-item`

    - `navigator`标签

        导航组件，类似超链接标签

        `target`: 在哪个目标发生跳转，默认当前小程序，可选值self/miniProgram

        `url`: 当前小程序内跳转链接

        `open-type`: 跳转方式

    - `video`

        视频。原生组件，类似于web中的video

    - 自定义组件

        一个组件由`json` `wxml` `wxss` `js` 4个文件组成

        1. 声明组件

            需要在json文件中进行自定义组件声明

            ```json
            {
                "component": true
            }
            ```
        2. 编辑组件

        3. 使用自定义组件

            在页面的`json`文件中进行引用声明，并提供对应的组件名和组件路径

            ```json
                {
                    // 引用声明
                    "usingComponents": {
                        // 要使用的组件名称     // 组件的路径
                        "component-tag-name": "path/to/the/custom/component"
                    }
                }
            ```

    ### 事件

    ### 数据绑定

    WXML文件中使用&#123;&#123;&#125;&#125;

    属性中要体现布尔类型的值，也必须加上两个大括号。

    错误写法: `<checkbox checked="false"></checkbox>`

    正确写法: `<checkbox checked="&#123;&#123;false&#125;&#125flase"></checkbox>`

    ### 运算

    - 三元运算

        `<view hidden="&#123;&#123; flag ? true : false &#125;&#125">Hidden</view>`
    
    - 算术运算

        在&#123;&#123;&#125;&#125;中直接进行算术运算
    
    - 逻辑判断

        `wx:if` if条件

    **花括号和引号之间如果有空格，最终将被解析成字符串**

### 列表渲染

`wx:for`

项的变量名默认为`item`，`wx:for-item`可以指定数组当前元素的变量名

下标变量名默认为`index`, `wx:for-inidex`可以指定数组当前下标的变量名

```html
<view wx:for="{{array}}">
    {{index}}: {{item.meaasge}}
</view>

Page({
    data: {
        array:[{
            message: 'hello'
        },{
            message:'what'
        }]
    }
})
```

### WXSS

WXSS(WeiXin Style Sheet)是一套样式语言，用于描述WXML的组件样式，与CSS相比，WXSS扩展的特性有： 尺寸单位、样式导入

- 尺寸单位`rpx`

    `rpx`(responsive pixel): 可根据屏幕宽度进行自适应

- 样式导入

使用`import`语句导入

`@import "被导入文件路径"`

**样式文件wxss中的注释不能用`//`,只能用`/**/`**

