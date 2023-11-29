---
layout: "post"
title: "Vue"
date: "2019-6-22 14:47:36"
categories: [web,vue]
tags: [Computer Language, web,vue]
---

# Vue使用

使用Vue的两种方式：

- 在页面中引入vue的js文件

- 脚手架 

    - 官方脚手架vue-cli

    - 其他民间脚手架，如`webpack-simple`

    - 手动搭建

# ES6相关

- 速写属性

  语法糖,属性名和变量名相同时可简写

  ```js
  var name = "测试";
  var age = 18;

  var person = {
    name: name,
    age: age
  }

  // person对象可以简写成如下样子
  person = {
    name,
    age
  }

  ```

- 速写方法

  语法糖，在对象中写方法时可以简化写法

  ```js

  var person = {
    name: "测试",
    age: 18,
    sayHello: function() {
      console.log("hellllo");
    }
  }

  // 等同于如下写法

  person = {
    name: "测试",
    age: 18,
    sayHello() {
      console.log("hellllo");
    }
  }
  ```



- 模板字符串

  为了解决字符串的拼接问题和转换问题

```js
var person = {
    name: "测试",
    age: 18,
    sayHello: function() {
      console.log("hellllo");
    }
  }

  // 普通写法
  var str1 = "my name is " + person.name + "\n my age is " + person.age;

  // 模板字符串，可以简化拼接，支持换行
  var str2 = `my name is ${person.name} 
  my age is ${person.age}`;
```

# 注入

配置对象中的部分内容会被提取到vue实例中：

- data

- methods

该过程称为注入

注入的目的有两个：

- 完成数据响应式

  vue2.0是通过`Object.defineProperty`方法完成了数据响应式，Vue3.0是通过`Class Proxy`完成的数据响应式

  `Class Proxy`效率会高于`Object.defineProperty`，`Object.defineProperty`无法感知新增和删除的属性，会无法完成数据响应式

- 绑定`this`

# 虚拟DOM树

为了提高渲染效率，vue会把模板编译成虚拟DOM树，然后再生成真实的Dom树

对于vue而言，提升效率的重点在于：

- 减少新的虚拟DOM的生成

- 保证对比之后只有必要的结点有变化

Vue提供了多种方式生成虚拟DOM树：

1. 在挂载的元素内部直接书写，此时将使用元素的outerHTML作为模板 

2. 在template配置中书写

3. 在render配置中用函数直接创建虚拟节点树，此时，完全脱离模板，将省略编译步骤

以上步骤从上到下，优先级逐步提升，写在render配置中的会覆盖前面两种情况生成的

**虚拟节点树必须是单根的**

# 挂载

将生成的DOM树放置到某个元素位置，称之为挂载。

挂载的方式： 

1. 通过`el: "css选择器"`进行配置

2. 通过`vue实例.$mount("css选择器")`进行配置

# 完整流程

实例被创建 --> 注入 --> 编译生成虚拟DOM树 --> 挂载 --> 已挂载

数据变动时，已挂载的DOM会重新生成DOM树 --> 对比新旧两树差异 --> 将差异应用到真实DOM

# 模板语法

## 内容

vue中的元素内容使用mustache模板引擎进行解析

## 指令

### `v-html`

设置元素的innerHtml，该指令会导致元素的模板内容失效

### `v-bind`

绑定动态属性，此指令因为十分常用，因此提供了简写`:`

### `v-on`

注册事件

- 此功能非常常用，因此提供了简写`@`

- 事件支持一些指令修饰符，如`prevent`

- 事件参数会自动传递

### `v-for`

html代码：

```javascript
  <p v-for="item in list"> {{ item }}</p>
```
javascript代码：

```javascript
  <script>
    var vm = new Vue({
      el: '#app',
      data: {
        list: [
          {id : 1, name: zs1},
          {id : 2, name: zs2},
          {id : 3, name: zs3},
          {id : 4, name: zs4},
        ]
      }
    })
  </script>
```
`v-for`指令除了能遍历数组还能遍历对象，遍历对象时，要写成：

