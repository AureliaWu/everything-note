---
layout: "post"
title: "Flutter"
date: "2019-10-23 10:29"
categories: framework,Flutter
tags: [Computer Language, framework, Flutter, UI]
---

# 写在最前面

初学flutter，以跑起来为主，其他细节慢慢补充

# 下载与安装(Windows系统)

官网地址: https://dart.dev/ 

## Windows系统两种安装方式

1. 通过命令行安装[不推荐]
2. 使用官方提供的软件安装

    - 下载地址： http://www.gekorm.com/dart-windows/
    - 下载安装完成后，在命令行中输入`dart --version`，出现版本号表示安装成功

**MAC系统只能通过命令行进行安装**

## Dart开发工具配置Dart

Dart的开发工具有很多: IntelliJ IDEA WebStorm Atom Vscode等。

### Vscode中配置Dart

1. 搜索安装`Dart`插件
2. 搜索安装`code runner`以运行文件

**Vscode安装完插件后需要重启才能生效**

# Dart 语法

## 入口方法

入口方法为`main`方法

```dart
main() {
    print('Hello Dart');
}
```
无返回值的`main`方法

```dart
void main() {
    print('Hello Dart');
}

```

## 注释方式

使用 `//`、 `///` 、`/**/` 均能注释

## 变量与常量

### 定义变量

dart定义变量时，可以不预先定义变量类型 也可以指定变量类型

不预先定义变量类型使用`var`进行声明

```dart
var str = 'this is var';
```

指定变量类型：

```dart
String str = 'this is String';
```

**使用了`var`就不能指定类型，指定了类型就不能使用`var`**

#### 变量名称命名规则

1. 变量名必须由数字、字母、下划线和美元符号(`$`)组成
2. 标识符开头不能是数字
3. 标识符不能是保留字和关键字
4. 变量的名字区分大小写
5. 标识符要见名思意： 变量名称建议用名词，方法名建议用动词

## 定义常量

使用修饰符`const`、`final`进行修饰

- `const` 定义的常量值不变，一开始就需要赋值
- `final` 可以先不赋值，但只能赋值一次 

    `final`不仅有`const`的编译时常量的特性，还有运行时常量的特性，调用方法时得到常量值可以用`final`修饰

```dart

main() {
    final a = new DateTime.now();

    print(a);

   //  const b = new DateTime.now(); 错误写法，运行会报错
}

```

## 数据类型

###  字符串 (String类型)

#### 字符串的定义方式

    - 可以用单引号('')或者双引号定义("")
    - 使用三个单引号('''  ''')或者三个双引号("""  """)可定义多行字符串

```dart
main() {
  var str = '单引号定义字符串';
  print(str);
  
  var str2 = "双引号定义字符串";
  print(str2);

  var str3 = ''' 
                三个单引号
                定义
                多行
                字符串
                ''';
  print(str3);

  var str4 = """ 三个双引号

                  定义

                  多行

                  字符串  
                  
                  """;
  print(str4);

}

```

#### 字符串的拼接

1. 使用`$`

    ```dart

    main() {
    var str1 = 'donkey';

    var str2 = 'monkey';

    print("one: $str1,$str2");

    print("two: $str1 $str2");
    
    }

    ```

    输出结果：

    ```
    one: donkey,monkey
    two: donkey monkey
    ```

2. 使用`+`

    ```dart
    main() {
        var str1 = 'donkey';

        var str2 = 'monkey';

        print("one: " + str1 + "," + str2);
        print("two: " + str1 + " " + str2);    
    }

    ```

    输出结果： 

    ```
    one: donkey,monkey
    two: donkey monkey
    ```

### 数值类型(Number型)

`int`  必须是整型

`double` 浮点型， 也可赋值整型,但会带上小数点

```dart

main() {
  double d = 1;
  int i = 1;
  
  print("d: " + "$d");
  
  print("i: " + "$i");
}

```

输出结果： 

```
d: 1.0
i: 1
```
注： 此处打印时使用`print("d: " + d); ` 会报类型错误

### 布尔类型

bool值只能为`true`或`false`

### 数组/集合类型 (List)

```dart
main() {

    // 定义List方式1
    var list = ["abc","aaa","ccc"];

    print(list);

    // 定义List方式2
    var list2 = new List();
    list2.add("nanana");
    list2.add("ninini");
    list2.add("nununu");

    print(list2);

    // 定义指定类型的List

    var list3 = new List<String>();// 只能添加String类型的元素

    list3.add("111");
    list3.add("222");
    list3.add("333");

    print(list3);
}
```

输出结果：

```
[abc, aaa, ccc]
[nanana, ninini, nununu]
[111, 222, 333]

```

### 字典类型(Map)

```dart
main() {

    // 第一种定义Map的方式
    var person = {
    "name": "张三",
    "age": 18

    };

    print(person);

    print(person["name"]);

    print(person["age"]);

    // 第二种定义Map的方式
    var p = new Map();

    p["name"] = "李四";
    p["age"] = 20;

    print(p);

    print(p["name"]);

    print(p["age"]);

}

```

输出结果： 

```
{name: 张三, age: 18}
张三
18
{name: 李四, age: 20}
李四
20
```

### 数据类型的判断

使用关键词`is`判断数据类型

## 运算符 (与java一样 先跳过)



## 循环语句 (与java一样 先跳过)

## 集合 (与java一样 先跳过)

## 方法的定义

### 基本格式

```
返回值类型 方法名称(参数1,参数2,[可选参数1,可选参数2],....) {
    方法体

    return 返回值;
}
```

### 箭头函数

箭头函数内只能写一行代码

## Dart中类和对象

Dart中没有`public` `private` `protected` 等修饰符,若要将属性或方法私有化可以使用`_`


# Flutter环境配置

## windows上搭建Flutter Android运行环境

1. 安装配置JDK
2. 安装Android Studio
3. 下载配置Flutter SDK
4. 配置Flutter镜像

    `build.gradle`中將`google()` `jcenter()`注釋掉，換成阿里鏡像地址：

      ```gradle
      maven{ url 'https://maven.aliyun.com/repository/google' }
      maven{ url 'https://maven.aliyun.com/repository/jcenter' }
      maven{url 'http://maven.aliyun.com/nexus/content/groups/public'}

      ```


# Flutter (V 1.9.1 2019年9月更新版)

## 跟随官网开始学(`https://flutter.dev/docs/get-started/codelab`)

### 说明

以下代码均为VsCode中完成，**光标移动到终端**后可执行一些快捷命令：

- `r`/`R` 热部署项目

- `p` 显示网格

- `o` 切换平台(IOS/Android平台切换)

- `q` 退出

#### 第一步 初始化Flutter app

1. 导入`material.dart` UI库，material官网： `https://material.io/`
2. 书写入口方法并调用

    ```
    void main() => runApp(MyApp());
    ```

    - `main()` 表示入口方法
    - `=>` 箭头函数，后面内容为一行时使用，一种语法糖
    - `MyApp()` 自定义的方法

3. 声明自定义方法

    ```
      class MyApp extends StatelessWidget {
        @override
        Widget build(BuildContext buildcontext) {
          return MaterialApp(
            title: 'This is for my note!',
            home: Scaffold(
              appBar: AppBar(title: Text('Demo Page'),),
              body: Center(
                child: Text('Hello World'),
              ),
            ),
          );
        }
      }
    ```
    - 上述demo创建了一个`Material app`,`Material`是遵循移动端和网页端标准的一种视觉设计语言，官网为 `https://material.io/`，Flutter中提供了丰富的Material组件

    - 自定义的`MyApp`必须继承`StatelessWidget`以将自己定义为组件，在Flutter中，万物皆组件，例如： `alignment`、`padding`、`layout`

    - `StatelessWidget`是抽象类，因此要重写`build`方法，重写需要加上`@override`注释,`build`方法中必须要有参数`BuildContext`

    - `Scaffold`是`Material`中的一个组件,提供了自定义`appbar`、`title`、`body`属性来维持`home`页面的组件树，`Scaffold`的子组件可以很复杂，用于构建所需界面

    - 一个组件的主要方法就是提供`build()`方法来将其它或者更低级的组件封装来定义界面显示

    - 上述demo中的`body`是由`Center`组件和其子组件`Text`组成的，`Center`组件表示将其子组件设置为居中屏幕对齐

