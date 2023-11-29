---
layout: "post"
title: "vsCode"
date: "2019-10-13 14:35"
categories: Tools, vsCode
tags: [Tools, vsCode]
---

# 主题

安装主题插件，个人偏好 `One Dark Pro`

# 快捷键

## 键入提示

vsCode安装成功后，内置了Emmet插件，用于对一些代码进行补全

`h1*6 + tab/enter键`: 

```html
   <h1></h1>
   <h1></h1>
   <h1></h1>
   <h1></h1>
   <h1></h1>
   <h1></h1>
```

`h1*6>{1级标题} + tab/enter键`:

```html
    <h1>1级标题</h1>
    <h1>1级标题</h1>
    <h1>1级标题</h1>
    <h1>1级标题</h1>
    <h1>1级标题</h1>
    <h1>1级标题</h1>
```

`h$*6>{$级标题} + tab/enter键`: 

```html
    <h1>1级标题</h1>
    <h2>2级标题</h2>
    <h3>3级标题</h3>
    <h4>4级标题</h4>
    <h5>5级标题</h5>
    <h6>6级标题</h6>
```

`lorem`： 乱数假文，没有任何实际含义的数字

例如： 

`p*6>lorem + tab/enter键` ： 生成六段乱数假文，用于写静态页面时测试排版

`p*6>lorem1 + tab/enter键`： 生成六段乱数假文，每段只有一个单词

`p*6>lorem1000 + tab/enter键`： 生成六段乱数假文，每段只有1000个单词

`(h2>{章节1})+p>lorem` : 

```html
    <h2>章节1</h2>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Sit veritatis perferendis sint ipsa consectetur eligendi fugiat magni officiis! Nisi repellendus dignissimos dolorem a adipisci odit omnis, id nobis in quod.   
    </p>
```

`(h2[id="chapter$"]>{章节$})*6`:

```html

    <h2 id="chapter1">章节1</h2>
    <h2 id="chapter2">章节2</h2>
    <h2 id="chapter3">章节3</h2>
    <h2 id="chapter4">章节4</h2>
    <h2 id="chapter5">章节5</h2>
    <h2 id="chapter6">章节6</h2>

```

## 其他快捷键

`ctrl + enter键`： 光标切换至下一行
`ctrl + shift + enter键`： 光标切换至上一行

## 其他操作

按住鼠标中间上下移动，可将光标选中多行进行编辑


---


