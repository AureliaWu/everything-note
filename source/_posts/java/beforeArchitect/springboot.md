---
layout: "post"
title: "SpringBoot"
date: "2020-4-29 17:18"
categories: framework,Springboot
tags: [Computer Language, framework, Springboot]
---

# SpringBoot基础

## 框架介绍

SpringBoot主要解决的是在微服务架构下简化配置（有快速配置）、前后端分离、快速开发

优点： 

- 提供了快速启动入门
- 开箱即用、提供默认配置
- 内嵌容器化web项目
- 没有冗余代码生成和XML配置要求
  
### 模板引擎
  
模板引擎： 如 `Thymeleaf`, `FreeMarker`

有嵌套和解析的过程，先加载静态页面，在静态页面上添加一些标记，模板引擎的内核会根据添加的标记动态渲染数据


**计算向数据移动**

### MVC架构思想

? JVM垃圾回收机制现在已经不是引入计数器的方式，改为GCroot

? Spring不支持循环引用，主要是因为其自身结构问题。

### 基于SpringBoot的MVC

- 数据的展示查询
  
### 分层解释

- `Controller`层
  
  一般写业务逻辑跳转

- `Service`层
  
  业务层逻辑代码

- `DAO`层
  
  操作持久层

### 各种依赖

#### JPA(Java Persistence API)
  
  添加依赖 `Spring-data-jpa`, 用于访问数据源的框架，可以把数据库的表映射成对象，一一对应

### 注释解说

#### `@RequestMapping`

请求路径

#### `@PathVariable("key")`

取URI中`key`对应的值


# 实践中报错记录

## 下载依赖包速度过慢

解决方法： 配置阿里云镜像地址

全局配置步骤： 

1. 找到maven的`setting.xml`文件，若没有可以新建
2. 在`setting.xml`文件的`mirrors`节点下面添加子节点
   
   ```xml
   <mirror>
      <id>alimaven</id>
      <name>aliyun maven</name>
	  <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
      <mirrorOf>central</mirrorOf>
    </mirror>
   ```

## 运行成功并退出

`Process finished with exit code 0`

原因： `Pom.xml`文件缺少依赖

```xml

 <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-web</artifactId>
  </dependency>

```

## 引入`spring-security`每次调用需要输入登录名密码

解决办法： 关闭验证

1. `springboot 2.0` 之前可通过yml配置关闭验证：

    ```yml

    security.basic.enabled=false
    management.security.enabled=false

    ```

2.  `springboot 2.x`后关闭验证

     `springboot 2.x` 后上述配置被废除，需要在启动类前的 `@SpringBootApplication` 注解中加入 `exclude` 属性 `scurityAutoConfiguration`

     ```java
      @SpringBootApplication(exclude = SecurityAutoConfiguration.class)
     ```

## 数据库连接报错

报错内容: `java.sql.SQLException: The server time zone value '�й���׼ʱ��' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the 'serverTimezone' configuration property) to use a more specifc time zone value if you want to utilize time zone support.`

报错原因： 数据库连接时区配置问题

解决方法： 数据库配置添加时区配置 `serverTimezone=UTC`

```yml
spring:
  datasource:
    username: ${MYSQL_USER:root}
    password: ${MYSQL_PASSWORD:123456}
    url: jdbc:mysql://${MYSQL_HOST:localhost}:${MYSQL_PORT:3306}/${MYSQL_DATABASE:dbname}?serverTimezone=UTC&useUnicode=true&useSSL=false&characterEncoding=utf8

```










---
参考资料：




