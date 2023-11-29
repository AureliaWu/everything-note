---
layout: "post"
title: "前端基础之HTML5"
date: "2019-7-21 14:26:05"
categories: web,html
tags: [Computer Language, web,html]
---

# 概述

## 超~~~基础概念（各种缩写）
HTML: Hyper Text Markup Language 超文本标记语言；定义网页中有什么
CSS： Cascading Style Sheets 层叠样式表；定义网页中的东西长什么样

VSCode： Visual Studio Code 通用编辑器
MD： MarkDown，文档格式标准

Web： 互联网
W3C: 万维网联盟，非营利性组织: w3.org 为互联网提供各种标准
XML: Extension markup language 可扩展标记语言，用于定义文档结构
MDN： Mozilla Development Network, Mozilla开发者社区

## 什么是HTML

HTML是W3C组织定义的语言标准： 用于描述页面结构的语言

## 什么是CSS
CSS是W3C定义的语言标准： CSS用于描述页面结构的语言

## 执行HTML CSS

HTML&CSS --> 浏览器内核 --> 页面

浏览器：由shell(外壳)和core(内核 JS执行引擎、渲染引擎)组成

常见浏览器(包含自己的内核)： 
1. IE: Trident
2. Firefox: Gecko
3. Chrome: Webkit / Blink
4. Safari: Webkit
5. Opera: Presto(已弃用) / Blink

## 版本和兼容性

HTML5、CSS3

HTML5： 2014年发布，目前浏览器基本都兼容

CSS3： 目前还未定制完成

XHTML： 可以认为是HTML的一种版本，完全符合XML的规范(HTML5发布后，已弃用)

# 第一个页面

Emmet插件： 自动生成Html代码的插件，VSCode自带此插件

快捷键：输入`!`后按`tab`键会自动生成html5代码；输入标签后按`tab`键可补全标签代码

## 代码注释

注释为diamante的阅读者提供帮助，注释不参与运行

使用 `<!-- -->` 进行注释，快捷键：`ctrl + /`

## 元素(标签、标记、element)

元素 = 起始标记(begin tag) + 结束标记(end tag) + 元素内容(页面上需要显示的内容) + 元素属性(描写元素的额外信息)

1. 空元素： 没有结束标记的元素，如： `<img/>` `<input/>`

    空元素的两种写法：
    ``` <meta charset="UTF-8">```
    ``` <meta charset="UTF-8"/>``` 

    html5中空元素可以不加后面的`/`

2. 元素属性 = 属性名 + 属性值

    属性的分类：

    - 局部属性： 某些元素特有的属性
    - 全局属性： 所有元素通用

## 元素的嵌套

父元素、子元素、祖先元素、后代元素、兄弟元素(拥有同一父元素)

## 标准文档结构

文档声明：告诉浏览器当前文档使用的HTML标准是HTML5。不写文档声明将导致浏览器进入怪异渲染模式

    ```html
    <!DOCTYPE html>
    ```

根元素(`<html>`)： 一个页面最多只能有一个，且该元素是所有元素的父元素或祖先元素。HTML5中没有强制要求写此元素，但最好写上以兼容以往版本。其中lang属性为全局属性，表示该元素内部使用的文字是哪种自然语言，声明此属性是为了触发浏览器中翻译、语音等插件。

    `lang="cmn-hans"`表示中国大陆官方简体中文，`lang="zh-CN"`已过时。

    ```html
    <html lang="en">
    </html>
    ```
文档头(`<head>`): 文档头内部的内容不会显示到页面上

文档的元数据(`<meta>`)： 附加信息

charset: 指定网页内容编码

计算机中，电子元件接触到低压电(0~2V)时，用0表示,接触到高压电(2~5 V)时，用1表示。因此计算机中只能存储数字

文字和数字进行对应

比如： a - 97, A - 64

此种规律(字典)叫做字符编码表，GB2312 大陆用的编码表  GBK 台湾用的编码表  UTF-8 是unicode编码的一个版本

Unicode是万国码 将全世界的文字融合 有很多版本 UTF-8 是其中之一

```html
<!DOCTYPE html> <!-- 文档声明 -->
<html lang="en"> <!-- 根元素 -->
<head> <!-- 文档头 -->
    <meta charset="UTF-8"> <!-- 元数据 -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0"> <!-- 用于适配手机端 -->    
    <meta http-equiv="X-UA-Compatible" content="ie=edge"><!-- 用于解决IE浏览器 -->
    <title>Document</title> <!-- 网页标题，显示在浏览器标签，不显示在网页内容中 -->
</head>
<body> <!-- 文档体，页面上所有要参与显示的元素都应该放在文档体中 -->
    
</body>
</html>
```

