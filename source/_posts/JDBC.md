---
title: JDBC
copyright_url: https://www.aobayu.cn/2022/09/26/JDBC/
tags: 
    - JDBC
categories: 学习之路
date: 2022-9-26
keywords: JDBC
description: JDBC的全称是Java数据库连接(Java Database connect)，它是一套用于执行SQL语句的Java API。可以访问任何类型表列数据，特别是存储在关系数据库中的数据。JDBC代表Java数据库连接。 --本文为自己学习中所写
---

## JDBC概述

在开发中我们使用的是java语言，那么势必要通过java语言操作数据库中的数据。这就是接下来要学习的JDBC。

**JDBC概念**
JDBC(Java Data Base Connectivity) 是 Java 访问数据库的标准规范.是一种用于执行SQL语句的Java API，可以为多种关系数据库提供统一访问，它由一组用Java语言编写的类和接口组成。是Java访问数据库的标准规范

**JDBC原理**
JDBC是接口，驱动是接口的实现，没有驱动将无法完成数据库连接，从而不能操作数据库！每个数据库厂商都需要提供自己的驱动，用来连接自己公司的数据库，也就是说驱动一般都由数据库生成厂商提供。

**JDBC好处**

- 各数据库厂商使用相同的接口，Java代码不需要针对不同数据库分别开发

- 可随时替换底层数据库，访问数据库的Java代码基本不变

以后编写操作数据库的代码只需要面向JDBC（接口），操作哪儿个关系型数据库就需要导入该数据库的驱动包，如需要操作MySQL数据库，就需要再项目中导入MySQL数据库的驱动包。

## JDBC快速入门

> **数据准备**

```sql
-- 创建 jdbc_user表
CREATE TABLE jdbc_user(
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50),
    PASSWORD VARCHAR(50),
    birthday DATE
);
-- 添加数据
INSERT INTO jdbc_user (username, PASSWORD,birthday)
VALUES('admin1', '123','1991/12/24'),
('admin2','123','1995/12/24'),
('test1', '123','1998/12/24'),
('test2', '123','2000/12/24');
```

> **引用驱动包** 

在项目根目录新建 lib 文件夹，里面存入 mysql-connector-java-5.1.48.jar 压缩包

打开IDEA，找到  mysql-connector-java-5.1.48.jar 压缩包，右键点击 ADD as Library 

出现窗口直接默认，点击确定，完成引用MySQL驱动包

### 第一个JDBC程序

> **API使用**

| 加载注册驱动的方式              | 描述                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| Class.forName(数据库驱动实现类) | 加载和注册数据库驱动,数据库驱动由数据库厂商MySql提供"com.mysql.jdbc.Driver" |

```java
public static void main(String[] args) throws ClassNotFoundException {
        //1.注册驱动   注册驱动（jar 8以下）
        // forName 方法执行将类进行初始化
        Class.forName("com.mysql.jdbc.Driver");
}
```

> 注:5.1以后版本需要带.cj 会默认自动注册
>
> Class.forName(“com.mysql.cj.jdbc.Driver”);

> **获得连接**

Connection 接口，代表一个连接对象 ,具体的实现类由数据库的厂商实现

使用 DriverManager类的静态方法,getConnection可以获取数据库的连接

| 获取连接的静态方法                                           | 说明                                            |
| ------------------------------------------------------------ | ----------------------------------------------- |
| Connection getConnection(String url, String user,String password) | 通过连接字符串和用户名,密码来获取数据库连接对象 |

url: jdbc:mysql://localhost:3306/db4?characterEncoding=UTF-8

第一部分是协议 jdbc，这是固定的；

第二部分是子协议，就是数据库名称，连接mysql数据库，第二部分当然是mysql了；

第三部分是由数据库厂商规定的，我们需要了解每个数据库厂商的要求，mysql的第三部分分别由数据库服务器的IP地址（localhost）、端口号（3306），以及要使用的数据库名称组成。

```java
public static void main(String[] args) throws ClassNotFoundException, SQLException {
        //1.注册驱动
        Class.forName("com.mysql.jdbc.Driver");
        //2.获取连接 url,用户名, 密码
        String url = "jdbc:mysql://localhost:3306/db4";
        Connection con = DriverManager.getConnection(url, "root", "123456");
        //com.mysql.jdbc.JDBC4Connection@2e3fc542
        System.out.println(con);
 }
```

> **获取语句执行平台**

通过Connection 的 createStatement方法 获取sql语句执行对象

| Connection接口中的方法      | 说明                 |
| --------------------------- | -------------------- |
| Statement createStatement() | 创建 SQL语句执行对象 |

Statement ：代表一条语句对象，用于发送 SQL 语句给服务器，用于执行静态SQL语句并返回它所生成结果的对象。

Statement类常用方法：

int executeUpdate(String sql);	执行insert update delete语句,返回int类型,代表受影响的行数

ResultSet executeQuery(Stringsql);	执行select语句, 返回ResultSet结果集对象

```java
 public static void main(String[] args) throws Exception {
		//1.注册驱动
        Class.forName("com.mysql.jdbc.Driver");
		//2.获取连接 url,用户名, 密码
        String url = "jdbc:mysql://localhost:3306/db4";
        Connection con = DriverManager.getConnection(url, "root", "123456");
		//3.获取 Statement对象
        Statement statement = con.createStatement();
		//4.执行创建表操作
        String sql = "create table test01(id int,name varchar(20),age int);";
		//5.增删改操作 使用executeUpdate,增加一张表
        int i = statement.executeUpdate(sql);
		//6.返回值是受影响的函数
        System.out.println(i);
		//7.关闭流 
        statement.close();
        con.close();
}
```

> **处理结果集**

只有在进行查询操作的时候, 才会处理结果集

```java
public static void main(String[] args) throws SQLException {
        //1.注册驱动 可以省略 
        //2.获取连接
        String url = "jdbc:mysql://localhost:3306/db4";
        Connection con = DriverManager.getConnection(url, "root", "123456");
        //3.获取 Statement对象 
        Statement statement = con.createStatement();
        String sql = "select * from jdbc_user";
        //执行查询操作,返回的是一个 ResultSet 结果对象
        ResultSet resultSet = statement.executeQuery(sql);
        //4.处理结果集 resultSet
}
```

### ResultSet接口