#### 第二步 引用外部包

此步骤中，使用一个外部开源包`english_words`,此包中含有常用英语以及一些实用短语。

`english_words`包以及其它开源包可在`https://pub.dev/`中获取

1. `pubspec`文件负责管理Flutter APP中的依赖和assets。打开项目根目录下的`pubspec.yaml`文件，将`english_words`及其版本添加到依赖列表中：

    ```
      name: flutter_app
      description: A new Flutter application.

      environment:
        sdk: ">=2.1.0 <3.0.0"

      dependencies:
        flutter:
          sdk: flutter
        cupertino_icons: ^0.1.2
        # 此处添加依赖
        english_words: ^3.1.5

      dev_dependencies:
        flutter_test:
          sdk: flutter
    ```
2. 依赖添加完成后，VSCode会自动导包，并在根目录下的`pubspec.lock`文件中自动生成对应外部包的相关信息。如果使用的是`Android Studio`则需要点击`Packages get`进行导包，无论使用哪种，只要控制台出现了`Running "flutter pub get" in 项目名...  `就表示已将外部包成功导入项目中

    ```
      english_words:
      dependency: "direct main"
      description:
        name: english_words
        url: "https://pub.dartlang.org"
      source: hosted
      version: "3.1.5"

    ```
3. 在`lib/main.dart`文件中引入

    ![flutter引入外包](../../../../data/img/flutter/flutter_importPackage.png)

    引入时编辑器会提示此包还未使用、

4. 使用`english_words`生成文字代替上述demo中的`Hello World`

    ```
    import 'package:flutter/material.dart';
    import 'package:english_words/english_words.dart';// 导包

    void main() => runApp(MyApp());

    class MyApp extends StatelessWidget {
      @override
      Widget build(BuildContext buildcontext) {
        // 注入
        final wordPair = WordPair.random();

        return MaterialApp(
          title: 'This is for my note!',
          home: Scaffold(
            appBar: AppBar(title: Text('Demo Page'),),
            body: Center(
              child: Text(wordPair.asPascalCase),// 使用
            ),
          ),
        );
      }
    }

    ```
    注： `wordPair.asPascalCase`中`PascalCase`表示将每个单词的首字母大写，如将`helloworld`写成`HelloWorld`

5. 上述代码每热部署(Android Studio快捷键`ctrl+s`; VScode在终端键入`r`)一次,界面就会随机显示不同的词语。因为该词语是在`build`方法中生成的，每启动一次项目或切换平台时，MaterialApp就会重新进行渲染。

#### 第三步 添加一个有状态的组件

`Stateless`组件是不可变的，即其所有属性都无法改变——所有值都为final。

`Stateful`组件的状态在组件的生命周期内可变化。实现一个有状态的组件至少需要两个类

  1) `StatefulWidget`类
  2) `State`类

创建一个`State`类的对象`StatefulWidget`

`StatefulWidget`类本身是不可变的，但`State`类在组件的生命周期中会一直存在

在此步骤中，会添加一个有状态的组件`RandomWords`继承新创建父类`RandomWordsState`，然后就能在无状态组件`MyApp`中作为`child`来使用`RandomWords`了。

1. 在`main.dart`中创建有状态类`RandomWordsState`

    ```
    class RandomWordsState extends State<RandomWords> {
  
    }
    ```

    `State<RandomWords>`表示声明一个泛型为`RandomWords`的通用类`State`。App中大多数的逻辑和状态都存在这，这里表示状态为`RandomWords`的组件。这个类将保存随着用户滚动而无限增长的生成的单词对， 以及喜欢的单词对，用户通过重复点击心形 ❤️ 图标来将它们从列表中添加或删除。(**啥玩意儿？没懂**)

    `RandomWordsState`依赖于`RandomWords`类

2.  在`main.dart`中添加有状态的`RandomWords`组件。

    ```
    class RandomWords extends StatefulWidget {
      @override
      RandomWordsState createState() => RandomWordsState();
    }
    ```
    添加完成后，编辑器会提示`RandomWordsState`缺少`build`方法,接下来就是通过将`MyApp`中的代码移动到`RandomWordsState`中，为`RandomWordsState`添加`build`方法。

3. 在`RandomWordsState`中添加`build`方法

    ```
    class RandomWordsState extends State<RandomWords> {
      @override
      Widget build(BuildContext buildContext) {
        final wordPair = WordPair.random();

        return Text(wordPair.asPascalCase);
      }
    }
    ```

4. 修改MyApp中生成随机文字部分的代码

    ```
    class MyApp extends StatelessWidget {
      @override
      Widget build(BuildContext buildcontext) {

        return MaterialApp(
          title: 'This is for my note!',
          home: Scaffold(
            appBar: AppBar(title: Text('Demo Page'),),
            body: Center(
              child: RandomWords(),
            ),
          ),
        );
      }
    }
    ```

5. 重启App。

#### 第四步 创建无限滚动的ListView

在此步骤中，你将`RandomWordsState`扩展成展示词语的列表。用户滚动屏幕，该列表将无限展示词语。

`ListView`的`builder`构造函数工厂可以根据需求快速创建列表。

1. 在`RandomWordsState`中创建一个`_suggestions`列表来保存推荐的成语。同时创建一个` _biggerFont`变量来使字体变大。

    ```
    class RandomWordsState extends State<RandomWords> {
      final _suggestions = <WordPair>[];
      final _biggerFont = const TextStyle(fontSize: 18);
      
      @override
      Widget build(BuildContext buildContext) {
        final wordPair = WordPair.random();

        return Text(wordPair.asPascalCase);
      }
    }

    ```
    注： 在Dart语法中，前缀用`_`表示私有

    接下来为`RandomWordsState`类添加方法`_buildSuggestions()`，此方法用于创建显示推荐的词语。

    `ListView`类中提供了属性`itemBuilder`,这是一个工厂匿名回调函数，含有两个参数： `BuildContext`和迭代器`i`。迭代器从0开始递增，每生成推荐的一次单词对就会自增两次，一次用于`ListTile`,一次用于`Divider`。此模式能随着用户的滚动无限出现单词对。

2. 在`RandomWordsState`类中添加`_buildSuggestions()`方法

    ```
      Widget _buildSuggestions() {
        return ListView.builder(
          padding: const EdgeInsets.all(16),
          itemBuilder: (context, i ) {
            if(i.isOdd) return Divider();

            final index = i ~/ 2;
            if(index >= _suggestions.length) {
              _suggestions.addAll(generateWordPairs().take(10));
            }
            return _buildRow(_suggestions[index]);
          },
        );
      } 
    ```

    - `itemBuilder`每产生一对单词对就会被回调一次，并将每对单词对放入`ListTile`行中。偶数行添加`ListTile`行；奇数行添加`Divider`组件将每对单词分开。需要注意的是，`Divider`在小屏上看起来可能不太明显

    - `if(i.isOdd) return Divider();`表示在`ListView`的每一行之前加上1像素的分割线

    - `final index = i ~/ 2;`表达式`~/`表示取`i/2`结果的整型，向下取整。例如：i为1,2,3,4,5时，得到的结果分别为0,1,1,2,2。此处用于计算`ListView`中减去分割线后实际的单词对数量。

    - 如果是建议列表中最后一个单词对，接着再生成10个单词对，然后添加到建议列表。

    `_buildSuggestions()`方法每生成一对单词对就会调用一次`_buildRow`。`_buildRow`用于在`ListTile`中显示新的单词对以使下一步中每行看起来更漂亮