```javascript
  <p v-for="(value, key) in user"> 值是:{{ value }} --- 键是{{ key }}</p>
```

除了value和key之外，在第三个位置还有索引。`v-for`指令中，`in`后面可以是普通数组、对象数组、对象、数字，若为数字时，`count in 10`的`count`从1开始

注意事项： 
1. vue 2.20+ 版本中，使用v-for指令时，需要指定key，保证数据的唯一性
2. key属性只能用number或者String
3. key在使用时必须使用`v-bind`属性的形式绑定

### `v-if`和 `v-show`指令

`v-if` 每次都会重新删除或创建元素，有较高的切换性能消耗
`v-show` 每次不会重新进行DOM的删除和创建操作，只是切换了元素的display:none样式，有较高的初始渲染消耗

如果元素涉及到频繁的切换，最好不要用`v-if`,如果元素可能永远不会被显示出来，则推荐使用`v-if`

### `v-model`

双向数据绑定，常用语表单元素，该指令是`v-on`和`v-bind`的复合版

### 特殊属性

- `key` 

  该属性可以干预diff算法，在同一层级，key值相同的节点会进行比对，key值不同的则不会

  虚拟dom生成真实dom使用的就是diff算法

  在循环生成的节点中，Vue强烈建议给予每个节点唯一且稳定的key值，建议key值用id而不是下标

# 计算属性

计算属性写在computed配置中，是本身不存在而需要靠计算出来的属性，与方法`methods`的区别在于：

1. 计算属性可以赋值，而方法不行

2. 计算属性会进行缓存，只有其依赖的属性发生变化是才会变化，否则直接使用缓存结果，不会重新计算

3. 方法只要调用一次，无论依赖的值有没有变化都会执行

4. 凡是根据已有数据计算的到的新数据的无参函数，都应该尽量写成计算属性而不是方法

```js
computed: {
  // 仅访问器 写法
  prop() {
    return ...
  }

  // 访问器 + 设置其器写法
  fullProp: {
    get() {
      return ...
    },

    set(val) {
      ...
    }
  }
}

```

# 数组的新方法

`forEach` `some` `filter` `findIndex` 都属于数组的新方法，都会对数组中的每一项进行遍历，执行相关操作 

# 过滤器

## 过滤器调用时的格式

```javascript &#123;&#123; data | 过滤器的名称 &#125; ```

## 过滤器的定义语法

```javascript
// 过滤器的第一个参数被定死，永远是管道符`|`前面传递过来的数据
Vue.filter('过滤器的名称', function(data) {})
```
`Vue.filter()`定义的是全局的过滤器，所有的vm实例共享

## 私有过滤器

```javascript
var vm = new Vue({
  el: '#xx',
  data: {},
  methods:{},
  filters: {
    // 定义私有过滤器，过滤器两个条件 【过滤器名称和处理函数】
  }
})
```

注： 过滤器调用的时候采用就近原则，如果私有过滤器和全局过滤器名称一致，优先调用私有过滤器

# 按键修饰符

官方文档提供默认的按键修饰符，除此之外还可以自定义按键修饰符(2.x版本)：

```javascript
// Vue.config.keyCodes.自定义名称 = 对应键盘码码值
Vue.config.keyCodes.f2 = 113;
```

# 自定义指令

vue中所有的指令，在调用时都以`v-`开头,自定义指令的时候，指令名称的前面不需要加`v-`前缀，但是调用时必须加上`v-`

