---
layout: "post"
title: "Spring"
date: "2020-08-10 21:13"
categories: framework,Spring
tags: [Computer Language, framework, Spring]
---

# Spring初识
## 框架

什么是框架？某些个人或组织定义了一系列的类或接口，提前定义好一些实现，用户可以在这些类和接口的基础上使用这些类来迅速形成某个领域或者某个行业的解决方案，简化开发过程，提高开发效率。

## 软件设计发展历程
### 单一应用架构
ORM： Object Relational Mapping 对象关系映射

当网站流量很小时，只需一个应用，将所有功能都部署在一起以减少部署节点和成本，此时用于简化增删改查工作量的数据访问框架(ORM)是关键。

### 垂直应用架构
当访问量逐渐增大，单一应用增加及其带来的及速度月俩月小，提升效率的方法之一是将应用拆成互不相干的几个应用，以提升效率此时用于加速前端页面开发的Web框架(MVC)是关键。

### 分布式服务架构
当垂直应用越来越多，应用之间交互不可避免，将核心业务抽取出来，作为独立的服务，逐渐形成稳定的服务中心，使前端应用能更快速的响应多变的市场需求。此时，用于提高业务服用及整合的分布式服务框架(RPC)是关键。

### 流动计算架构
当服务越来越多，容量的评估，小服务资源的浪费等问题逐渐显现，此时需要增加一个调度中心基于访问压力实时管理集群容量，提高集群利用率。此时，用于提高机器利用率的资源调度和治理中心(SOA)是关键。

**Spring出现之前使用的是EJB**

## 主流框架演变之路
1. JSP + Servlet + JavaBean
   - JSP: Java Server Page 能内置Java代码，但配置比较麻烦
  
   - Servlet: Server Applet
  
   - JavaBean: 更多用于描述现实世界某个具体事物的抽象

2. MVC三层架构
   
   Model + View + Control

    层次分清，耦合性低

3. 使用EJB进行应用开发，但是EJB是重量级框架，使用时有过多的接口和依赖，侵入性强，在使用上比较麻烦
   
4. SSH(Struts1/Struts2 + Hibernate + Spring)
   
5. SpringMVC + MyBatis + Spring
   
6. SpringBoot开发，约定大于配置
   
# Spring理论概念

**Spring框架作为主流框架立于不败之地在于其生态**

官网： https://spring.io/

## 关于版本

- GA（General Availability）：表示正式发布的版本，官方推荐使用此版本
  
- PRE： 预览版，内部测试版，主要给开发人员和测试人员测试用
- SNAPSHOT： 快照版，可稳定使用，且仍在继续改进版本

## 核心解释

Spring是一个开源框架，为了简化企业开发而生，使开发变得更加优雅和简洁

#### 优点

1. 通过DI、AOP和消除样板式代码来简化企业开发
   
2. Spring框架之外还存在一个构建在核心框架之上的庞大生态圈，它将Spring扩展到不同领域，如Web服务、REST、移动开发以及NoSQL
3. 低侵入式设计，代码的污染极低
4. 独立于各种应用服务器，基于Spring的框架的应用可以真正实现Write Once, Run Anywhere
5. Spring的IOC容器降低了业务对象替换的复杂性，提高了组件之间的解耦
6. Spring的AOP支持允许将一些通用任务如安全、事务、日志等进行集中式处理，从而提供了更好的服用
7. Spring的ORM和DAO提供了与第三方持久层框架的良好整合，并简化了底层的数据库访问
8. Spring的高度开放性，并不强制应用完全依赖于Spring,开发者可自由选用Spring框架的部分或者全部

## IOC(Inversion of Control) 控制反转

### 什么是IOC

IOC与依赖注入(DI)同理，这是一个通过依赖注入对象的过程，也就是说他们所使用的对象，是通过构造函数参数、工厂方法的参数或从工厂方法的构造函数或返回值的对象实例设置的属性，然后容器在创建bean时注入这些需要的依赖。这个过程相对于普通创建对象的过程是反向的，因此称之为IOC。

谁控制谁： IOC容器控制对象

控制什么： 实现过程中所需要依赖的对象

什么是反转： IOC容器之前我们都是在对象中主动去创建依赖的对象，这是正转；有了IOC之后依赖的对象直接由IOC容器创建后注入到对象中，由主动创建变成了被动接受，这是反转

哪些方面被反转：依赖的对象

### IOC与DI

IOC是设计思想，DI是具体的实现方式

DI： Dependency Injecttion 依赖注入

### 解耦

耦合关系不仅是对象与对象之间，也会出现在软件系统的各个模块之间。可通过IOC来实现对象之间的解耦

# Spring的使用

Spring核心模块包：Beans Core Context SpEL(Spring expression)

beans和context包是Spring IoC的核心包。

```java
ApplicationContext context = new ClassPathXmlApplicationContext("配置文件路径");
context.getBean("对象名");
```

ApplicationContext表示IOC容器入口，想要获取对象，必须要创建该类。该类有两个读取配置文件的实现类：

