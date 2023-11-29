---
layout: "post"
title: "前端基础之canvas"
date: "2020-3-21 10:59"
categories: web,CSS
tags: [Computer Language, web,CSS]
---

canvas最早由Apple引入WebKit，用于Mac OS X的dashboard，后来又在safari和Google Chrome被实现。基于Geoko 1.8的浏览器（如firefox1.5）支持此元素。

`<canvas>`元素是WhatWG Web applications 1.0规范的一部分，也包含于HTML5中。`<canvas>`不再是语义化标签，存在兼容性问题，因此使用语义化标签兼容插件无法解决兼容问题。

# canvas体验

绘图步骤：

1. 准备画布

    使用`<canvas>`标签定义一个画布，默认画布为透明色(`rgba(0, 0, 0, 0)`)，大小为300*150

    可在`<canvas>`的样式中设置边框，但不设置大小，画布大小在`<canvas>`属性中设置

    ## canvas尺寸设置

    - 在样式中设置`canvas`尺寸：

        ```css
        canvas{
            border: 1px solid pink;
            width: 600px;
            height: 400px;
        }
        ```
        运行结果：

        ![canvas使用样式设置尺寸](/source/data/img/html/canvas/canvas尺寸样式.png)

    - 使用`canvas`属性设置画布尺寸

        ```html
        <canvas width="600px" height="400px"></canvas>
        ```

        运行结果：

        ![canvas使用属性设置尺寸](/source/data/img/html/canvas/canvas尺寸属性.png)

    可以看出虽然两种方法设置的画布最终大小是一致的，但画布中的内容却不一样。

    **使用样式设置画布大小，相当于对画布进行了放大操作，画布中的内容也会被拉伸；使用canvas自带属性设置画布大小设置的是画布的实际大小，内容不会有影响**

2. 准备绘图工具

    `<canvas>`标签中不能写内容，因此绘图工具只能在js中设置

3. 利用工具绘图

    绘图步骤也需写在JS中

    ```javascript

    // 1. 获取canvas元素
    var myCanvas = document.querySelector('canvas');

    // 2. 获取上下文(此处上下文为canvas的回执工具箱)
    var ctx = myCanvas.getContext('2d');

    // 3. 移动画笔
    ctx.moveTo(100,100);

    // 4. 绘制直线(轨迹/绘制路径)
    ctx.lineTo(200,100);

    // 5. 描边
    ctx.stroke();

    ```

**canvas不支持3d效果，一般使用web gl绘制3d效果的网页**

# 绘制平行线

## 绘制两条平行线

```javascript
var myCanvas = document.querySelector('canvas');
var ctx = myCanvas.getContext('2d');

// 绘制第一条线
ctx.moveTo(100,100);
ctx.lineTo(300,100);

// 绘制第二条线
ctx.moveTo(100,200);
ctx.lineTo(300,200);

// 描边
ctx.stroke();

```

## 关于描边

描边默认的宽度是1px,默认颜色为黑色，但实际在浏览器显示为2px,浅黑色

描边线的中心位置与刻度线对齐，因此描边线会占据浏览器上下各0.5px，但浏览器无法解析0.5px，只能解析1px，因此最终显示结果是宽度为2px,颜色饱和度降低

解决方案： 前后(Y轴)移动0.5px

### 绘制三条不同颜色的平行线

```javascript
    var myCanvas = document.querySelector('canvas');
    var ctx = myCanvas.getContext('2d');

    // 开启新路径
    ctx.beginPath();

    // 绘制第一条蓝线
    ctx.moveTo(100,100);
    ctx.lineTo(300,100);
    ctx.strokeStyle = 'blue';
    ctx.lineWidth = 10;
    ctx.stroke();

    // 开启新路径
    ctx.beginPath();
    // 绘制第二条红线
    ctx.moveTo(100,200);
    ctx.lineTo(300,200);
    ctx.strokeStyle = 'red';
    ctx.lineWidth = 20;
    ctx.stroke();

    // 开启新路径
    ctx.beginPath();
    // 绘制第三条绿线
    ctx.moveTo(100,300);
    ctx.lineTo(300,300);
    ctx.strokeStyle = 'green';
    ctx.lineWidth = 30;
    ctx.stroke();

```