```javascript
// 使用v-derective()定义全局的指令
Vue.derective(指令的名称, {
  // 在每个函数中，第一个参数永远是el,表示被绑定了指令的元素，这个el参数是一个原生的JS对象
  bind: function(el) {
    // 每当指令绑定到元素上的时候，会立即执行这个bind函数，只执行一次
    // 和样式相关的可以放在bind中
  },
  inserted: function(el) {
    // 元素插入到DOM中的时候，会执行insert函数，只触发一次
  },
  updated: function(el) {
    // 当VNode更新的时候，会执行updated,可能会触发多次
  }
})
```

更多钩子函数的参数具体可见官方文档: https://cn.vuejs.org/v2/guide/custom-directive.html#%E9%92%A9%E5%AD%90%E5%87%BD%E6%95%B0

## 自定义私有指令

```javascript
var vm = new Vue({
  el: '#xx',
  data: {},
  methods:{},
  directive: {
    // 定义私有指令
    指令名: {
      bind: function(el) {

      }
    }

  }
})
```
## 函数简写

在很多时候，你可能想在 bind 和 update 时触发相同行为，而不关心其它的钩子，可以简写成：

```javascript
Vue.directive('color-swatch', function (el, binding) {
  el.style.backgroundColor = binding.value
})
```

# Vue实例的生命周期

## 概念

生命周期钩子 = 生命周期函数 = 生命周期时间 = Vue实例从创建、运行到销毁期间运行的各种各样的事件

## 分类

创建期间的生命周期函数、运行期间的生命周期函数、销毁创建期间的生命周期函数

![Vue生命周期图解](/data/img/vue/lifecycle.png) 

### 创建生命周期

第一个生命周期函数: `beforeCreate()`,与`data`和`methods`平级，在实例完全被创建出来之前执行，执行时，`data`和`methods`都还没初始化

第二个生命周期函数： `created()`,与`data`和`methods`平级，此时`data`和`methods`已初始化，可以操作`data`中的数据，也可以调用`methods`中的方法

第三个生命周期函数： `beforeMount()`,表示模板已经在内存中编译完成，但尚未把模板输出到页面中。`beforeMount()`执行时，页面中的元素没有被真正替换过来，只是之前写的一些模板字符，如在`beforeMount()`中打印对应页面中的`javascript {{ msg }}`出现的结果是插值表达式`javascript {{ msg }}`，而不是`data`中定义的`msg`的值

第四个生命周期函数: `mounted()`，表示内存中的模板已经挂载到了页面中，用户可以看到渲染好的页面，在`mounted()`中打印对应页面中的`javascript {{ msg }}`不再是差值表达式，而是`data`中定义的`msg`的值；`mounted()`是实例创建期间的最后一个生命周期函数，当执行完`mounted()`就表示实例已经被完全创建好了，此时组件已经脱离了创建阶段，进入运行阶段。如果要通过某些插件操作页面上的DOM节点，最早要在`mounted()`中进行。

### 运行期间的生命周期

运行期间的生命周期函数的触发条件是数据被改变

- `beforeUpdate()` 界面还没有被更新，页面上显示的数据还是旧数据，但data中的数据被更新了，此时页面尚未和最新数据保持同步

- `updated()`,执行时，页面和data数据已经保持同步了，都是最新的

### 销毁阶段的生命周期

- `beforeDestory()` 当执行此钩子函数时，Vue实例已经从运行阶段进入到了销毁阶段，此时所有的`data`和所有的`methods`以及过滤器、指令都处于可用状态，还没有真正执行销毁

- `destoryed()` 此时组件中所有的`data`和所有的`methods`以及过滤器、指令都处于不可用状态

# vue-resource实现get,post,jsonp请求

除了vue-resource之外，还可以使用叫做`axios`的第三方包实现数据的请求。目前使用`axios`比较多，`vue-resource`此部分只做了解，嘿嘿~

## get请求

```javascript
  this.$http.get(请求地址).then(function(result) {
      // 通过result.body拿到服务器返回的成功数据
  });
```
## post请求