- ClassPathXmlApplicationContext： 表示从classpath中读取数据（常用）
- FileSysytemXmlApplicationContext: 表示从当前文件系统读取数据

使用`context.getBean("person")`来获取对象，需要进行类型强转

`context.getBean("person", Person.Class)` 这种方式获取对象时不需要强转数据类型

这种方式无需手动创建对象，而是将创建对象的过程交给了spring容器。容器中的对象在容器创建完成之前就已经把对象创建好了，
即使没有使用getBean方法来获取对象，对象也已经创建好了，而不是get的时候再创建

对象的配置文件：

```xml
<bean id="person" class="对象所在包">
   <property name="id" value="1"></property>
   <property name="name" value="xxx"></property>
    ...
</bean>

```

`<bean>`标签表示要创建的bean对象：
- id为bean的唯一标识，为了与其他bean进行区分
- class表示要创建的bean的完全限定名
- property标签表示bean的属性，name为名称，value为具体的属性值

## 通过Maven的方式来创建项目

### 第一步 导包

使用IDEA选择Maven创建Spring项目，创建完成后会自动生成pom.xml配置文件

在Pom.xml文件里面添加Spring配置包

```xml
<dependencies>
   <!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->
   <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>5.2.3.RELEASE</version>
   </dependency>

</dependencies>

```

### 第二步 创建对象文件

在java文件夹下创建所需的对象属性

### 第三步 创建配置文件

在resource文件夹下创建对应的配置文件

### 第四步 测试对象是否创建成功

注意： 配置文件的位置不要放错

## Spring总结

1. ApplicationContext就是IOC容器的接口，可以通过此对象获取容器中创建的对象

2. 对象在Spring容器中默认是在容器创建完成之前就已经创建完成，不是需要用的时候才创建。多例模式下不会提前创建对象

3. 对象在IOC容器中存储的时候都是单例的，如果需要多例则需要修改属性

   在xml配置文件的bean上添加属性 `scope=prototype`,变成多例模式

   ```xml
   <bean id="person" class="com.qiyixing.bean.Person" scope="prototype">
        <property name="id" value="1" ></property>
        <property name="name" value="奇一星"></property>
        <property name="age" value="20"></property>
        <property name="gender" value="女"></property>
    </bean>
   ```

4. 创建对象给属性赋值的过程是通过setter方法实现的

5. 对象的属性是由setter/getter方法决定的，而不是定义的成员属性

## Spring对象的获取和属性赋值的方式

1. 通过bean的id获取IOC容器中的对象： `context.getBean("bean的id")`

2. 通过bean的类型获取对象: `context.getBean(Person.class)`

   根据类型获取对象时，如果存在两个相同的类型的对象则会报错

3. 通过构造器给bean对象进行赋值

   当需要从容器中获取对象的时候，最好要保留无参构造方法，因为底层的实现是反射

   ```xml
   <bean id="person2" class="com.qiyixing.bean.Person">
        <constructor-arg name="id" value="2"></constructor-arg>
        <constructor-arg name="name" value="LuckyStar"></constructor-arg>
        <constructor-arg name="age" value="20"></constructor-arg>
        <constructor-arg name="gender" value="男"></constructor-arg>
    </bean>
   ```

   配置构造器时如果出现了报错，说明对应的对象里面没有找到该构造函数。此时参数的name属性是根据构造方法的参数名称决定的。name属性可以省略不写，但是需要注意顺序

   ```java
      ApplicationContext context = new ClassPathXmlApplicationContext("ioc.xml");
      Person person = context.getBean("person2", Person.class);
      System.out.println(person);
   ```

   在进行框架配置的时候，可以使用xml文件，也可以使用注解的方式。实际项目中是xml配置和注解配置一起使用

4. 通过命名空间为bean赋值，简化配置文件中属性声明的写法

   使用p命名空间来给属性赋值

   1. 引入p命名空间， 添加`xmlns:p="http://www.springframework.org/schema/p"`；xmlns xml命名空间(namespace) 简称

   ```xml
      <beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p" 
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   ```

   2. 使用p命名空间简写，省略property

   ```xml
      <bean id="person3" class="com.qiyixing.bean.Person" p:id="3" p:name="一星" p:age="18" p:gender="男"></bean>
   ```

