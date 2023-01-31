---
title: MySQL
copyright_url: https://www.aobayu.cn/2022/09/23/MySQL/
tags: 
    - MySQL
categories: 学习之路
date: 2022-9-23
keywords: MySQL
description: MySQL是一个关系型数据库管理系统，由瑞典MySQL AB 公司开发，属于 Oracle 旗下产品。MySQL 是最流行的关系型数据库管理系统之一，在 WEB 应用方面，MySQL是最好的RDBMS应用软件之一。--本文为自己学习中所写，主要为MySQL详解！
---

## 数据库相关概念

**数据库**: 存储数据的仓库，数据是有组织的进行存储,英文：DataBase，简称 DB

- 存储和管理数据的仓库 

- 其本质是一个文件系统, 还是以文件的方式,将数据保存在电脑上

| 存储方 | 优点                                                         | 缺点                                           |
| ------ | ------------------------------------------------------------ | ---------------------------------------------- |
| 内存   | 速度快                                                       | 不能够永久保存,数据是临时状态的                |
| 文件   | 数据是可以永久保存的                                         | 使用IO流操作文件,不方便                        |
| 数据库 | 1.数据可以永久保存<br>2.方便存储和管理数据<br>3.使用统一的方式操作数据库 | 占用资源,有些数据库需要付费(比如Oracle数据库） |

**数据库管理系统：**管理数据库的大型软件英文：DataBase Management System，简称 DBMS，指一种操作和管理维护数据库的大型软件。

MySQL就是一个 数据库管理系统软件, 安装了Mysql的电脑,我们叫它数据库服务器

**数据库管理系统的作用**

用于建立、使用和维护数据库，对数据库进行统一的管理

**SQL**英文：Structured Query Language，简称 SQL，结构化查询语言

是一种特殊目的的编程语言，是一种数据库 查询和程序设计语言，用于存取数据以及查询、更新和管理关系数据库系统。

**常见的关系型数据库管理系统:**

- **Oracle**：收费的大型数据库，Oracle 公司的产品 ---->甲骨文  银行Oracle 
- **MySQL**： 开源免费的中小型数据库。后来 Sun 公司收购了 MySQL，而 Sun 公司又被 Oracle 收购  java
- **SQL Server**：MicroSoft 公司收费的中型的数据库。C#、.net 等语言常使用
- **PostgreSQL**：开源免费中小型的数据库 定位
- **DB2**：IBM 公司的大型收费数据库产品 
- **SQLite**：嵌入式的微型数据库。如：作为 Android 内置数据库  
- **MariaDB**：开源免费中小型的数据库--mysql 的一个分支

## SQL 

**SQL 简介**

- 英文：Structured Query Language，简称 SQL

- 结构化查询语言，一门操作关系型数据库的编程语言

- 定义操作所有关系型数据库的统一标准

- 对于同一个需求，每一种数据库操作的方式可能会存在一些不一样的地方，我们称为“方言”

**通用语法**

- SQL语句可以单行 或者 多行书写，以分号 结尾 ; 
- 可以使用空格和缩进来增加语句的可读性。
- MySql中使用SQL不区分大小写，一般关键字大写，数据库名 表名列名 小写。 
- 注释方式

| 注释语法 | 说明                        |
| :------- | --------------------------- |
| #        | Mysql特有的单行注释(不建议) |
| /**/     | 多行注释                    |
| -- 空格  | 单行注释                    |

**SQL分类**

| 分类         | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| 数据定义语言 | 简称DDL(Data Definition Language)，用来定义数据库对象:数据库，表，列 |
| 数据操作语言 | 简称DML(Data Manipulation Language)，用来对数据库中表的记录进行更新。 |
| 数据查询语言 | 简称DQL(Data Query Language)，用来查询数据库中表的记录。     |
| 数据查询语言 | 简称DCL(Data Control Language)，用来定义数据库的访问权限和安全级别，<br>及创建用户。(了解) |

## MySQL 数据库

**关系型数据库：**

> 关系型数据库是建立在关系模型基础上的数据库，简单说，关系型数据库是由多张能互相连接的 二维表组成的数据库

**关系型数据库的优点**：

- 都是使用表结构，格式一致，易于维护。

- 使用通用的 SQL 语言操作，使用方便，可用于复杂查询。

- 关系型数据库都可以通过SQL进行操作，所以使用方便。

- 数据存储在磁盘中，安全。

**数据模型：**

![数据模型](https://image.aobayu.cn/images/mysql.png)

创建一个数据库，会在本地文件夹生成.frm 表文件 和 .MYD 数据文件，在安装目录下的 data文件下

```sql
mysql> create database db1;
```

- MySQL中可以创建多个数据库，每个数据库对应到磁盘上的一个文件夹

- 在每个数据库中可以创建多个表，每张都对应到磁盘上一个 frm 文件

- 每张表可以存储多条数据，数据会被存储到磁盘中  MYD 文件中

## 数据定义语言DDL

### DDL:操作数据库

| 命令                                        | 说明                                               |
| ------------------------------------------- | -------------------------------------------------- |
| create database数据库名;                    | 创建指定名称的数据库。                             |
| create database数据库名character set字符集; | 创建指定名称的数据库，并且指定字符集（一般都utf-8) |
| use数据库                                   | 切换数据库                                         |
| select database();                          | 查看当前正在使用的数据库                           |
| show databases;                             | 查看Mysql中都有哪些数据库                          |
| show create database 数据库名;              | 查看一个数据库的定义信息                           |
| alter database数据库名character set字符集;  | 数据库的字符集修改操作                             |
| drop database 数据库名                      | 从MySql中永久的删除某个数据库                      |

```sql
net start mysql -- 启动mysql
mysql -uroot -p123456-- 连接数据库
mysql> --成功进入mysql 
update mysq1.user set authentication_string=password('123456') where user='root' and Host ='localhost';-- 修改root用户密码
flush privileges;--刷新权限

show databases;--查看所有的数据库
use schoo1--切换数据库use数据库名
-- tab键的上面,如果你的表名或者字段名是一个特殊字符，就需要带` `
use `schoo1`

show tables; --查看数据库中所有的表
describe student; --显示数据库中所有的表的信息

create database westos; --创建一个数据库
CREATE database if not exists westos;--为了避免错误IF NOT EXISTS
DROP DATABASE westos;-- 删除某个数据库
DROP DATABASE IF EXISTS westos;-- 删除某个数据库 为了避免错误IF EXISTS

exit--退出连接
net stop mysql -- 关闭mysql
```

### DDL:操作表

操作表也就是对表进行增（Create）删（Retrieve）改（Update）查（Delete）。

> 查询当前数据库下所有表名称

```sql
SHOW TABLES;
```

> 查询表结构

```sql
DESC 表名称;
```

> 创建表

```java
CREATE TABLE 表名(
    字段名称1 字段类型(长度),
    字段名称2 字段类型(长度) /*注意 最后一列不要加逗号*/
);
```

**常见数据类型**

| 整型    | 描述                                               |
| ------- | -------------------------------------------------- |
| int     | 整型                                               |
| double  | 浮点型                                             |
| varchar | 字符串型                                           |
| date    | 日期类型，给是为yyyy-MM-dd ,只有年月日，没有时分秒 |

注意：MySQL中的 char类型与 varchar类型，都对应了 Java中的字符串类型，

**区别在于：** 

char类型是固定长度的： 根据定义的字符串长度分配足够的空间。

varchar类型是可变长度的： 只使用字符串长度所需的空间 

**适用场景：** char类型适合存储 固定长度的字符串，比如 密码，性别一类，varchar类型适合存储 在一定范围内，有长度变化的字符串 

> 创建测试表 

```sql
--切换到数据库
USE db1;
-- 创建表
CREATE TABLE test1(
    cid INT,
    cname VARCHAR(20)
);
```

> 快速创建一个表结构相同的表（复制表结构）

```sql
create table 新表名 like 旧表名
```

```sql
-- 创建一个表结构与 test1 相同的 test2表
CREATE TABLE test2 LIKE test1;
-- 查看表结构
DESC test2;
-- 查看创建表的SQL语句
SHOW CREATE TABLE category;
```

> 删除表

| 命令                      | 说明                                              |
| ------------------------- | ------------------------------------------------- |
| drop table表名;           | 删除表（从数据库中永久删除某一张表)               |
| drop table if exists表名; | 判断表是否存在，存在的话就删除,不存在就不执行删除 |