绘制不同属性的线条时，需要用`ctx.beginPath();`来开启新路径解决样式覆盖问题

# 绘制三角形

```javascript
    ctx.moveTo(200,100);
    ctx.lineTo(300,200);
    ctx.lineTo(100,200);
    ctx.lineTo(200,100);
    ctx.lineWidth = 10;
    ctx.stroke();
```

使用此方法绘制出的三角形会出现起始点和lineto的连接点无法闭合产生缺角的问题:

![canvas绘制手动闭合三角形](/source/data/img/html/canvas/canvas手动闭合三角形.png)

解决方案：使用`ctx.closePath()`让canvas自动闭合

```javascript
    ctx.moveTo(200,100);
    ctx.lineTo(300,200);
    ctx.lineTo(100,200);
    // ctx.lineTo(200,100);
    ctx.closePath();// 关闭路径
    ctx.lineWidth = 10;    
    ctx.stroke();
```

![canvas绘制自动闭合三角形](/source/data/img/html/canvas/canvas自动闭合三角形.png)

## 绘制填充的三角形

```javascript
    ctx.moveTo(200,100);
    ctx.lineTo(300,200);
    ctx.lineTo(100,200);
    ctx.lineTo(200,100);
    ctx.fillStyle = '#FF4040';
    ctx.fill();
```

绘制结果：

![canvas绘制填充三角形](/source/data/img/html/canvas/canvas填充三角形.png)

**填充时不再使用`ctx.stroke()`而是使用`ctx.fill()`,同样的，填充样式属性用的是`fillStyle`而不是`strokeStyle`**

# 绘制镂空正方形

```javascript
    // 顺时针绘制100*100小正方形
    ctx.moveTo(100,100);
    ctx.lineTo(100,200);
    ctx.lineTo(200,200);
    ctx.lineTo(200,100);
    ctx.closePath();

    // 逆时针绘制200*200大正方形
    ctx.moveTo(50,50);
    ctx.lineTo(250,50);
    ctx.lineTo(250,250);
    ctx.lineTo(50,250);
    ctx.closePath();

    ctx.fill();// 非零环绕填充规则进行填充
```

绘制结果：

![canvas绘制镂空正方形](/source/data/img/html/canvas/canvas绘制镂空正方形.png)

**非零环绕规则**：从区域内往外画一条足够长的线，线与顺时针路径相交，计数器+1，与逆时针路径相交，计数器-1，计数器最终不为0则填充

![非零环绕规则图解](/source/data/img/html/canvas/非零环绕规则图解.png)

## 与线条相关的属性(画笔状态)

- `lineWidth`: 线宽，默认1px

- `lineCap`: 线末端属性： butt、round、square

- `lineJoin`: 相交线的拐点： miter(默认)、round、bevel

- `strokeStyle`: 线的颜色

- `fillStyle`: 填充颜色

- `setLineDash()`: 设置虚线

    `setLineDash()`方法中需要传一个数组，用来描述虚线的排列方式,如`ctx.setLineDash([5,10,15,20])`


- `getLineDash()`: 获取虚线宽度集合

- `lineDashOffset`: 设置虚线偏移量(负值向右偏移)

# 绘制渐变色矩形

绘制思路： 绘制点组成线，为每个点上色

# 绘制折线图

绘制流程： 绘制网格 --> 绘制坐标系 --> 绘制点 --> 连点成线

具体实现： 