作用：封装数据库查询的结果集，对结果集进行遍历，取出每一条记录。

```
boolean next()
```

1、游标向下一行;

2、返回 boolean 类型，如果还有下一条记录，返回 true，否则返回 false

```
xxx getXxx( String or int)
```

1、通过列名，参数是 String 类型。返回不同的类型

2、通过列号，参数是整数，从1开始。返回不同的类型

```java
public static void main(String[] args) throws SQLException {
        //1.注册驱动 可以省略
        //2.获取连接
        String url = "jdbc:mysql://localhost:3306/db4";
        Connection con = DriverManager.getConnection(url, "root", "123456");
        //3.获取 Statement对象
        Statement statement = con.createStatement();
        String sql = "select * from jdbc_user";
        //执行查询操作,返回的是一个 ResultSet 结果对象
        ResultSet resultSet = statement.executeQuery(sql);
        //4.处理结果集
        //next 方法判断是否还有下一条数据
        // boolean next = resultSet.next();
        // System.out.println(next);
        //getXXX 方法获取数据 两种方式
        // int id = resultSet.getInt("id");//列名
        // System.out.println(id);
        int anInt = resultSet.getInt(1);//列号
        // System.out.println(anInt);
        //使用while循环
        while(resultSet.next()){
            //获取id
            int id = resultSet.getInt("id");
            //获取姓名
            String username = resultSet.getString("username");
            //获取生日
            Date birthday = resultSet.getDate("birthday");
            System.out.println(id + " = " +username + " : " + birthday);
        }
        //关闭连接
        resultSet.close();
        statement.close();
        con.close();
}
```

### 释放资源

需要释放的对象：ResultSet 结果集，Statement 语句，Connection 连接

释放原则：先开的后关，后开的先关。ResultSet ==> Statement ==> Connection

放在哪个代码块中：finally 块

与IO流一样，使用后的东西都需要关闭！关闭的顺序是先开后关, 先得到的后关闭，后得到的先关闭

```java
public static void main(String[] args) {
        Connection connection = null;
        Statement statement = null;
        ResultSet resultSet = null;
        try {
            //1.注册驱动（省略） 
            //2.获取连接 
            String url = "jdbc:mysql://localhost:3306/db4";
            connection = DriverManager.getConnection(url, "root", "123456");
            //3.获取 Statement对象 
            statement = connection.createStatement();
            String sql = "select * from jdbc_user";
            resultSet = statement.executeQuery(sql);
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            /**
             * 开启顺序: connection ==> statement => resultSet 
             * 关闭顺序: resultSet ==> statement ==> connection 
             */
            try {
                connection.close();
                resultSet.close();
                statement.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
}
```

### JDBC流程

> 创建工程，导入驱动jar包

注册驱动（jar 8以下）

```Java
Class.forName("com.mysql.jdbc.Driver");
```

获取连接

```java
Connection conn = DriverManager.getConnection(url, username, password);
```

> Java代码需要发送SQL给MySQL服务端，就需要先建立连接

定义SQL语句

  ```java
String sql =  “update…” ;
  ```

获取执行SQL对象

执行SQL语句需要SQL执行对象，而这个执行对象就是Statement对象

  ```java
Statement stmt = conn.createStatement();
  ```

 Statement stmt = conn.createStatement();

执行SQL

```java
stmt.executeUpdate(sql);  
```

> 处理返回结果 

> 释放资源

```java
xxxx.close();
```

## JDBC增删改查

 **JDBC工具类**

什么时候自己创建工具类？

如果一个功能经常要用到，我们建议把这个功能做成一个工具类，可以在不同的地方重用。

“获得数据库连接”操作，将在以后的增删改查所有功能中都存在，可以封装工具类JDBCUtils。提供获取连接对象的方法，从而达到代码的重复利用。

工具类包含的内容

可以把几个字符串定义成常量：用户名，密码，URL，驱动类

得到数据库的连接：getConnection()

关闭所有打开的资源：

```java
public class JdbcUtils {
    //定义字符串常量, 记录获取连接所需要的信息
    public static final String driver = "com.mysql.jdbc.Driver";
    public static final String url = "jdbc:mysql://localhost:3306/school?useSSL=false";
    public static final String username = "root";
    public static final String password = "123456";
	//静态代码块, 随着类的加载而加载
    static{
        try {
            Class.forName(driver);
        } catch (ClassNotFoundException e) {
            e.printStackTrace(); 
            throw new RuntimeException(e);
        }
    }
    //获取连接的静态方法
    public static Connection getConnection(){
        Connection conn =null;
        try {
            conn = DriverManager.getConnection(url, username, password);
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
        //返回连接对象
        return conn;
    }
    //关闭资源的方法
    public static void close(ResultSet resultSet){
        try {
            if (resultSet != null){
                resultSet.close();
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }
    public static void close(Statement statement){
        try {
            if (statement != null){
                statement.close();
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }
    public static void close(Connection connection){
        try {
            if (connection != null){
                connection.close();
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }
	//方法重载 关闭资源的方法
    public static void close(ResultSet resultSet,Statement statement,Connection connection){
        close(resultSet);
        close(statement);
        close(connection);
    }
}
```

### DML操作

**解决插入中文乱码问题**

```java
jdbc:mysql://localhost:3306/db4?characterEncoding=UTF-8
//characterEncoding=UTF-8 指定字符的编码、解码格式
```

```java
public void testInsert() throws SQLException {
        //1.通过工具类获取连接
        Connection connection = JDBCUtils.getConnection();
        //2.获取Statement
        Statement statement = connection.createStatement();
        //2.1 编写Sql
        String sql = "insert into jdbc_user values(null,'张百万','123','2020/1/1')";
        //2.2 执行Sql
        int i = statement.executeUpdate(sql);
        System.out.println(i);
        //3.关闭流
        JDBCUtils.close(connection,statement);
}
```

### 更新记录

```java
//修改id为1的用户名为广坤
public void testUpdate() throws SQLException {
        Connection connection = JDBCUtils.getConnection();
        Statement statement = connection.createStatement();
        String sql = "update jdbc_user set username = '广坤' where id = 1";
        statement.executeUpdate(sql);
        JDBCUtils.close(connection,statement);
}
```

###  删除记录