```javascript
  this.$http.post(请求地址,请求数据,{ emulateJSON: true }).then(result => {
      // 请求数据不能省略，手动发起的post请求默认没有表单格式，所以有的服务器接收不了
      // 将post的第三个参数 { emulateJSON: true }设置提交内容为普通表达数据格式，防止以上情况发生
  });
```
## jsonp请求

```javascript
  this.$http.jsonp(请求地址).then(result => {});
```

# Vue中的动画(此部分先跳过，用到时再看)

## 使用第三方类实现动画(animate.css)

引入`animate.css`后直接使用

## 动画钩子函数

1. 动画钩子的第一个参数el，表示要执行动画的DOM元素，那个是原生的JS DOM 对象，可认为是通过document.getElementById('')方式获取到的原生Js对象
2. beforeEnter表示动画入场之前，此时，动画尚未开始，可以在beforeEnter中，设置元素开始动画之前的起始样式

# 组件

## 知识补充

1. 箭头函数

    - 任何可以书写匿名函数的位置均可以书写箭头函数

      ```js
      var sum = function(a, b) {
        return a + b；
      }
      ```

      可以写成：
      ```js
      var sum = (a, b) => {
        return a + b；
      }
      ```

      当只有一个参数时，可以进一步简化成： 
      ```js
      var print = data => {
        console.log(data)
      }
      ```

      当返回语句只有一条内容时可以省略`{}`:
      ```js
      var print = data => console.log(data)
      ```

    - 箭头函数将会绑定`this`为函数书写位置的`this`值

2. 模块化

    - 没有模块化的世界：全局变量污染、难以管理依赖

    - 常见的模块化标准： CommonJs、ES6 Module、AMD、CMD、UMD

### ES6

每一个JS文件可以认为是一个模块，引入时加上`type="module"`就能将此js文件模块化，此方式引入后，界面使用windows.xxx(xxx为引入js文件的方法名)将无法访问，以此保证不污染全局变量。

使用`export default function...` 可以将自身模块暴露出去供别的模块使用，使用时需要用`import`进行导入

为了拆分Vue实例的代码量，能以不同的组件来划分不同的功能模块。

### 组件化和模块化的区别

 - 模块化是从代码逻辑的角度进行划分的，方便代码分层开发，保证每个功能模块的职能单一

 - 组件化是从UI界面的角度进行划分的，方便UI组件的重复利用


## 概念

一个完整的网页是复杂的，如果将其作为一个整体来进行开发，将会遇到以下困难：

- 代码凌乱臃肿

- 不易协作

- 难以复用

vue推荐使用一种更加精细的控制方案——组件化开发

所谓组件化就是吧一个页面中区域功能细分，每一个区域成为一个组件，每个组件包含：

- 功能（js代码）

- 内容（模板代码）

- 样式（css代码）

由于没有构建工具的支撑，css代码暂时无法放到组件中

## 创建组件的方式

1. 使用`Vue.extend`创建全局Vue组件，通过`template`属性指定组件要展示的html结构

```javascript
// 创建组件模板对象
var com1 = Vue.extend({
  template: '<h3>这是用 Vue.extend 创建的组件</h3>'
});

// 使用Vue.component('组件的名称', 创建出来的组件模板对象)
Vue.component('myCom1', com1);

```

如果要使用组件，直接把组件的名称以HTML标签的形式引用。如果使用`Vue.component`定义全局组件，组件名称使用了驼峰命名，在引用时，需要将大写的驼峰改成小写字母，并加上`-`。
例如： 组件名称`myCom1`,在引用时，页面的标签应为`<my-com1></my-com1>`;组件名称`mycom1`,在引用时，页面的标签应为`<mycom1></mycom1>`

简化写法：

```javascript

Vue.component('myCom1', Vue.extend({
  template: '<h3>这是用 Vue.extend 创建的组件</h3>'
}));

```

2. 使用`Vue.component`注册组件

```javascript
Vue.component('myCom2', {
  template: '<h3>这是用 Vue.extend 创建的组件</h3>'
});
```