5. 为复杂类型进行赋值操作

   复杂类型如集合、数组、其他对象等。

   对象实体类Person.java

   ```java
   package com.qiyixing.bean;

   import java.util.Arrays;
   import java.util.List;
   import java.util.Map;
   import java.util.Properties;
   import java.util.Set;

   public class Person {
      public int getId() {
         return id;
      }

      public void setId(int id) {
         this.id = id;
      }

      public String getName() {
         return name;
      }

      public void setName(String name) {
         this.name = name;
      }

      public int getAge() {
         return age;
      }

      public void setAge(int age) {
         this.age = age;
      }

      public String getGender() {
         return gender;
      }

      public void setGender(String gender) {
         this.gender = gender;
      }

      private int id;

      private String name;

      private int age;

      private String gender;

      private String[] hobbies;

      private Address address;

      private List<Address> lists;

      private Map<String, Object> map;

      private Set<String> sets;

      @Override
      public String toString() {
         return "Person{" +
                  "id=" + id +
                  ", name='" + name + '\'' +
                  ", age=" + age +
                  ", gender='" + gender + '\'' +
                  ", hobbies=" + Arrays.toString(hobbies) +
                  ", address=" + address +
                  ", lists=" + lists +
                  ", map=" + map +
                  ", sets=" + sets +
                  ", properties=" + properties +
                  '}';
      }

      private Properties properties;

      public String[] getHobbies() {
         return hobbies;
      }

      public void setHobbies(String[] hobbies) {
         this.hobbies = hobbies;
      }

      public Address getAddress() {
         return address;
      }

      public void setAddress(Address address) {
         this.address = address;
      }

      public List<Address> getLists() {
         return lists;
      }

      public void setLists(List<Address> lists) {
         this.lists = lists;
      }

      public Map<String, Object> getMap() {
         return map;
      }

      public void setMap(Map<String, Object> map) {
         this.map = map;
      }

      public Set<String> getSets() {
         return sets;
      }

      public void setSets(Set<String> sets) {
         this.sets = sets;
      }

      public Properties getProperties() {
         return properties;
      }

      public void setProperties(Properties properties) {
         this.properties = properties;
      }

      public Person () {
         System.out.println("person被创建");
      }

      public Person(int id, String name, int age, String gender) {
         this.id = id;
         this.name = name;
         this.age = age;
         this.gender = gender;
      }

   }

   ```

   对应的配置文件ioc.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
      <beans xmlns="http://www.springframework.org/schema/beans"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xmlns:p="http://www.springframework.org/schema/p"
            xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
         <bean id="person" class="com.qiyixing.bean.Person">
            <property name="id" value="1" ></property>
            <property name="name" value="奇一星"></property>
            <property name="age" value="20"></property>
            <property name="gender" value="女"></property>
            <!-- 使用array标签为数组赋值 -->
            <property name="hobbies">
                  <array>
                     <value>book</value>
                     <value>movie</value>
                  </array>
            </property>

            <!-- 使用ref给引用类型赋值 -->
            <property name="address" ref="address"></property>

            <!-- 给list赋值-->
            <property name="lists">
                  <list>
                     <!-- 使用内部bean,无法从容器中直接获取对象的值，即使用context.getBean("address2")是无法获取到数据的-->
                     <bean id="address2" class="com.qiyixing.bean.Address">
                        <property name="province" value="江西"></property>
                     </bean>
                     <bean class="com.qiyixing.bean.Address">
                        <property name="province" value="湖北"></property>
                     </bean>

                     <!-- 使用外部bean， 可以使用context.getBean("address")获取到address对象-->
                     <ref bean="address"></ref>
                  </list>
            </property>

            <!-- 给set属性赋值-->
            <property name="sets">
                  <set>
                     <value>张三</value>
                     <value>李四</value>
                  </set>
            </property>

            <!-- 给Map赋值,entry可以有各种写法-->
            <property name="map">
                  <map>
                     <entry key="a" value="111"></entry>
                     <entry key="address" value-ref="address"></entry>
                     <entry key="address2">
                        <bean class="com.qiyixing.bean.Address">
                              <property name="province" value="江西"></property>
                        </bean>
                     </entry>
                     <entry>
                        <key><value>keykeykey</value></key>
                        <value>val</value>
                     </entry>
                  </map>
            </property>

            <!--给properties赋值-->
            <property name="properties">
                  <props>
                     <prop key="111">aaa</prop>
                     <prop key="222">bbb</prop>
                  </props>
            </property>
         </bean>

         <bean id="address" class="com.qiyixing.bean.Address">
            <property name="city" value="上海"></property>
            <property name="province" value="上海"></property>
            <property name="town" value="上海"></property>
         </bean>
      </beans>

   ```

6. 继承关系bean的配置

   ```xml
   <bean id="parent" class="com.qiyixing.bean.Person">
      <property name="id" value="4" ></property>
      <property name="name" value="父类"></property>
      <property name="age" value="20"></property>
      <property name="gender" value="女"></property>
   </bean>

   <bean id="son" class="com.qiyixing.bean.Person" parent="parent">
      <property name="name" value="子类"></property>
   </bean>
   ```

   使用`context.getBean("son")`能将son和parent的值都获取到

   如果只想实例化子类不想实例化父类，可以将父类变成抽象类

   ```xml
   <bean id="parent" class="com.qiyixing.bean.Person" abstract="true">
      <property name="id" value="4" ></property>
      <property name="name" value="父类"></property>
      <property name="age" value="20"></property>
      <property name="gender" value="女"></property>
   </bean>

   ```

   此时`context.getBean("parent")`会报错，因为抽象类不能被实例化

7. bean对象创建的依赖关系

   bean对象创建时，是按照xml配置文件定义的顺序创建的，写在前面的类会先被创建，后面的类后创建。如果需要打乱这种创建顺序，可以使用属性`depends-on`

   ```xml
      <bean id="person" class="com.qiyixing.bean.Person"></bean>
      <bean id="address" class="com.qiyixing.bean.Address"></bean>
   ```

   上述情况会先创建person对象后创建address对象

   ```xml
      <bean id="person" class="com.qiyixing.bean.Person" depends-on="address"></bean>
      <bean id="address" class="com.qiyixing.bean.Address"></bean>
   ```

   加上属性`depends-on`之后则是先创建address对象后创建person对象。实际工作中不需要关注bean的创建顺序

8. bean的作用于控制，是否是单例

   `scope`属性可以指定当前bean的作用域，默认是单例模式singleton;prototype表示多例模式；

   Spring4.x版本中还包含另外两种作用域：request和session

   request表示请求，每次发送请求都会有一个新的对象

   session表示吗，每次会话都会有一个新的对象

   但request和session几乎不用，因此5.x之后就淘汰了

   单例作用域在IOC容器创建之前就已经创建了bean对象，多例作用域只有在获取对象的的时候才会创建对象

9. 利用工厂模式创建bean对象

   之前的案例中，所有bean对象都是通过反射得到bean实例，Spring中还包含另外一种通过工厂模式创建对象的方式。利用工厂模式创建bean对象分为静态工厂和实例工厂

   静态工厂： 工厂本身不需要创建对象，但可以通过静态方法调用，对象=工厂类.静态方法名()

      - 创建java静态工厂类

         ```java

         public class PersonStaticFactory {
            public static Person getInstance(String name) {
               Person person = new Person();
               person.setId(1);
               person.setName(name);
               person.setAge(18);

               return person;
            }
         }
         ```

      - 配置xml文件

         ```xml
         <!-- 利用静态工厂方法创建bean -->
         <bean id="personStatic" class="com.qiyixing.factory.PersonStaticFactory" factory-method="getInstance">
            <constructor-arg value="静态工厂创建的bean"></constructor-arg>
         </bean>
         ```

   实例工厂： 工厂本身需要创建对象，工厂类 工厂对象=new 工厂类； 工厂对象.get对象名()

      - 创建java实例工厂类

         ```java
         public class PersonInstanceFactory {
            public Person getInstance(String name) {
               Person person = new Person();
               person.setId(2);
               person.setName(name);
               person.setAge(20);

               return person;
            }
         }
         ```

      - 配置xml文件

         ```xml
         <!-- 利用实例工厂方法创建bean -->
         <!-- 1. 先创建工厂实例-->
         <bean id="factory" class="com.qiyixing.factory.PersonInstanceFactory"></bean>

         <!-- 2. 调用工厂实例方法 -->
         <bean id="personInstance" class="com.qiyixing.bean.Person" factory-bean="factory" factory-method="getInstance">
            <constructor-arg value="实例工厂创建的bean"></constructor-arg>
         </bean>

         ```
   
   `factory-bean`是指具体的工厂实例；`factory-method`指的是工厂类中的方法，方法中的参数写在`constructor-arg`中



10. 继承FactoryBean来创建对象

      FactoryBean是Spring规定的一个接口，当前接口的实现FactoryBean类时，Spring都会将其作为一个工厂，但是在ioc容器启动的时候不会创建实例，只有在使用的时候才会创建对象。

      - 创建自定义对象实现FactoryBean类

         ```java
         public class MyFactoryBean implements FactoryBean<Person> {
            /**
             * 返回获取的bean
            * @return
            * @throws Exception
            */
            @Override
            public Person getObject() throws Exception {
               Person person = new Person();
               person.setId(7);
               person.setName("继承FactoryBean创建对象");

               return person;
            }

            /**
             * 返回获取的bean的类型
            * @return
            */
            @Override
            public Class<?> getObjectType() {
               return Person.class;
            }

            /**
             * 判断当前bean是否是单例
            * @return
            */
            @Override
            public boolean isSingleton() {
               return false;
            }
         }

         ```
      - 在配置文件中配置此对象,即表示将自定义的FactoryBean交由spring的IoC容器管理

         ```xml
         <bean id="myFactoryBean" class="com.qiyixing.factory.MyFactoryBean"></bean>
         ```
   
      此方式是Spring创建对象的一种补充，用户可以按照需求创建对象，创建的对象交由Spring IoC进行管理，对象只有在被用到时才会被创建

11. 对象的初始化和销毁方法

    Spring在创建对象的时候可以指定具体的初始化和销毁方法,属性分别为`init-method`和`destory-method`

12. 配置bean对象初始化方法的前后处理方法

    Spring中包含一个BeanPostProcessor的接口，可以在bean的初始化方法的前后调用该方法，如果配置了初始化方法的潜质和后置处理器，无论是否包含初始化方法，都会进行调用

    - 编写前置/后置处理器业务代码

      ```java
      public class MyBeanPostProcessor implements BeanPostProcessor {
         /**
         * 初始化方法前置处理器
         * 在每一个对象的初始化方法前面执行
         * @param bean
         * @param beanName
         * @return
         * @throws BeansException
         */
         @Override
         public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
            System.out.println("postProcessBeforeInitialization: " + beanName);
            return bean;
         }

         /**
         * 初始化方法后置处理器
         * 在每一个对象的初始化方法后面执行
         * @param bean
         * @param beanName
         * @return
         * @throws BeansException
         */
         @Override
         public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
            System.out.println("postProcessAfterInitialization: " + beanName);
            return bean;
         }
      }

      ```
    - 配置xml文件，交由Spring容器管理

      ```xml
         <bean id="myBeanPostProcessor" class="com.qiyixing.factory.MyBeanPostProcessor"></bean>
      ```
   
   运行测试用例后可以看出，无论是否指定初始化方法，`postProcessBeforeInitialization`和`postProcessAfterInitialization`都会被执行，并且是在每个对象创建之后都会执行一次

## Spring创建第三方bean对象

Spring中，很多对象都是单例的，日常开发中经常需要使用某些外部的单实例对象，例如数据库连接池等，此时就需要在Spring中创建第三方Bean实例。

1. 导入数据库连接池的Pom文件

   在`pom.xml`文件中添加以下依赖

   ```xml
   <!-- https://mvnrepository.com/artifact/com.alibaba/druid -->
   <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>druid</artifactId>
      <version>1.1.21</version>
   </dependency>

   <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
   <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>5.1.48</version>
   </dependency>

   ```
2. 配置xml文件管理bean对象

   ```xml
   <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
      <property name="username" value="root"></property>
      <property name="password" value="root"></property>
      <property name="url" value="jdbc:mysql://localhost:3360/demo"></property>
      <property name="driverClassName" value="com.mysql.jdbc.Driver"></property>
   </bean>
   ```

3. 使用`context.getBean("dataSource", DruidDataSource.class)`获取bean对象

## Spring引入第三方配置文件

1. 新建properties文件 `db.properties`,在配置文件中写业务相关配置

   ```properties
   username=root
   password=root
   url=jdbc:mysql://localhost:3360/demo
   driverClassName=com.mysql.jdbc.Driver
   ```

2. 在ioc.xml文件中导入一些context命名空间

   `xmlns:context="http://www.springframework.org/schema/context"`

   ` http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context.xsd`

   完整配置文件：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
      <beans xmlns="http://www.springframework.org/schema/beans"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xmlns:context="http://www.springframework.org/schema/context"
            xsi:schemaLocation="http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans.xsd
            http://www.springframework.org/schema/context
            http://www.springframework.org/schema/context/spring-context.xsd
      ">
         <context:property-placeholder location="classpath:db.properties"></context:property-placeholder>
         <bean id="dataSource2" class="com.alibaba.druid.pool.DruidDataSource">
            <property name="username" value="${username}"></property>
            <property name="password" value="${password}"></property>
            <property name="url" value="${url}"></property>
            <property name="driverClassName" value="${driverClassName}"></property>
         </bean>
      </beans>
   ```
   Spring容器在进行启动的时候会读取当前系统的某些环境变量的配置，因此最好的方式是添加前缀来做区分，例如数据库中的username改为jdbc.username