```javascript

    // 1. 构造函数
    var LineChart = function(ctx) {
        // 获取绘制工具
        this.ctx = ctx || document.querySelector('canvas').getContext('2d');

        // 设置画布大小
        this.canvasWidth = this.ctx.canvas.width;
        this.canvasHeight = this.ctx.canvas.height;

        // 设置网格大小
        this.gridSize = 10;

        // 设置坐标系的间距
        this.space = 20;

        // 设置坐标原点位置
        this.x0 = this.space;
        this.y0 = this.canvasHeight - this.space;

        // 设置箭头大小
        this.arrowSize = 10;

        // 设置点的大小
        this.dotSize = 6;
    }

    // 2. 行为和方法

    // 初始化
    LineChart.prototype.init = function(data) {
        this.drawGrid();
        this.drawCoordinate();
        this.drawDots(data);
    };

    // 绘制网格
    LineChart.prototype.drawGrid = function () {
        // X轴方向线条数 = 画布高度 / 网格大小  向下取整
        var xLine = Math.floor(this.canvasHeight / this.gridSize);

        // 绘制x轴方向线
        for (let i = 0; i <= xLine; i++) {
           this.ctx.beginPath();
           this.ctx.moveTo(0, i * this.gridSize - 0.5);
           this.ctx.lineTo(this.canvasWidth, i * this.gridSize - 0.5);
           this.ctx.strokeStyle = '#eee';
           this.ctx.stroke();            
        }

        // Y轴方向线条数 = 画布宽度 / 网格大小 向下取整
        var yLine = Math.floor(this.canvasWidth / this.gridSize);

        // 绘制Y轴方向线
        for (let i = 0; i <= yLine; i++) {
           this.ctx.beginPath();
           this.ctx.moveTo(i * this.gridSize - 0.5, 0);
           this.ctx.lineTo(i * this.gridSize - 0.5, this.canvasHeight);
           this.ctx.strokeStyle = '#eee';
           this.ctx.stroke();            
        }

    }

    // 绘制坐标系
    LineChart.prototype.drawCoordinate = function () {
        // 绘制X轴
        this.ctx.beginPath();
        this.ctx.moveTo(this.x0, this.y0);
        this.ctx.lineTo(this.canvasWidth - this.space, this.y0);

        // X轴箭头
        this.ctx.lineTo(this.canvasWidth - this.space - this.arrowSize, this.y0 - this.arrowSize / 2);
        this.ctx.lineTo(this.canvasWidth - this.space - this.arrowSize, this.y0 + this.arrowSize / 2);
        this.ctx.lineTo(this.canvasWidth - this.space, this.y0);

        this.ctx.fill();
        this.ctx.strokeStyle = 'black';
        this.ctx.stroke();

        // 绘制Y轴
        this.ctx.beginPath();
        this.ctx.moveTo(this.x0, this.y0);
        this.ctx.lineTo(this.space, this.space);

        // Y轴箭头
        this.ctx.lineTo(this.x0 + this.arrowSize / 2, this.space + this.arrowSize);
        this.ctx.lineTo(this.x0 - this.arrowSize / 2, this.space + this.arrowSize);
        this.ctx.lineTo(this.space, this.space);

        this.ctx.fill();
        this.ctx.stroke();

    }

    // 绘制点
    LineChart.prototype.drawDots = function (data) {
        let _this = this;
        // 传入数据的坐标不是canvas坐标，因此需要先转换成canvas坐标，再进行绘制和连线
        for (let i = 0; i < data.length; i++) {
            const item = data[i];
            
            var canvasX = _this.x0 + item.x;// canvas x轴坐标 = canvas原点X轴坐标 + 数据X轴坐标
            var canvasY = _this.y0 - item.y;// canvas y轴坐标 = canvas原点y轴坐标 - 数据Y轴坐标

            // 绘制点
            _this.ctx.beginPath();
            _this.ctx.moveTo(canvasX - _this.dotSize / 2, canvasY - _this.dotSize / 2);// 起始位置为点的左上角位置
            _this.ctx.lineTo(canvasX + _this.dotSize / 2, canvasY - _this.dotSize / 2);
            _this.ctx.lineTo(canvasX + _this.dotSize / 2, canvasY + _this.dotSize / 2);
            _this.ctx.lineTo(canvasX - _this.dotSize / 2, canvasY + _this.dotSize / 2);
            _this.ctx.closePath();

            _this.ctx.fill();

            // 将点连成线 (第一个点起点为(x0,y0),其他坐标起点为上一个点)
            _this.ctx.beginPath();
            if(i == 0) {
                _this.ctx.moveTo( _this.x0,  _this.y0);                
            }else {
                _this.ctx.moveTo( _this.x0 + data[i-1].x, _this.y0 - data[i-1].y);
            }
            _this.ctx.lineTo(canvasX, canvasY);

            _this.ctx.stroke();
        }
    }

    // 3. 初始化
    var data = [
        {
            x: 100,
            y: 120
        },
        {
            x: 150,
            y: 300
        },
        {
            x: 400,
            y: 360
        },
        {
            x: 430,
            y: 200
        },
        {
            x: 470,
            y: 100
        }
    ];

    var lineChart = new LineChart();
    lineChart.init(data);

```

