---
layout: "post"
title: "数据库"
date: "2020-10-25 21:06"
categories: Database
tags: [Computer Language, Database]
---

# 数据库表的创建、表的约束、索引、数据库

## 创建表

### 标准的建表语法

数据库连接池： `C3P0` `DBCP` `druid`

`CREATE TABLE[schema.]table(column datatype [DEFAULT])` 

例如：

建立一张用来存储学生信息的表，表中的字段包含学生的学号、姓名、年龄、入学日期、年纪、班级、email等信息，且为grade指定默认值为1

- 创建
  
  `create table student (sty_id number(10), name varcher2(20), age number(3), hiredate date,grade varchar2(10) default 1, classes varchar2(10), email varchar2(50))`

- 插入

  - `insert into student values(20201025, 'zhangshan', 22, to_date('2020-10-25', 'YYYY-MM-DD'), '2', '1', '123@xx.com')`

  - `insert into student(sty_id, name, age, hiredate,classes,email) values(20201025, 'zhangshan', 22, to_date('2020-10-25', 'YYYY-MM-DD'), '1', '123@xx.com')`


注意事项： 

- 创建新表时，指定的表名必须不存在，否则报错
- 使用默认值时，当插入行不给出值，dbms将自动采用默认值
- 使用create语句创建基本表时，最初只是一个空的框架，用户可以使用insert命令将数据插入表中，即只包含表结构不包含表数据

**正规的表结构设计需要使用第三方工具**

- 修改表
  
  例如： 在上述`student`表中添加字段`address`

  `alter table student add address varchar2(100)`

  注： 新增加的列不能设置为 `not null`，基本表在增加一列后，原有元组在新增加的列上的值都定义为空值

- 删除表字段
  
  `alter table 表名 drop column 列名`

  `alter table student drop column address`

- 修改表字段类型

  `alter table 表名 modify(字段 字段类型);`

  `alter table student modify(email varchar2(100));`

- 删除表
  
  `drop table 表名`

  多表关联时不能随意删除，需要使用
  
    - 级联删除`cascade`: 如果表A和表B，A中的某一个字段与B中的某一个字段做关联，那么删除A表的时候，需要先将B表删除

    - `set null`删除时，把表的关联字段设置为空

    - `restrict`，只有当依赖表中没有一个外键值与要删除的主表中主键值相对应时，才可执行删除操作

- 修改表名称
  
  `rename 原表名 to 新表名;`

  `rename student to stu;`

## 约束

创建表时同时可以指定所插入数据的一些规则，比如说某个字段不能为空，某个字段你的值不能小于0等，这些规则统称为约束。约束是在表上强制执行的**数据校验规则**

Oracle支持以下五类完整型约束：

- NOT NULL 非空，插入数据时，指定列不允许为空
- UNIQUE Key 唯一键， 可以限定某一列的值唯一，唯一键的列一般被用作索引列
- PRIMARY KEY 主键， 非空且唯一，任何一张表一般情况下最好有主键用来唯一的标识一行记录
- FOREIGN KEY 外键，多个表之间有关联关系(一个表的某个列的值依赖于另一张表的某个值)时，需要使用外键
  
  - 外键是表中的一个列，其值必须在另一表的主键或者唯一键中列出
  - 作为“主键”的表称为“主表”，作为外键的关系称为“依赖表”
  - 外键参照的是主表的主键或者唯一键
  - 对于主表的删除和修改主键值的操作，回怼依赖关系产生影响，如要删除主表的某个记录（即删除一个主键值），那么对依赖的影响可采取`RESTRICT方式`、`CASCADE方式`、`SET NULL方式`

  插入DEPT表中的DEPTNO列作为外键
  `create table student (sty_id number(10), name varcher2(20), age number(3), hiredate date,grade varchar2(10) default 1, classes varchar2(10), email varchar2(50)), foreign key [DEPTNO] references DEPT[DEPTNO]`

- CHECK 自定义检查约束，可以根据用户自己的需求去限定某些列的值
  
  例如： 限制0<年龄<150

     `create table student (sty_id number(10), name varcher2(20), age number(3) check(age > 0 and age < 150), hiredate date,grade varchar2(10) default 1, classes varchar2(10), email varchar2(50))`

## 索引

- 索引是为了加快对数据的搜索速度而设立的。索引是方案(schema)中的一个数据库对象，与表独立存放
- 索引的作用： 在数据库中用来加速对表的查询，通过使用快速路径访问方法快读定位数据，减少了磁盘的I/O
- sql中的索引是非显示索引，也就是在索引创建之后，在用户撤销它之前不会再用到该索引的名字，但是索引在用户查询时会自动起作用
- 索引的创建有两种情况
  
  - 自动： 当在表上定义一个`primary key` 或者 `unique 约束条件`时，Oracle数据库自动创建一个对应的唯一索引
  - 手动： 用户可以创建索引以加速查询
  