## 基于xml文件自动装配

   Spring自动装配会把某些bean注入到另外的bean中，使用`autowire`属性实现，`autowire`属性取值：

   -  `default/no`不装配

   - `byName` 根据set方法后面首字母小写的名称装配
   
   - `byType` 按照bean的类型进行装配，但是如果有多个类型就会报错

   - `constructor` 按照构造器进行装配，先按照有参构造器参数的类型进行装配，没有就直接配null；如果按类型找到了多个，那么就是用参数名为id继续匹配，匹配不到就null

## 基于SpEL的使用

   SpEL： Spring Expression Language. Spring的表达式语言，支持运行时查询操作对象，使用`#{}`作为语法规则，所有的大括号中的字符都认为是SpEL

## Spring Ioc的注解应用

### 使用注解的方式将bean注册到spring IoC容器中

常用注解： `@Component` `@Controller` `@Service` `@Repository` 

这四个注解写在类上面的时候就能完成注册bean的功能，Spring并不会根据这些注解进行区分，而是直接扫描注册，这四个注解主要是为了在实际开发中区分开来以提高代码的可读性

-  `@Component`

   组件，理论上可以在任何类上添加，扫描时会完成注册

- `@Controller`

   放在控制层，用于接收用户的请求

- `@Service`

   放在业务逻辑层