```sql
-- 直接删除test1表
DROP TABLE test1;
-- 先判断再删除test2表
DROP TABLE IF EXISTS test2;
```

> 修改表名 

```sql
rename table 旧表名 to 新表名
```

> 修改表的字符集 

```sql
alter table 表名 character set 字符集
```

> 向表中添加列， 关键字 ADD 

```sql
alert table 表名 add 字段名称 字段类型
```

> 修改表中列的 数据类型或长度 ， 关键字 MODIFY 

```sql
alter table 表名 modify 字段名称 字段类型
```

> 修改列名称 , 关键字 CHANGE

```sql
alter table 表名 change 旧列名 新列名 类型(长度);
```

> 删除列 ，关键字 DROP

```sql
alter table 表名 drop 列名;
```

## 数据操作语言DML

DML主要是对数据进行增（insert）删（delete）改（update）操作。

### 添加数据

```sql
insert into 表名 （字段名1，字段名2...） values(字段值1，字段值2...);
```

```sql
/*表名：student 表中字段：
学员 ID,sid int,
姓名 sname varchar(20),
年龄 age int,
性别 sex char(1),
地址 address varchar(40)  */
# 创建学生表
CREATE TABLE student(
    sid INT,
    sname VARCHAR(20),
    age INT,
    sex CHAR(1),
    address VARCHAR(40)
);
```

> 向学生表中添加数据，3种方式

```sql
-- 插入全部字段， 将所有字段名都写出来
INSERT INTO student (sid,sname,age,sex,address)
VALUES(1,'孙悟空',20,'男','花果山');
```

```sql
-- 插入全部字段，不写字段名 
INSERT INTO student VALUES(2,'孙悟饭',10,'男','地球');
```

```sql
-- 插入指定字段的值 
INSERT INTO category (cname) VALUES('白骨精');
```

> 批量添加数据

```sql
INSERT INTO 表名(列名1,列名2,…) VALUES(值1,值2,…),(值1,值2,…),(值1,值2,…)…;
INSERT INTO 表名 VALUES(值1,值2,…),(值1,值2,…),(值1,值2,…)…;
```

```sql
INSERT INTO student VALUES
(2,'孙悟饭',10,'男','地球'),
(3,'孙悟饭1',10,'男','地球');
```

### 修改数据

> 不带条件的修改 

```sql
update 表名 set 列名 = 值
```

> 带条件的修改 

```sql
update 表名 set 列名 = 值 [where 条件表达式：字段名 = 值 ]
```

```sql
-- 一次修改多个列，将sid为 2 的学员，年龄改为 20，地址改为 北京
UPDATE student SET age = 20,address = '北京' WHERE sid = 2;
```

### 删除数据

```sql
DELETE FROM 表名 [WHERE 条件];
```

> 删除 sid 为 1 的数据 

```sql
DELETE FROM student WHERE sid = 1;
```

> 删除所有数据

```sql
DELETE FROM student;
truncate table student;
```

如果要删除表中的所有数据,有两种做法:

delete from 表名; 不推荐. 有多少条记录 就执行多少次删除操作. 效率低 

truncate table 表名: 推荐. 先删除整张表, 然后再重新创建一张一模一样的表. 效率高 

## 数据查询语言DQL

### 查询表中数据

```sql
-- 查询语法
SELECT 字段列表(想要查询的字段)
FROM 表名列表（来源表）
WHERE 条件列表 
GROUP BY 分组字段
HAVING 分组后条件
ORDER BY 排序字段
LIMIT 分页限定
```

> 准备初试数据

```sql
use school;
# 删除emp表
drop table if exists emp;
# 创建员工表
CREATE TABLE emp
(
    eid       INT,
    ename     VARCHAR(20),
    sex       CHAR(1),
    salary    DOUBLE,
    hire_date DATE,
    dept_name VARCHAR(20)
);
# 添加数据
INSERT INTO emp
VALUES (1, '孙悟空', '男', 7200, '2013-02-04', '教学部');
INSERT INTO emp
VALUES (2, '猪八戒', '男', 3600, '2010-12-02', '教学部');
INSERT INTO emp
VALUES (3, '唐僧', '男', 9000, '2022-09-08', '教学部');
INSERT INTO emp
VALUES (4, '白骨精', '女', 5000, '2022-10-07', '市场部');
INSERT INTO emp
VALUES (5, '蜘蛛精', '女', 5000, '2022-09-14', '市场部');
INSERT INTO emp
VALUES (6, '玉兔精', '女', 200, '2022-03-14', '市场部');
INSERT INTO emp
VALUES (7, '林黛玉', '女', 10000, '2019-10-07', '财务部');
INSERT INTO emp
VALUES (8, '黄蓉', '女', 3500, '2022-09-14', '财务部');
INSERT INTO emp
VALUES (9, '吴承恩', '男', 20000, '2022-03-14', NULL);
INSERT INTO emp
VALUES (10, '孙悟饭', '男', 10, '2020-03-14', '财务部');
INSERT INTO emp
VALUES (11, '兔八哥', '女', 300, '2022-03-14', '财务部');
```

### 简单查询

```sql
-- 查询多个字段
SELECT 字段列表 FROM 表名;
SELECT * FROM 表名;-- 查询所有数据
-- 去除重复记录
SELECT DISTINCT 字段列表 FROM 表名;
--起别名
AS: AS --也可以省略
```

```sql
-- 查询emp中的 所有数据 
SELECT * FROM emp;-- 使用 * 表示所有列
-- 查询emp表中的所有记录，仅显示id和name字段
SELECT eid,ename FROM emp;
-- 将所有的员工信息查询出来，并将列名改为中文
# 使用 AS关键字,为列起别名
SELECT  
eid AS '编号',
ename AS '姓名' ,
sex AS '性别',
salary AS '薪资',
hire_date '入职时间',-- AS 可以省略
dept_name '部门名称'
FROM emp;
-- 查询一共有几个部门 
-- 使用distinct 关键字,去掉重复部门信息
SELECT DISTINCT dept_name FROM emp;
-- 将所有员工的工资 +1000 元进行显示
SELECT ename , salary + 1000 FROM emp;
```

### 条件查询

```sql
 SELECT 字段列表 FROM 表名 WHERE 条件列表;
```