3. 在`RandomWordsState`中添加`_buildRow`方法

    ```
      Widget _buildRow(WordPair wordPair) {
      return ListTile(
        title: Text(
          wordPair.asPascalCase,
          style: _biggerFont,
        ),
      );
    }
    ```

4. 更新`RandomWordsState`类中的`build`方法，使用`_buildSuggestions()`代替直接调用单词生成库。脚手架(Scaffold)实现了基本的`Material`设计视觉布局。将`body`中的内容改成：

    ```
    @override
    Widget build(BuildContext buildContext) {
      return Scaffold(
        appBar: AppBar(title: Text('Infinity scroll word pairs')),
        body: _buildSuggestions(),
      );
    }
    ```
  
5. 更新`MyApp`类中`build`方法，修改`title`并将`home`改成`RandomWords`组件

    ```
    class MyApp extends StatelessWidget {
      @override
      Widget build(BuildContext buildcontext) {

        return MaterialApp(
          title: 'Startup Name Generator',
          home: RandomWords(),
        );
      }
    }
    ```

6. 重启项目即可查看结果


## Flutter内置组件

### 基本结构

MaterialAPP组件作为根组件，具有`home`属性，`home`属性调用`Scaffold`组件

实例化类时，关键字`new`可以省略。

### Scaffold组件 

- `appBar`

  顶部导航栏

- `body`

  页面内容


- `bottomNavigationBar`

  底部导航栏

- `floatingActionButton`

  右下角浮动按钮

- `drawer` 、 `endDrawer`

  `drawer`左侧侧边栏 `endDrawer`
  
  值类型为`Drawer`,详见`Drawer`组件


### Text组件

属性写在`Text()`中，内容为必填，还有很多可选参数。例如`style`用来设置文本的样式，值需要使用内置组件`TextStyle`，`TextStyle`中可以设置字体大小、颜色等文字相关样式

Flutter中的文本都不能直接写，必须使用Text进行封装

- `textAlign`(文本对齐方式)

    - `TextAlign.center` 居中

    - `TextAlign.left` 左对齐

    - `TextAlign.right` 右对齐

    - `TextAlign.justify` 两端对齐

- `textDirection` (文本方向)

    - `TextDirection.ltr` 从左到右
 
    - `TextDirection.rtl` 从右到左

- `overflow` 文本溢出后的处理方式

    - `TextOverflow.ellipsis` 溢出部分用`...`代替

    - `TextOverflow.fade` 文字溢出，从上往下为渐变效果

    - `TextOverflow.clip` 溢出部分裁剪(默认)

- `textScaleFactor` 字体显示倍率

  相对于谁的倍率？父元素？

- `maxLines` 文字最大显示行数

- `style` 字体样式设置

  值需要用`TextStyle`进行封装，可设置字体样式

  - `decoration` 文字装饰线

    - `TextDecoration.overline` 上划线

    - `TextDecoration.lineThrough` 中划线(删除线)
    
    - `TextDecoration.underline` 下划线

    - `TextDecoration.none` 无装饰(默认)

  - `decorationColor` 文字装饰线颜色

  - `decorationStyle` 文字装饰线样式

  - `decorationThickness` 文字装饰线粗细

  - `color` 字体颜色

  - `backgroundColor`(文字填充色)

  - `fontSize` (字体大小)

    默认为14像素，若设置了字体显示倍率`textScaleFactor`,则渲染出来的字体大小 = `fontSize` * `textScaleFactor`

  - `fontWeight`(字体粗细)

    - `FontWeight.bold` 加粗 (w700)

    - `FontWeight.normal` 正常(默认 w400)

    - `FontWeight.wxxx` `xxx`为自定义加粗数值

  - `fontStyle` (字体样式是否倾斜)

    - `FontStyle.italic` 字体倾斜

  - `letterSpacing` (字间距，常用于中文字体)

  - `wordSpacing` (单词间距)

---
  以下以后慢慢研究

  - `textBaseline`
  - `height`
  - `locale`
  - `foreground`
  - `background`
  - `shadows`
  - `fontFeatures` 
  - `debugLabel`
  - `fontFamily`
  - `fontFamilyFallback`
  - `package`

```flutter

import 'package:flutter/material.dart'; // 引入material.io的UI包

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {

  @override
  Widget build(BuildContext buildContext) {
    return MaterialApp(
      title: 'Welcome to flutter',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Welcome to Flutter for bar ')
        ),
        body: Center(
          child: Text(
            'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Sunt corrupti reprehenderit aliquid harum, perspiciatis aliquam omnis?',// 文本内容
            textAlign: TextAlign.left,// 文字对齐样式
            maxLines: 1,//最大显示行
            // overflow: TextOverflow.ellipsis,// 文字溢出使用...代替
            overflow: TextOverflow.fade, // 文字溢出，从上往下为渐变效果
          ),
        ),
      ),
    );
  }
}

```

### Container组件/容器组件

作用类似于`div`

常用属性(键值对)：

- `width` 、 `height`

  宽度和高度，此宽高将`padding`的值包含在内,相当于CSS中的填充盒宽高

  不设置宽高时，`Container`会自动充满屏幕

  **宽高的取值类型定义为了`double`，好几个视频老师强调如果是整数也需要写成浮点型，但实际写成`int`型也能执行，有可能是版本更新的原因，暂不深究**

- `alignment`(**内容**对齐方式)
  
  `alignment: Alignment.topLeft`值为`Alignment`类型，取值一般为以下

  - `Alignment.topLeft` 上部靠左对齐

  - `Alignment.topCenter` 上部居中对齐

  - `Alignment.topRight` 上部靠右对齐

  - `Alignment.center` 居中对齐

  - `Alignment.bottomLeft` 下部靠左对齐

  - `Alignment.bottomCenter` 下部居中对齐

  - `Alignment.bottomRight` 下部靠右对齐

- `padding` (内边距)

  默认值为0,类型为`EdgeInsets`

  - `EdgeInsets.all(10)`  上下左右内边距均为10

  -  `EdgeInsets.fromLTRB(left, top, right, bottom)` 左上右下分别设置内边距

- `margin`(外边距)

  基本用法参见`padding`

- `color` (背景填充色)

  `color: Colors.pink` 
  
  - 此背景色填充范围涵盖`padding`,相当于CSS中的填充盒

  - 取值为`Color`类
  
    - `Colors.内置颜色单词` 框架内置颜色

    - `Color.fromARGB(a, r, g, b)` a、r、g、b分别表示透明度、红、绿、蓝，类型均为`int`

    - `Color.fromRGBO(r, g, b, opacity)` opacity表示透明度，类型为`double`,其他均为`int`

  `color`实际上是`BoxDecoration(color: color)`的简写，因此设置了这里的颜色就不能设置`decoration`中的任意`color`(例如`border`中的颜色),否则执行会报错: ` Cannot provide both a color and a decoration`

- `decoration` (边框及背景颜色)

  ```
  decoration: BoxDecoration(
    color: Colors.pink,
    border: Border.all(
      color: Colors.blue,
      width: 20
    )
  )
  ```
  `decoration`取值为`BoxDecoration`类，可以设置边框样式及背景填充色

  `decoration`也可设置背景色为渐变，写法如下： 

    ```Flutter
    body: Center(
      child: Container(
        child: new Text('Flutter盒模型', style: TextStyle(fontSize: 40.0)),
        alignment: Alignment.topRight,
        width: 300,
        height: 300,
        // color: Colors.pink,
        padding: const EdgeInsets.fromLTRB(10, 20, 30, 40),
        margin: const EdgeInsets.all(10),
        decoration: new BoxDecoration(
          gradient: const LinearGradient(
            colors: [Colors.pink,Colors.purple,Colors.white]
          ),
          border: Border.all(width: 6,color: Colors.lightBlue)
        ),
      
      )
    ),
  ```