- `@Repository`

   放在数据访问层

在使用注解的时候必须先告诉Spring应该从哪个包开始扫描，在配置文件中进行配置

```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
   http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
      
      <context:component-scan base-package="com.qiyixing"></context:component-scan>

   </beans>

```

在使用注解的时候没有定义id和class,需要把当前类的名称首字母小写作为识别。例如定义一个`PersonController`类，添加注解`@Controller`

```java
   @Controller
   public class PersonController {
   }

```

在测试用例中使用`context.getBean("personController", PersonController.class)`就能获取到对象，但如果getBean的名称不是personController则会报错`No bean named 'xxx' available`。如果需要改变名称，则需要在注解上添加value属性
即 `@Controller(value="xxx")`

组件默认情况下都是单例的，如果需要配置多例模式，可以在注解下添加`@Scope`注解

```java

   @Controller
   @Scope(value = "prototype")
   public class PersonController {
   }

```

### 定义扫描包时要包含的类和不包含的类

`<context:component-scan base-package="com.qiyixing"></context:component-scan>`这种写法只能定义需要扫描的包，如果想要跳过一些包的扫描，则需要使用属性`context:exclude-filter`

```xml

<context:component-scan base-package="com.qiyixing">
   <!-- 需要包含扫描的注解-->
   <context:include-filter type="" expression=""/>

   <!-- 需要排除扫描的注解-->
   <context:exclude-filter type="" expression=""/>
</context:component-scan>

```