# 绘制图形

矩形：

- `rect(x轴坐标,Y轴坐标,长度,高度)` 

    - X轴坐标、Y轴坐标表示矩形左上角的点的位置

    - 此方法绘制的是轨迹，要显示出来还必须使用`stroke()`或`fill()`进行描边或填充

    - 绘制的路径不是独立路径

- `strokeRect(x轴坐标,Y轴坐标,长度,高度)`

    - 绘制描边矩形

    - 此方法绘制有自己的独立路径，即默认自带`beginPath()`，不会被其他路径样式覆盖

- `fillRect(x轴坐标,Y轴坐标,长度,高度)`

    - 绘制填充矩形

    - 此方法绘制有自己的独立路径，即默认自带`beginPath()`，不会被其他路径样式覆盖

- `clearRect(x轴坐标,Y轴坐标,长度,高度)`

    - 清除矩形内容

## 绘制渐变矩形

```javascript
var linearGradient = ctx.createLinearGradient(100,100,400,100);// 设置渐变方向，以两点的坐标来定
linearGradient.addColorStop(0,'pink');// 起始颜色，若中间需要加别的颜色可以调整第一个参数为0~1之间
linearGradient.addColorStop(1,'blue');// 结束颜色

ctx.fillStyle = linearGradient;

ctx.fillRect(100,100,300,200);

```

# 绘制曲线

## 弧形

一个弧度 = 一个半径的长度

- `arc(圆心x轴,圆心y轴,起始弧度,结束弧度,绘制方向)`

    - 圆心x轴,圆心y轴为圆心坐标，类型为`number`

    - 起始弧度与结束弧度类型为`number`,π用`Math.PI`表示

    - 绘制方向类型为`boolean`，默认为顺时针

    - 此方法绘制的是路径，需要使用描边才能显示
## 扇形

起始点放在弧线的圆心位置，绘制弧线，闭合路径

```javascript
    var ctx = document.querySelector('canvas').getContext('2d');

    ctx.moveTo(100,100);
    ctx.arc(100,100,50,Math.PI * 3 / 2, 0);
    ctx.closePath();

    ctx.fill();
```

起始点若不设置直接闭合，则绘制出的为扇形

## n等分随机颜色的圆

```javascript
    var ctx = document.querySelector('canvas').getContext('2d');
    var num = 8;// 等分数
    var angle = Math.PI * 2 / num;// 每份弧度
    var startAngle = 0;
    var w = ctx.canvas.width;// 画布宽度
    var h = ctx.canvas.height;// 画布高度

    // 获取随机颜色
    var getRandomColor = function() {
        var r = Math.floor(Math.random() * 256);
        var g = Math.floor(Math.random() * 256);
        var b = Math.floor(Math.random() * 256);

        return 'rgb('+ r + ',' + g + ',' + b +')';
    };

    // 绘制随机等分圆形
    for (let i = 0; i < num; i++) {
        startAngle = i * angle;
        var endAngle = (i + 1) * angle;
        ctx.beginPath();
        ctx.moveTo(w / 2,h / 2);
        ctx.arc(w / 2,h / 2, h / 2,startAngle,endAngle);
        ctx.closePath();
        ctx.fillStyle = getRandomColor();
        ctx.fill();
    }
```

## 根据数据绘制饼图