- `foregroundDecoration` (暂不研究)

- `constraints`(暂不研究)

- `transform`(旋转Container)

  类似CSS3中的`transform`属性，待深究

- `child` (子元素) **此部分待考究，先往下学**

  `Container`的子元素(大概要称为子组件？)

  不设置`child`和`constraints`时，内容会自动撑满可用空间。

    - 若未设置宽高值，可用空间为整个父类；

    - 若设置了宽高且未设置`constraints`时，可用空间为所设置的范围内

    - 若只设置宽或高，不设置`constraints`时，未设置的那部分会自动撑满


### image(图片组件)

为图片添加滤镜(图片混合模式)

- `Image.network` 添加网络图片

  - `src` 直接填写，不用封装成字典形式，除`src`可以直接填写以外，其他属性都要使用字典样式

  - `alignment` 图片对齐方式

  - `color` `colorBlendMode` 联合使用 用于将图片和背景色混合

    ```
      child: new Image.network(
        'https://w.wallhaven.cc/full/dg/wallhaven-dgv8qo.png',
        color: Colors.greenAccent,
        colorBlendMode: BlendMode.darken,
      )
    ```
  - `fit` 

    控制图片在容器中显示的效果(拉伸、 挤压等),使用`BoxFit`类封装

    - `BoxFit.fill` 充满父容器

    - `BoxFit.fitHeight` 高度方向拉伸充满父容器

    - `BoxFit.fitWidth` 宽度方向拉伸充满父容器

    - `BoxFit.contain` 全图显示，保持原比例，可能会有空隙

    - `BoxFit.cover` 充满父容器且保持原比例，可能会有部分内容被裁切
  
  - `repeat` 

    图片在容器中的平铺效果，默认只显示一张图片

    - `ImageRepeat.repeatY` Y方向平铺

    - `ImageRepeat.repeatX` X方向平铺

#### 圆角图片实现的两种方式

1. 使用`Container`的圆角属性`borderRadius`和 `image`

    ```
    class MyApp extends StatelessWidget {
      @override
      Widget build(BuildContext context) {
        return MaterialApp(
          home: Scaffold(
            appBar: AppBar(title: Text('I am learning Container')),
            body: Container(
              width: 300,
              height: 300,
              decoration: BoxDecoration(
                color: Colors.pinkAccent,
                borderRadius: BorderRadius.circular(150),// 指定弧度为宽高的一半就能变成圆形
                image: DecorationImage(
                  image: NetworkImage('https://w.wallhaven.cc/full/vm/wallhaven-vmg8r3.jpg'),
                  fit: BoxFit.cover
                )
              ),
            ),
          ),
          theme: ThemeData(primaryColor: Colors.lime),
        );
      }
    }
    ```

2. 使用`ClipOval`组件

   `ClipOval`会自动子图片设置弧度，若要设置圆形的图片，需要设置图片的宽高的`fit`属性，以保证每一张图片都为圆形

    ```
    class MyApp extends StatelessWidget {
      @override
      Widget build(BuildContext context) {
        return MaterialApp(
          home: Scaffold(
            appBar: AppBar(title: Text('I am learning Container')),
            body: Container(
              child: ClipOval(
                child: Image.network('https://w.wallhaven.cc/full/42/wallhaven-4277l6.jpg',
                  height: 100,
                  width: 100,
                  fit: BoxFit.cover
                ),
              ),
            ),
          ),
          theme: ThemeData(primaryColor: Colors.lime),
        );
      }
    }
    ```

#### 引入本地图片

一般建议存放图标等内容

1. 在根目录中新建文件夹`images`,在`images`下创建子文件夹`2.0x`、`3.0x`、`4.0x`... 官网要求必须有`2.0x`和`3.0x`

2. 将图片复制到上面新建的每一个子文件夹中

  **Flutter项目运行在手机上时会根据不同屏幕的分辨率加载不同文件夹下对应的图片，因此必须按照上述步骤配置多个文件夹**

3. 在`pubspec.yaml`文件中的`assets`配置图片路径

    ```json
      assets:
        - images/a_dot_burr.jpeg
        - images/a_dot_ham.jpeg
    ```
4. 引入本地图片时使用`Image.asset`来设置图片地址，其他属性设置与`Image.network`相同

**更正：本地图片的文件夹不需要按照步骤1、2中所说的方式定死，只要在`pubspec.yaml`文件中配置好自定义的文件简爱就可以了，上述步骤可能是老版本限制**

### 列表组件 ListView

可用于新闻列表。Fluter中提供了五种常见的列表：垂直列表、垂直图文列表、水平列表、动态列表、矩阵式列表

#### 列表组件中的参数

- `children`

  列表中的元素，使用`<Widget>[]`封装，`<Widget>[]`中可以添加任何组件，如`Container()` `Image.network(src)`等,但一般都是配合`ListTile`组件使用

  - `ListTile`参数

    官方文档： `A single fixed-height row that typically contains some text as well as a leading or trailing icon.`
    
    - `title` 标题

    - `subtitle` 二级标题

    - `leading` 列表前图标： `Icon(Icons.内置图标名)`； `Icon()`中还可以设置其他属性，如图标大小、颜色等，可以以后研究

    - `trailing` 列表末尾图标，设置同`leading`

    **`leading`和`trailing`还可以使用`Image.asset()`设置图片**

- `padding` 列表整体的内边距

- `scrollDirection` 列表方向

  默认为垂直列表，将`scrollDirection`设置成为`Axis.horizontal`时，变为水平列表但此处有坑，当`children`为`ListTile`时，无法设置`ListTile`的宽度，此时若设置成为水平列表则会报错 `BoxConstraints forces an infinite width`。

  水平列表无法使用`ListTile`??需要研究下`ListTile`是个啥

#### 动态列表

1. 通过循环语句实现动态列表

  - 在同一类中直接获取数组

    - 自定义一个私有方法返回一个数组，返回类型必须为`List<Widget>`

    - 调用自定义方法

      ```
      class MyApp extends StatelessWidget {

        List<Widget> _getData() {
          List<Widget> list = new List();

          for(var i=0; i<20; i++) {
            list.add(ListTile(title: Text('这是第$i个列表')));
          }
          return list;
        }

        @override
        Widget build(BuildContext context) {
          return MaterialApp(
            home: Scaffold(
              appBar: AppBar(title: Text('I am learning Container')),
              body: Container(
                child: ListView(
                    children: _getData()
                  ),
              ) 
            ),
            theme: ThemeData(primaryColor: Colors.lime),
          );
        }
      }

      ```

  - 导入外部文件中的数据

    假设有外部数据文件`data/list.dart`如下：

      ```Flutter
      List listData = [
                          {
                            "title": "myhome",
                            "author": "lalaby",
                            "imageUrl": "https://w.wallhaven.cc/full/nk/wallhaven-nk1gkd.jpg"
                          },
                          {
                            "title": "work",
                            "author": "nino",
                            "imageUrl": "https://w.wallhaven.cc/full/vm/wallhaven-vmg8r3.jpg"
                          },
                          {
                            "title": "ala",
                            "author": "kiyo",
                            "imageUrl": "https://w.wallhaven.cc/full/47/wallhaven-47kkd3.jpg"
                          },
                          {
                            "title": "olo",
                            "author": "mizu",
                            "imageUrl": "https://w.wallhaven.cc/full/42/wallhaven-4277l6.jpg"
                          },
                          {
                            "title": "yojo",
                            "author": "yama",
                            "imageUrl": "https://w.wallhaven.cc/full/4x/wallhaven-4x93gv.png"
                          },
                          {
                            "title": "yolo",
                            "author": "sla",
                            "imageUrl": "https://w.wallhaven.cc/full/4v/wallhaven-4vo7vl.jpg"
                          }
                        ];
      ```
      
    - 导入文件数据`import './data/list.dart';`

    - 遍历数据并将结果转成`List`

      ```
        List<Widget> _getData() {
          var tempList = listData.map((value) {
            return ListTile(
              title: Text(value["title"]),
              subtitle: Text(value["author"]),
              leading: Image.network(value["imageUrl"]),
            );
          });

          return tempList.toList();
        }
      ```
    - 调用私有方法`_getData()`