type表示规则的类型，expression为表达式。type的可选值有： 

- assignable

   可以指定对应类的名称，但expression必须是完全限定名，不能写*这种通配符

- annotation

   注解，expression必须是注解的完全限定名

- regex

   正则表达式 一般不用

- aspectj

   使用切面的方式，一般不用

- custom

   使用自定义方式，自定义筛选规则，一般不用

### 自动装配的注解@Autowired和@Resource

#### @Autowired

`@Autowired` 自动注入的注解，默认情况下是按照byType来进行装配的
   
   - 如果只找到一个类型，直接赋值；

   - 如果没找到则抛出异常；

   - 如果找到多个类型一样的，则会按照id来进行查找，默认id是类名首字母小写(存在多个类型的时候不能乱取名字)

如果想要通过名字进行查找，可以规定自己的名称，使用注解`@Qualifier`

```java

   @Autowired
   @Qualifier("personService")
   private PersonService personService2;

```
Autowired一般放在属性上，还能别的地方。

当@Autowired放在方法上时，此方法在创建对象的时候会默认调用，方法中的参数会进行自动装配；

@Qualifier注解也可以定义在方法的参数列表中，可以指定当前属性的id名称

#### @Resource

使用@Resource可以完成与@Autowired相同的功能，但两者还有些区别：

- @Resource是JDK提供的功能，@Autowired是Spring提供的功能

- @Resource可以在其他框架中使用，@Autowired只能在Spring中提供

- @Resource扩展性好，@Autowired支持的框架比较单一

- @Resource是按照名称进行装配的，如果名字找不到就使用类型；@Autowired是按照类型进行装配，类型找不到就使用名字

### 泛型依赖注入

# Spring AOP

AOP Aspect Oriented Programming 面向切面编程

OOP Object Oriented Programming 面向对象编程

面向切面编程是基于OOP基础上的新的编程思维，OOP面向的主要对象是类，而AOP面向的主要时切面，在处理日志、安全管理、事务管理等方面有非常重要的作用。

AOP是Spring中重要的核心点，虽然IoC容器没有依赖AOP，但AOP提供了非常强大的功能，用来作IoC的补充。

通俗来说，AOP就是将某段代码动态切入到指定方法的指定位置进行运行的编程方式

Spring中使用两种动态代理方式，一种是JDK提供的，另一种是cglib
 
使用JDK提供的reflect包下的类要求每个类都要有实现的接口，但实际开发中并不能保证如此，因此需要换cglib的方式

Spring AOP 的底层原理是动态代理

切面： 关注点模块化。Spring SOP中，切面可以使用通用类基于模式方式或者在普通类中使用注解@AspectJ来实现

通知： 在切面的某个特定的连接点上执行的动作，很多AOP框架，包括Spring在内，都是以拦截器做通知模型的，并维护着一个以连接点为中心的拦截器链

      通知的注解有以下几种类型： 
      - @Before 前置通知，在方法执行前完成
      - @After 后置通知，在方法执行后完成
      - @AfterReturning 返回通知，在返回结果之后运行
      - @AfterThrowing 异常通知，出现异常的时候使用
      - @Around 环绕通知，

连接点： 每个方法中可以填入额外代码的地方

切入点： 切入点是连接点的子集，是直接切入代码的连接点。可以通过表达式来控制切入点

织入： 把切面连接到其他应用程序类型或对象上，并创建一个被通知的对象的过程

## AOP的使用

1. 导入依赖: `spring-aop`(可不导入，Spring-context中已集成此依赖) `cglib` `aspectJ` `aop alliance` `Spring Aspects`

   ```xml
   <!-- https://mvnrepository.com/artifact/org.springframework/spring-aop -->
   <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aop</artifactId>
      <version>5.2.3.RELEASE</version>
   </dependency>
   <!-- https://mvnrepository.com/artifact/cglib/cglib -->
   <dependency>
      <groupId>cglib</groupId>
      <artifactId>cglib</artifactId>
      <version>3.3.0</version>
   </dependency>
   <!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
   <dependency>
      <groupId>org.aspectj</groupId>
      <artifactId>aspectjweaver</artifactId>
      <version>1.9.5</version>
   </dependency>
   <!-- https://mvnrepository.com/artifact/aopalliance/aopalliance -->
   <dependency>
      <groupId>aopalliance</groupId>
      <artifactId>aopalliance</artifactId>
      <version>1.0</version>
   </dependency>
   <!-- https://mvnrepository.com/artifact/org.springframework/spring-aspects -->
   <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aspects</artifactId>
      <version>5.2.3.RELEASE</version>
   </dependency>


   ```