```javascript
    var ctx = document.querySelector('canvas').getContext('2d');
    var data = [5,10,12,12,3];// 动态数据    
    var w = ctx.canvas.width;// 画布宽度
    var h = ctx.canvas.height;// 画布高度

    // 获取随机颜色
    var getRandomColor = function() {
        var r = Math.floor(Math.random() * 256);
        var g = Math.floor(Math.random() * 256);
        var b = Math.floor(Math.random() * 256);

        return 'rgb('+ r + ',' + g + ',' + b +')';
    };

    // 获取总数
    let total = 0;
    for (let i = 0; i < data.length; i++) {
        total = total + data[i];
    }

    // 根据每份比例绘制饼图
    var startAngle = 0;
    for (let i = 0; i < data.length; i++) {      
        var endAngle = startAngle +  Math.PI * 2 * (data[i] / total);
        ctx.beginPath();
        ctx.moveTo(w / 2,h / 2);
        ctx.arc(w / 2,h / 2, h / 2,startAngle,endAngle);
        ctx.closePath();
        ctx.fillStyle = getRandomColor();
        ctx.fill();

        startAngle = endAngle;// 下一区域起始弧度为本区域结束弧度，此处必须要赋值
    }

```
# 绘制文本

- `strokeText(文本内容,x坐标,y坐标)`

    - 文本绘制的起点在左下角，矩形绘制的起点在左上角

    - `strokeText`绘制出的是描边的文字，字体为空心，若要实心则使用`fillText`绘制

- `textAlign`

    - 文本对齐方式，基于起始坐标的对齐方式

- `font`

    - 设置文本大小、字体

- `textBaseline`

    - 设置基线（垂直对齐方式），基于起始坐标的对齐方式

    - 可取值： `top`、`middle`、 `bottom`、 `hanging`、 `alphabetic`、 `ideographic`

    - `hanging` 文本的基线处于文本的正上方并且和文本相粘合(适用于印度文)

    - `alphabetic` 默认值，基线处于文本下方，并穿过文字(适用于英文)

    - `ideographic` 与 `bottom` 相似(适用于中文)

- `measureText(文本内容)`

    - 获取文本的宽度对象

    - **若取文本长度则需要xxx.ctx.measureText(xx).width**

# 绘制带文本的饼图

https://garden.aezo.cn/demos/canvas饼状图.html


# 绘制图片

绘制图片使用方法`drawImage()`,可传三个参数、五个参数、九个参数

## 绘制思路

1. 加载图片至内存,创建image对象

    ```javascript
        // 方法1
        var img = doucment.createElement('img');
        img.src = 'image/dude.png';

        // 方法2
        var image = new Image();// Image()为JS提供的内置构造函数
        img.src = 'image/dude.png';
    ```

2. 图片加载完成才能执行代码，因此必须写在onload函数里面

    **部分浏览器如果有缓存时，图片可能会在onload函数触发之前就已经加载完毕，第一次加载图片时已经触发了onload事件，含有缓存时不再触发onload事件，为保证兼容性，最好把onload事件写在图片加载之前**

    ```javascript
        var image = new Image();// Image()为JS提供的内置构造函数
        image.onload = function() {
            // 此处实现图片绘制
        }
        img.src = 'image/dude.png';

    ```


## 三种绘制方法

- 三个参数 `darwImage(img, x, y)`

    - `img` 图片对象、canvas对象、 video对象

    - `x`、`y` 图片绘制的左上角

- 五个参数 `darwImage(img, x, y, w, h)`

    - `img` 图片对象、canvas对象、 video对象

    - `x`、`y` 图片绘制的左上角

    - `w`、`h` 图片绘制尺寸设置，会对图片进行缩放而不是裁剪

- 九个参数 `drawImage(img, x, y, w, h, x1, y1, w1, h1)`

    - `img` 图片对象、canvas对象、 video对象

    - `x`、`y`、`w`、`h` 图片中的一个矩形区域

    - `x1`、`y1`、`w1`、`h1` 画布中的一个矩形区域, `w1`、`h1`是图片的缩放尺寸而不是裁剪

## 帧动画

### 绘制关键思路

1. 动态获取当前图片的尺寸

    ```javascript
    var imageWidth = image.width;
    var imageHeight = image.height;
    ```

2. 计算出每个小人物的尺寸

### 示例

https://garden.aezo.cn/demos/canvas帧动画.html

### 方向键控制精灵行走的帧动画

https://garden.aezo.cn/demos/canvas方向键控制行走动画.html

## 转换






















---

参考视频

 https://www.bilibili.com/video/av53813293?p=2 (canvas视频【高级教程】)