2. 利用`ListView`提供的`builder()`方法来实现动态列表

    ```
    class MyApp extends StatelessWidget {

      @override
      Widget build(BuildContext context) {
        return MaterialApp(
          home: Scaffold(
            appBar: AppBar(title: Text('I am learning Container')),
            body: Component(), 
          ),
          theme: ThemeData(primaryColor: Colors.lime),
        );
      }
    }

    class Component extends StatelessWidget {
      List list = new List();
      Component() {    
        for(var i=0; i<20; i++) {
          list.add(Text('这是第$i个列表'));
        }
      }

      @override
      Widget build(BuildContext buildContext) {
        return ListView.builder(
          itemCount: list.length,
          itemBuilder: (context, index) {
            return ListTile(
              title: list[index],
            );
          },
        );
      }
    }

    ```

### GridView组件

网格布局，可用于实现商品列表。

常用两种方式实现网格布局： 

1. 通过`GridView.count`实现

2. 通过`GridView.builder`实现

#### GridView常用属性

- `children`

  子元素列表，使用`<Widget>[]`封装

- `crossAxisCount` 

  一行中Widget的数量

- `mainAxisSpacing`

  子Widget之间垂直距离

- `crossAxisSpacing`

  子Widget之间水平距离

- `childAspectRatio`

  子Widget宽高比,通过调整宽高比来控制子组件的高度，直接设置子组件的高度是无效的

#### 通过`GridView.count`实现网格布局

```flutter

class MyApp extends StatelessWidget{
  @override
  Widget build(BuildContext buildContext)  {

    return MaterialApp(
      title: 'listView',
      home: Scaffold(
        appBar: AppBar(title: Text('Change Your Mind'), backgroundColor: Colors.transparent),
        body: GridView.count(
                crossAxisCount: 3,
                mainAxisSpacing: 2,
                crossAxisSpacing: 2,
                childAspectRatio: 0.7,
                children: <Widget>[
                  Image.network('https://w.wallhaven.cc/full/nk/wallhaven-nk1gkd.jpg',fit: BoxFit.cover),
                  Image.network('https://w.wallhaven.cc/full/vm/wallhaven-vmg8r3.jpg',fit: BoxFit.cover),
                  Image.network('https://w.wallhaven.cc/full/47/wallhaven-47kkd3.jpg',fit: BoxFit.cover),
                  Image.network('https://w.wallhaven.cc/full/42/wallhaven-4277l6.jpg',fit: BoxFit.cover),
                  Image.network('https://w.wallhaven.cc/full/4x/wallhaven-4x93gv.png',fit: BoxFit.cover),
                  Image.network('https://w.wallhaven.cc/full/4v/wallhaven-4vo7vl.jpg',fit: BoxFit.cover)
                ],
              )
      ),
    );
  }
```

使用动态数据：

- 处理动态数据

  ```Flutter
    import 'data/list.dart';

    List<Widget> _getData() {
    var tempList = listData.map((value) {
      return Container(
        child: Column(
          children: <Widget>[
            Image.network(value["imageUrl"],fit: BoxFit.cover,),
            Text(value["title"])
          ],
        ),
      );
    });

    return tempList.toList();
  }

  ```

- 调用数据渲染

  ```
  @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: Scaffold(
          appBar: AppBar(title: Text('I am learning Container')),
          body: Component(), 
        ),
        theme: ThemeData(primaryColor: Colors.lime),
      );
    }
  }

  class Component extends StatelessWidget {
    @override
    Widget build(BuildContext buildContext) {
      return GridView.count(
        crossAxisCount: 3,
        mainAxisSpacing: 1,
        crossAxisSpacing: 2,
        children: _getData(),
      );    
    }
  ```

#### 通过`GridView.builder`实现网格布局

```
class Component extends StatelessWidget {
  @override
  Widget build(BuildContext buildContext) {
    return GridView.builder(
      gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
        crossAxisCount: 3
      ),
      itemCount: listData.length,
      itemBuilder: _getData
    );    
  }

  Widget _getData(context, index) {
    var value = listData[index];
    return Container(
        child: Column(
          children: <Widget>[
            Image.network(value["imageUrl"],fit: BoxFit.cover,),
            Text(value["title"])
          ],
        ),
      );
  }
}

```

使用`GridView.builder`注意事项：
- `itemCount`表示需要处理的数据的长度

- `itemBuilder`表示处理数据的方法，需要传入`context`和`index`两个参数

- `gridDelegate` 用来控制每行显示的组件个数及组件之间横向纵向距离以及宽高比等，使用`SliverGridDelegateWithFixedCrossAxisCount`封装

- `gridDelegate`为必填项，若为空，运行时会报错30486` The following assertion was thrown building Component(dirty): 'package:flutter/src/widgets/scroll_view.dart': Failed assertion: line 1491 pos 15: 'gridDelegate != null': is not true.`

### 常见的页面布局组件 (`padding` `Row` `Column` `Expanded`)

#### Padding组件

HTML中常见的布局标签都有`padding`属性，但Flutter中很多组件都没有`padding`属性，一般采用`Padding`组件来处理容器与子容器间接的间距

常用属性

- `padding`

  设置内边距值

- `child`

  放入需要设置内边距的子组件

### Row组件

水平布局组件

常用参数

- `mainAxisAlignment`

  主轴的排序方式(水平方向)

  - `MainAxisAlignment.center` 子元素整体居中显示

  - `MainAxisAlignment.end` 子元素整体靠最右显示

  - `MainAxisAlignment.spaceAround` 子元素之间的距离是元素到两边的距离的两倍

  - `MainAxisAlignment.between` 子元素之间两边的距离为0，元素中间距离相等

  - `MainAxisAlignment.spaceEvenly` 子元素之间和两边的距离平均分配

- `crossAxisAlignment`

  次轴(垂直方向)的排序方式，相对于外层Y轴方向的显示方式

  - `CrossAxisAlignment.start` Y轴最上方

  - `CrossAxisAlignment.end` Y轴最下方
 
  - `CrossAxisAlignment.stretch` Y方向上拉伸至充满父元素 
  
  - `CrossAxisAlignment.baseline` 设置成`baseline`时，必须设置`textBaseline`,否则会运行出错

- `children`

  组件子元素

### Column组件

垂直布局组件

属性和Row组件基本一致，但主轴方向是垂直方向，次轴方向为水平方向

### Expanded组件

类似于Web中的Flex布局

常用属性：

- `flex`

- `child`

```
class Component extends StatelessWidget {
  @override
  Widget build(BuildContext buildContext) {
    return Container(
      color: Colors.grey,
      child:  Row(
          children: <Widget>[
            Expanded(
              flex: 1,
              child: Container(child: Text('sdfsdfs'), color: Colors.blue,),
            ),
            Expanded(
              flex: 2,
              child: Container(child: Text('rstgs rrtgs'), color: Colors.pink,),
            ),
            Expanded(
              flex: 2,
              child: Container(child: Text('uyki tkjh'), color: Colors.green,),
            ),
            Expanded(
              flex: 2,
              child: Container(child: Text('sdhbev '), color: Colors.deepOrange,),
            ),
          ],
        ),
    );
  }
```

### SizeBox组件