### 开发使用索引的要点

1. 索引改善检索操作的性能，但降低数据插入、修改和删除的性能。在执行这些操作时，DBMS必须动态地更新索引
2. 索引数据可能要占用大量的存储空间
3. 并非所有数据都适合于索引。唯一性不好的数据（如省）从索引得到的好处不比具有股鞥多可能值的数据（如姓名）从索引中得到的好处多
4. 索引用于数据过滤和数据排序。如果你经常以某种特定的顺序排序数据，则该数据可能是索引的备选
5. 可以在索引中定义多个列（例如省+市），这样的索引只在省+市的顺序排序时游泳。如果想按城市排序，则这种索引没用

### 索引的操作

- 创建
  
  `create index 索引名称 on 表名(列名1[,列名2]...);`

- 删除
  
  `drop index 索引名`

# 数据库设计三范式

在设计和数据库有关的系统时，数据库表的设计至关重要，这些设计关系整个系统的架构，需要精心的仔细考虑。数据库的设计主要包含了设计表结构和表之间的联系，在设计的过程中，有一些规则应该遵守

**三范式的存在是为了减少数据库中的数据冗余**

## 第一范式(1NF)： 确保每列保持原子性

第一范式是最基本的范式，如果数据库表中的所有字段值都是不可分解的原子值，就说明该数据库表满足了第一范式

第一范式的合理遵循需要根据系统的实际需求来定。比如某些数据库系统中需要用到“地址”这个属性，本来直接将“地址”属性设计成一个数据库表的字段就行，但是如果系统经常会访问“地址”属性中的“城市”部分，那么就非要将“地址”这个属性重新拆分为省份、城市、详细地址等多个部分进行存储，这样在对“地址”中某一部分操作的时候将非常方便，这样设计才满足了数据库的第一范式。

所谓的第一范式是指数据库表的每一列都是不可分割的基本数据项，同一列中不能有多个值，即**列不可分**

## 第二范式(2NF)： 确保表中的每列都和主键相关

第二范式在第一范式的基础之上更进一层。第二范式需要确保数据库表中的每一列都和主键相关，而不能只与主键的某一部分相关（主要针对联合主键而言）。在一个数据库表中，一个表中只能保存一种数据，不可以把多种数据保存在同一张数据库表中。

## 第三范式(3NF): 必须先满足第二范式

第三范式要求在一个数据库表中不包含已在其他表中已包含的非主关键字信息。

例如： 存在一个部门信息表，其中每个部门有部门编号(dep_id)、部门名称、部门简介等信息，那么在员工信息表中列出部门编号后就不能再将部门名称、部门简介等与部门先关的信息加入员工信息表中。如果不存在部门信息表，则根据第三范式，应该创建部门信息表，否则会有大量的数据冗余。

第三范式就是属性不依赖于其他非主属性

第三范式需要确保数据表中的每一列数据都和主键直接相关，而不能间接相关

# DBUtil及数据库连接池

## DBUtil

Commons DbUtils: JDBC Utility Component

Apache封装的JDBC工具组件

## 数据库连接池
 
数据库连接池的目的是为了减少频繁开关连接的时间，提高整个系统的响应能力，数据库连接池应该具备几个属性值：

1. 初始大小
2. 每次扩容的大小
3. 连接池的最大个数
4. 空闲连接的死亡时间
   
各种数据库连接池：

- DBCP
- C3P0
- Druid
- hikariCP
  
### `DBCP`

Apache提供的数据库连接池，目前用的比较少

### `C3P0`

开源的数据库连接池

1. 下载Jar包并导入项目中

2. 使用步骤
   
   ```java

  import com.mchange.v2.c3p0.*;
    
  ...
  // 加载mysql驱动
  ComboPooledDataSource cpds = new ComboPooledDataSource();
  cpds.setDriverClass( "com.mysql.jdbc.Driver" );

  // 设置URL、用户名、密码         
  cpds.setJdbcUrl( "jdbc:postgresql://localhost/testdb" );
  cpds.setUser("dbuser"); 
  cpds.setPassword("dbpassword");   
   ```

   `c3p0`若要通过配置文件进行参数配置，则配置文件必须放置在根目录，且文件名为`c3p0.properties`(properties文件)或`c3p0-config.xml`(xml文件)

**JDBC4之前是必须要填写驱动名称的，但是之后的版本不需要填写**

### `druid`

### `hikariCP`

配置参见官方文档