## 组件切换

1. 使用 `v-if`、`v-else` 实现组件的切换
2. 使用 `component` 标签控制组件的切换(Vue内置组件： `component` `template` `transition` `transitionGroup`)
3. 使用组件切换动画切换

## 父子组件传值

### 父组件向子组件传值(通过属性传值，通过事件绑定`v-on`传递方法)

父组件可以在引用子组件时，通过属性绑定的形式(:)把需要传递给子组件的数据，以属性绑定的形式传递到子组件内部，供子组件使用。

父组件传递的数据放在子组件的`props`数组中，组件中的所有`props`中的数据都是通过父组件传递给子组件的。 

注： 
1. 子组件中的`data`数据并不是通过父组件传递过来的，而是子组件本身私有的，比如子组件通过Ajax请求回来的数据都可以放在data中
2. `data`中的数据都是可读可写的，`props`中的数据都是只读的

父组件传递方法给子组件，使用事件绑定机制`v-on`定义需要传递的方法，子组件通过`this.$emit('传递的方法名'，'参数1'， '参数2'...)`进行调用。

### 子组件向父组件传值
通过事件回传

# webpack(version 3.6)

## webpack-dev-server(自动编译打包工具)

用于实现自动打包编译功能，依赖于webpack，因此安装此工具前即使全局已经装过webpack，在本地项目中也必须安装webpack以保证正常使用。

1. 运行 `npm i webpack-dev-server -D`命令，将此工具安装到项目的本地开发依赖
2. 安装完毕后，在终端输入`webpack-dev-server`即可使用
3. `webpack-dev-server`安装在本地项目中，无法把它当成脚本命令，因此在`powershell`命令中无法直接使用，因此要在项目的`package.json`中加入依赖。
4. `webpack-dev-server`打包生成的`bundle.js`文件并没有存放到实际的物理磁盘中，而是直接托管到电脑的内存中，所以在项目的根目录中找不到这个打包好的`bundle.js`

### webpack-dev-server常用命令参数

第一种方式（推荐写法）： 在`package.json`中配置
```javascript
"scripts" : {
  "dev" : "webpack-dev-server --open --port 3000 --contentBase src --hot"
}
```
`open`——编译完成后自动打开浏览器

`port`—— 自定义端口

`contentBase` —— 设置托管目录

`hot` —— 打补丁；热部署，实现浏览器的不刷新重载

第二种方式（了解即可）：在`webpack.config.js`中配置
```javascript
const webpack = require('webpack');// 启用热更新的第2步
module.exports = {
...
  devServer : {
    open: true,
    port: 3000,
    contBase: 'src',
    hot: true // 启用热更新的第1步
  },
  plugins: [// 配置插件的节点
    // 启用热更新的第3步
    new webpack.HotModuleReplacementPlugin()// new一个热更新的模块对象
  ]
}
...
```

## html-webpack-plugin

在内存中，根据index模板页面生成内存页面

1. 安装`html-webpack-plugin`插件(`npm i html-webpack-plugin -D`)
2. 在`webpack.config.js`中导入此插件
```javascript
// 只要是插件，都需要放到plugins节点中
const htmlWebpackPlugin = require('html-webpack-plugin');
module.exports = {
...
  plugins: [// 配置插件的节点
    // 创建一个在内存中生成html页面插件
    new htmlWebpackPlugin({
      // 指定模板页面，将来会根据指定页面路径去生成内存中的页面
      template: path.join(_dirname, './src/index.html'),
      // 指定生成的页面名称
      filename: 'index123.html'
    })
  ]
...
}
```
3. `html-webpack-plugin`会自动把打包好的`bundle.js`追加到页面中

## loader(第三方处理器)

webpack默认只能打包处理js类型的文件，不能处理其它非js类型的文件，如果需要处理非js类型的文件，则需要手动安装一些合适的第三方loader加载器。如需要打包处理css文件，需要安装`style-loader`和`css-loader`