元素与元素之间的间距可以用`margin属性`也可以用`SizeBox`组件，一般常用的是`SizeBox`

### Stack层叠组件

用于实现定位布局可单独使用，也可以`Align`组件或`Positioned`组件联用

#### 常用属性

- `alignment`

  `Stack`组件中的所有元素对齐方式,无法对单个元素进行定位，可与`Align`或`Positioned`联用控制单个元素定位

  `Align`组件通过设置`alignment`来对单个元素进行定位

  `Positioned`组件通过设置`left` `right` `top` `bottom`等的值来对单个元素进行定位

  ```
  class Component extends StatelessWidget {
    @override
    Widget build(BuildContext buildContext) {
      return Center(
        child: Container(
          height: 400,
          width: 300,
          color: Colors.pinkAccent,
          child: Stack(
            children: <Widget>[
              Align(
                alignment: Alignment.center,
                child: Image.network("https://w.wallhaven.cc/full/42/wallhaven-42pr69.jpg",width: 120,height: 120),
              ),
              Align(
                alignment: Alignment.topLeft,
                child: Image.network("https://w.wallhaven.cc/full/4l/wallhaven-4lepvl.jpg",width: 120,height: 120),
              ),
              Align(
                alignment: Alignment.bottomLeft,
                child: Image.network("https://w.wallhaven.cc/full/4g/wallhaven-4g3dgq.jpg",width: 120,height: 120),
              ),
              Align(
                alignment: Alignment.topRight,
                child: Image.network("https://w.wallhaven.cc/full/vm/wallhaven-vmx6gm.jpg",width: 120,height: 120),
              ),
              Align(
                alignment: Alignment.bottomRight,
                child: Image.network("https://w.wallhaven.cc/full/x1/wallhaven-x15qpv.jpg",width: 120,height: 120),
              ),
            ],
          ),
        ),
      );
    }
  }

  ```

- `children`

### AspectRatio组件

调整子元素child的宽高比

### Card组件

卡片组件，内容可由大多数类型的组件组成，`Card`具有圆角和阴影，让它看起来更具立体感

常用属性：

- `margin`

  外边距

- `child`

  子组件

- `Shape`

  设置阴影效果，默认阴影效果为圆角的长方形边

卡片组件可以包含任何组件，但建议结合`ListView`组件一起使用,但需要注意的是`ListView`组件不能嵌套`ListView`组件

#### 图文卡片的实现

```
class Component extends StatelessWidget {
  @override
  Widget build(BuildContext buildContext) {
    return ListView(
      children: <Widget>[
        Card(
          margin: EdgeInsets.all(10),
          child: Column(
            children: <Widget>[
              AspectRatio(
                aspectRatio: 4/3,
                child: Image.network("https://w.wallhaven.cc/full/ox/wallhaven-ox7357.jpg",fit: BoxFit.cover,),
              ),
              ListTile(
                leading: ClipOval(                  
                  child: Image.network("https://w.wallhaven.cc/full/13/wallhaven-13op8v.jpg",fit: BoxFit.cover,height: 50,width: 50,),
                ),
                title: Text("Candy Nija"),
                subtitle: Text("my first photo"),
              )
            ],
          ),
        ),
        Card(
          margin: EdgeInsets.all(10),
          child: Column(
            children: <Widget>[
              AspectRatio(
                aspectRatio: 4/3,
                child: Image.network("https://w.wallhaven.cc/full/13/wallhaven-13op8v.jpg",fit: BoxFit.cover,),
              ),
              ListTile(
                leading: ClipOval(                  
                  child: Image.network("https://w.wallhaven.cc/full/ey/wallhaven-eyv2z8.jpg",fit: BoxFit.cover,height: 50,width: 50,),
                ),
                title: Text("Cindy Casio"),
                subtitle: Text("stop and think"),
              )
            ],
          ),
        ),
        Card(
          margin: EdgeInsets.all(10),
          child: Column(
            children: <Widget>[
              AspectRatio(
                aspectRatio: 4/3,
                child: Image.network("https://w.wallhaven.cc/full/vg/wallhaven-vg2gl8.jpg",fit: BoxFit.cover,),
              ),
              ListTile(
                // leading: ClipOval(                  
                //   child: Image.network("https://w.wallhaven.cc/full/39/wallhaven-397326.jpg",fit: BoxFit.cover,height: 50,width: 50,),
                // ),
                leading: CircleAvatar(backgroundImage: NetworkImage("https://w.wallhaven.cc/full/39/wallhaven-397326.jpg"),),
                title: Text("Joker Nija"),
                subtitle: Text("Another life"),
              )
            ],
          ),
        ),
      ],
    );
  }
}
```
###  Wrap组件

`Row`组件和`Column`组件分别是控制的是单行单列的布局，`Wrap`组件在主轴方向上空间不足时，会自动向次轴方向上扩展显示以实现流布局

常用属性： 

- `direction` 主轴方向

    `Axis.vertical` 垂直

    `Axis.horizontal` 水平

- `alignment` 主轴对齐方式

- `spacing` 元素之间主轴方向上的间距，直接输入数值即可

- `runSpacing` 元素之间在次轴方向上的间距

### 按钮组件

按钮的属性基本一致，只是显示的样式不同

- `RaiseButton` 凸起按钮组件

  `Create a filled button.`

  默认为一个灰色填充效果的按钮

  `RaiseButton`组件中必须有属性`onPressed`监听，否则设置的样式等会无效

- `FlatButton` 扁平化按钮

- `OutlineButton` 线框按钮

- `IconButton` 图标按钮

- `ButtonBar` 按钮组

- `FloatingActionButton` 浮动按钮


### StatefulWidget组件

Flutter中自定义组件其实就是在定义一个类，这个类需要继承`StatelessWidget`/`StatefulWidget`

- `StatelessWidget` 表示无状态组件，状态不可变

- `StatefulWidget` 表示有状态组件，持有的状态可在Widget生命周期改变。如果想改变页面中的数据，则需要使用`StatefulWidget`

VsCode中装插件`Awesome Flutter Snippets`后,输入`statelessW`/`statefulW`即可自动生成自定义组件的基本结构

`State`类中有一个方法`setState()`可以改变值重新渲染页面

### BottomNavigationBar组件

底部导航条组件，是Scaffold的参数

常用参数

- `items`

  - 底部导航条按钮集合，至少要有两个`BottomNavigationBarItem`，否则运行报错`'items.length >= 2': is not true.`

  - 返回类型为`BottomNavigationBarItem`集合，参数有：

    - `icon` 图标

    - `title` 标题名

    - `activeIcon` 选中时图标

- `currentIndex`

  默认选中第几个

- `onTap`

  选中变化回调函数

- `fixedColor`

  选中的颜色

- `type`

  配置底部导航栏可以有多个按钮

  - `BottomNavigationBarType.shifting`

    切换导航时有淡入淡出效果且不显示未选中的按钮

  - `BottomNavigationBarType.fixed`

### 路由

Flutter中通过`Navigator`组件管理路由导航，并提供了管理堆栈的方法，如`Navigator.push`和`Navigator.pop`

Flutter提供了额两种配置路由跳转的方式： 基本路由和命名路由

#### 基本路由

固定写法： 

- `Navigator.push` 跳转至下一级子页面

  ```Flutter
  Navigator.of(context).push(
    MaterialPageRoute(
      builder: (context) => SearchPage() // SearchPage为需要跳转的页面
    )
  );

  ```

- `Navigator.pop` 退出当前页面，返回上一级页面

  ```Flutter
  Navigator.of(context).pop();
  ```

#### 命名路由

1. 在`main.dart`文件中的`MaterialApp`中的`routes`属性进行配置路由

    ```Flutter
      routes: {
        '/search' : (context) => SearchPage(),
      }
    ```

2. 通过使用`Navigator.pushNamed(context,'路由名')`跳转

    路由名必须要跟`routes`中的名字对应