| 符号               | 功能                               |
| ------------------ | ---------------------------------- |
| >                  | 大于                               |
| <                  | 小于                               |
| >=                 | 大于等于                           |
| <=                 | 小于等于                           |
| =                  | 等于                               |
| <>或!=             | 不等于                             |
| BETWEEN ...AND ... | 在某个范围之内(都包含)             |
| IN(...)            | 多选一                             |
| LIKE占位符         | 模糊查询_单个任意字符%多个任意字符 |
| lS NULL            | 是NULL                             |
| IS NOT NULL        | 不是NULL                           |
| AND或&&            | 并且                               |
| OR或\|\|           | 或者                               |
| NOT或!             | 非，不是                           |

```sql
# 查询员工姓名为黄蓉的员工信息
SELECT * FROM emp WHERE ename = '黄蓉';
# 查询薪水价格为5000的员工信息
SELECT * FROM emp WHERE salary = 5000;
# 查询薪水价格不是5000的所有员工信息
SELECT * FROM emp WHERE salary != 5000;
SELECT * FROM emp WHERE salary <> 5000;
# 查询薪水价格大于6000元的所有员工信息
SELECT * FROM emp WHERE salary > 6000;
# 查询薪水价格在5000到10000之间所有员工信息
SELECT * FROM emp WHERE salary BETWEEN 5000 AND 10000;
# 查询薪水价格是3600或7200或者20000的所有员工信息
-- 方式1: or
SELECT * FROM emp WHERE salary = 3600 OR salary = 7200 OR salary = 20000;
-- 方式2: in()匹配括号中指定的参数
SELECT * FROM emp WHERE salary IN(3600,7200,20000);
```

> 模糊查询练习

模糊查询使用like关键字，可以使用通配符进行占位:

- _ : 代表单个任意字符
- % : 代表任意个数字符

```sql
# 查询含有'精'字的所有员工信息
SELECT * FROM emp WHERE ename LIKE '%精%';
# 查询以'孙'开头的所有员工信息
SELECT * FROM emp WHERE ename LIKE '孙%';
# 查询第二个字为'兔'的所有员工信息
SELECT * FROM emp WHERE ename LIKE '_兔%';
# 查询没有部门的员工信息
SELECT * FROM emp WHERE dept_name IS NULL;
-- SELECT * FROM emp WHERE dept_name = NULL;
# 查询有部门的员工信息
SELECT * FROM emp WHERE dept_name IS NOT NULL;
```

###  排序查询

```sql
SELECT 字段列表 FROM 表名 ORDER BY 排序字段名1 [排序方式1],排序字段名2 [排序方式2] …;
```

上述语句中的排序方式有两种，分别是：

- ASC ： 升序排列 **（默认值）**

- DESC ： 降序排列

> 注意：如果有多个排序条件，当前边的条件值一样时，才会根据第二条件进行排序

> 单列排序  使用 salary 字段,对emp 表数据进行排序 (升序/降序)

```sql
-- 默认升序排序
ASCSELECT * FROM emp ORDER BY salary;
-- 降序排序
SELECT * FROM emp ORDER BY salary DESC;
```

> 组合排序 

同时对多个字段进行排序, 如果第一个字段相同 就按照第二个字段进行排序,以此类推

在薪水排序的基础上,再使用id进行排序, 如果薪水相同就以id 做降序排序

```sql
-- 组合排序
SELECT * FROM emp ORDER BY salary DESC, eid DESC;
```

### 聚合函数   

之前我们做的查询都是横向查询，它们都是根据条件一行一行的进行判断，而使用聚合函数查询是纵向查询，它是对某一列的值进行计算，然后返回一个单一的值(另外聚合函数会忽略null空值。)；

 **聚合函数分类**

| 函数名      | 功能                             |
| ----------- | -------------------------------- |
| count(列名) | 统计数量（一般选用不为null的列） |
| max(列名)   | 最大值                           |
| min(列名)   | 最小值                           |
| sum(列名)   | 求和                             |
| avg(列名)   | 平均值                           |

**聚合函数语法**

```sql
SELECT 聚合函数名(列名) FROM 表;
```

```sql
# 1 查询员工的总数
-- 统计表中的记录条数 使用 count()
SELECT COUNT(*) FROM emp;-- 使用 *
#2 查看员工总薪水、最高薪水、最小薪水、薪水的平均值
-- sum函数求和, max函数求最大, min函数求最小, avg函数求平均值
SELECTSUM(salary) AS '总薪水',
MAX(salary) AS '最高薪水',
MIN(salary) AS '最低薪水',
AVG(salary) AS '平均薪水'FROM emp;
#3 查询薪水大于4000员工的个数
SELECT COUNT(*) FROM emp WHERE salary > 4000;
#4 查询部门为'教学部'的所有员工的个数
SELECT COUNT(*) FROM emp WHERE dept_name = '教学部';
#5 查询部门为'市场部'所有员工的平均薪水
SELECT AVG(salary) AS '市场部平均薪资' FROM emp WHERE dept_name = '市场部';
```

### 分组查询

**语法**

```sql
SELECT 字段列表 FROM 表名 [WHERE 分组前条件限定] GROUP BY 分组字段名 [HAVING 分组后条件过滤];
```

> 注意：分组之后，查询的字段为聚合函数和分组字段，查询其他字段无任何意义

```sql
-- 通过性别字段 进行分组,求各组的平均薪资
SELECT sex, AVG(salary) FROM emp GROUP BY sex;
-- 查询有几个部门
SELECT dept_name AS '部门名称' FROM emp GROUP BY dept_name;
-- 查询每个部门的平均薪资
SELECT dept_name AS '部门名称', AVG(salary) AS '平均薪资' FROM emp GROUP BY dept_name;
-- 查询每个部门的平均薪资, 部门名称不能为null
SELECT dept_name AS '部门名称', AVG(salary) AS '平均薪资' FROM emp WHERE dept_name IS NOT NULL GROUP BY dept_name;
-- 查询平均薪资大于6000的部门
SELECT dept_name,AVG(salary) FROM emp WHERE dept_name IS NOT NULL GROUP BY dept_name HAVING AVG(salary) > 6000 ;
```

**where 和 having 区别：**

- 执行时机不一样：where 是分组之前进行限定，不满足where条件，则不参与分组，而having是分组之后对结果进行过滤。

- 可判断的条件不一样：where 不能对聚合函数进行判断，having 可以。

### 分页查询

**语法**

```sql
SELECT 字段1,字段2... FROM 表名 LIMIT offset , length;
# limit offset , length;关键字可以接受一个 或者两个 为0 或者正整数的参数
# offset 起始行数, 从0开始记数, 如果省略 则默认为 0
# length 返回的行数
```

> 注意： 上述语句中的起始索引是从0开始

```sql
# 查询emp表中的前5条数据
# 参数1 起始值,默认是0 , 参数2 要查询的条数
SELECT * FROM emp LIMIT 5;
SELECT * FROM emp LIMIT 0 , 5;
# 查询emp表中 从第4条开始,查询6条
SELECT * FROM emp LIMIT 3 , 6;
```

> 分页操作 每页显示3条数据

```sql
-- 分页操作 每页显示3条数据
SELECT * FROM emp LIMIT 0,3;-- 第1页
SELECT * FROM emp LIMIT 3,3;-- 第2页2-1=1 1*3=3
SELECT * FROM emp LIMIT 6,3;-- 第三页
-- 分页公式 起始索引 = (当前页 - 1) * 每页条数
-- limit是MySql中的方言
/*
起始索引计算公式：起始索引 = (当前页码 - 1) * 每页显示的条数
*/
```

### 附加查询