1. 安装命令： `npm i style-loader css-loader -D`
2. 在`webpack.config.js`的`module`节点中配置

```javascript
...
module.exports = {
...
  module: {// 此节点用于配置所有第三方木块加载器
    rules: [
      // 配置处理.css文件第三方loader规则,webpack1.x版本的use中可省略-loader，2.x及以后的版本都不能省略
      {test: /\.css$/, use: ['style-loader', 'css-loader']}
    ]
  }
  ...
}
```
`webpack`处理第三方文件类型的过程：
1. 发现这个文件的类型不是js，去配置文件中查找是否有第三方loader规则
2. 若能找到对应规则，调用对应的loader处理此文件类型
3. 调用loader时，是从后往前调用(如上述`['style-loader', 'css-loader']`,先调用的是`css-loader`后调用`style-loader`)
4. 当最后一个loader调用完毕时，会把处理结果直接交给webpack进行打包合并，最终输出到`bundle.js`中

### 处理less文件的loader

1. 安装`less`: `npm i less`
2. 安装`less-loader`: `npm i less-loader -D`
3. 在上述`module.rules`中配置`less-loader`规则： ` {test: /\.less$/, use: ['style-loader', 'css-loader','less-loader']}`

注： less是less-loader内部依赖，因此需要先安装less，但无需将less配置到`webpack.config.js`中

### 处理scss文件的loader
`node-sass`是`sass-loader`内部依赖，需要先安装`node-sass`，但无需将`node-sass`配置到`webpack.config.js`中

1. 安装`node-sass`: `cnpm i node-sass -D`(`node-sass`一般都用cnpm安装，npm一般比较难装成功)
2. 安装`sass-loader`:  `npm i sass-loader -D`
3. 在`module.rules`中配置`sass-loader`规则：`{test: /\.scss$/, use: ['style-loader', 'css-loader','sass-loader']}`

### 处理css文件中的url地址的loader

默认情况下webpack无法处理文件中的url地址，无论是图片还是字体库，只要是url地址都处理不了，需要安装`url-loader`

`file-loader`是`url-loader`内部依赖，需要先安装`file-loader`，但无需将`file-loader`配置到`webpack.config.js`中

1. 安装`file-loader`和`url-loader`: `cnpm i url-loader file-loader -D`
2. 在`module.rules`中配置`url-loader`规则：`{test: /\.jpg|png|gif|bmp|jpeg$/, use: 'url-loader?limit=7631&name=[name].[ext]'}`

注： 配置`url-loader`时，`'url-loader?limit=7631&name=[name].[ext]'`中:
- `?`后面表示传参数
- `limit=7631`表示limit给定的图片大小值，单位为kb; 当图片的大小>7631kb时，图片路径会被base64加密，当图片大小<=limit时，则不会被转为base64的字符串
- `name=[name].[ext]` 表示文件名沿用原始名称，而不用自动生成的hash值

#### 使用`url-loader`处理字体文件
在`module.rules`中配置`url-loader`规则：`{test: /\.ttf|eot|svg|woff|woff2$/, use: 'url-loader'}`

一般不要把图片文件和字体文件的url-loader配置写一起，而是分成两条规则写。



# tips

## 填充字符串

ES6中的字符串新方法`String.prototype.padStart(maxLength, filterString= ' ')` 或 `String.prototype.padEnd(maxLength, filterString= ' ')`来填充字符串

- `maxLength` 表示填充完毕的总长度
- `filterString= ' '` 表示填充的字符
- `padStart`表示从前面填充，`padEnd`从后面填充

例如填充时间格式中的月

```javascript
var m = ((new Date()).getMonth() + 1).toString().padStart(2, '0');
```

## 使用脚手架搭建工程

vue-cli




---

参考视频: https://www.bilibili.com/video/av27969216/?p=1