```java
//删除id为3和4的记录
public void testDelete() throws SQLException {
        Connection connection = JDBCUtils.getConnection();
        Statement statement = connection.createStatement();
        statement.executeUpdate("delete from jdbc_user where id in(3,4)");
        JDBCUtils.close(connection,statement);
}
```

### DQL操作

```java
//查询姓名为张百万的一条记录
public static void main(String[] args) throws SQLException {
        //1.获取连接对象
        Connection connection = JDBCUtils.getConnection();
        //2.获取Statement对象
        Statement statement = connection.createStatement();
        String sql = "SELECT * FROM jdbc_user WHERE username = '张百万';";
        ResultSet resultSet = statement.executeQuery(sql);
        //3.处理结果集
        while(resultSet.next()){
        //通过列名 获取字段信息
            int id = resultSet.getInt("id");
            String username = resultSet.getString("username");
            String password = resultSet.getString("password");
            String birthday = resultSet.getString("birthday");
            System.out.println(id+" "+username+" " + password +" " + birthday);
        }
        //4.释放资源
        JDBCUtils.close(connection,statement,resultSet);
}
```

## SQL注入

**SQL注入问题**

```sql
-- 向jdbc_user表中 插入两条数据
INSERT INTO jdbc_user VALUES(NULL,'jack','123456','2020/2/24');
INSERT INTO jdbc_user VALUES(NULL,'tom','123456','2020/2/24');
```

```sql
## SQL注入演示
-- 填写一个错误的密码
SELECT * FROM jdbc_user WHERE username = 'tom' AND PASSWORD = '123' OR '1' = '1';
```

> 如果这是一个登陆操作,那么用户就登陆成功了.显然这不是我们想要看到的结果

**用户登陆**

用户在控制台上输入用户名和密码, 然后使用 Statement 字符串拼接的方式 实现用户的登录

步骤:

- 得到用户从控制台上输入的用户名和密码来查询数据库
- 写一个登录的方法
  - 通过工具类得到连接
  - 创建语句对象，使用拼接字符串的方式生成 SQL 语句
  - 查询数据库，如果有记录则表示登录成功，否则登录失败
  - 释放资源

```java
/*用户登录案例
     使用 Statement字符串拼接的方式完成查询*/
    public static void main(String[] args) throws SQLException {
        //1.获取连接
        Connection connection = JDBCUtils.getConnection();
        //2.获取Statement
        Statement statement = connection.createStatement();
        //3.获取用户输入的用户名和密码
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入用户名: ");
        String name = sc.nextLine();
        System.out.println("请输入密码: ");
        String pass = sc.nextLine();
        System.out.println(pass);
        //4.拼接Sql,执行查询
        // String pass = "xxx' or '1'='1";
        String sql = "select * from jdbc_user where username ='"+name+"' and password ='"+pass+"';";
        System.out.println(sql);
        ResultSet resultSet = statement.executeQuery(sql);
        //5.处理结果集,判断结果集是否为空
        if(resultSet.next()){
            System.out.println("登录成功! 欢迎您: " + name);
        }else {
            System.out.println("登录失败!");
        }
        //释放资源
        JDBCUtils.close(connection,statement,resultSet);
}
```

**问题分析：**

1. 什么是SQL注入?
   我们让用户输入的密码和 SQL 语句进行字符串拼接。用户输入的内容作为了 SQL 语句语法的一部分，改变了 原有SQL 真正的意义，以上问题称为 SQL 注入 
2. 如何实现的注入
   根据用户输入的数据,拼接处的字符串

```sql
select * from jdbc_user where username = 'abc' and password = 'abc' or '1'='1';
/*name='abc' and password='abc' 为假'1'='1' 真
相当于 select * from user where true=true;查询了所有记录*/
```

> 要解决 SQL 注入就不能让用户输入的密码和我们的 SQL 语句进行简单的字符串拼接

## 预处理对象

**PreparedStatement 接口**

PreparedStatement 是 Statement 接口的子接口，继承于父接口中所有的方法。它是一个预编译的 SQL 语句对象

预编译: 是指SQL 语句被预编译,并存储在 PreparedStatement 对象中。然后可以使用此对象多次高效地执行该语句。

**PreparedStatement 特点**

因为有预先编译的功能，提高 SQL 的执行效率。

可以有效的防止 SQL 注入的问题，安全性更高

**获取PreparedStatement对象**

通过Connection创建PreparedStatement对象

| Connection 接口中的方法                        | 说明                                                         |
| ---------------------------------------------- | ------------------------------------------------------------ |
| PreparedStatement prepareStatement(String sql) | 指定预编译的 SQL 语句，SQL 语句中使用占位符 ? 创建一个语句对象 |

**PreparedStatement接口常用方法**

| 常用方法                  | 说明                                   |
| ------------------------- | -------------------------------------- |
| int executeUpdate();      | 执行insert update delete语句           |
| ResultSet executeQuery(); | 执行select语句. 返回结果集对象 Resulet |

> 编写 SQL 语句，未知内容使用?占位：

```slq
"SELECT * FROM jdbc_user WHERE username=? AND password=?";
```

| setXxx重载方法                               | 说明                                   |
| -------------------------------------------- | -------------------------------------- |
| ResultSet executeQuery();                    | 执行select语句. 返回结果集对象 Resulet |
| void setDouble(int parameterIndex, double x) | 将指定参数设置为给定 Java double 值。  |
| void setString(int parameterIndex, String x) | 将指定参数设置为给定 Java String 值。  |
| void setObject(int parameterIndex, Object x) | 使用给定对象设置指定参数的值。         |
### PreparedStatement完成登录案例

> 使用 PreparedStatement 预处理对象,可以有效的避免SQL注入

```java
public static void main(String[] args) throws SQLException {
        //1.获取连接 
        Connection connection = JDBCUtils.getConnection();
        //2.获取Statement 
        Statement statement = connection.createStatement();
        //3.获取用户输入的用户名和密码
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入用户名: ");
        String name = sc.nextLine();
        System.out.println("请输入密码: ");
        String pass = sc.nextLine();
        System.out.println(pass);
        //4.获取 PrepareStatement 预编译对象
        //4.1 编写SQL 使用 ? 占位符方式
        String sql = "select * from jdbc_user where username = ? and password = ?";
        PreparedStatement ps = connection.prepareStatement(sql);
        //4.2 设置占位符参数
        ps.setString(1,name);
        ps.setString(2,pass);
        //5. 执行查询 处理结果集
        ResultSet resultSet = ps.executeQuery();
        if(resultSet.next()){
            System.out.println("登录成功! 欢迎您: " + name);
        }else{
            System.out.println("登录失败!");
        }
        //6.释放资源 
        JDBCUtils.close(connection,statement,resultSet);
}
```