2. 编写配置

 - 将目标类和切面类加入到Ioc容器中，在对应的类上添加组件注解

   @Aspect 将类声明成切面类 @Component 将类交由Spring管理

   ```java 
   @Aspect
   @Component
   public class LogUtil {

      /**
      * @Before的后面固定写execution，execution里面写方法名的完全限定名
      */
      @Before("execution(public Integer com.qiyixing.service.MyCalculator.add(Integer, Integer))")
      public static void start() {
         System.out.println("方法开始执行");
      }

      @AfterReturning("execution(public Integer com.qiyixing.service.MyCalculator.add(Integer, Integer))")
      public static void stop() {
         System.out.println("方法结束执行" );
      }

      @AfterThrowing("execution(public Integer com.qiyixing.service.MyCalculator.add(Integer, Integer))")
      public static void logException() {
         System.out.println("方法抛出异常");
      }

      @After("execution(public Integer com.qiyixing.service.MyCalculator.add(Integer, Integer))")
      public static void logFinally() {
         System.out.println("方法执行结束： over");
      }
   }
   ```

   将服务注册到Spring Ioc 容器

   ```java
   @Service
   public class MyCalculator implements Calculator{
      public Integer add(Integer i, Integer j) {
         Integer result = i+j;
         return result;
      }
   }
   ```

   配置spring扫描包，配置AOP注解

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xmlns:aop="http://www.springframework.org/schema/aop"
         xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
   http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
   http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">

      <!-- 开启包的扫描 -->
      <context:component-scan base-package="com.qiyixing"></context:component-scan>

      <!-- 开启AOP注解 -->
      <aop:aspectj-autoproxy></aop:aspectj-autoproxy>
   </beans>
   ```

Spring AOP底层使用动态代理，使用时会判断当前对象是否有对应的接口，若有则使用JDK代理模式，没有接口则是cglib代理模式

早期JDK性能不如cglib，但由于JDK不断在更新，cglib没在更新，两者性能差不多

### 切入点的表达式

切入点的表达式使用完全限定名（如`@Before("execution(public Integer com.qiyixing.service.MyCalculator.add(Integer, Integer))")`）过于死板，实际开发中更多使用的是通配符的方式

- 通配符 `*` 
   1. 可以用来匹配一个或多个字符

      `execution(public Integer com.qiyixing.service.MyCalculator.*(Integer, Integer))`

      匹配MyCalculator类中所有的方法
   
   2. 可以用来匹配任意类型的参数

      `execution(public Integer com.qiyixing.service.MyCalculator.*(*, *))`
   
   3. *在进行匹配的时候只能匹配一层路径，不能匹配多层

   4. *不能用来匹配访问修饰符，如果不确定访问修饰符可以不写

       `execution(Integer com.qiyixing.service.MyCalculator.*(*, *))`

   5. 返回值可以使用*来匹配

       `execution(* com.qiyixing.service.MyCalculator.*(*, *))`
   
- 通配符`..`

   1. 可以用来匹配多个参数，任意类型

      `execution(* com.qiyixing.service.MyCalculator.*(..))`

   2. 可以匹配多层路径

      `execution(* com.qiyixing.service..*(..))`

表达式最偷懒的方式就是写成`* *(..)`,表达式以`*`开头能代表所有

使用通配符不是越简洁越好，更多的是要符合要求或者符合项目规则的匹配方式

- 逻辑运算`&&`(与) `||`(或) `!`(非)

   `execution(* com.qiyixing.service.MyCalculator.*(..)) && execution(* *(..))`

   同时满足两种表达式

   `execution(* com.qiyixing.service.MyCalculator.*(..)) || execution(* *(..))`

   两种表达式满足一种就行

    `execution(* com.qiyixing.service.MyCalculator.*(..)) || execution(* *(..))`

通知的执行顺序：

   正常执行： @Before --> @After --> @AfterReturning

   发生异常： @Before --> @After --> @AfterThrowing
   
如果要在方法中获取对应的参数或者方法名称等信息，必须使用JoinPoint对象，且此参数必须是第一个。

   ```java 
   public static void start(JoinPoint joinPoint) {
      Signature signature = joinPoint.getSignature();// 获取方法签名
      Object[] args = joinPoint.getArgs();// 获取参数信息


      System.out.println("方法开始执行.方法签名：" + signature + ";方法参数："+ args);
   }
   ```

如果方法中有返回值，那么必须要在注解中添加Returning="xxx"，这个xxx必须要和参数列表中的参数名称保持一致

   ```java
   @AfterReturning(value = "execution(public Integer com.qiyixing.service.MyCalculator.add(Integer, Integer))",returning = "result")
    public static void stop(JoinPoint joinPoint, Object result) {
        System.out.println("方法结束执行" + result);
    }
   ```
如果需要添加异常信息，注解中需要添加throwing="xxx",xxx必须和参数列表中的名称保持一致

   ```java
   @AfterThrowing(value = "execution(public Integer com.qiyixing.service.MyCalculator.add(Integer, Integer))", throwing = "e")
    public static void logException(JoinPoint joinPoint, Throwable e) {
        System.out.println("方法抛出异常" + e.getMessage());
    }
   ```

通知方法在定义时，对于访问修饰符 类型都没有明确要求，但是参数不能随便添加


若多个匹配的表达式相同，则可以将表达式抽象出来

   先定义一个无返回值的空方法，将此空方法添加注释@PointCut,填入表达式

   ```java
   @Pointcut("execution(public Integer com.qiyixing.service.MyCalculator.add(Integer, Integer))")
    public void myPointCut(){};
   ```

   使用时可直接调用空方法

   ```java
   @Before(value = "myPointCut()")
    public static void start(JoinPoint joinPoint) {
        Signature signature = joinPoint.getSignature();// 获取方法签名
        Object[] args = joinPoint.getArgs();// 获取参数信息


        System.out.println("方法开始执行.方法签名：" + signature + ";方法参数："+ args);
    }

   ```

### Around通知

环绕通知`@Around`,执行时优先于普通通知

正常结束执行顺序： 

环绕前置通知 --> @Before --> 环绕后置通知 --> 环绕返回通知 --> @After --> @AfterReturning

发生异常的执行顺序：

环绕前置通知 --> @Before --> 环绕异常通知 --> 环绕返回通知 --> @After --> @AfterThrowing

如果环绕通知中捕获了异常，那么在普通通知中无法接收到的，如果想要普通通知接收异常，则不能捕获异常只能抛出

   ```java

    @Around(value = "myPointCut()")
    public Object around(ProceedingJoinPoint pjp) {
      Signature signature = pjp.getSignature();
      Object[] args = pjp.getArgs();
      Object result = null;

      try {
         // 通过反射的方式调用目标方法，相当于执行method.invoke()
         result = pjp.proceed(args);
      } catch (Throwable throwable) {
         throwable.printStackTrace();
      }finally {
      }

      return result;
   }
   ```

### 多个切面类执行顺序

   当应用程序中包含多个切面类时，默认的执行顺序是按照切面类的类名首字母进行排序，按照字典序

   如果要指定执行顺序，需要在切面类上添加注释`@Order()` 例如`@Order(100)` 比 `@Order(200)`先执行

### 使用配置文件配置AOP

1. 创建xml文件，导入aop命名空间

2. 配置bean，扫描切面

3. 配置切面

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xmlns:aop="http://www.springframework.org/schema/aop"
         xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
   http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
   http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">

      <bean id="logUtil" class="com.qiyixing.utils.LogUtil"></bean>
      <bean id="myCalculator" class="com.qiyixing.service.MyCalculator"></bean>

      <aop:config>
         <aop:aspect ref="logUtil">
               <aop:before method="start" pointcut="execution(public Integer com.qiyixing.service.MyCalculator.*(..))"></aop:before>

               <aop:after method="logFinally" pointcut="execution(public Integer com.qiyixing.service.MyCalculator.*(..))"></aop:after>

               <aop:after-returning method="stop" pointcut="execution(public Integer com.qiyixing.service.MyCalculator.*(..))"
               returning="result"></aop:after-returning>

               <aop:after-throwing method="logException" pointcut="execution(public Integer com.qiyixing.service.MyCalculator.*(..))"
               throwing="e"></aop:after-throwing>

               <aop:around method="around" pointcut="execution(public Integer com.qiyixing.service.MyCalculator.*(..))"></aop:around>
         </aop:aspect>
      </aop:config>
   </beans>
   ```