> **UNION ALL**

UNION 操作符用于合并两个或多个 SELECT 语句的结果集。

请注意，UNION 内部的 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每条 SELECT 语句中的列的顺序必须相同。

```sql
-- UNION 语法
SELECT column_name(s) FROM table_name1
UNION
SELECT column_name(s) FROM table_name2;
```

**注释：**默认地，UNION 操作符选取不同的值。如果允许重复的值，请使用 UNION ALL。

```sql
-- UNION ALL 语法
SELECT column_name(s) FROM table_name1
UNION ALL
SELECT column_name(s) FROM table_name2;
```

> **case when用法**

当我们需要从数据源上 直接判断数据显示代表的含义的时候 ,就可以在SQL语句中使用 Case When这个函数了

Case具有两种格式。简单Case函数和Case搜索函数。

**简单Case函数**

```sql
/*case 列名

　　　　when 条件值1 then 选择项1

　　　　when 条件值2 then 选项2.......

　　　　else 默认值 end*/
SELECT name,
CASE score
	WHEN 'A' THEN '优'
    WHEN 'B' THEN '良'
    WHEN 'C' THEN '不及格'
    ELSE '不及格' END
FROM studen;
```

**Case搜索函数**

```sql
　/*case

　　　　when 列名= 条件值1 then 选择项1

　　　　when 列名=条件值2 then 选项2.......

　　　　else 默认值 end*/
SELECT name,
CASE 
	WHEN score>90 THEN '优'
    WHEN score>70 THEN '良'
    WHEN score<60 THEN '不及格'
    ELSE '不及格' END AS get
FROM studen;
```

## MySQL约束

**约束的作用:** 

对表中的数据进行进一步的限制，从而保证数据的正确性、有效性、完整性. 违反约束的不正确数据,将无法插入到表中 

**常见的约束**

| 约束名 | 约束关键字  |
| ------ | ----------- |
| 主键   | primary key |
| 唯一   | unique      |
| 非空   | not null    |
| 外键   | foreign key |

### 主键约束

> 不可重复唯一非空，用来表示数据库中的每一条记录

```sql
字段名 字段类型 primary key
```

```sql
# 方式1 创建一个带主键的表
CREATE TABLE emp2(
    -- 设置主键 唯一 非空 
    eid INT PRIMARY KEY,
    ename VARCHAR(20),
    sex CHAR(1)
);
# 方式2 创建一个带主键的表
CREATE TABLE emp2(
    eid INT ,
    ename VARCHAR(20),
    sex CHAR(1),
    -- 指定主键为 eid字段
    PRIMARY KEY(eid)
);
# 方式3 创建一个带主键的表
# 创建的时候不指定主键,然后通过 DDL语句进行设置 
CREATE TABLE emp2(
    eid INT,
    ename VARCHAR(20),
    sex CHAR(1)
);
ALTER TABLE emp2 ADD PRIMARY KEY(eid);
```

> 测试主键的唯一性 非空性

```sql
# 正常插入一条数据
INSERT INTO emp2 VALUES(1,'宋江','男');
# 插入一条数据,主键为空
-- Column 'eid' cannot be null 主键不能为空
INSERT INTO emp2 VALUES(NULL,'李逵','男');
# 插入一条数据,主键为 1
-- Duplicate entry '1' for key 'PRIMARY' 主键不能重复
INSERT INTO emp2 VALUES(1,'孙二娘','女');
```

> 删除主键约束

```sql
-- 使用DDL语句 删除表中的主键
ALTER TABLE emp2 DROP PRIMARY KEY;
DESC emp2;
```

> 主键的自增
>
> 主键如果让我们自己添加很有可能重复,我们通常希望在每次插入新记录时,数据库自动生成主键字段的值

```sql
-- 创建主键自增的表
CREATE TABLE emp2(
    -- 关键字 AUTO_INCREMENT,主键类型必须是整数类型
    eid INT PRIMARY KEY AUTO_INCREMENT,
    ename VARCHAR(20),
    sex CHAR(1)
);
```

> 修改主键自增的起始值
>
> 默认地 AUTO_INCREMENT 的开始值是 1,

```sql
-- 创建主键自增的表,自定义自增其实值
CREATE TABLE emp2(
    eid INT PRIMARY KEY AUTO_INCREMENT,
    ename VARCHAR(20),
    sex CHAR(1)
)AUTO_INCREMENT=100;
```

> DELETE和TRUNCATE对自增长的影响

| 清空表数据 | 特点                                                         |
| ---------- | ------------------------------------------------------------ |
| DELETE     | 只是删除表中所有数据,对自增没有影响                          |
| TRUNCATE   | truncate 是将整个表删除掉,然后创建一个新的表 自增的主键,重新从 1开始 |

通常针对业务去设计主键,每张表都设计一个主键id

主键是给数据库和程序使用的,跟最终的客户无关,所以主键没有意义没有关系,只要能够保证不重复 就好,比如 身份证就可以作为主键

### 非空约束

> 非空约束的特点: 某一列不允许为空

```sql
字段名 字段类型 not null
```

```sql
# 非空约束CREATE TABLE emp2(
    eid INT PRIMARY KEY AUTO_INCREMENT,
    -- 添加非空约束, ename字段不能为空
    ename VARCHAR(20) NOT NULL,
    sex CHAR(1)
);
```

### 唯一约束

> 唯一约束的特点: 表中的某一列的值不能重复( 对null不做唯一的判断 )

```sql
字段名 字段类型 unique
```

```sql
#创建emp3表 为ename 字段添加唯一约束
CREATE TABLE emp3(
    eid INT PRIMARY KEY AUTO_INCREMENT,
    ename VARCHAR(20) UNIQUE,
    sex CHAR(1)
);
```

```sql
-- 测试唯一约束 添加一条数据
INSERT INTO emp3 (ename,sex) VALUES('张百万','男');
-- 添加一条 ename重复的 数据
-- Duplicate entry '张百万' for key 'ename' ename不能重复
INSERT INTO emp3 (ename,sex) VALUES('张百万','女');
```

**主键约束与唯一约束的区别:**

- 主键约束 唯一且不能够为空
- 唯一约束,唯一 但是可以为空
- 一个表中只能有一个主键 , 但是可以有多个唯一约束

###  默认约束

> 默认值约束用来指定某列的默认值

```sql
字段名 字段类型 DEFAULT 默认值 
```

```sql
-- 创建带有默认值的表
CREATE TABLE emp4(
    eid INT PRIMARY KEY AUTO_INCREMENT,
    -- 为ename 字段添加默认值
    ename VARCHAR(20) DEFAULT '奥利给',
    sex CHAR(1)
);
```

```sql
-- 添加数据 使用默认值
INSERT INTO emp4(ename,sex) VALUES(DEFAULT,'男');
INSERT INTO emp4(sex) VALUES('女');
-- 不使用默认值
INSERT INTO emp4(ename,sex) VALUES('艳秋','女');
```

### 外键约束

>FOREIGN KEY 表示外键约束
>
>外键用来让两个表的数据之间建立链接，保证数据的一致性和完整性。

```sql
-- 创建表时添加外键约束
CREATE TABLE 表名( 列名 数据类型,…[CONSTRAINT] [外键名称] FOREIGN KEY(外键列名) REFERENCES 主表(主表列名) );
-- 建完表后添加外键约束
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称);
-- 删除外键约束
ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
```

