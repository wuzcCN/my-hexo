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

```jso
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql:///db1?useSSL=false&useServerPrepStmts=true
username=root
password=1234
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
// 需求 查询 薪资在3000 到 5000之间的员工的姓名 
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