命名路由传值

官方demo只是为了指定路由传值，以下写法可以改成通用传值: 

- 配置

  ```java
  // 定义路由 arguments表示可选参数
  final routes  = {
    '/search' : (context, {arguments}) => SearchPage(arguments: arguments),
    '/form' : (context, {arguments}) => SearchPage(arguments: arguments),
  };

    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        // 切换路由时的操作
        onGenerateRoute: (settings) {
          final String name = settings.name;// 获取路由名称
          final Function pageContentBuilder = this.routes[name];// 将自定义配置的路由名赋给pageContentBuilder

          if(pageContentBuilder != null) {
            // pageContentBuilder不为空，利用MaterialPageRoute进行跳转
            if (settings.arguments != null) {
              final Route route = MaterialPageRoute(
                builder: (context) => 
                  pageContentBuilder(context,arguments: settings.arguments));// settings.arguments为传递的参数
              return route;
            }else {
              final Route route= MaterialPageRoute(
                builder: (context) => 
                  pageContentBuilder(context));
              return route;
            }
          }
        },
        home: Tabs(),
        theme: ThemeData(primaryColor: Colors.lime)
      );
    }

  ```

- 使用

  ```java
  import 'package:flutter/material.dart';

  class SearchPage extends StatelessWidget {
    final arguments;

    const SearchPage({this.arguments});
      @override
      Widget build(BuildContext context) {
        return Container(
          child: Scaffold(
            appBar: AppBar(title: Text('搜索'),),
            body: Container(
              child: Row(
                children: <Widget>[
                  RaisedButton(
                    child: Text('查询${arguments != null ? arguments['id'] : '0'}'),
                    onPressed: () {
                      
                    },
                  )
                ],
              ),
            ),
          ),
        );
      }
    }

  ```

路由配置可最终抽离成一个单独的文件`Routes.dart`:

  ``` java

  import 'package:flutter/material.dart';
  import '../pages/Search.dart';
  import '../pages/Tabs.dart';

  // 配置路由
  final routes  = {
    '/' : (context, {arguments}) => Tabs(),
    '/search' : (context, {arguments}) => SearchPage(arguments: arguments),
    '/form' : (context, {arguments}) => SearchPage(arguments: arguments),
  };

  // 配置路由跳转
  var onGenerateRoute = (settings) {
          final String name = settings.name;
          final Function pageContentBuilder = routes[name];

          if(pageContentBuilder != null) {
            // If you push the route
            if (settings.arguments != null) {
              // Cast the arguments to the correct type: ScreenArguments.
              final Route route = MaterialPageRoute(
                builder: (context) => 
                  pageContentBuilder(context,arguments: settings.arguments));
              return route;
            }else {
              final Route route= MaterialPageRoute(
                builder: (context) => 
                  pageContentBuilder(context));
              return route;
            }
          }
        };
  ```

`main.dart`配置如下:

  ```java
  import 'package:flutter/material.dart';
  import 'routes/Routes.dart';

  void main() => runApp(MyApp());

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        onGenerateRoute: onGenerateRoute,
        initialRoute: '/', // 初始化加载的路由
        theme: ThemeData(primaryColor: Colors.lime),
        // routes: {
        //   '/search' : (context) => SearchPage(),
        // },
      );
    }
  }
  ```
### 路由替换以及返回到根路由

- `Navigator.of(context).pushReplacementNamed('路由名')`

  替换路由，将当前页面替换成指定页面，替换后的页面点击返回时，返回的还是当前页面的上一级

  因此可以借助路由替换来实现返回根路由

- `Navigator.of(context).pushAndRemoveUntil(newRoute, predicate)`

  直接返回根目录

  ```java
  Navigator.of(context).pushAndRemoveUntil(MaterialPageRoute(
                  builder: (context) => Tabs(),// 根路由页面
                ), (route) => route = null); 
  ```

### AppBar组件

将`MaterialApp`中的`debugShowCheckedModeBanner`设置成为`false`则不显示右上角`debugg`图标

顶部导航

- `title` 

  顶部导航文字 

- `backgroundColor`

  导航栏背景颜色

- `leading`

  导航栏左侧加元素，一般是图标,如果需要点击图标监听事件，则需要用`IconButton`

- `actions`

  导航栏右侧添加元素

- `centerTitle`

  设置文本是否居中

- `automaticallyImplyLeading`

  导航栏左侧是否显示自动生成的`leading`图标

  - 
  
    /// Controls whether we should try to imply the leading widget if null.
  ///
  /// If true and [leading] is null, automatically try to deduce what the leading
  /// widget should be. If false and [leading] is null, leading space is given to [title].
  /// If leading widget is not null, this parameter has no effect.

### TabController

- 在`MaterialApp`的`home`内添加`DefaultTabController()`,设置标签长度`length`

    若不配置`length`,运行时会报错：
    ```
      The method '>=' was called on null.
      ···
      When the exception was thrown, this was the stack:
      I/flutter ( 3567): #0      Object.noSuchMethod (dart:core-patch/object_patch.dart:51:5)
      I/flutter ( 3567): #1      new DefaultTabController (package:flutter/src/material/tab_controller.dart:315:22)
    ```

- 在`AppBar()`的`bottom`属性中添加`TabBar()`

- 在`body`中设置`TabView()`,定义标签切换对应的页面

  `TabView()`的长度必须与`TabBar()`中的一致，否则报错：

  ```
    The following assertion was thrown building TabBarView(dirty, dependencies: [_TabControllerScope],
    I/flutter ( 3567): state: _TabBarViewState#351c0):
    I/flutter ( 3567): Controller's length property (2) does not match the
    I/flutter ( 3567): number of tabs (3) present in TabBar's tabs property.
  ```
  
demo示例：

```dart
MaterialApp(
  theme: ThemeData(primaryColor: Colors.lime),
  home: DefaultTabController(
    length: 2,
    child: Scaffold(
      appBar: AppBar(
        title: Text("data"),
        bottom: TabBar(
          tabs: <Widget>[
            Tab(text: "热门",),
            Tab(text: "推荐",)
          ],
        ),
      ),
      body: TabBarView(
              children: <Widget>[
                ListView(
                  children: <Widget>[
                    ListTile(title: Text("热门标签内容"),),
                    ListTile(title: Text("热门标签内容"),),
                    ListTile(title: Text("热门标签内容"),),
                    ListTile(title: Text("热门标签内容"),),
                    ListTile(title: Text("热门标签内容"),),
                  ],
                ),
                ListView(
                  children: <Widget>[
                    ListTile(title: Text("推荐标签内容"),),
                    ListTile(title: Text("推荐标签内容"),),
                    ListTile(title: Text("推荐标签内容"),),
                    ListTile(title: Text("推荐标签内容"),),
                    ListTile(title: Text("推荐标签内容"),),
                  ],
                ),
              ],
            ),
    ),
))
```

### Divider组件

分割线

### Drawer组件

`Drawer`组件中可以设置`DrawerHeader`组件,设置抽屉头部样式

`UserAccountsDrawerHeader`组件可以快速实现头部组件样式，显示用户头像信息等

### 表单

#### `TextField` 文本框组件

## 第三方库

### flutter_swiper 轮播图


## 实践中的踩坑记录

### 更换APP图标及名称

- 更换图标 

  Android & IOS 图标一键生成网站： http://icon.wuruihong.com/

  上传一张原图片后，会自动生成压缩包，下载解压后可以看到Android和IOS两个文件夹

  - 将Android文件夹的内容复制到`项目根目录\android\app\src\main\res`,将原文件夹替换

  - 将IOS文件夹的内容复制到`项目根目录\ios\Runner\Assets.xcassets`下，将原`AppIcon.appiconset`文件夹替换