配置文件也能将表达式抽取出来：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xmlns:aop="http://www.springframework.org/schema/aop"
         xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
   http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
   http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">

      <bean id="logUtil" class="com.qiyixing.utils.LogUtil"></bean>
      <bean id="myCalculator" class="com.qiyixing.service.MyCalculator"></bean>

      <aop:config>
         <aop:aspect ref="logUtil">
               <aop:pointcut id="myPointcut" expression="execution(public Integer com.qiyixing.service.MyCalculator.*(..))"/>
               
               <aop:before method="start" pointcut-ref="myPointcut"></aop:before>

               <aop:after method="logFinally" pointcut-ref="myPointcut"></aop:after>

               <aop:after-returning method="stop" pointcut-ref="myPointcut" returning="result"></aop:after-returning>

               <aop:after-throwing method="logException" pointcut-ref="myPointcut" throwing="e"></aop:after-throwing>

               <aop:around method="around" pointcut-ref="myPointcut"></aop:around>
         </aop:aspect>
      </aop:config>
   </beans>
   ```

也可以将表达式抽取到最外层，这样多个切面都能用

   ```xml
   <aop:config>
      <aop:pointcut id="globalPointcut" expression="execution(public Integer com.qiyixing.service.MyCalculator.*(..))"/>

      <aop:aspect ref="aaa"></aop:aspect>
      <aop:aspect ref="bbb"></aop:aspect>
   </aop:config>
   ```


## 声明式事务和传播特性