```sql
-- 部门表
CREATE TABLE dept(
    id int primary key auto_increment,
    dep_name varchar(20),
    addr varchar(20)
);
-- 员工表
CREATE TABLE emp(
    id int primary key auto_increment,
    name varchar(20),
    age int,
    dep_id int,
    -- 添加外键 dep_id,关联 dept 表的id主键
    CONSTRAINT fk_emp_dept FOREIGN KEY(dep_id) REFERENCES dept(id)
);

-- 添加 2 个部门
insert into dept(dep_name,addr) values('研发部','郑州'),
('销售部', '北京');
-- 添加员工,dep_id 表示员工所在的部门
INSERT INTO emp (NAME, age, dep_id) VALUES ('张三', 20, 1),
('李四', 20, 1),
('王五', 20, 1),
('赵六', 20, 2),
('孙七', 22, 2),
('周八', 18, 2);
-- 此时删除研发部这条数据,会发现无法删除。
-- 删除外键
alter table emp drop FOREIGN key fk_emp_dept;
-- 重新添加外键
alter table emp add CONSTRAINT fk_emp_dept FOREIGN key(dep_id) REFERENCES dept(id);
```

## 数据库设计

### 数据库设计简介

**数据库设计概念**

- 数据库设计就是根据业务系统的具体需求，结合我们所选用的DBMS，为这个业务系统构造出最优的数据存储模型。

- 建立数据库中的表结构以及表与表之间的关联关系的过程。

- 有哪些表？表里有哪些字段？表和表之间有什么关系？

**数据库设计的步骤**

- 需求分析（数据是什么? 数据具有哪些属性? 数据与属性的特点是什么）

  逻辑分析（通过ER图对数据库进行逻辑建模，不需要考虑我们所选用的数据库管理系统）

- ER图（entity relationship diagram) 实体关系图 ：提供了实体类型、属性和关系的方法，用来描述现实世界的概念模型

- 实体用矩形表示，属性用椭圆表示，主键学号需要加下划线

- 表关系

    - 一对一  一夫一妻制
      - 如：用户（用户名字 密码 ） 和 用户详情 ()
      - 一对一关系多用于表拆分，将一个实体中经常使用的字段放一张表，不经常使用的字段放另一张表，用于提升查询性能

  - 一对多

    - 如：部门 和 员工

    - 一个部门对应多个员工，一个员工对应一个部门。

  - 多对多

     - 如：商品 和 订单
     
     - 一个商品对应多个订单，一个订单包含多个商品。

###  表关系(一对多)

>实现方式：在多的一方建立外键，指向一的一方的主键

我们还是以 员工表 和 部门表 举例:
员工表属于多的一方，而部门表属于一的一方，此时我们会在员工表中添加一列(dep_id)，指向于部门表的主键（id）

```sql
-- 部门表
CREATE TABLE tb_dept(
    id int primary key auto_increment,
    dep_name varchar(20),
    addr varchar(20)
);
-- 员工表
CREATE TABLE tb_emp(
    id int primary key auto_increment,
    name varchar(20),
    age int,
    dep_id int,
    -- 添加外键 dep_id,关联 dept 表的id主键
    CONSTRAINT fk_emp_dept FOREIGN KEY(dep_id) REFERENCES tb_dept(id)
);
```

###  表关系(多对多)

>实现方式：建立第三张中间表，中间表至少包含两个外键，分别关联两方主键

我们以 订单表 和 商品表 举例：
经过分析发现，订单表和商品表都属于多的一方，此时需要创建一个中间表，在中间表中添加订单表的外键和商品表的外键指向两张表的主键

```sql
-- 订单表
CREATE TABLE tb_order(
    id int primary key auto_increment,
    payment double(10,2),
    payment_type TINYINT,
    status TINYINT
);
-- 商品表
CREATE TABLE tb_goods(
    id int primary key auto_increment,
    title varchar(100),
    price double(10,2)
);
-- 订单商品中间表
CREATE TABLE tb_order_goods(
    id int primary key auto_increment,
    order_id int,
    goods_id int,
    count int
);
-- 建完表后，添加外键
alter table tb_order_goods add
CONSTRAINT fk_order_id FOREIGN key(order_id) REFERENCES tb_order(id);
alter table tb_order_goods add
CONSTRAINT fk_goods_id FOREIGN key(goods_id) REFERENCES tb_goods(id);
```

###  表关系(一对一)

>实现方式：在任意一方加入外键，关联另一方主键，并且设置外键为唯一(UNIQUE)

```sql
create table tb_user_desc (
    id int primary key auto_increment,
    city varchar(20),
    edu varchar(10),
    income int,
    status char(2),
    des varchar(100)
);
create table tb_user (
    id int primary key auto_increment,
    photo varchar(100),
    nickname varchar(50),
    age int,
    gender char(1),
    desc_id int unique,
    -- 添加外键
    CONSTRAINT fk_user_desc FOREIGN KEY(desc_id)
    REFERENCES tb_user_desc(id)
);
```

## 多表查询

> DQL: 查询多张表,获取到需要的数据

```sql
-- 创建 db3_2 数据库,指定编码
CREATE DATABASE db3_2 CHARACTER SET utf8;
-- 分类表 (一方 主表)
CREATE TABLE category (
    cid VARCHAR(32) PRIMARY KEY,
    cname VARCHAR(50)
);
-- 商品表 (多方 从表)
CREATE TABLE products(
    pid VARCHAR(32) PRIMARY KEY,
    pname VARCHAR(50),
    price INT,
    flag VARCHAR(2),
    -- 是否上架标记为:1表示上架、0表示下架
    category_id VARCHAR(32),
    -- 添加外键约束
    FOREIGN KEY (category_id) REFERENCES category (cid)
);

-- 插入数据
-- 分类数据
INSERT INTO category(cid,cname) VALUES('c001','家电');
INSERT INTO category(cid,cname) VALUES('c002','鞋服');
INSERT INTO category(cid,cname) VALUES('c003','化妆品');
INSERT INTO category(cid,cname) VALUES('c004','汽车');
-- 商品数据
INSERT INTO products(pid, pname,price,flag,category_id) VALUES('p001','小米电视 机',5000,'1','c001');
INSERT INTO products(pid, pname,price,flag,category_id) VALUES('p002','格力空调',3000,'1','c001');
INSERT INTO products(pid, pname,price,flag,category_id) VALUES('p003','美的冰箱',4500,'1','c001');
INSERT INTO products(pid, pname,price,flag,category_id) VALUES('p004','篮球鞋',800,'1','c002');
INSERT INTO products(pid, pname,price,flag,category_id) VALUES('p005','运动裤',200,'1','c002');
INSERT INTO products(pid, pname,price,flag,category_id) VALUES('p006','T恤',300,'1','c002');
INSERT INTO products(pid, pname,price,flag,category_id) VALUES('p007','冲锋衣',2000,'1','c002');
INSERT INTO products(pid, pname,price,flag,category_id) VALUES('p008','神仙水',800,'1','c003');
INSERT INTO products(pid, pname,price,flag,category_id) VALUES('p009','大宝',200,'1','c003');
```

### 笛卡尔积

> 交叉连接查询,因为会产生笛卡尔积,所以 基本不会使用

```sql
SELECT 字段名 FROM 表1, 表2;
```

```sql
-- 使用交叉连接查询 商品表与分类表
SELECT * FROM category,products;
```

### 内连接查询

> 通过指定的条件去匹配两张表中的数据, 匹配上就显示,匹配不上就不显示

