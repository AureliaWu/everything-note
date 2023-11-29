---
layout: "post"
title: "JDBC"
date: "2020-10-25 22:54"
categories: Database
tags: [Computer Language, JDBC]
---

# JDBC

## 一些概念

- `ODBC`: 一套连接数据源的标准

- `JDBC`: `Java Database Connectivity`

    基于Java语言访问数据库的一种技术。

    JDBC是一种用于执行SQL语句的Java API，可以为多种关系数据库提供统一访问，由一组用Java语言编写的类和接口组成。JDBC提供了一种基准，据此可以构建更高级的工具和接口，使数据库开发人员能够编写数据库应用程序，同时JDBC也是个商标名

    JDBC设计思想： 由SUN公司提供访问数据库的接口，由数据库厂商提供对这些接口的实现，程序员编程时都是针对接口进行编程的。

    JDBC包括一套JDBC的API和一套程序员和数据库厂商都必须去遵守的规范。

      - java.sql包： 提供访问数据库基本的功能
      - javax.sql包： 提供扩展的功能
        
    JDBC是数据库的中间件

    JDBC可以做什么？

      - 连接到数据库
      - 在java app中执行SQL命令
      - 处理结果

- `SPI`
  
  `Service Provider Interface`
  。是JDK内置的一种服务提供发现机制，SPI是一种动态替换发现的机制，比如有个接口，想运行时动态给它添加实现，你只需要添加一个实现。我们经常遇到的就是`java.sql.Driver`接口，其他不同厂商可以针对同一接口做出不同的实现，`mysql`和`posthresql`都有不同的实现提供给客户，而Java的SPI机制可以为某个接口寻找服务实现
  
## 面向接口编程 java.sql

如果需要建立连接，java中提供了一套标准，数据库厂商来进行实现，包含实现子类，实现子类的jar文件一般放在数据库安装目录下

1. java.sql.Driver 驱动
2. java.sql.Connection 连接
3. java.sql.Statement 静态处理快
   
   java.sql.PreparedStatement 预处理块

4. java.sql.ResultSet 结果集
5. java.sql.ResultSetMetaData 结果集元数据

### JDBC连接数据库

```java
// 1. 加载驱动
/* 当执行了当前代码之后，会返回一个class对象，在此对象的创建过程中，会调用具体类的静态代码块 */

Class.forName("oracle.jdbc.driver.OracleDriver");

// 2. 建立连接
/** 第一步已经将driver对象注册到了drivermanager中，所以此时可以直接通过DriverManager来获取数据库连接

需要输入连接数据库的参数：

- url: 数据库的地址

- username： 用户名

- password： 密码

**/

Connection connection = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:orcl", "scott", "123456");

// 3. 测试连接是否成功
System.out.println(connection);

// 4. 定义sql语句
String sql = "select * from emp";

// 5. 准备静态处理块对象，需要一个对象来存放sql语句，将对象进行执行的时候调用的是数据库的服务，数据库会从当前对象中拿到对应的sql语句进行执行
Statement statement = connection.createStatement();

// 6. 执行sql语句，返回值对象是结果集合
ResultSet resultSet = statement.executeQuery(sql);

// 7. 循环处理
while(resultSet.next()) {
    // 通过下标索引编号获取值，索引从1开始
    int anInt = resultSet.getInt(1);

    // 通过列名获取值
    String ename = resultSet.getString("ename");
}

// 8. 关闭连接
statement.close();
connection.close();

```
   