### PreparedStatement的执行原理

> 分别使用 Statement对象 和 PreparedStatement对象进行插入操作

```java
public static void main(String[] args) throws SQLException {
        Connection con = JDBCUtils.getConnection();
        //获取 Sql语句执行对象 
        Statement st = con.createStatement();
        //插入两条数据 
        st.executeUpdate("insert into jdbc_user values(null,'张三','123','1992/12/26')");
        st.executeUpdate("insert into jdbc_user values(null,'李四','123','1992/12/26')");

        //获取预处理对象 
        PreparedStatement ps = con.prepareStatement("insert into jdbc_user values(?,?,?,?)");
        //第一条数 设置占位符对应的参数 
        ps.setString(1,null);
        ps.setString(2,"hd");
        ps.setString(3,"qwer");
        ps.setString(4,"2000/1/10");
        //执行插入 
        ps.executeUpdate();
        //第二条数据 
        ps.setString(1,null);
        ps.setString(2,"jc");
        ps.setString(3,"1122");
        ps.setString(4,"2000/1/10");
        //执行插入 
        ps.executeUpdate();
        //释放资源 
        st.close();
        ps.close();
        con.close();
    }
```

![Prepared](https://s1.328888.xyz/2022/09/26/ViHfP.png)

**Statement 与 PreparedStatement的区别**

Statement用于执行静态SQL语句，在执行时，必须指定一个事先准备好的SQL语句。

PrepareStatement是预编译的SQL语句对象，语句中可以包含动态参数“?”，在执行时可以为“?”动态设置参数值。

PrepareStatement可以减少编译次数提高数据库性能。

## JDBC 控制事务

**数据准备**

```sql
-- 创建账户表
    CREATE TABLE account(
	-- 主键
    id INT PRIMARY KEY AUTO_INCREMENT,
	-- 姓名
    NAME VARCHAR(10),
	-- 转账金额
    money DOUBLE
);
-- 添加两个用户
    INSERT INTO account (NAME, money) VALUES ('tom', 1000), ('jack', 1000);
```

**事务相关API**

| 方法                                   | 说明                                                         |
| -------------------------------------- | ------------------------------------------------------------ |
| void setAutoCommit(boolean autoCommit) | 参数是 true 或 false 如果设置为 false，表示关闭自动提交，相当于开启事务 |
| void commit()                          | 提交事务                                                     |
| void rollback()                        | 回滚事务                                                     |

**开发步骤**

- 获取连接
- 开启事务
- 获取到 PreparedStatement , 执行两次更新操作
- 正常情况下提交事务
- 出现异常回滚事务
- 最后关闭资源

```java
public static void main(String[] args) {
        Connection con = null;
        PreparedStatement ps = null;
        try {
            //1. 获取连接 
            con = JDBCUtils.getConnection();
            //2. 开启事务 
            con.setAutoCommit(false);
            //3. 获取到 PreparedStatement 执行两次更新操作 
            //3.1 tom 账户 -500 
            ps = con.prepareStatement("update account set money = money - ? where name = ? ");
            ps.setDouble(1,500.0);
            ps.setString(2,"tom");
            ps.executeUpdate();
            //模拟tom转账后 出现异常 
            System.out.println(1 / 0);
            //3.2 jack 账户 +500 
            ps = con.prepareStatement("update account set money = money + ? where name = ? ");
            ps.setDouble(1,500.0);
            ps.setString(2,"jack");
            ps.executeUpdate();
            //4. 正常情况下提交事务 
            con.commit();
            System.out.println("转账成功!");
        } catch (SQLException e) {
            e.printStackTrace();
            try {
                //5. 出现异常回滚事务 
                con.rollback();
            } catch (SQLException ex) {
                ex.printStackTrace();
            }
        } finally {
            //6. 最后关闭资源 
            JDBCUtils.close(con,ps);
        }
}
```

## 数据库连接池

**连接池介绍**

实际开发中“获得连接”或“释放资源”是非常消耗系统资源的两个过程，为了解决此类性能问题，通常情况我们 采用连接池技术，来共享连接Connection。这样我们就不需要每次都创建连接、释放连接了，这些操作都交给了连接池.

**连接池的好处**

用池来管理Connection，这样可以重复使用Connection。 当使用完Connection后，调用Connection的close()方法也不会真的关闭Connection，而是把Connection“归还”给池。

Java为数据库连接池提供了公共的接口:javax.sql.DataSource，各个厂商需要让自己的连接池实现这个接口。这样应用程序可以方便的切换不同厂商的连接池!

常见的连接池有 DBCP连接池, C3P0连接池, Druid连接池

Druid（德鲁伊）是阿里巴巴开发的号称为监控而生的数据库连接池，Druid是目前最好的数据库连接池。在功能、性能、扩展性方面，都超过其他数据库连接池，同时加入了日志监控，可以很好的监控DB池连接和SQL的执行情况。

**数据准备**

```sql
#创建数据库
CREATE DATABASE db5 CHARACTER SET utf8;
#使用数据库
USE db5;
#创建员工表
CREATE TABLE employee (
       eid INT PRIMARY KEY AUTO_INCREMENT,
       ename VARCHAR (20),-- 员工姓名
       age INT,-- 员工年龄
       sex VARCHAR (6), -- 员工性别
       salary DOUBLE, -- 薪水
       empdate DATE -- 入职日期
);
#插入数据
INSERT INTO employee (eid, ename, age, sex, salary, empdate) VALUES(NULL,'李清照',22,'女',4000,'2018-11-12');
INSERT INTO employee (eid, ename, age, sex, salary, empdate) VALUES(NULL,'林黛玉',20,'女',5000,'2019-03-14');
INSERT INTO employee (eid, ename, age, sex, salary, empdate) VALUES(NULL,'杜甫',40,'男',6000,'2020-01-01');
INSERT INTO employee (eid, ename, age, sex, salary, empdate) VALUES(NULL,'李白',25,'男',3000,'2017-10-01');
```

**导入 jar包 配置文件**

在项目根目录 lib 文件夹里存入 druid-1.1.12.jar 压缩包

打开IDEA，找到   druid-1.1.12.jar 压缩包，右键点击 ADD as Library 

出现窗口直接默认，点击确定，完成引用MySQL驱动包

在 src 目录下右键创建 druid.properties 存入以下代码

```jso
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql:///db1?useSSL=false&useServerPrepStmts=true&characterEncoding=UTF-8
username=root
password=123456
#初始化连接数量
initialSize=5
#最大连接数
maxActive=10
#最大等待时间
maxWait=3000
```

### 编写Druid工具类

获取数据库连接池对象
通过工厂来来获取 DruidDataSourceFactory类的createDataSource方法
createDataSource(Properties p) 方法参数可以是一个属性集对象

```java
public class DruidUtils {
        //1.定义成员变量 
        public static DataSource dataSource;
        //2.静态代码块 
        static{
            try {
                //3.创建属性集对象 
                Properties p = new Properties();
                //4.加载配置文件 Druid 连接池不能够主动加载配置文件 ,需要指定文件 
                InputStream inputStream = DruidUtils.class.getClassLoader().getResourceAsStream("druid.properties");
                //5. 使用Properties对象的 load方法 从字节流中读取配置信息 
                p.load(inputStream);
                //6. 通过工厂类获取连接池对象 
                dataSource = DruidDataSourceFactory.createDataSource(p);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }

        //获取连接的方法 
        public static Connection getConnection(){
            try {
                return dataSource.getConnection();
            } catch (SQLException e) {
                e.printStackTrace();
                return null;
            }
        }
        //释放资源 
        public static void close(Connection con, Statement statement){
            if(con != null && statement != null){
                try {
                    statement.close();
                    //归还连接 
                    con.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
        public static void close(Connection con, Statement statement, ResultSet resultSet){
            if(con != null && statement != null && resultSet != null){
                try {
                    resultSet.close();
                    statement.close();
                    //归还连接 
                    con.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
}
```

### 测试工具类

```java
//需求 查询 薪资在3000 到 5000之间的员工的姓名 
    public static void main(String[] args) throws SQLException {
        //1.获取连接 
        Connection con = DruidUtils.getConnection();
        //2.获取Statement对象 
        Statement statement = con.createStatement();
        //3.执行查询 
        ResultSet resultSet = statement.executeQuery("select ename from employee where salary between 3000 and 5000");
        //4.处理结果集 
        while(resultSet.next()){
            String ename = resultSet.getString("ename");
            System.out.println(ename);
        }
        //5.释放资源 
        DruidUtils.close(con,statement,resultSet);
    }
```

> 对象数组接收 sql 数据

```java
public static void main(String[] args) throws SQLException {
        Connection conn = DruidUtils.getConnection();
        Statement statement = conn.createStatement();
        ResultSet resultSet = statement.executeQuery("select * FROM employee");
        List<Student> students = new ArrayList<>();
        while (resultSet.next()){
            Student student = new Student();
            String name =resultSet.getString("ename");
            int age = resultSet.getInt("age");
            student.setName(name);
            student.setAge(age);
            System.out.println(student);
        }
        DruidUtils.close(resultSet,statement,conn);
}
```

```java
public class Student {
    String name;
    int age;

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

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

## DBUtils工具类

**DBUtils简介**

使用JDBC我们发现冗余的代码太多了,为了简化开发 我们选择使用 DbUtils

Commons DbUtils是Apache组织提供的一个对JDBC进行简单封装的开源工具类库，使用它能够简化JDBC应用程序的开发，同时也不会影响程序的性能。

使用方式:

DBUtils就是JDBC的简化开发工具包。需要项目导入**commons-dbutils-1.6.jar**。

**Dbutils核心功能介绍**

- **QueryRunner** 中提供对sql语句操作的API.
- **ResultSetHandler**接口，用于定义select操作后，怎样封装结果集.
- DbUtils类,他就是一个工具类,定义了关闭资源与事务处理相关方法.

**JavaBean组件**

JavaBean 就是一个类, 开发中通常用于封装数据,有一下特点

1. 需要实现 序列化接口, Serializable (暂时可以省略)

1. 提供私有字段: private 类型 变量名;

1. 提供 getter 和 setter

1. 提供 空参构造

创建Employee类和数据库的employee表对应，我们可以创建一个 entity包,专门用来存放 JavaBean类

### QueryRunner核心类

**构造方法**

- QueryRunner()

- QueryRunner(DataSource ds) ,提供数据源（连接池），DBUtils底层自动维护连接connection

**常用方法**

- update(Connection conn, String sql, Object… params) ，用来完成表数据的增加、删除、更新操作

- query(Connection conn, String sql, ResultSetHandler rsh, Object… params) ，用来完成表数据的查询操作

```java
//手动方式 创建QueryRunner对象具体使用到的时候在给信息
QueryRunner qr = new QueryRunner();
//自动创建 传入数据库连接池对象  直接给DataSource
QueryRunner qr2 = new QueryRunner(DruidUtils.getDataSource());
```

> 工具类需要返回dataSource

```java
//获取连接池对象
public static DataSource getDataSource(){
	return dataSource;
}
```

### 增、删、改操作

**核心方法**

- update(Connection conn, String sql, Object… params)

- Object... param Object类型的 可变参,用来设置占位符上的参数

**步骤:**

1.创建QueryRunner(手动或自动)

2.占位符方式 编写SQL

3.设置占位符参数

4.执行

>添加

```java
@Test
    public void testInsert() throws SQLException {
        //1.创建 QueryRunner 手动模式创建
        QueryRunner qr = new QueryRunner();

        //2.编写 占位符方式
        String sql = "insert into employee values(?,?,?,?,?,?)";

        //3.设置占位符的参数
        Object[] param = {null,"张百万",20,"女",10000,"1990-12-26"};

        //4.执行 update方法
        Connection con = DruidUtils.getConnection();
        int i = qr.update(con, sql, param);

        //5.释放资源
        DbUtils.closeQuietly(con);
    }
```

> 修改

```java
//修改操作 修改姓名为张百万的员工工资 
    @Test
    public void testUpdate() throws SQLException {
        //1.创建QueryRunner对象 自动模式,传入数据库连接池 
        QueryRunner qr = new QueryRunner(DruidUtils.getDataSource());

        //2.编写SQL 
        String sql = "update employee set salary = ? where ename = ?";

        //3.设置占位符参数 
        Object[] param = {0,"张百万"};

        //4.执行update, 不需要传入连接对象 
        qr.update(sql,param);
    }
```

> 删除

```java
//删除操作 删除id为1 的数据 
    @Test
    public void testDelete() throws SQLException {
        QueryRunner qr = new QueryRunner(DruidUtils.getDataSource());
        String sql = "delete from employee where eid = ?";
        //只有一个参数,不需要创建数组 
        qr.update(sql,1);
    }
```

### 实现查询操作

**ResultSetHandler接口简介**

ResultSetHandler可以对查询出来的ResultSet结果集进行处理，达到一些业务上的需求。

**ResultSetHandler 结果集处理类**

本例展示的是使用ResultSetHandler接口的几个常见实现类实现数据库的增删改查，可以大大减少代码量，优化程序。

每一种实现类都代表了对查询结果集的一种处理方式

**ResultSetHandler 实现类**	

- ArrayHandler	将结果集中的第一条记录封装到一个Object[]数组中，数组中的每一个元素就是这条记录中的每一个字段的值 id,ename,eage

- ArrayListHandler	将结果集中的每一条记录都封装到一个Object[]数组中，将这些数组在封装到List集合中。

- BeanHandler	将结果集中第一条记录封装到一个指定的javaBean中.

- BeanListHandler	将结果集中每一条记录封装到指定的javaBean中，再将这些javaBean在封装到List集合中

- ColumnListHandler	将结果集中指定的列的字段值，封装到一个List集合中

- KeyedHandler	将结果集中每一条记录封装到Map<String,Object>,在将这个map集合做为另一个Map的value,另一个Map集合的key是指定的字段的值。

- MapHandler	将结果集中第一条记录封装到了Map<String,Object>集合中，key就是字段名称，value就是字段值

- MapListHandler	将结果集中每一条记录封装到了Map<String,Object>集合中，key就是字段名称，value就是字段值，在将这些Map封装到List集合中。

- ScalarHandler	它是用于封装单个数据。例如 select count(*) from 表操作。

**ResultSetHandler 常用实现类测试**

- QueryRunner的查询方法

- query方法的返回值都是泛型,具体的返回值类型,会根据结果集的处理方式,发生变化

**方法**	

- query(String sql, handler ,Object[] param)	自动模式创建QueryRunner, 执行查询

- query(Connection con,String sql,handler,Object[] param)	手动模式创建QueryRunner, 执行查询

> 查询id为5的记录,封装到数组中

```java
	/**查询id为5的记录,封装到数组中 
     * ArrayHandler 将结果集的第一条数据封装到数组中 
     */
    @Test
    public void testFindById() throws SQLException {
        //1.创建QueryRunner 
        QueryRunner qr = new QueryRunner(DruidUtils.getDataSource());
        //2.编写SQL 
        String sql = "select * from employee where eid = ?";
        //3.执行查询 
        Object[] query = qr.query(sql, new ArrayHandler(), 5);
        //4.获取数据 
        System.out.println(Arrays.toString(query));
    }
```

> 查询所有数据,封装到List集合中

```java
	/**
     * 查询所有数据,封装到List集合中  
     * ArrayListHandler可以将每条数据先封装到数组中, 再将数组封装到集合中 
     */
    @Test
    public void testFindAll() throws SQLException {
        //1.创建QueryRunner 
        QueryRunner qr = new QueryRunner(DruidUtils.getDataSource());
        //2.编写SQL 
        String sql = "select * from employee";
        //3.执行查询 
        List<Object[]> query = qr.query(sql, new ArrayListHandler());
        //4.遍历集合获取数据 
        for (Object[] objects : query) {
            System.out.println(Arrays.toString(objects));
        }
    }
```

> 根据ID查询,封装到指定JavaBean中

```java
	/**
     * 查询id为3的记录,封装到指定JavaBean中 
     * BeanHandler 将结果集的第一条数据封装到 javaBean中 
     */
    @Test
    public void testFindByIdJavaBean() throws SQLException {
        QueryRunner qr = new QueryRunner(DruidUtils.getDataSource());
        String sql = "select * from employee where eid = ?";
        Employee employee = qr.query(sql,
                new BeanHandler<Employee>(Employee.class), 3);
        System.out.println(employee);
    }
```

> 查询薪资大于 3000 的所员工信息,封装到JavaBean中再封装到List集合中

```java
	/**
     * 查询薪资大于 3000 的所员工信息,封装到JavaBean中再封装到List集合中 
     * BeanListHandler 将结果集的每一条和数据封装到 JavaBean中 
     * 再将JavaBean 放到list集合中 
     **/
    @Test
    public void testFindBySalary() throws SQLException {
        QueryRunner qr = new QueryRunner(DruidUtils.getDataSource());
        String sql = "select * from employee where salary > ?";
        List<Employee> list = qr.query(sql,
                new BeanListHandler<Employee>(Employee.class), 3000);
        for (Employee employee : list) {
            System.out.println(employee);
        }
    }
```

> 查询姓名是 张百万的员工信息,将结果封装到Map集合中

```java
	/**
     * 查询姓名是 张百万的员工信息,将结果封装到Map集合中 
     * MapHandler 将结果集的第一条记录封装到 Map<String,Object>中 
     * key对应的是 列名 value对应的是 列的值 
     **/
    @Test
    public void testFindByName() throws SQLException {
        QueryRunner qr = new QueryRunner(DruidUtils.getDataSource());
        String sql = "select * from employee where ename = ?";
        Map<String, Object> map = qr.query(sql, new MapHandler(), "张百万");
        Set<Map.Entry<String, Object>> entries = map.entrySet();
        for (Map.Entry<String, Object> entry : entries) {
            //打印结果 
            System.out.println(entry.getKey() +" = " +entry.getValue());
        }
    }
```

> 查询所有员工的薪资总额

```java
	/**
     * 查询所有员工的薪资总额 
     * ScalarHandler 用于封装单个的数据 
     **/
    @Test
    public void testGetSum() throws SQLException {
        QueryRunner qr = new QueryRunner(DruidUtils.getDataSource());
        String sql = "select sum(salary) from employee";
        Double sum = (Double)qr.query(sql, new ScalarHandler<>());
        System.out.println("员工薪资总额: " + sum);
    }
```

## MySql元数据

**除了表之外的数据都是元数据,可以分为三类**

- 查询结果信息： UPDATE 或 DELETE语句 受影响的记录数。

- 数据库和数据表的信息： 包含了数据库及数据表的结构信息。

- MySQL服务器信息： 包含了数据库服务器的当前状态，版本号等。

**常用命令**

```sql
-- 元数据相关的命令介绍
-- 1.查看服务器当前状态
show status;
-- 2.查看MySQl的版本信息
select version();
-- 3.查询表中的详细信息   和desc table_name一样
show columns from table_name;
-- 4.显示数据表的详细索引信息
show index from table_name;
-- 5.列出所有数据库 
show databases;
-- 6.显示当前数据库的所有表
show tables;
-- 7.获取当前的数据库名
select database();
```

> 使用JDBC 获取元数据

通过JDBC 也可以获取到元数据,比如数据库的相关信息,或者当我们使用程序查询一个不熟悉的表时, 我们可以通过获取元素据信息,了解表中有多少个字段,字段的名称 和 字段的类型.

> JDBC中描述元数据的类

| 元数据类          | 作用                   |
| ----------------- | ---------------------- |
| DatabaseMetaData  | 描述数据库的元数据对象 |
| ResultSetMetaData | 描述结果集的元数据对象 |

- 获取元数据对象的方法 : getMetaData ()
  - connection 连接对象, 调用 getMetaData () 方法,获取的是DatabaseMetaData 数据库元数据对象
  - PrepareStatement 预处理对象调用 getMetaData () , 获取的是ResultSetMetaData , 结果集元数据对象

- DatabaseMetaData的常用方法
  - getURL() : 获取数据库的URL
  - getUserName(): 获取当前数据库的用户名
  - getDatabaseProductName(): 获取数据库的产品名称
  - getDatabaseProductVersion(): 获取数据的版本号
  - getDriverName(): 返回驱动程序的名称
  - isReadOnly(): 判断数据库是否只允许只读 true 代表只读

- ResultSetMetaData的常用方法
  - getColumnCount() : 当前结果集共有多少列
  - getColumnName(int i) : 获取指定列号的列名, 参数是整数 从1开始
  - getColumnTypeName(int i): 获取指定列号列的类型, 参数是整数 从1开始

```java
//1.获取数据库相关的元数据信息 使用DatabaseMetaData 
    @Test
    public void testDataBaseMetaData() throws SQLException {
        //1.获取数据库连接对象 
        Connection connection = DruidUtils.getConnection();
        //2.获取代表数据库的 元数据对象 
        DatabaseMetaData DatabaseMetaData metaData = connection.getMetaData();
        //3.获取数据库相关的元数据信息 
        String url = metaData.getURL();
        System.out.println("数据库URL: " + url);
        String userName = metaData.getUserName();
        System.out.println("当前用户: " + userName );
        String productName = metaData.getDatabaseProductName();
        System.out.println("数据库产品名: " + productName);
        String version = metaData.getDatabaseProductVersion();
        System.out.println("数据库版本: " + version);

        String driverName = metaData.getDriverName();
        System.out.println("驱动名称: " + driverName);
        //判断当前数据库是否只允许只读 
        boolean b = metaData.isReadOnly();
        //如果是 true 就表示 只读 
        if(b){
            System.out.println("当前数据库只允许读操作!");
        }else{
            System.out.println("不是只读数据库");
        }
        connection.close();
    }
    //获取结果集中的元数据信息 
    @Test
    public void testResultSetMetaData() throws SQLException {
        //1.获取连接 
        Connection con = DruidUtils.getConnection();
        //2.获取预处理对象 
        PreparedStatement ps = con.prepareStatement("select * from employee");
        ResultSet resultSet = ps.executeQuery();
        //3.获取结果集元素据对象 
        ResultSetMetaData metaData = ps.getMetaData();
        //1.获取当前结果集 共有多少列 
        int count = metaData.getColumnCount();
        System.out.println("当前结果集中共有: " + count + " 列");
        //2.获结果集中 列的名称 和 类型 
        for (int i = 1; i <= count; i++) {
            String columnName = metaData.getColumnName(i);
            System.out.println("列名: "+ columnName);
            String columnTypeName = metaData.getColumnTypeName(i);
            System.out.println("类型: " +columnTypeName);
        }
    //释放资源 
        DruidUtils.close(con,ps,resultSet);
    }
```

## Dao模式

**什么是Dao模式**

DAO（Data Access Object）顾名思义是一个为数据库或其他持久化机制提供了抽象接口的对象，在不暴露底层持久化方案实现细节的前提下提供了各种数据访问操作

**为什么要使用DAO模式**

在目前的企业应用系统设计中，MVC，即 Model（模型）- View（视图）- Control（控制）为主要的系统架构模式。MVC 中的 Model 包含了复杂的业务逻辑和数据逻辑，以及数据存取机制（如 JDBC的连接、SQL生成和Statement创建、还有ResultSet结果集的读取等）等。将这些复杂的业务逻辑和数据逻辑分离，以将系统的紧耦合关系转化为松耦合关系（即解耦合），是降低系统耦合度迫切要做的。MVC 模式需要解决2个问题：

- 将表现层（即View）和数据处理层（即Model）分离的解耦合。

- 将数据处理层内部的业务逻辑和数据访问分离的解耦合。

第一个问题可以使用控制器来解决，第二个问题可以使用DAO模式来解决。

（1）JDBC访问数据时，将业务代码和数据访问代码混在一起编写（藕合），造成程序的

-  可读性差。

-  不利于后期修改和维护。

-  不利于代码复用。

（2）用面向接口编程，可以降低代码间的耦合性。

-  隔离业务逻辑代码和数据访问代码。

-  隔离不同数据库的实现。

业务逻辑代码是指程序需要实现的功能算法，如银行ATM机实现的功能有存款、取款、转账等，这些属于程序需要实现的功能。而数据访问代码是指对存储在数据库的数据进行CRUD（增、查、改、删）操作代码。存款、取款和转账的逻辑代码是不同的，但最终都是对数据库中的余额进行修改，使用Dao模式可以将业务逻辑代码和数据访问代码分离，降低代码间的耦合性

**对象关系映射ORM**

**什么是ORM**

对象关系映射（Object Relational Mapping，简称ORM）。ORM指的是面向对象的对象模型和关系型数据库的数据结构之间的相互转换。它的作用是在关系型数据库和对象之间作一个映射，这样，我们在具体的操作数据库的时候，就不需要再去和复杂的SQL语句打交道，也不需要数据编写大量的DAO层的代码，用来从数据库保存、删除和读取对象信息，只要像平时操作对象一样操作它就可以了 。ORM很好的实现了数据持久化。数据持久化就是将内存中的数据模型转换为存储模型，以及将存储模型转换为内存中的数据模型的统称。

ORM拱了三种映射为实现数据持久化

- 类—表映射。在开发系统时，数据库中有几张表，在Java中就应该编写几个类。

- 属性—列映射。表对应的类的属性名与列名一样，数据类型与列的数据类型一样。

- 对象—行映射。一个对象可以转化为一行数据，同样，一行数据也可以转化为一个对象。

Dao模式项目结构

实体类:和数据库表格一一对应的类,单独放入一个包中,包名往往是 pojo/entity/bean,要操作的每个表格都应该有对应的实体类

emp > class Emp  

dept > class Dept  

account > class Account 

DAO 层:定义了对数据要执行那些操作的接口和实现类,包名往往是 dao/mapper,要操作的每个表格都应该有对应的接口和实现类

emp > interface EmpDao >EmpDaoImpl

dept > interface DeptDao> DeptDaoImpl

Mybatis/Spring JDBCTemplate 中,对DAO层代码进行了封装,代码编写方式会有其他变化

**简单的Java对象POJO**

**什么是POJO**

POJO（Plain Ordinary Java Object）简单的Java对象，实际就是普通JavaBeans。方便程序员使用数据库中的数据表，POJO有一些private的参数作为对象的属性。然后针对每个参数定义了get和set方法作为访问的接口。

**POJO的作用**

在MVC的设计模式，视图层、业务层、数据访问层和数据库之间都是通过JavaBean进行数据封装和传递。

- 持久化对象**Entity**：Entity称为实体类，封装持久化的数据，数据库做orm映射，一个Entity对应一数据库中一张表。

- 查询参数对象**VO**：VO（View object）被称为视图对象，html jsp 上显示的对象

- 数据转换对象**DTO**：data transfer object 数据传输对象 并不在页面上做展示，只是传输用 简化数据

- **domain** 领域模型 银行 保险 电商 物流 医疗 DDD 领域驱动设计

- 银行职员 user Account 账户 VIP 积分

### 准备测试数据

```sql
# 创建数据库
create database db6 character set utf8;
# 创建商品表
CREATE TABLE product (
       pid varchar(32)  PRIMARY KEY, -- 商品id
       pname varchar(50) , -- 商品名称
       price double, -- 商品价格
       pdesc varchar(255), -- 商品描述
       pflag int(11) -- 商品状态 1 上架 ,0 下架
);
INSERT INTO `product` VALUES
('1','小米12',2200,'小米 移动联通电信4G手机 双卡双待',0),
('2','华为Mate50',2599,'华为 双卡双待 高清大屏',0),
('3','OPPO',3000,'移动联通 双4G手机',0),
('4','华为荣耀',1499,'3GB内存标准版 黑色 移动4G手机',0),
('5','华硕台式电脑',5000,'爆款直降，满千减百',0),
('6','MacBook',6688,'128GB 闪存',0),
('7','ThinkPad',4199,'轻薄系列1)',0),
('8','联想小新',4499,'14英寸超薄笔记本电脑',0),
('9','李宁音速',500,'实战篮球鞋',0),
('10','AJ11',3300,'乔丹实战系列',0),
('11','AJ1',5800,'精神小伙系列',0);
```

**项目结构**

com.aaa.app 测试包 用于对DAO代码进行测试

com.aaa.dao dao包 数据访问层,包含所有对数据库的相关操作的类

com.aaa.entity 实体包 保存根据数据库表 对应创建的JavaBean类

com.aaa.utils 工具包 

**导入所需Jar包**

commons-dbutils-1.6.jar

druid-1.1.21.jar

mysql-connector-java-5.1.48.jar

**导入配置文件及工具类**

resource --> druid.properties

utils-------->DruidUtils

### JavaBean类创建

```java
public class Product {
 
        private String pid;
 
        private String pname;
 
        private double price;
 
        private String pdesc;
 
        private int pflag; //是否上架 1 上架 ,0 下架

        //提供 get set toString方法
}
```

### 编写DAO类

```java
public class ProductDao {
    //查询所有商品信息
    public List<Product> findProduct() throws SQLException {
        
    QueryRunner qr = new QueryRunner(DruidUtils.getDataSource());
    String sql = "select * from product";
           //查询结果是一个List集合, 使用BeanListHandler 封装结果集
    List<Product> list = qr.query(sql, new BeanListHandler<Product>(Product.class));
    return list;
    }
    //根据商品ID 获取商品
    public Product findProductById(String pid) throws SQLException {
           QueryRunner qr = new QueryRunner(DruidUtils.getDataSource());
           String sql = "select * from product where pid = ?";
           Product product = qr.query(sql, new BeanHandler<Product>(Product.class), pid);
           return product;
    }

	//2查询商品个数
    public int getCount() throws SQLException {
           QueryRunner qr = new QueryRunner(DruidUtils.getDataSource());
           String sql = "select count(*) from product";
           //获取的单列数据 ,使用ScalarHandler 封装
           Long count = (Long)qr.query(sql,new ScalarHandler<>());
           //将Lang类型转换为 int 类型,并返回
           return count.intValue();
    }
}
```

### 测试 ProductDao

```java
public class TestProductDao {
 
        ProductDao productDao = new ProductDao();
 
        @Test
        public void testFindProduct() throws SQLException {
            List<Product> list = productDao.findProduct();
            for (Product product : list) {
                System.out.println(product);
            }
        }
    
        @Test
        public void testFindProductById() throws SQLException {
            Product product = productDao.findProductById("1");
            System.out.println(product);
        }

        @Test
        public void testGetCount() throws SQLException {
            //查询商品总数量
            int count = productDao.getCount();
            System.out.println("商品个数: " + count);
        }
    }
```