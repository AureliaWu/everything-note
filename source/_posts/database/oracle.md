---
layout: "post"
title: "Oracle数据库"
date: "2019-7-24 13:31:43"
categories: Database, Oracle
tags: [Computer Language, Database, Oracle]
---

# Oracle的安装

## 数据库和数据仓库

数据库： 对数据进行持久化存储，将数据直接存储到磁盘

- 关系型数据库： 

  - Mysql(最常用)

  - Oracle(最安全)

  - QLserver(.net)

  - Db2(金融、银行)


# 创建表空间

1. 登录：sqlplus / as sysdba
2. 创建表空间：`create tablespace aezocn datafile 'd:/tablespace/aezo' size 800m extent management local segment space management auto;` ，需要先建好路径 `d:/tablespace` ，最终会在该目录下建一个 AEZO 的文件(表空间之后可以修改)

    - 删除表空间：`drop tablespace aezocn including contents and datafiles;`
3. 创建用户：`create user aezo identified by aezo default tablespace aezocn;`
4. 授权
  -  `grant create session to aezo;`
  - `grant unlimited tablespace to aezo;`
  -  `grant dba to aezo;` 导入导出时，只有dba权限的账户才能导入由dba账户导出的数据，因此不建议直接设置用户为dba

# 导入导出

`.dmp`适合大数据导出，`.sql`适合小数据导出(表中含有CLOB类型字段则不能导出)

## 命令行 ^4

-  输入 `imp/exp` 用户名/密码 可根据提示导入导出。直接`cmd`运行。
- 成功提示 `Export terminated successfully [with/without warnings]`；失败提示 `Export terminated unsuccessfully [with/without warnings]`

## dmp格式导出导入(cmd)

### 导出

#### 用户模式
- `exp system/manager file=d:/exp.dmp owner=scott` 导出scott用户的所有对象，前提是system有相关权限

- 远程导出：此时`system/manager`默认连接的是本地数据库。如果使用`exp system/manager@remote_orcl file=d:/exp.dmp owner=scott` (`remote_orcl`为在本地建立的远程数据库网络服务名. 即tnsnames.ora里面的配置项名称)则可导出远程数据库的相关数据，下同。或者`system/manager@192.168.1.1:1521/orcl`
  - 加上 `compress=y` 表示压缩数据
  - 加上 `rows=n` 表示不导出数据行，只导出结构

#### 表模式 
- `exp scott/tiger file=d:/exp.dmp tables=emp` 导出`scott`的`emp`表
  - 导出其他用户的表：`exp system/manager file=d:/exp.dmp tables=scott.emp`, `scott.dept` 导出`scott`的`emp`、`dept`表，用户`system`需要相关权限
  - 导出部分表数据：`exp scott/tiger file=d:/exp.dmp tables=emp query=\" where ename like '%AR%'\"`

  - 常见错误(EXP-00011)：原因为11g默认创建一个表时不分配segment，只有在插入数据时才会产生。

- 导出全部：`exp system/manager file=d:/exp.dmp full=y`
  - 用户 `system/manager` 必须具有相关权限
  - 导出的是整个数据库，包括所有的表空间

### 导入

####  用户模式：
- `imp system/manager file=d:/exp.dmp fromuser=scott touser=aezo ignore=y`
  - `ignore=y`忽略创建错误, 不少情况下要先将表彻底删除，然后导入

#### 表模式
- `imp system/manager file=d:/exp.dmp fromuser=scott tables=emp, dept touser=aezo ignore=y`
  - 将`scott`的表`emp`、``dept导入到用户`aezo`
  - 此处 `file/fromuser/touser` 都可以指定多个

- 导入全部：`imp system/manager file=d:/exp.dmp full=y ignore=y`
  - 用户 `system/manager` 必须具有相关权限
  - 导入的是整个数据库，包括所有的表空间

# Oracle报错记录

## EXP-00011

`EXP-00011: XXX does not exist`

- 报错内容： 表XXX不存在
- 报错场景： 直接用命令行导出单张表时，执行命令 `exp user/psw file=d:/exp.dmp tables=emp;` 提示表`emp`不存在，而实际查询时此表存在且有数据
- 报错原因之一：`exp`执行语句多加了一个'`;`' 网上还有记录其它原因，但实际只遇到的是多加了分号，所以暂不记他人的情况
- 解决方案： 将命令中的分号去掉就好啦

## ORA-01940

`ORA-01940: cannot drop a user that is currently connected`

- 报错内容： 无法删除当前已连接用户
- 报错场景： 执行`drop user`时出现此报错
- 报错原因： 有用户在连接，无法执行`drop`
- 解决方案： 
  - 锁定用户: `alter user XXX account lock;`
  - 查询进程号: `SELECT * FROM V$SESSION WHERE USERNAME='xxx';`
  - 删除对应的进程: `alter system kill session 'xx,xx';`
  - 删除对应用户: `drop user xx cascade;`

# Oracle sql语句

## 将查询结果存入新表

`create table 临时表名 as select * from table_name `

  - `select * from table_name`表示得到查询结果的查询语句
  - 此方法无需先创建表设置字段，而是会将查询结果的字段和字段类型直接赋予新表
  - 此方法创建的不属于临时表，可以根据需求作为缓存表，用完可以删除

# 存储过程

## 使用plsql创建存储过程

1. plsql --> Objects --> Procedures 右键--> 新建 --> 弹出框中输入存储过程的名字

2. 书写存储过程逻辑，以下为清理作废数据的存储过程

```sql
create or replace procedure clear_ycama_lock_data is
cursor c is select t.id from ycama_box_lock t where t.yes_status in (0,3);
type tb_records is table of c%rowtype;
rd_records tb_records;
begin
  open c;
  loop
    fetch c bulk collect into rd_records limit 500;
    forall i in 1..rd_records.count
     delete from ycama_box_lock c where c.id = rd_records(i).id;
    commit;
    exit when c%notfound;
  end loop;
  close c;
end clear_ycama_lock_data;

```

3. 直接执行存储过程，执行完成后，在Procedures底下会出现此存储过程

4. 调用存储过程： 在sql窗口输入以下命令后运行：

  ```sql
  begin
    CLEAR_YCAMA_LOCK_DATA(); // 此处为存储过程的名称，注意最后的分号;不能省略
  end;
  ```


---

参考文章

http://blog.aezo.cn/2016/10/12/db/oracle-dba/  (aezo blog)