**隐式内连接**

>from子句后面直接写多个表名使用where指定连接条件的 这种连接方式是 隐式内连接
>
>使用where条件过滤无用的数据

```sql
SELECT 字段名 FROM 左表, 右表 WHERE 连接条件;
```

```sql
-- 查询所有商品信息和对应的分类信息
SELECT * FROM products,category WHERE category_id = cid;
```

查询商品表的商品名称 和 价格,以及商品的分类信息

可以通过给表起别名的方式, 方便我们的查询

```sql
SELECT
p.`pname`,
p.`price`,
c.`cname`FROM products p,category c WHERE p.`category_id` = c.`cid`;
-- 查询 格力空调是属于哪一分类下的商品
SELECT p.`pname`,c.`cname`
FROM products p,category c
WHERE p.`category_id` = c.`cid` AND p.`pid` = 'p002';
```

**显式内连接**

> 使用 inner join …on 这种方式, 就是显式内连接

```sql
SELECT 字段名 FROM 左表 [INNER] JOIN 右表 ON 条件-- inner 可以省略
```

```sql
-- 查询所有商品信息和对应的分类信息
SELECT * FROM products p INNER JOIN category c ON p.category_id = c.cid;
-- 查询鞋服分类下,价格大于500的商品名称和价格
-- 我们需要确定的几件事
-- 1.查询几张表 products & category
-- 2.表的连接条件 从表.外键 = 主表的主键
-- 3.查询的条件 cname = '鞋服' and price > 500 
-- 4.要查询的字段 pname price
SELECT p.pname,p.price
FROM products p INNER JOIN category c
ON p.category_id = c.cid
WHERE p.price > 500 AND cname = '鞋服';
```

### 外连接查询

**左外连接**

- 左外连接 , 使用 LEFT OUTER JOIN , OUTER 可以省略

- 左外连接的特点
  - 以左表为基准, 匹配右边表中的数据,如果匹配的上,就展示匹配到的数据
  - 如果匹配不到, 左表中的数据正常展示, 右边的展示为null

```sql
SELECT 字段名 FROM 左表 LEFT [OUTER] JOIN 右表 ON 条件
-- 左外连接查询
SELECT * FROM category c LEFT JOIN products p ON c.`cid`= p.`category_id`;
-- 查询每个分类下的商品个数
/*1.连接条件: 主表.主键 = 从表.外键
2.查询条件: 每个分类 需要分组
3.要查询的字段: 分类名称, 分类下商品个数*/
SELECT	c.`cname` AS '分类名称',
COUNT(p.`pid`) AS '商品个数'
FROM category c LEFT JOIN products p
ON c.`cid` = p.`category_id`
GROUP BY c.`cname`;
```

**右外连接**

- 右外连接 , 使用 RIGHT OUTER JOIN , OUTER 可以省略

- 右外连接的特点
  - 以右表为基准，匹配左边表中的数据，如果能匹配到，展示匹配到的数据
  - 如果匹配不到，右表中的数据正常展示, 左边展示为null

  ```sql
SELECT 字段名 FROM 左表 RIGHT [OUTER ]JOIN 右表 ON 条件
-- 右外连接查询
SELECT * FROM products p RIGHT JOIN category c ON p.`category_id` = c.`cid`;
  ```

