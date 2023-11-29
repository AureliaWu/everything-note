---
layout: "post"
title: "Maven"
date: "2023年6月6日14:04:55"
categories: Spring
tags: [Computer Language, Spring]
---

Maven：

项目对象模型POM

核心配置文件： setting.xml

Maven工程关系： 依赖关系、继承关系、聚合关系

## 常见的插件

### 编译器插件

`settings.xml`文件里面可配置全局默认的JDK版本,`settings.xml`文件中的id不能随便取名

```xml
<profiles>
    <profile>
      <id>jdk-1.4</id>
      <activation>
        <jdk>1.4</jdk>
      </activation>
      <repositories>
        <repository>
          <id>jdk14</id>
          <name>Repository for JDK 1.4 builds</name>
          <url>http://www.myhost.com/maven/jdk14</url>
          <layout>default</layout>
          <snapshotPolicy>always</snapshotPolicy>
        </repository>
      </repositories>
    </profile>
</profiles>

```

若不想用setting.xml中默认的JDK，可以在项目的`pom.xml`文件中添加一个编译器插件的配置

```xml
<build>
    <plugins>
        <!-- JDK编译插件-->
        <plugin>
            <!--插件坐标-->
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.2</version>
            <configuration>
                <!--源代码使用JDK版本-->
                <source>1.7</source>
                <!--源代码编译为class文件的版本，要与上面版本保持一致-->
                <target>1.7</target>
                <encoding>UTF-8</encoding>
            </configuration>
        </plugin>
    </plugins>
</build>

```

### 资源拷贝插件

配置文件一般都放在`src/main/resources`目录下，打包后配置文件会在`target/classes`目录中,默认情况下不放在`src/main/resources`的配置文件打包后不会存在`target/classes`目录中，若想要把指定路径下的配置文件打包到`target/classes`目录中需要添加以下配置：

```xml
<build>
    <resources>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.xml</include>
            </includes>
        </resource>
        <resource>
            <directory>src/main/resources</directory>
            <includes>
                <include>**/*.xml</include>
                <include>**/*.properties</include>
            </includes>
        </resource>
    </resources>
</build>
```

上述配置表示`src/main/java`目录下的xml文件和`src/main/resources`目录下的xml文件、properties文件都会被打包到`target/classes`中

### Tomcat插件

```xml
<build>
    <plugins>
        <!-- 配置Tomcat插件-->
        <plugin>
            <groupId>org.apache.tomcat.maven</groupId>
            <artifactId>tomcat7-maven-plugin</artifactId>
            <version>2.2</version>
            <configuration>
                <!--配置Tomcat监听端口-->
                <port>8080</port>
                <!--配置项目的访问路径(Application Context)-->
                <path>/</path>
            </configuration>
        </plugin>
    </plugins>
</build>
```

使用Tomcat插件发布部署并执行war工程的时候，需要使用启动命令，启动命令为: `tomcat7:run`.命令中的tomcat7是插件命名，由插件提供商决定。run为插件中的具体功能。

Tomcat是可运行插件，必须要通过命令来运行控制

## 常见命令

`mvn install`

本地安装，包含编译、打包、安装到本地仓库

`mvn clean`

清除已编译信息，删除工程中的target目录

常用的命令在IDEA都有可视化界面可以操作