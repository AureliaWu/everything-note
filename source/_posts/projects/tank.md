---
layout: "post"
title: "坦克大战"
date: "2023年6月6日14:04:55"
categories: 实战
tags: [Computer Language, 实战]
---

# Frame类

```java
    Frame f = new Frame(); // 新建Frame类
    f.setSize(800, 600);// 设置窗口大小
    f.setResizable(false);// 设置窗口不能调整大小
    f.setTitle("Tank War");// 设置窗口名称
    f.setVisible(true);// 设置窗口可见

    // 添加窗口监听事件
    f.addWindowListener(new WindowAdapter() {
        // 添加窗口关闭事件
        @Override
        public void windowClosing(WindowEvent e) {
            System.exit(0);
        }
    });
```

# 坦克大战

## 创建TankFrame类继承Frame类
`public class TankFrame extends Frame {}`

## 在构造函数中设置默认值

```java

    public TankFrame() {
        setSize(800, 600);
        setResizable(false);
        setTitle("Tank War");
        setVisible(true);

        addKeyListener(new KeyListener());// 监听键盘按键事件

        addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }

```

## 创建内部类KeyListener控制键盘按键

`class KeyListener extends KeyAdapter {}`

重写KeyAdapter类中的`keyPressed()`和`keyReleased()`方法


## 判断两个方块相交

使用工具类Rectangle,`Rectangle.intersects()`

```java
Rectangle rect1 = new Rectangle(x, y, WIDTH, HEIGHT);
Rectangle rect2 = new Rectangle(x2, y2, WIDTH2, HEIGHT2);

if(rect1.intersects(rect2)) System.out.println("两者相交");

```

## 坦克大战中的设计模式

1. 单例模式

    应用场景：只需要一个实例 比如各种各样的manager、Factory

    - 饿汉式

        类加载到内存后就实例化一个单例，JVM保证线程安全，缺点是无论是否会用都会在类装载完成时完成实例化

        ```java

            public class SingletonDemo {
                private static final SingletonDemo INSTANCE = new SingletonDemo();

                private SingletonDemo() {};
                
                public static SingletonDemo getInstance() { return INSTANCE; }    
            }
        ```
    
    - 懒汉式

        按需使用
        
        - 多线程使用不安全写法

        ```java

        public class SingletonDemo {
            private static SingletonDemo INSTANCE = null;

            private SingletonDemo() {};

            public static SingletonDemo getInstance() {
                if(INSTANCE == null) INSTANCE = new SingletonDemo();
                
                return INSTANCE;
            }
        }

        ```

        - 多线程使用安全写法
            
            类加载时不会产生实例，只有在调用`getInstance()`时调用静态内部类会实例化对象

        ```java
        public class SingletonDemo {
            private SingletonDemo() {};

            private static class SingletonDemoHolder {
                private final static SingletonDemo INSTANCE = new SingletonDemo();
            }

            public static SingletonDemo getInstance() {
                return SingletonDemoHolder.INSTANCE;
            }
        }
        ```

        - 目前语法上最完美的写法，既能解决线程同步问题，还能防止反序列化

            调用时直接使用 `SingletonDemo.INSTANCE`

        ```java
        public enum SingletonDemo {
            INSTANCE;
        }
        ```

        枚举类没有构造方法，所以能防止反序列化

    实际使用时常用的还是饿汉式


2. 策略模式

    `Comparator`接口 和 `Comparable`接口

    - `Comparator`接口是java.util包内的接口，包含两个抽象方法： `compare(o1，o2)`和`equals(obj)`

    - `Comparable`接口是java.lang包内的接口，只有一个方法： `compareTo(obj)`

    开闭原则： 对修改关闭，对扩展开放

    实现`Comparable`接口时只能有一个compareTo方法

3. 工厂模式

    简单工厂和静态工厂

    任何产生对象的方法或类都可以称为工厂

    形容词用接口，名词用抽象类

    工厂模式更好的方法是spring里面的bean工厂

    坦克大战里面利用抽象工厂完成一键风格替换

    父类抽象方法时，方法要尽量少，因为父类方法越多实现时子类就会要覆写越多

    生产一系列的类是抽象工厂
    
    抽象工厂在实际的开发过程中使用的不是特别多


4. facade模式（门面模式）

5. Mediator模式(调停者模式)

6. 责任链模式

## 总结

1. 面向对象设计时，慎用继承关系，因为继承是一种强关系，父类变了，子类必须变。

强关系对于代码的扩展性是有局限的。

2. Java转exe需要java虚拟机、jar包和转换工具