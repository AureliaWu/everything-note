---
layout: "post"
title: "Python3"
date: "2022年01月13日16:49:23"
categories: others
tags: [Computer Language, Python, basic]
---

# 安装

## 在Mac上安装Python3

方法一： 从Python官网下载Python3 `https://www.python.org/downloads/`，下载完成后双击运行并安装

方法二： 如果安装了Homebrew,直接通过命令`brew install python3`安装即可,若要指定版本，使用命令`brew install --build-from-source python@3.8`

### 使用Homebrew安装可能出的错

Mac升级为macOS Big Sur系统11.1之后，需要先升级Homebrew，否则使用`brew`命令时会报错 `Version value must be a string; got a NilClass ()`

Homebrew升级命令： `brew update-reset`

查看Homebrew版本命令： `brew --version`

查看python3版本的命令： `python3 --version`

# Mac直接运行`.py`文件

1. 在`.py`文件的第一行加特殊的注释: `#!/usr/bin/env python3`
2. 通过命令行给文件以执行权限 `chmod a+x xx.py`

# Python基础

- 以`#`开头的语句是注释，每一行都是一个语句，当语句以`:`冒号结尾时，缩进的语句视为代码块
- Python程序大小写敏感
  
## 数据类型和变量

### 数据类型

整数、浮点数、字符串、布尔值、空值、列表、字典、自定义数据类型

- 使用`r''`表示`''`内部的字符串默认不转义
- 使用`'''...'''`的格式表示多行内容
- 空值是Python里的一个特殊的值，用`None`表示

### 变量

Python中，可以把任意数据类型赋值给变量，同一个变量可以反复赋值，而而且可以是不同类型的变量。

这种本身类型不固定的语言称之为`动态语言`,与之对应的是`静态语言`静态语言在定义变量时必须指定变量类型，如Java语言。

## 编码

Python源代码是一个文本文件，当源代码中包含中文的时候，保存源代码时就务必要指定保存为UTF-8编码；当Python解释器读取源代码时，为了让它按UTF-8编码读取，通常在文件开头写上以下两行：

```python
# !/usr/bin/env python3
# -*- coding: utf8 -*-
```

第一行注释是为了告诉Linux/OS X系统，这是一个Python可执行程序，Windows系统会忽略此注释

第二行注释是为了告诉Python解释器，按照UTF-8编码读取源代码，否则在源代码中写的中文输出可能会有乱码

## 字符串格式化

Python中采用的格式化方式和C语言是一致的，用`%`实现

```python

'hello, %s' % 'world' --> hello, world

'Hi, %s, you have $%d.' % ('Michael', 10000) --> Hi, Michael, you have $10000.

```

- `%s`表示用字符串替换
- `%d`表示用整数替换
- `%f`表示用浮点数替换
- `%x`表示用十六进制整数替换

**格式化整数和浮点数还可以指定是否补0和整数与小数的位数**

```python

print('%2d-%02d' % (3,1)) --> '3-01'

print('%.2f' % 3.1415926) --> '3.14'

```

## 列表

### list

Python内置的一种数据类型是列表： list

list是一个有序的集合，可以随时添加和删除其中的元素

list.len() 获得list中元素的个数

list[index] 访问每一个指定位置的元素

list.append(xx) 将元素追加到list末尾

list.insert(index, xx) 将元素插入到索引号为index的位置

list.pop() 删除list末尾的元素

list.pop(index) 删除指定位置的元素

**list里面的元素数据类型可以不同，也可以是另一个list**

### tuple

另一种有序列表叫元组： tuple

tuple和list非常类似，但是tuple一旦初始化就不能修改，没有
`append()` `insert()`这样的方法

`t = ()` 定义一个空的tuple


list和tuple是Python内置的有序组合，一个可变一个不可变。

## 条件判断

`if: ... elif: ... else: ...`

`elif`是`else if` 的缩写

## 循环

### for循环

`for...in` 依次把list或tuple中的每个元素迭代出来

`range()`函数可以申请改成一个整数序列，`range(5)`表示生成的序列是从0开始小于5的整数

```python
list(range(5)) --> [0,1,2,3,4]

```

### while循环

只要满足条件就会不断循环

使用`break`可提前退出循环

使用`continue`可跳过当前循环直接开始下次循环

## 字典

Python内置了字典：`dict`，全称`dictionary`,使用键值对存储，具有极快的查找速度

如果key不存在，dict就会报错，为避免key不存在的错误，有两种办法：

- 通过使用`xx in dict`判断key是否存在
- 通过dict.get(xx)，如果key不存在可以返回None或者自己指定的value

返回None的时候，Python的交互环境不显示结果

使用dict.pop(key)会将key对应的键值对一起删除

### set

set和dict类似，也是一组key的集合，但不存储value。set中没有重复的key.

要创建一个set，需要提供一个list作为输入集合，重复元素在set中会被自动过滤

set.add(key) 添加元素到set中，可以重复添加，但是不会有效果

set.remove(key) 删除元素

set可以看成是数学意义上的无需和无重复元素的集合

## 函数

### 调用函数

函数就是最基本的一种代码抽象的方式

Python内置了很多函数可以直接调用，使用函数名和参数就能直接调用函数。

abs() 求绝对值函数

max() 接收任意多个参数并返回最大的那个

int() 把其他数据类型转换成整数

### 定义函数

使用`def`语句定义一个函数，依次写出函数名、括号、括号中的参数、冒号，然后在缩进块在红编写函数体，函数的返回值用`return`语句返回

```python

def my_abs(x):
    if x >= 0 :
        return x
    else:
        return -x
```

#### 空函数

如果想定义一个什么也不做的空函数，可以用pass语句

```python
def nop():
    pass
```

`pass`可以用来作为一个占位符让代码先运行起来