![SQL JOINS](https://image.aobayu.cn/images/join.png)

### 子查询

- 子查询概念
  - 一条select 查询语句的结果, 作为另一条 select 语句的一部分

- 子查询的特点
  - 子查询必须放在小括号中
  - 子查询一般作为父查询的查询条件使用

- 子查询常见分类
  - where型 子查询: 将子查询的结果, 作为父查询的比较条件
  - from型 子查询 : 将子查询的结果, 作为 一张表,提供给父层查询使用
  - exists型 子查询: 子查询的结果是单列多行, 类似一个数组, 父层查询使用 IN 函数 ,包含子查询的结果

```sql
SELECT 查询字段 FROM 表 WHERE 字段=(子查询);
```

```sql
-- 通过子查询的方式, 查询价格最高的商品信息
-- 1.先查询出最高价格
SELECT MAX(price) FROM products;
-- 2.将最高价格作为条件,获取商品信息
SELECT * FROM products WHERE price = (SELECT MAX(price) FROM products);
-- #查询化妆品分类下的 商品名称 商品价格
-- 先查出化妆品分类的id
SELECT cid FROM category WHERE cname = '化妆品';
-- 根据分类id ,去商品表中查询对应的商品信息
SELECT	p.`pname`,p.`price` FROM products p WHERE p.`category_id` = (SELECT cid FROM category WHERE cname = '化妆品');
-- 1.查询平均价格
SELECT AVG(price) FROM products;-- 1866
-- 2.查询小于平均价格的商品
SELECT * FROM products WHERE price < (SELECT AVG(price) FROM products);
```

**子查询的结果作为一张表**

```sql
SELECT 查询字段 FROM (子查询)表别名 WHERE 条件;
```

```sql
-- 查询商品中,价格大于500的商品信息,包括 商品名称 商品价格 商品所属分类名称
-- 1.先查询分类表的数据
SELECT * FROM category;
-- 2.将上面的查询语句 作为一张表使用 
SELECT p.`pname`,p.`price`,c.cname FROM products p
-- 子查询作为一张表使用时 要起别名 才能访问表中字段
INNER JOIN (SELECT * FROM category) c
ON p.`category_id` = c.cid WHERE p.`price` > 500;
```

**子查询结果是单列多行**

子查询的结果类似一个数组, 父层查询使用 IN 函数 ,包含子查询的结果

```sql
SELECT 查询字段 FROM 表 WHERE 字段 IN (子查询);
```

```sql
-- 查询价格小于两千的商品,来自于哪些分类(名称)
-- 先查询价格小于2000 的商品的,分类
IDSELECT DISTINCT category_id FROM products WHERE price < 2000;
-- 在根据分类的id信息,查询分类名称
-- 报错: Subquery returns more than 1 row
-- 子查询的结果 大于一行
SELECT * FROM category WHERE cid = (SELECT DISTINCT category_id FROM products WHERE price < 2000);
-- 子查询获取的是单列多行数据
SELECT * FROM category WHERE cid
IN (SELECT DISTINCT category_id FROM products WHERE price < 2000);
```

```sql
-- 查询家电类 与 鞋服类下面的全部商品信息
-- 先查询出家电与鞋服类的 分类ID
SELECT cid FROM category WHERE cname IN ('家电','鞋服');
-- 根据cid 查询分类下的商品信息
SELECT * FROM products
WHERE category_id
IN (SELECT cid FROM category WHERE cname IN ('家电','鞋服'));
```

**子查询总结**

- 子查询如果查出的是一个字段(单列), 那就在where后面作为条件使用
- 子查询如果查询出的是多个字段(多列), 就当做一张表使用(要起别名)

## 事务

>数据库的事务（Transaction）是一种机制、一个操作序列，包含了一组数据库操作命令。
>
>事务把所有的命令作为一个整体一起向系统提交或撤销操作请求，即这一组数据库命令要么同时成功，要么同时失败。
>
>事务是一个不可分割的工作逻辑单元。

张三和李四账户中各有100块钱，现李四需要转换500块钱给张三，具体的转账操作为

- 第一步：查询李四账户余额

- 第二步：从李四账户金额 -500

- 第三步：给张三账户金额 +500

现在假设在转账过程中第二步完成后出现了异常第三步没有执行，就会造成李四账户金额少了500，而张三金额并没有多500；这样的系统是有问题的。如果解决呢？使用事务可以解决上述问题

 **语法**

```sql
-- 开启事务
START TRANSACTION; 或者 BEGIN;
-- 提交事务
commit;
-- 回滚事务
rollback;
```

### 模拟转账操作

```sql
-- 创建账户表
CREATE TABLE account(
    -- 主键
    id INT PRIMARY KEY AUTO_INCREMENT,
    -- 姓名
    NAME VARCHAR(10),
    -- 余额
    money DOUBLE
);
-- 添加两个用户
INSERT INTO account (NAME, money) VALUES ('tom', 1000), ('jack', 1000);
```

> 模拟tom 给 jack 转 500 元钱，一个转账的业务操作最少要执行下面的 2 条语句:

```sql
-- tom账户 -500元
UPDATE account SET money = money - 500 WHERE NAME = 'tom';
-- jack账户 + 500元
UPDATE account SET money = money + 500 WHERE NAME = 'jack';
```

假设当tom 账号上 -500 元,服务器崩溃了。jack 的账号并没有+500 元，数据就出现问题了。 我们要保证整个事务执行的完整性,要么都成功, 要么都失败. 这个时候我们就要学习如何操作事务

### Mysql事务操作

MYSQL 中可以有两种方式进行事务的操作:

- 手动提交事务

- 自动提交事务

| 功能     | 语句                           |
| -------- | ------------------------------ |
| 开启事务 | start transaction; 或者 BEGIN; |
| 提交事务 | commit;                        |
| 回滚事务 | rollback;                      |

```sql
START TRANSACTION
    -- 这个语句显式地标记一个事务的起始点。
COMMIT
    -- 表示提交事务，即提交事务的所有操作，具体地说，
    -- 就是将事务中所有对数据库的更新都写到磁盘上的物理数据库中，事务正常结束。
ROLLBACK
    -- 表示撤销事务，即在事务运行的过程中发生了某种故障，事务不能继续执行，
    -- 系统将事务中对数据库的所有已完成的操作全部撤销，回滚到事务开始时的状态
```

**手动提交事务流程**

- 执行成功的情况: 开启事务 -> 执行多条 SQL 语句 -> 成功提交事务

- 执行失败的情况: 开启事务 -> 执行多条 SQL 语句 -> 事务的回滚

模拟张三给李四转 500 元钱

```sql
-- 开启事务
start transaction;
```

```sql
-- tom账户 -500
update account set money = money - 500 where name = 'tom'
-- jack账户 +500
update account set money = money + 500 where name = 'jack';
```

```sql
-- 注：由于未提交事务，此时数据并未变化
-- 在控制台执行 commit 提交事务
commit;
```

以上操作为提交事务后，才会真正执行，中间有异常也不会对数据有影响

如是自动事务，每次update数据都会真实改变

> 查看autocommit状态

```sql
SHOW VARIABLES LIKE 'autocommit';
-- on :自动提交
-- off : 手动提交
SELECT @@autocommit;

-- 把 autocommit 改成 off;
SET @@autocommit=off;
-- 1表示自动 0 表示手动
set @@autocommit = 0;

-- 修改数据
update account set money = money - 500 where name = 'jack';
-- 手动提交
commit;
```

### 事务的四大特征

- 原子性（Atomicity）: 事务是不可分割的最小操作单位，要么同时成功，要么同时失败

- 一致性（Consistency） :事务完成时，必须使所有的数据都保持一致状态

- 隔离性（Isolation） :多个事务之间，操作的可见性

- 持久性（Durability） :事务一旦提交或回滚，它对数据库中的数据的改变就是永久的

### 事务的隔离级别（了解）

MySQL是一个客户端／服务器架构的软件，对于同一个服务器来说，可以有若干个客户端与之连接，每个客户端与服务器连接上之后，就可以称之为一个会话（Session）。每个客户端都可以在自己的会话中向服务器发出请求语句，一个请求语句可能是某个事务的一部分，也就是对于服务器来说可能同时处理多个事务。

**事务并发执行遇到的问题**

> **脏读(Dirty Read)**

 如果一个事务读到了另一个未提交事务修改过的数据，那就意味着发生了**脏读**

![Dirty Read](https://image.aobayu.cn/images/DirtyRead.png)

如上图，Session A和Session B各开启了一个事务，Session B中的事务先将number列为1的记录的name列更新为'关羽'，然后Session A中的事务再去查询这条number为1的记录，如果读到列name的值为'关羽'，而Session B中的事务稍后进行了回滚，那么Session A中的事务相当于读到了一个不存在的数据，这种现象就称之为脏读。

> **不可重复读（ Non-Repeatable Read）**

如果一个事务只能读到另一个已经提交的事务**修改**过的数据，并且其他事务每对该数据进行一次修改并提交后，该事务都能查询得到最新值，那就意味着发生了**不可重复读**

![Non-Repeatable Read](https://image.aobayu.cn/images/Non-Repeatable-Read.png))

如上图，我们在Session B中提交了几个隐式事务（注意是隐式事务，意味着语句结束事务就提交了），这些事务都修改了number列为1的记录的列name的值，每次事务提交之后，如果Session A中的事务都可以查看到最新的值，这种现象也被称之为不可重复读。

> **幻读（Phantom）**

如果一个事务先根据某些条件查询出一些记录，之后另一个事务又向表中**插入**了符合这些条件的记录，原先的事务再次按照该条件查询时，能把另一个事务插入的记录也读出来，那就意味着发生了幻读

![Phantom](https://image.aobayu.cn/images/Phantom.png)

如上图，Session A中的事务先根据条件number > 0这个条件查询表hero，得到了name列值为'刘备'的记录；之后Session B中提交了一个隐式事务，该事务向表hero中插入了一条新记录；之后Session A中的事务再根据相同的条件number > 0查询表hero，得到的结果集中包含Session B中的事务新插入的那条记录，这种现象也被称之为幻读。

**tips:**

那对于先前已经读到的记录，之后又读取不到这种情况，算啥呢？其实这相当于对每一条记录都发生了不可重复读的现象。幻读只是重点强调了读取到了之前读取没有获取到的记录

**SQL标准中的四种隔离级别**

根据以上严重程度，做一个排序

脏读 > 不可重复读 > 幻读

根据以上问题 ，SQL设置了隔离级别

- READ UNCOMMITTED：未提交读。
- READ COMMITTED：已提交读。
- REPEATABLE READ：可重复读。
- SERIALIZABLE：可串行化。

**存在的问题:**

| **隔离级别**               | **脏读** | **不可重复读** | **幻读** |
| -------------------------- | -------- | -------------- | -------- |
| 读未提交(READ UNCOMMITTED) | √        | √              | √        |
| 读已提交(READ COMMITTED)   | ×        | √              | √        |
| 可重复读(REPEATABLE READ)  | ×        | ×              | √        |
| 可串行化(SERIALIZABLE)     | ×        | ×              | ×        |

也就是说:

- READ UNCOMMITTED 隔离级别下，可能发生脏读、不可重复读和幻读问题。
- READ COMMITTED 隔离级别下，可能发生不可重复读和幻读问题，但是不可以发生脏读问题。
- REPEATABLE READ 隔离级别下，可能发生幻读问题，但是不可以发生脏读和不可重复读的问题。
- SERIALIZABLE隔离级别下，各种问题都不可以发生。

## 数据库设计三大范式

**第一范式（1NF）**: 确保每一列的原子性（做到每列不可拆分）

**第二范式（2NF）**:在第一范式的基础上，每一行必须可以唯一的被区分，因此需要为表加上主键列

**第三范式（3NF）**:在第二范式的基础上，一个表中不包含已在其他表中包含的非主关键字信息（外键）

**反范式**: 有时候为了兼顾效率，可以不遵循范式，设计冗余字段，如订单（总价）和订单项（单价）

## 数据库的备份和还原

```sql
-- 备份
mysqldump -u用户名 -p密码 数据库名 > 保存的路径
mysqldump -uroot -p123456 db1 > d://a.sql
```

```sql
-- 还原
drop database db1;
create database db1;
use db1;
source d://a.sql
```

## MySQL存储引擎

**什么是存储引擎：**

sql  ----> 解析器 ------>优化器 ----->搜索引擎

数据库存储引擎是数据库底层软件组织，数据库管理系统（DBMS）使用数据引擎进行创建、查询、更新和删除数据。不同的存储引擎提供不同的**存储机制、索引技巧、锁定水平**等功能，使用不同的存储引擎，还可以 获得特定的功能。现在许多不同的数据库管理系统都支持多种不同的数据引擎。MySQL的核心就是存储引擎。

```sql
-- 查看当前mysql默认引擎: 
show variables like '%engine%';
```

```sql
-- 查看mysql支持哪些引擎：
show engines;
```

```sql
-- 修改默认存储引擎
-- 如果修改本次会话的默认存储引擎(重启后失效)，只对本会话有效，其他会话无效：
set default_storage_engine=innodb;
```

```sql
-- 修改全局会话默认存储引擎(重启后失效)，对所有会话有效
set global default_storage_engine=innodb;
```

### InnoDB

InnoDB是一个健壮的事务型存储引擎，这种存储引擎已经被很多互联网公司使用，为用户操作非常大的数据存储提供了一个强大的解决方案。

InnoDB还引入了行级锁定和外键约束，在以下场合下，使用InnoDB是最理想的选择：

 **优点:**

-  更新密集的表。 InnoDB存储引擎特别适合处理多重并发的更新请求。 

-  事务。 InnoDB存储引擎是支持事务的标准MySQL存储引擎。 

-  自动灾难恢复。 与其它存储引擎不同，InnoDB表能够自动从灾难中恢复。 

-  外键约束。 MySQL支持外键的存储引擎只有InnoDB。 

-  支持自动增加列AUTO_INCREMENT属性。 

-  从5.5开始innodb存储引擎成为默认的存储引擎。 

一般来说，如果需要事务支持，并且有较高的并发读取频率，InnoDB是不错的选择。

InnoDB是一个健壮的事务型存储引擎,这种存储引擎已经被很多互联网公司使用,为用户操作非常大的数据存储提供了一个强大的解决方案。 

InnoDB还引入了行级锁定和外键约東,在以下场合下,使用 InnoDB是最理想的选择

**优点**

- Innodb引擎提供了对数据库ACID事务的支持,并且实现了SQL标准的四种隔离级别

- 支持多版本并发控制的行级锁,由于锁粒度小,写操作和更新操作并发高、速度快

- 支持自增长列。

- 支持外键 

- 适合于大容量数据库系统,

- 支持自动灾难恢复

**缺点**

- 它没有保存表的行数 SELECT COUNT(*) FROM TABLE时需要扫描全表

**应用场景**

- 当需要使用数据库事务时,该引擎当然是首选。由于锁的粒度更小,写操作不会锁定全表,所以在并发较高时,使用 Innodb引擎会提升效率。更新密集的表, InnoDB.存储引擎特别适合处理多重并发的更新请求

### MyISAM

MyISam引擎不支持事务、也不支持外键,优势是访问速度快,对事务完整性没有要求或者以 select, Insert为主的应用基本上可以用这个引擎来创建表

**优点**

- MyISAM表是独立于操作系统的,这说明可以轻松地将其从 windows服务器移植到Liux服务器

- MyISAM存储引擎在查询大量数据时非常迅速,这是它最突出的优点

- 另行大批量插入操作时执行速度也比较快

**缺点**

- MyISAM表没有提供对数据库事务的支持。

- 不支持行级锁和外键。

- 不适合用于经常 UPDATE(更新)的表

**应用场景**

- 以读为主的业务,例如:图片信息数据库,博客数据库,商品库等业务

- 对数据一致性要求不是非常高的业务(不支持事务)

- 硬件资源比较差的机器可以用 MyISAM(占用资源少)

### MEMORY

MEMORY的特点是将表中的数据放在内存中,适用于存储临时数据的临时表和数据仓库中的纬度表

**优点**

- memory类型的表访问非常的快,因为它的数据是放在内存中的

**缺点**

- 一旦服务关闭,表中的数据就会丢失掉

- 只支持表锁,并发性能差,不支持TEXT和BLOB列类型,存储 varchar时是按照char的方式

**应用场景**

- 目标数据较小,而且被非常频繁地访问。

- 如果数据是临时的,而且要求必须立即可用,那么就可以存放在内存表中。

- 存储在 Memory表中的数据如果突然丢失,不会对应用服务产生实质的负面影响

**存储引擎的选择**

不同的存储引擎都有各自的特点，以适应不同的需求，如下表所示：

| **功 能**    | **MYISAM** | **Memory** | **InnoDB** | **Archive** |
| ------------ | ---------- | ---------- | ---------- | ----------- |
| 存储限制     | 256TB      | RAM        | 64TB       | None        |
| 支持事务     | No         | No         | Yes        | No          |
| 支持全文索引 | Yes        | No         | No         | No          |
| 支持数索引   | Yes        | Yes        | Yes        | No          |
| 支持哈希索引 | No         | Yes        | No         | No          |
| 支持数据缓存 | No         | N/A        | Yes        | No          |
| 支持外键     | No         | No         | Yes        | No          |

- 如果要提供提交、回滚、崩溃恢复能力的事物安全（ACID兼容）能力，并要求实现并发控制，InnoDB是一个好的选择

- 如果数据表主要用来插入和查询记录，则MyISAM引擎能提供较高的处理效率

- 如果只是临时存放数据，数据量不大，并且不需要较高的数据安全性，可以选择将数据保存在内存中的Memory引擎，MySQL中使用该引擎作为临时表，存放查询的中间结果

- 如果只有INSERT和SELECT操作，可以选择Archive，Archive支持高并发的插入操作，但是本身不是事务安全的。Archive非常适合存储归档数据，如记录日志信息可以使用Archive

使用哪一种引擎需要灵活选择，**一个数据库中多个表可以使用不同引擎以满足各种性能和实际需求**，使用合适的存储引擎，将会提高整个数据库的性能。

### Mysql索引数据结构 B-树和B+树

**索引类型:**

- 哈希索引 
  - 只能做等值比较，不支持范围查找
  - 无法利用索引完成排序
  - 如果存在大量重复键值的情况下，哈希索引效率会比较低，可能存在哈希碰撞

- B-树/B+树
  - B 代表 balance 平衡的意思，是一种多路自平衡的搜索树
  - InnoDB 引擎 默认使用B+树，Memory默认使用 B树
  - B树所有节点都储存数据，B+树只在叶子节点储存，为了降低树的高度，每一层可以保存多个节点（>2个）
  - 为了支持范围查询，B+树在叶子节点之间加上了双向链表，减少IO次数