- 更换APP名称

  - Android名称： 打开`项目根目录\android\app\src\main`文件夹下的`AndroidManifest.xml`文件，修改`android:label`：

    ```xml
    <application
        android:name="io.flutter.app.FlutterApplication"
        android:label="聖巡"
        android:icon="@mipmap/ic_launcher">
        <activity
            android:name=".MainActivity"
            android:launchMode="singleTop"
            android:theme="@style/LaunchTheme"
            android:configChanges="orientation|keyboardHidden|keyboard|screenSize|locale|layoutDirection|fontScale|screenLayout|density|uiMode"
            android:hardwareAccelerated="true"
            android:windowSoftInputMode="adjustResize">
            <!-- This keeps the window background of the activity showing
                 until Flutter renders its first frame. It can be removed if
                 there is no splash screen (such as the default splash screen
                 defined in @style/LaunchTheme). -->
            <meta-data
                android:name="io.flutter.app.android.SplashScreenUntilFirstFrame"
                android:value="true" />
            <intent-filter>
                <action android:name="android.intent.action.MAIN"/>
                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>
        </activity>
    </application>

    ```

  - IOS名称： 打开`项目根目录\ios\Runner`下的`info.plist`文件，修改`dict.String`

    ```xml
    <dict>
      <key>CFBundleDevelopmentRegion</key>
      <string>$(DEVELOPMENT_LANGUAGE)</string>
      <key>CFBundleExecutable</key>
      <string>$(EXECUTABLE_NAME)</string>
      <key>CFBundleIdentifier</key>
      <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
      <key>CFBundleInfoDictionaryVersion</key>
      <string>6.0</string>
      <key>CFBundleName</key>
      <string>聖巡</string>
      <key>CFBundlePackageType</key>
      <string>APPL</string>
      <key>CFBundleShortVersionString</key>
      <string>$(FLUTTER_BUILD_NAME)</string>
      <key>CFBundleSignature</key>
      <string>????</string>
      <key>CFBundleVersion</key>
      <string>$(FLUTTER_BUILD_NUMBER)</string>
      <key>LSRequiresIPhoneOS</key>
      <true/>
      <key>UILaunchStoryboardName</key>
      <string>LaunchScreen</string>
      <key>UIMainStoryboardFile</key>
      <string>Main</string>
      <key>UISupportedInterfaceOrientations</key>
      <array>
        <string>UIInterfaceOrientationPortrait</string>
        <string>UIInterfaceOrientationLandscapeLeft</string>
        <string>UIInterfaceOrientationLandscapeRight</string>
      </array>
      <key>UISupportedInterfaceOrientations~ipad</key>
      <array>
        <string>UIInterfaceOrientationPortrait</string>
        <string>UIInterfaceOrientationPortraitUpsideDown</string>
        <string>UIInterfaceOrientationLandscapeLeft</string>
        <string>UIInterfaceOrientationLandscapeRight</string>
      </array>
      <key>UIViewControllerBasedStatusBarAppearance</key>
      <false/>
    </dict>

    ```

### 命名规范

此命名规范来自Dart官方网站： `https://dart.dev/guides/language/effective-dart/style`

Dart中的命名方式有三种： `UpperCamelCase` 首字母大写(包括第一个字母)的驼峰式、`lowerCamelCase`首字母大写，第一个字母小写的驼峰式、`lowercase_with_underscores`带有下划线的小写字母

1. `Classes, enums, typedefs, and type parameters should capitalize the first letter of each word (including the first word), and use no separators.`

    类名、枚举、`typedefs`(这啥？)、泛型参数采用`UpperCamelCase`

2. `DO name libraries, packages, directories, and source files using lowercase_with_underscores.`

  库名、包名、文件夹名、文件名采用`lowercase_with_underscores`(小写字母+下划线)

3. `DO name import prefixes using lowercase_with_underscores.`

  重命名导入的包时，采用`lowercase_with_underscores`(小写字母+下划线)

4. `DO name other identifiers using lowerCamelCase.`

  命名其他时采用`lowerCamelCase`

5. `PREFER using lowerCamelCase for constant names.`

  最好使用`lowerCamelCase`来命名常量

### 嵌入地图

我为啥一上来就用了个这么虐心的组件？？？o(╥﹏╥)o

#### 高德地图

`amap_base_flutter`插件可以实现定位、简单的地图展示、导航、搜索等功能

Android版：

  - 在`pubspec.yaml`文件中引入依赖，无需添加版本号：

    ```properties
    dependencies:
      amap_location:

    ```

  - 至高德地图`https://lbs.amap.com/api/android-sdk/guide/create-project/get-key`注册`API key`

  - 修改 `项目目录/app/build.gradle` 在`android/defaultConfig`节点修改`manifestPlaceholders`,新增百度地图AK配置

    ```properties
    android {
      .... 你的代码

      defaultConfig {
          .....
          manifestPlaceholders = [
                  AMAP_KEY : "你的高德地图AK", // 高德地图AK
          ]

      }

    ```

### Http请求

1. 引入`dio`包

    `dio`是一个强大的`Dart Http`请求库，支持`Restful API`、`FormData`、拦截器、请求取消、Cookie管理、文件上传/下载、超时、自定义适配器等...

    在`pubspec.yaml`文件中添加依赖:

  ```yaml
      dependencies:
        dio: ^3.x.x  // 请使用pub上3.0.0分支的最新版本(本人用的是3.0.5)
  ```

常见报错信息：

- `SocketException: Failed host lookup: 'www.baidu.com' (OS Error: No address associated with hostnam, errno = 7)`

    测试DIO做请求时，写了个方法get百度首页数据，返回此报错，结果发现是手机没联网导致，emmm...

- `Unhandled Exception: DioError [DioErrorType.RESPONSE]: Http status error [400]`

    - 状态为400可能有很多原因，此为碰到的其中之一
      
      `post`发送请求时一直没反应，状态为400，后来终于发现是封装方法是出现问题
      
      `get`方法： 

      ```dart
        get(url, {data, options, cancelTocken}) async{
          Response response;
          try {
            response = await dio.get(url, queryParameters: data, options: options, cancelToken: cancelToken);
            print('get success---------${response.statusCode}');
            print('get success---------${response.data}');
      
          } on DioError catch (e) {
            print('get error---------$e');
          }
          return response.data;
        }
      ```

      `post`方法：

        ```dart
          post(url, {data, options, cancelToken}) async {
            Response response;
            try {
              response = await dio.post(url, data: data, options: options, cancelToken: cancelToken);
              print('get success---------${response.statusCode}');
              print('get success---------${response.data}');
            } on DioError catch (e) {
              print('get error---------$e');
            } 
            return response.data;
          }
        ```

        `get`方法中，接收参数的属性是`queryParameters`,`post`方法中，接收参数的属性是`data`,一开始将`post`方法中接收参数的属性写成了`queryParameters`,结果做请求时一直毫无反应，debug进去发现报了`Http status error [400]`的错。坑！

- `DioError [DioErrorType.RESPONSE]: Http status error [415]`

  

  

## 报错集锦

- `* Error running Gradle: ProcessException: Process "D:\vscodework\yardApp\android\gradlew.bat" exited abnormally: Configure project :app`

  八成是被墙了，下载不下来依赖，在环境变量中配置一下两个参数就解决了：

  ```
    FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn

    PUB_HOSTED_URL=https://pub.flutter-io.cn
  ```
  环境变量配置好后需要重启电脑才能生效








---
参考资料：

1. Flutter官网： https://flutter.dev/

2. 技术胖教学视频： https://www.bilibili.com/watchlater/#/av35800108/p1

3. Material官网： https://material.io/

4. Flutter教程_2019年最新Flutter 零基础入门实战教程:  https://www.bilibili.com/watchlater/?spm_id_from=666.19.b_62696c692d6865616465722d6d.17#/av53072584/p17