# 语义化

## 什么是语义化

1. 每一个HTML元素都有具体的含义

a元素： 超链接
p元素： 段落
h1元素： 一级标题

2. 所有元素与展示效果无关

元素展示到页面的效果，应该由CSS决定

因为浏览器带有默认的CSS样式，所以每个元素有一些默认样式

**重要： 选择什么元素，取决于内容的含义，而不是显示出的效果**

## 为什么需要语义化？

1. 为了搜索引擎优化(SEO)

搜索引擎： 百度、搜搜、Bing、Google

每隔一段时间，搜索引擎会从整个互联网中，抓取网页源代码，搜索引擎根据语义化标签来理解网页，语义化越好，搜索引擎就越能理解网页

2. 为了让浏览器理解网页

阅读模式、语音模式

# 文本元素

HTML5中支持的元素： HTML5元素周期表 (http://www.xuanfengge.com/funny/html5/element/)

## h

标题： head

h1~h6： 表示一级标题到六级标题

## p

段落: paragraphs

## span【无语义】

没有语义，仅用于设置样式

某些元素在显示时会独占一行(Html5之前称为块级元素,h5已弃用此说法)，而某些元素不会(Html5之前称为行级元素，h5已弃用此说法)；

## pre

预格式化文本元素

空白折叠： 在源代码中的连续空白字符（空格、换行、制表tab），在页面显示时会被折叠成一个空格

在pre元素中的内容不会出现空白折叠，即在pre元素内部出现的内容，会按照源代码格式显示到页面上

该元素通常用于在网页中显示一些代码。

pre元素功能的本质： 它有一个默认的CSS属性 `white-space: pre`

显示代码时，通常外面套code元素，code表示代码区域。

# HTML实体

实体字符， HTML Entity

通常用于在页面中现实一些特殊符号。

书写格式： 

1. &单词缩写; (常用)
2. &#数字;

常用的实体字符：

- 小于符号：

`&lt;`  (lt是less than 的缩写)
`&#60;`

- 大于符号: 

`&gt;` (gt 是 greater than 的缩写)

- 空格符号：

`&nbsp;` (nbsp 是 non-breaking space 的缩写)

- 版权符号 `©`

`&copy;`

- `&`符号

`&amp;`

# a元素

超链接

## href属性

hyper reference： 通常表示跳转地址

1. 普通链接： 跳转地址 (`href="www.baidu.com"` 跳转到百度)
2. 锚链接： 跳转某个锚点,需要定义id属性(`href="#id"` 定位到当前页面id的位置)

    id属性： 全局属性，表示元素在整个HTML中的唯一标识
    `href="#"` 表示回到顶部

3. 功能链接： 点击后，触发某个功能

- 执行JS代码
- 发送邮件,mailto: (要求用户计算机安装有邮件发送软件：exchange)
- 拨打电话, tel: (要求用户计算机上安装有拨号软件，或使用的是移动端访问)

## target属性

表示跳转窗口位置。

target的取值：

- `_self`: 在当前页面窗口中打开，默认值
- `_blank`: 在新窗口中打开

# 路径的写法

## 站内资源和站外资源

站内资源： 当前网站的资源

站外资源： 非当前网站的资源

## 绝对路径和相对路径

对站外资源使用绝对路径，对站内资源进行相对路径

1. 绝对路径

绝对路径的书写格式：

url地址

```
协议名：//主机名:端口号/路径

schema://host:port/path
```

协议名： http、https、file

主机名： 域名、IP地址

端口： 如果协议是http协议，默认端口号是80；如果协议是https协议，默认端口号是443； 

当跳转目标和当前页面的协议相同时，可以省略协议

2. 相对路径

以`./`开头，`./`表示当前资源所在的目录

可以书写`../`表示返回上一级目录

相对路径中`./`可以省略

# 图片元素

## img元素

image缩写，空元素

src属性： source
alt属性： 当图片资源失效时，将使用该属性的文字替代图片

## 和a元素的联用

```html
<a href="">
    <img src="./xx/xx.jpg">
</a>
```

## 和map元素联用

map： 地图

map的子元素： area

area属性：

shape： 形状 circle 圆形 rect 矩形 poly 多边形
coords： 坐标 根据shape属性的不同而不同

```

原点坐标在图片的左上角，横向往右为X轴，纵向向下为Y轴

 shape="circle" coords="X轴坐标,Y轴坐标,圆的半径" 

 shape="rect" coords="矩形左上角X轴坐标,矩形左上角Y轴坐标,矩形右下角X轴坐标,矩形右下角Y轴坐标" 

 shape="poly" coords="角1的X轴坐标，角1的Y轴坐标，角2的X轴坐标，角2的Y轴坐标..." 

```

**注： 衡量坐标时，为了避免衡量误差，需要使用专业的衡量工具： ps、pxcook 等**
   
```html
<a href="">
    <img usemap="#solarMap" src="./xx/xx.jpg">
</a>
<map name="solarMap">
    <area shape="circle" coords="" href="" alt="">
</map>
```

## 和figure元素联用

指代、定义，通常用于把图片、图片标题、描述包裹起来

子元素： figcaption 通常用于包裹图片标题

# 多媒体元素

video 视频

audio 音频

## video

controls: 控制控件的显示，取值只能为controls

某些属性只有两种状态：1. 不写 2. 取值为属性名，这种属性叫做布尔属性

布尔属性在HTML5中可以不写属性值

```html
<video controls="controls" src=""></video>

<video controls src=""></video><!-- 布尔属性，省略属性值 -->
```

video中的布尔属性： 

controls 控制控件

autoplay 自动播放

muted 静音播放

loop 循环播放

## audio

音频和视频的使用完全一致，属性相同

## 兼容性

1. 旧版本的浏览器不支持这两个元素

对于不支持的浏览器，以前可以换成flash,但由于谷歌浏览器宣布不再支持flash，因此只能提示用户更新浏览器

2. 不同的浏览器支持的音频、视频格式可能不一致

使用`<video>`的子元素`<source>`放置多种格式以获得浏览器最好的兼容性

```html
<body>
    <video controls="controls">
        <source src="xxx/xxx.mp4">
        <source src="xxx/xxx.webm">
    </video>
</body>
```

# 列表元素

## 有序列表

ol: ordered list

li: list item

```html
<body>
把大象装冰箱，总共分几步？
    <ol>
        <li>打开冰箱门</li>
        <li>大象进去</li>
        <li>关上冰箱门</li>
    </ol>
</body>
```

### 常用属性

- `type`(不建议使用)

 1 表示使用数字排列 
 
 i 表示使用罗马数字排列 
 
 a表示使用字母排列

 **type属性曾经在HTML4被弃用过，但是在HTML5中被重新引入。除非列表中序号很重要（比如法律或技术文件中条目通常被需要所引用），否则请使用 CSS list-style-type 属性代替**

 - `reversed`

 顺序倒叙

 ## 无序列表

 ul: unordered list

 li: list item

 无序列表常用于制作菜单或新闻列表

 ## 定义列表

 通常用于一些术语的定义

 dl: difinition list

 dt: definition title

 dd: definition description

# 容器元素

容器元素： 该元素代表一个块区域，内部用于放置其他元素

## div元素

无语义

## 语义化容器元素

header： 通常用于表示页头，也可以表示文章的头部

footer: 通常用于表示页脚，也可以表示文章的尾部

article: 通常用于表示整篇文章

section: 通常用于表示文章的章节

aside: 通常用于表示侧边栏(附加信息)

```html

<body>
    <header>
        页头
    </header>
    <article>
        <header>文章头</header>
        <section>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Pariatur excepturi, eius deserunt incidunt sint eveniet earum adipisci obcaecati, unde repellendus nam minus minima blanditiis nesciunt quas qui veritatis dicta at.</p>
            <p>Amet nobis deserunt facere in nulla consectetur consequatur quos doloremque nam dolor impedit sequi quas veniam, harum, recusandae, tenetur ducimus assumenda. Totam ad repudiandae ipsam ducimus harum recusandae, quaerat eum?</p>
            <p>Porro deleniti, corporis totam autem quos inventore quis voluptas, eum ex, molestias eos aperiam vero voluptate error qui a? Ipsam impedit alias odio ab vitae voluptatibus quas suscipit numquam non?</p>
        </section>
        <footer>文章尾</footer>
    </article>
    <aside>边侧栏</aside>
    <footer>
        页脚
    </footer>    
</body>

```

# 元素包含关系

以前： 块级元素可以包含行级元素，行级元素不可以包含块级元素，a元素除外

现在： 元素的包含关系由元素的内容类别决定

例如，查看h1元素中是否可以包含p元素

总结：

1. 容器元素可以包含任何元素
2. a元素中几乎可以包含任何元素
3. 某些元素有固定的子元素(ul>li,ol>li,dl>dt+dd)
4. 标题元素和段落元素不能相互嵌套，并且不能包含容器元素

---

参考视频

 https://www.bilibili.com/video/av57100756?from=search&seid=2646463889570770154 (2019年 HTML+CSS 零基础权威入学宝典【渡一教育】p1~p15)