---
title: MyBatis
copyright_url: https://www.aobayu.cn/2022/11/07/MyBatis/
tags: 
    - MyBatis
categories: 学习之路
date: 2022-11-7
keywords: MyBatis
description: MyBatis是一个开源、轻量级的数据持久化框架，是JDBC Hibernate的替代方案。MyBatis内部封装了 JDBC，简化了加载驱动、创建连接、创建statement等繁杂的过程，开发者只需要关注SQL语句。MyBatis支持定制化 SQL、存储过程以及高级映射，可以在实体类和SQL语句之间建立映射关系，是一种半自动化的ORM实现。--本文为自己学习中所写。
---

## mybatis

### 三层架构

软件开发常用的架构是三层架构，之所以流行是因为有着清晰的任务划分。一般包括以下三层： 

- 持久层：主要完成与数据库相关的操作，即对数据库的增删改查。 因为数据库访问的对象一般称为Data Access Object（简称DAO），所以有人把持久层叫做DAO 层。 

- 业务层：主要根据功能需求完成业务逻辑的定义和实现。 因为它主要是为上层提供服务的，所以有人把业务层叫做Service层或Business层。 

- 表现层：主要完成与最终软件使用用户的交互，需要有交互界面（UI）。 因此，有人把表现层称之为web层或View层。 

三层架构之间调用关系为:表现层调用业务层，业务层调用持久层。 各层之间必然要进行数据交互，我们一般使用java实体对象来传递数据。

### 框架

**什么是框架**

框架就是一套规范，既然是规范，你使用这个框架就要遵守这个框架所规定的约束。 框架可以理解为半成品软件，框架做好以后，接下来在它基础上进行开发。 

**为什么使用框架**

框架为我们封装好了一些冗余，且重用率低的代码。并且使用反射与动态代理机制，将代码实现了通 用性，让 开发人员把精力专注在核心的业务代码实现上。  

比如在使用servlet进行开发时，需要在servlet获取表单的参数，每次都要获取很麻烦，而框架底层 就使用反射机制和拦截器机制帮助我们获取表单的值，使用jdbc每次做专一些简单的crud的时候都必须 写sql，但使用框架就不需要这么麻烦了，直接调用方法就可以。当然，既然是使用框架，那么还是要 遵循其一些规范进行配置 

**常见的框架** 

Java世界中的框架非常的多，每一个框架都是为了解决某一部分或某些问题而存在的。下面列出在目 前企业中 流行的几种框架（一定要注意他们是用来解决哪一层问题的）：

-  持久层框架：专注于解决数据持久化的框架。常用的有mybatis、hibernate、spring jdbc等等。 

-  表现层框架：专注于解决与用户交互的框架。常见的有struts2、spring mvc等等。 

-  全栈框架: 能在各层都给出解决方案的框架。比较著名的就是spring。

我们以企业中最常用的组合为准来学习Spring + Spring MVC + mybatis（SSM）

### Mybatis入门

**为什么要学习mybatis**

原始jdbc开发存在的问题如下： 

- 数据库连接创建、释放频繁造成系统资源浪费从而影响系统性能

- sql 语句在代码中硬编码，造成代码不易维护，实际应用 sql 变化的可能较大，sql 变动需要改变java 代码。

- 查询操作时，需要手动将结果集中的数据手动封装到实体中。

应对上述问题给出的解决方案： 

-  使用数据库连接池初始化连接资源 

-  将sql语句抽取到xml配置文件中 

-  使用反射、内省等底层技术，自动将实体与表进行属性与字段的自动映射

**Mybatis简介**

MyBatis是一个优秀的基于ORM的半自动轻量级持久层框架，它对jdbc的操作数据库的过程进行封装， 使开发者只需要关注 SQL 本身，而不需要花费精力去处理例如注册驱动、创建connection、创建 statement、手动设置参数、结果集检索等jdbc繁杂的过程代码 

**ORM思想** 

ORM（Object Relational Mapping）对象关系映射 

- O（对象模型）

- 实体对象，即我们在程序中根据数据库表结构建立的一个个实体javaBean 

- R（关系型数据库的数据结构）： 

- 关系数据库领域的Relational（建立的数据库表） 

- M（映射）

- 从R（数据库）到O（对象模型）的映射，可通过XML文件映射 

实现：  

- 让实体类和数据库表进行一一对应关系  

- 先让实体类和数据库表对应  再让实体类属性和表里面字段对应  

- 不需要直接操作数据库表，直接操作表对应的实体类对象 

## 编写mybatis(核心)

**案例需求：**通过mybatis查询数据库user表的所有记录，封装到User对象中，打印到控制台上

**流程分析:**

1. 创建数据库及user表 

2. 创建maven工程，导入依赖（MySQL驱动、mybatis、junit） 

3. 编写User实体类 

4. 编写UserMapper.xml映射配置文件（ORM思想）

5. 编写SqlMapConfig.xml核心配置文件 数据库环境配置 映射关系配置的引入(引入映射配置文件的路径) 

6. 编写测试代码 

**创建user数据表** 

```sql
CREATE DATABASE `mybatis_db`;
USE `mybatis_db`;
CREATE TABLE `user` (
                        `id` int(11) NOT NULL auto_increment,
                        `username` varchar(32) NOT NULL COMMENT '用户名称',
                        `birthday` datetime default NULL COMMENT '生日',
                        `sex` char(1) default NULL COMMENT '性别',
                        `address` varchar(256) default NULL COMMENT '地址',
                        PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

insert into `user`(`id`,`username`,`birthday`,`sex`,`address`)
values (1,'zxh','2022-08-23 00:00:00','男','河南郑州'),
       (2,'gy','2022-08-24 00:00:00','男','河南郑州');
```

**导入MyBatis的坐标和其他相关坐标**

```xml
		<!--mysql驱动坐标-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.38</version>
            <scope>runtime</scope>
        </dependency>
		<!--mybatis坐标-->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.4</version>
        </dependency>
      	<!--单元测试坐标-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
```

**编写User实体**

com.example.demo2.domain

User.java

```java
public class User {
    private Integer id;
    private String username;
    private Date birthday;
    private String sex;
    private String address;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public Date getBirthday() {
        return birthday;
    }

    public void setBirthday(Date birthday) {
        this.birthday = birthday;
    }

    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", birthday=" + birthday +
                ", sex='" + sex + '\'' +
                ", address='" + address + '\'' +
                '}';
    }
}
```

**编写UserMapper映射文件**

resource文件夹下，com.example.mapper 一层一层创建，一次创建三层会报错找不到文件

usermapper.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="UserMapper">
    <!--查询所有-->
    <select id="findAll" resultType="com.example.demo2.domain.User">
        select * from user
    </select>
</mapper>
```

resource文件夹下 创建核心配置文件,可以叫mybatis-config.xml 或其他都可以，这里我们叫sqlMapConfig.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--环境配置-->
    <environments default="development">
        <!--使用MySQL环境-->
        <environment id="development">
            <!--使用JDBC类型事务管理器-->
            <transactionManager type="JDBC"></transactionManager>
            <!--使用连接池-->
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"></property>
                <property name="url" value="jdbc:mysql:///mybatis_db?useSSL=false&amp;useServerPrepStmts=true&amp;characterEncoding=utf-8&amp;serverTimezone=Asia/Shanghai"></property>
                <property name="username" value="root"></property>
                <property name="password" value="123456"></property>
            </dataSource>
        </environment>
    </environments>
    <!--加载映射配置-->
    <mappers>
        <mapper resource="com/example/mapper/UserMapper.xml"></mapper>
    </mappers>
</configuration>
```

如果有乱码问题 url改为 

```java
jdbc:mysql:///mybatis_db?useUnicode=true&amp;characterEncoding=utf-8
```

**编写测试类**

```java
public class MybatisTest {
    public static void main(String[] args) throws IOException {
        /* 加载核心配置文件 */
        InputStream is = Resources.getResourceAsStream("SqlMapConfig.xml");
        /* 获取SqlSessionFactory工厂对象 */
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);
        /* 获取SqlSession会话对象 */
        SqlSession sqlSession = sqlSessionFactory.openSession();
        /* 执行sql */
        List<User> list = sqlSession.selectList("UserMapper.findAll");
        for (User user : list) {
            System.out.println(user);
        }
        /*  释放资源  */
        sqlSession.close();
    }
}
```

## Mybatis增删改查

**增加映射文件UserMapper.xml** 

```xml
<!-- 插入语句使用insert标签 -->
<insert id="save" parameterType="com.example.demo2.domain.User">
    insert into user(username,birthday,sex,address) values(#{username},#{birthday},#{sex},#{address})
</insert>
```

**编写测试类**

```java
	@Test
    public void testSave() throws Exception {
        /* 加载核心配置文件 */
        InputStream is = Resources.getResourceAsStream("SqlMapConfig.xml");
        /* 获取SqlSessionFactory工厂对象 */
        SqlSessionFactory sqlSessionFactory = new
                SqlSessionFactoryBuilder().build(is);
        /* 获取SqlSession会话对象 */
        SqlSession sqlSession = sqlSessionFactory.openSession();
        /* 执行sql */
        User user = new User();
        user.setUsername("zxl");
        user.setBirthday(new Date());
        user.setSex("男");
        user.setAddress("河南郑州");
        sqlSession.insert("UserMapper.save", user);

        /* DML语句，手动提交事务 */
        sqlSession.commit();
        /* 释放资源 */
        sqlSession.close();
    }
```

**增加映射文件UserMapper.xml** 

```xml
<!--修改语句使用update标签 -->
    <update id="update" parameterType="com.example.demo2.domain.User">
        update user set username = #{username},birthday = #{birthday},
                        sex = #{sex},address = #{address} where id = #{id}
    </update>
```

**编写测试类**

```java
	@Test
    public void testUpdate() throws Exception {
        /* 加载核心配置文件 */
        InputStream is = Resources.getResourceAsStream("SqlMapConfig.xml");
        /* 获取SqlSessionFactory工厂对象 */
        SqlSessionFactory sqlSessionFactory = new
                SqlSessionFactoryBuilder().build(is);
        /* 获取SqlSession会话对象 */
        SqlSession sqlSession = sqlSessionFactory.openSession();
        /* 执行sql */
        User user = new User();
        user.setId(3);
        user.setUsername("zxl");
        user.setBirthday(new Date());
        user.setSex("女");
        user.setAddress("河南郑州");
        sqlSession.update("UserMapper.update", user);
        /* DML语句，手动提交事务 */
        sqlSession.commit();
        /* 释放资源 */
        sqlSession.close();
    }
```

**增加映射文件UserMapper.xml** 

```xml
<!--删除语句使用delete标签 -->
    <delete id="delete" parameterType="com.example.demo2.domain.User">
        delete from user where id = #{id}
    </delete>
```

**编写测试类**

```java
	@Test
    public void testDelete() throws Exception {
        /* 加载核心配置文件 */
        InputStream is = Resources.getResourceAsStream("SqlMapConfig.xml");
        /* 获取SqlSessionFactory工厂对象 */
        SqlSessionFactory sqlSessionFactory = new
                SqlSessionFactoryBuilder().build(is);
        /* 获取SqlSession会话对象 */
        SqlSession sqlSession = sqlSessionFactory.openSession();
        /* 执行sql */
        sqlSession.delete("UserMapper.delete", 3);
        /* DML语句，手动提交事务 */
        sqlSession.commit();
        /* 释放资源 */
        sqlSession.close();
    }
```

## MyBatis常用配置解析

###  environments标签 

**sqlMapConfig.xml**

resource文件夹下 jdbc.properties

```properties
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql:///mybatis_db?useSSL=false&useServerPrepStmts=true&characterEncoding=utf-8&serverTimezone=Asia/Shanghai
jdbc.username=root
jdbc.password=123456
```

sqlMapConfig.xml 中

```xml
	<!--导入jdbc.properties文件-->	
	<properties resource="jdbc.properties"></properties>
    <!--环境配置 指定默认的环境名称-->
    <environments default="development">
        <!--使用MySQL环境 指定当前的环境名称-->
        <environment id="development">
            <!--使用JDBC类型事务管理器-->
            <transactionManager type="JDBC"></transactionManager>
            <!--使用连接池-->
            <!--数据源配置的参数-->
            <dataSource type="POOLED">
                <property name="driver" value="${jdbc.driver}"></property>
                <property name="url" value="${jdbc.url}"></property>
                <property name="username" value="${jdbc.username}"></property>
                <property name="password" value="${jdbc.password}"></property>
            </dataSource>
        </environment>
    </environments>
```

事务管理器（transactionManager）类型有两种：

- JDBC： 这个配置就是直接使用了JDBC 的提交和回滚设置，它依赖于从数据源得到的连接来管理事务作用域。 

-  MANAGER： 这个配置几乎没做什么。它从来不提交或回滚一个连接，而是让容器来管理事务的整个生命周期。

 数据源（dataSource）常用类型有三种：

- UNPOOLED

- 这个数据源的实现只是每次被请求时打开和关闭连接。

- POOLED：

- 这种数据源的实现利用“池”的概念将 JDBC 连接对象组织起来。

-  JNDI :

- 这个数据源实现是为了能在如 EJB 或应用服务器这类容器中使用，容器可以集中或在外部配置数据源，然后放置一个 JNDI 上下文的数据源引用

### properties标签 

实际开发中，习惯将数据源的配置信息单独抽取成一个properties文件，该标签可以加载额外配置的 properties

```properties
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql:///mybatis_db?useSSL=false&useServerPrepStmts=true&characterEncoding=utf-8&serverTimezone=Asia/Shanghai
jdbc.username=root
jdbc.password=123456
```

### typeAliases标签 

类型别名是为 Java 类型设置一个短的名字。 为了简化映射文件 Java 类型设置，mybatis框架为我们设置好的一些常用的类型的别名

**为domain 下的类配置别名**

```xml
<!--设置别名 sqlMapConfig.xml 里面-->
<typeAliases>
	<!--方式一: 给单个实体起别名-->
    <typeAlias type="com.aaa.domain.User" alias="user"/>
    <!--方式二: 批量起别名 不区分大小写 配置后方式一不可写-->
    <package name="com.aaa.domain"/>
   <!--配置后，使用domain包下的类，只需类名即可-->
</typeAliases>
```

### **mappers标签** 

该标签的作用是加载映射的，加载方式有如下几种：

```xml
1. 使用相对于类路径的资源引用，例如：
<mapper resource="xxx/xxx/xxx/userMapper.xml"/>
2. 使用完全限定资源定位符（URL），例如：
<mapper url="file:///xxx/xxx/userMapper.xml"/>
《下面两种mapper代理开发中使用:暂时了解》
3. 使用映射器接口实现类的完全限定类名，例如：
<mapper class="xxx.xxx.xxx.userMapper"/>
4. 将包内的映射器接口实现全部注册为映射器，例如：
<package name="xxx.xxx.builder"/>
```

### plugins标签

plugins 标签是配置 MyBatis 的插件

MyBatis可以使用第三方的插件来对功能进行扩展，分页助手PageHelper是将分页的复杂操作进行封装，使用简单的方式即可获得分页的相关数据

开发步骤：导入通用PageHelper的坐标，在mybatis核心配置文件中配置PageHelper插件，测试分页数据获取

pom.xml

```xml
		<!-- 分页助手 -->
        <dependency>
            <groupId>com.github.pagehelper</groupId>
            <artifactId>pagehelper</artifactId>
            <version>3.7.5</version>
        </dependency>
        <dependency>
            <groupId>com.github.jsqlparser</groupId>
            <artifactId>jsqlparser</artifactId>
            <version>0.9.1</version>
        </dependency>
```

在mybatis核心配置文件( sqlMapConfig.xml )中配置PageHelper插件

```xml
<!-- typeAliases 标签后插入 分页助手的插件 -->
    <plugins>
        <plugin interceptor="com.github.pagehelper.PageHelper">
            <!--dialect: 指定方言 limit-->
            <property name="dialect" value="mysql"/>
        </plugin>
    </plugins>
```

测试分页代码实现

```java
	@Test
    public void testPageHelper() throws IOException {
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        //设置分页参数 第一个参数是页数,第二个参数是条数，每页查询的条数
        PageHelper.startPage(1,2);
        List<User> select = mapper.findAll();
        for(User user : select){
            System.out.println(user);
        }
    }
```

获得分页相关的其他参数

```java
	@Test
    public void testPageHelper() throws IOException {
        //设置分页参数
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        PageHelper.startPage(1,2);
        List<User> select = mapper.findAll();
        for(User user : select){
            System.out.println(user);
        }
        //其他分页的数据
        PageInfo<User> pageInfo = new PageInfo<User>(select);
        System.out.println("总条数："+pageInfo.getTotal());
        System.out.println("总页数："+pageInfo.getPages());
        System.out.println("当前页："+pageInfo.getPageNum());
        System.out.println("每页显示长度："+pageInfo.getPageSize());
        System.out.println("是否第一页："+pageInfo.isIsFirstPage());
        System.out.println("是否最后一页："+pageInfo.isIsLastPage());
    }
```

## Mybatis的API概述 

> API介绍

### SqlSessionFactoryBuilder

常用API：SqlSessionFactory build(InputStream inputStream)

通过加载mybatis的核心文件的输入流的形式构建一个SqlSessionFactory对象

```java
InputStream inputStream = Resources.getResourceAsStream("SqlMapConfig.xml"); 

SqlSessionFactoryBuilder builder = new SqlSessionFactoryBuilder(); 

SqlSessionFactory factory = builder.build(inputStream);
```

其中， Resources 工具类，这个类在 org.apache.ibatis.io 包中。Resources 类帮助你从类路径下文件系统或一个 web URL 中加载资源文件。

### SqlSessionFactory

SqlSessionFactory 有多个个方法创建SqlSession 实例。常用的有如下两个：

```java
SqlSessionFactory factory = builder.build(inputStream);
SqlSession sqlSession = factory.openSession();

SqlSession sqlSession = factory.openSession(true);//自动提交事务
```

**SqlSession会话对象** 

SqlSession 实例在 MyBatis 中是非常强大的一个类。在这里你会看到所有执行语句、提交或回滚事务 和获取映射器实例的方法。 执行语句的方法主要有：

```java
<T> T selectOne(String statement, Object parameter)

<E> List<E> selectList(String statement, Object parameter)

int insert(String statement, Object parameter)

int update(String statement, Object parameter)

int delete(String statement, Object parameter)
```

操作事务的方法主要有：

```java
void commit() 
void rollback()
```

## Mybatis的dao层开发使用

### 传统开发方式

**编写UserMapper接口**

```java
public interface UserMapper {
    public List findAll() throws Exception;
}
```

**编写UserMapper实现**

```java
public class UserMapperImpl implements UserMapper {
    @Override
    public List<User> findAll() throws Exception {
        //加载配置文件
        InputStream is = Resources.getResourceAsStream("SqlMapConfig.xml");
        //获取SqlSessionFactory工厂对象
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);
        //获取SqlSe会话对象
        SqlSession sqlSession = sqlSessionFactory.openSession();
        //执行sql
        List<User> list = sqlSession.selectList("UserMapper.findAll");
        //释放资源
        sqlSession.close();
        return list;
    }
}
```

**编写UserMapper.xml**

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="UserMapper">
    <!--查询所有-->
    <select id="findAll" resultType="user">
        select * from user
    </select>
</mapper>
```

**测试**

```java
    @Test
    public void testFindAll() throws Exception {
        /* 创建UserMapper 实现类 */
        UserMapper userMapper = new UserMapperImpl();
        /* 执行查询 */
        List<User> list = userMapper.findAll();
        for (User user : list) {
            System.out.println(user);
        }
    }
```

**传统方式问题思考**： 

1.实现类中，存在mybatis模板代码重复

2.实现类调用方法时，xml中的sql statement 硬编码到java代码中 

思考：能否只写接口，不写实现类。只编写接口和Mapper.xml即可？

因为在dao（mapper）的实现类中对sqlsession的使用方式很类似。因此mybatis提供了接口的动态代理。 

### 代理开发方式 

采用 Mybatis 的基于接口代理方式实现 持久层 的开发，这种方式是我们后面进入企业的主流。 基于接口代理方式的开发只需要程序员编写 Mapper 接口，Mybatis 框架会为我们动态生成实现类的对象。 

这种开发方式要求我们遵循一定的规范：

```xml
    <mapper namespace="UserDao">
        <!--查询所有-->
        <select id="findAll" parameterType="int" resultType="user">
            select * from user where id=#{id}
        </select>
    </mapper>
```

```java
public interface UserDao {
    User findAll(int id) throws Exception;
}
```

- Mapper.xml映射文件中的namespace与mapper接口的全限定名相同 

- Mapper接口方法名和Mapper.xml映射文件中定义的每个statement的id相同 

- Mapper接口方法的输入参数类型和mapper.xml映射文件中定义的每个sql的parameterType的类型相同 

- Mapper接口方法的输出参数类型和mapper.xml映射文件中定义的每个sql的resultType的类型相同 

Mapper 接口开发方法只需要程序员编写Mapper 接口（相当于Dao 接口），由Mybatis 框架根据接口 定义创建接口的动态代理对象，代理对象的方法体同上边Dao接口实现类方法。

**编写UserMapper接口**

```java
public interface UserMapper {
    public List<User> findAll() throws Exception;
}
```

**编写UserMapper.xml**

```xml
    <mapper namespace="com.aaa.mapper.UserMapper">
        <!--查询所有-->
        <select id="findAll" resultType="user">
            select * from user
        </select>
    </mapper>
```

**测试**

```java
    @Test
    public void testFindAll() throws Exception {
        //加载核心配置文件
        InputStream is = Resources.getResourceAsStream("SqlMapConfig.xml");
        //获得SqlSessionFactory工厂对象
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);
        //获得SqlSession会话对象
        SqlSession sqlSession = sqlSessionFactory.openSession();
        //获得Mapper代理对象
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        // 执行查询
        List<User> list = userMapper.findAll();
        for (User user : list) {
            System.out.println(user);
        }
        //释放资源
        sqlSession.close();
    }
```

## Mybatis高级查询

### ResutlMap属性

**建立对象关系映射**

```
resultType 如果实体的属性名与表中字段名一致，将查询结果自动封装到实体类中
ResutlMap 如果实体的属性名与表中字段名不一致，可以使用ResutlMap实现手动封装到实体类中
```

**封装SqlSession**

```java
public class GetSqlSession {
    public SqlSession getSqlSession() throws IOException {
        /* 加载核心配置文件 */
        InputStream is = Resources.getResourceAsStream("SqlMapConfig.xml");
        /* 获取SqlSessionFactory工厂对象 */
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);
        /* 获取SqlSession会话对象 true 自动提交事务 */
        SqlSession sqlSession = sqlSessionFactory.openSession(true);
        return sqlSession;
    }
}
```

**编写UserMapper接口**

```java
public interface UserMapper {
    public List<User> findAllResultMap();
}
```

**编写UserMapper.xml** 

```xml
<!--实现手动映射封装
resultMap id="userResultMap" 此标签唯一标识  type="user" 封装后的实体类型  
<id column="uid" property="id"></id> 表中主键字段封装
column="uid" 表中的字段名
property="id" user实体的属性名
<result column="NAME" property="username"></result> 表中普通字段封装
column="NAME" 表中的字段名
property="username" user实体的属性名
补充：如果有查询结果有 字段与属性是对应的，可以省略手动封装 【了解】-->
	<resultMap id="UserResultMap" type="user">
        <id column="id" property="id"></id>
        <result column="username" property="username"></result>
        <result column="s" property="sex"></result>
    </resultMap>

    <select id="findAllMap" resultMap="UserResultMap">
        select id,username,sex as s from user
    </select>
```

**代码测试**

```java
	@Test
    public void findAllNap() throws IOException {
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        for (User user : mapper.findAllMap()) {
            System.out.println(user);
        }
    }
```

### 多条件查询

**根据id和username查询user表**

**方式一：使用 #{arg0} - #{argn} 或者 #{param1} - #{paramn} 获取参数**

UserMapper接口

```java
public interface UserMapper {
    public List<User> findByIdAndUsername(Integer id, String username);
} 
```

UserMapper.xml

```xml
    <select id="findByIdAndUsername" resultType="user">
        <!-- select * from user where id = #{arg0} and username = #{arg1} -->
        select * from user where id = #{param1} and username = #{param2}
    </select>
```

测试

```java
    @Test
    public void testFindByIdAndUsername() throws IOException {
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        List<User> gy = mapper.findByIdAndUsername(2, "gy");
        for (User user : gy) {
            System.out.println(user);
        }
    }
```

**方式二：使用注解，引入 @Param() 注解获取参数**

UserMapper接口

```java
public interface UserMapper {
    public List findByIdAndUsername2(
        @Param("id") Integer id,@Param("username") String username
    ); 
}
```

UserMapper.xml 

```xml
    <select id="findByIdAndUsername2" resultType="user">
        select * from user where id = #{id} and username = #{username}
    </select>
```

测试

```java
    @Test
    public void testFindByIdAndUsername2() throws IOException {
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        List<User> gy = mapper.findByIdAndUsername2(2, "gy");
        for (User user : gy) {
                System.out.println(user);
        }
    }
```

**方式三（推荐）：使用pojo对象传递参数** 

UserMapper接口

```java
public interface UserMapper {
    public List<User> findByIdAndUsername3(User user); 
}
```

UserMapper.xml

```xml
    <select id="findByIdAndUsername3" parameterType="com.aaa.domain.User" resultType="com.aaa.domain.User">
        select * from user where id = #{id} and username = #{username}
    </select>
```

测试

```java
    @Test
    public void testFindByIdAndUsername3() throws IOException {
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        User param = new User();
        param.setId(2);
        param.setUsername("gy");
        List<User> list = mapper.findByIdAndUsername3(param);
        System.out.println(list);
    }
```

### 模糊查询 

**根据username模糊查询user表** 

UserMapper接口 

```java
public interface UserMapper { 
	public List<User> findByusername(String username);
}
```

UserMapper.xml 

```xml
	<select id="findByusername" parameterType="string" resultType="user">
        <!-- select * from user where username like '${value}'
			 不推荐使用，因为会出现sql注入问题
		-->
        select * from user where username like #{username}
    </select>
```

测试 

```java
@Test
    public void testByusername() throws IOException {
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        for (User user : mapper.findByusername("g%")) {
            System.out.println(user);
        }
    }
```

 ${} 与 #{} 区别【笔试题】

\#{} :表示一个占位符号  ?

- 通过 #{} 可以实现preparedStatement向占位符中设置值，自动进行java类型和jdbc类型转换，# {}可以有效防止sql注入。 

- \#{} 可以接收简单类型值或pojo属性值。 

- 如果parameterType传输单个简单类型值， #{} 括号中名称随便写。

${} :表示拼接sql串 

- 通过 ${} 可以将parameterType 传入的内容拼接在sql中且不进行jdbc类型转换，会出现sql注入问题。 

- ${} 可以接收简单类型值或pojo属性值。 

- 如果parameterType传输单个简单类型值， ${} 括号中只能是value。

### 返回主键

向数据库插入一条记录后，希望能立即拿到这条记录在数据库中的主键值。

**方式一 useGeneratedKeys**

UserMapper接口

```java
public interface UserMapper {
    public void save1(User user);
}
```

UserMapper.xml

```xml
    <!--useGeneratedKeys="true" 声明返回主键
		keyProperty="id" 把返回主键的值，封装到实体的id属性中
		注意：只适用于主键自增的数据库，mysql和sqlserver支持，oracle不支持-->
	<insert id="save1" parameterType="user" useGeneratedKeys="true" keyProperty="id">
        insert into user(username,birthday,sex,address) 
        values(#{username},#{birthday},#{sex},#{address})
    </insert>
```

测试

```java
	@Test
    public void TestSave1() throws IOException {
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        User user = new User();
        user.setUsername("zxl");
        user.setBirthday(new Date());
        user.setSex("男");
        user.setAddress("河南郑州");
        mapper.save1(user);
        System.out.println(user.getId());
        sqlSession.close();
    }
```

**方式二 selectKey**

UserMapper接口

```java
public interface UserMapper {
    public void save2(User user);
}
```

UserMapper.xml

```xml
    <!--selectKey 适用范围广，支持所有类型数据库
		keyColumn="id" 指定主键列名
		keyProperty="id" 指定主键封装到实体的id属性中
		resultType="int" 指定主键类型
		order="AFTER" 设置在sql语句执行前（后），执行此语句-->
	<insert id="save2" parameterType="user" useGeneratedKeys="true" keyProperty="id">
        <selectKey keyColumn="id" keyProperty="id" resultType="int" order="AFTER">
        <!--得到刚 insert 进去记录的主键值，只适用与自增主键-->
        select LAST_INSERT_ID();
        </selectKey>
        insert into user(username,birthday,sex,address)
        values(#{username},#{birthday},#{sex},#{address})
    </insert>
```

测试

```java
	@Test
    public void TestSave1() throws IOException {
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        User user = new User();
        user.setUsername("zxl");
        user.setBirthday(new Date());
        user.setSex("男");
        user.setAddress("河南郑州");
        mapper.save2(user);
        System.out.println(user.getId());
        sqlSession.close();
    }
```

## 动态SQL

### 动态SQL之 if

根据id和username查询，但是不确定两个都有值,if + where 解决动态的拼接and关键字 and可能造成的语法错误

UserMapper接口

```java
public interface UserMapper {
    public List<User> findByIdAndUsernameIf(User user);
}
```

UserMapper.xml映射

```xml
	<select id="findByIdAndUsernameIf" parameterType="user" resultType="user">
        SELECT * FROM user
		<!--where标签相当于 where 1=1，但是如果没有条件，就不会拼接where关键字-->
        <where>
            <if test="id != null">
                AND id = #{id}
            </if>
            <if test="username != null">
                AND username = #{username}
            </if>
        </where>
    </select>
```

测试代码

```java
	@Test
    public void testFindByIdAndUsernameIf() throws Exception {
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        User param = new User();
        param.setId(7);
        param.setUsername("zxl");
        List<User> list = userMapper.findByIdAndUsernameIf(param);
        System.out.println(list);
    }
```

### 动态SQL之 set

set标签 代替set 关键字，可以再拼接sql语句时，动态拼接 "，" 避免拼接语法错误

UserMapper接口

```java
public interface UserMapper {
   	public void updateIf(User user);
}
```

```xml
<!--set标签在更新的时候，自动加上set关键字，然后去掉最后一个条件的逗号-->
	<update id="updateIf" parameterType="user">
        UPDATE user
        <set>
            <if test="username != null">
                username = #{username},
            </if>
            <if test="birthday != null">
                birthday = #{birthday},
            </if>
            <if test="sex !=null">
                sex = #{sex},
            </if>
            <if test="address !=null">
                address = #{address},
            </if>
        </set>
        WHERE id = #{id}
    </update>
```

测试代码

```java
	@Test
    public void testUpdateIf()throws Exception{
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        User user = new User();
        user.setId(1);
        user.setUsername("小寒");
        user.setSex("女");
        userMapper.updateIf(user);
    }
```

### 动态SQL之 foreach

foreach主要是用来做数据的循环遍历

例如：select * from user where id in (1,2,3) 在这样的语句中, 传入的参数部分必须依靠 foreach遍历才能实现。

**foreach标签用于遍历集合，它的属性**

- collection：代表要遍历的集合元素
- open：代表语句的开始部分
- close：代表结束部分
- item：代表遍历集合的每个元素，生成的变量名
- sperator：代表分隔符

集合 UserMapper接口 

```java
public interface UserMapper {
   	public List<User> findByList(List<Integer> ids)
}
```

UserMaper.xml映射 

```xml
<!--如果查询条件为普通类型 List集合，collection属性值为：collection 或者 list-->
	<select id="findByList" parameterType="list" resultType="user" >
        SELECT * FROM user
        <where>
            <foreach collection="collection" open="id in(" close=")" item="id"
                     separator=",">
                #{id}
            </foreach>
        </where>
    </select>
```

测试代码

```java
	@Test
    public void testFindByList() throws Exception {
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        List<Integer> ids = new ArrayList<>();
        ids.add(1);
        ids.add(2);
        ids.add(3);
        List<User> list = userMapper.findByList(ids);
        System.out.println(list);
    }
```

数组 UserMapper接口

```java
public interface UserMapper {
   	public List<User> findByArray(Integer[] ids);
}
```

UserMaper.xml映射

```xml
<!-- 如果查询条件为普通类型 Array数组，collection属性值为：array-->
	<select id="findByArray" parameterType="int" resultType="user" >
        SELECT * FROM user
        <where>
            <foreach collection="array" open="id in(" close=")" item="id"
                     separator=",">
                #{id}
            </foreach>
        </where>
    </select>
```

测试代码

```java
    @Test
    public void testFindByArray() throws Exception {
      SqlSession sqlSession = new GetSqlSession().getSqlSession();
      UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
      Integer[] ids = {1, 2, 3};
      List<User> list = userMapper.findByArray(ids);
      System.out.println(list);
    }
```

### SQL片段

映射文件中可将重复的 sql 提取出来，使用时用 include 引用即可，最终达到 sql 重用的目的

```xml
    <!--抽取的sql片段-->
    <sql id="selectUser">
        SELECT * FROM user
    </sql>
    <select id="findByList" parameterType="list" resultType="user" >
        <!--引入sql片段-->
        <include refid="selectUser"></include>
        <where>
            <foreach collection="collection" open="id in(" close=")" item="id"    separator=",">
                #{id}
            </foreach>
        </where>
    </select>
```

## Mybatis多表查询

**案例环境准备**

```sql
DROP TABLE IF EXISTS `orders`;
CREATE TABLE `orders` (
                          `id` INT(11) NOT NULL AUTO_INCREMENT,
                          `ordertime` VARCHAR(255) DEFAULT NULL,
                          `total` DOUBLE DEFAULT NULL,
                          `uid` INT(11) DEFAULT NULL,
                          PRIMARY KEY (`id`),
                          KEY `uid` (`uid`),
                          CONSTRAINT `orders_ibfk_1` FOREIGN KEY (`uid`) REFERENCES `user` (`id`)
) ENGINE=INNODB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8;

INSERT INTO `orders` VALUES ('1', '2020-12-12', '3000', '1');
INSERT INTO `orders` VALUES ('2', '2020-12-12', '4000', '1');
INSERT INTO `orders` VALUES ('3', '2020-12-12', '5000', '2');

DROP TABLE IF EXISTS `role`;
CREATE TABLE `role` (
                        `id` INT(11) NOT NULL AUTO_INCREMENT,
                        `rolename` VARCHAR(255) DEFAULT NULL,
                        `roleDesc` VARCHAR(255) DEFAULT NULL,
                        PRIMARY KEY (`id`)
) ENGINE=INNODB AUTO_INCREMENT=3 DEFAULT CHARSET=utf8;

INSERT INTO `role` VALUES ('1', 'CTO', 'CTO');
INSERT INTO `role` VALUES ('2', 'CEO', 'CEO');

DROP TABLE IF EXISTS `user_role`;
CREATE TABLE `user_role` (
                             `userid` INT(11) NOT NULL,
                             `roleid` INT(11) NOT NULL,
                             PRIMARY KEY (`userid`,`roleid`),
                             KEY `roleid` (`roleid`),
                             CONSTRAINT `user_role_ibfk_1` FOREIGN KEY (`userid`) REFERENCES `user`
                                 (`id`),
                             CONSTRAINT `user_role_ibfk_2` FOREIGN KEY (`roleid`) REFERENCES `role`(`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8;

INSERT INTO `user_role` VALUES ('1', '1');
INSERT INTO `user_role` VALUES ('2', '1');
INSERT INTO `user_role` VALUES ('1', '2');
INSERT INTO `user_role` VALUES ('2', '2');
```

###  一对一（多对一） 

**一对一查询模型**

用户表和订单表的关系为，一个用户有多个订单，一个订单只从属于一个用户

一对一查询的需求：查询所有订单，与此同时查询出每个订单所属的用户 

一对一查询语句 ：

```sql
SELECT * FROM orders o LEFT JOIN user u ON o.uid=u.id;
```

Order实体

```java
@Data
@ToString
public class Orders {
    private int id;
    private Date ordertime;
    private double total;
    private User user;
}
```

OrderMapper接口

```java
public interface OrdersMapper {
    public List<Orders> findAllWithUser();
}
```

OrderMapper.xml映射

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.example.mapper.OrdersMapper">
    <resultMap id="OrdersMap" type="Orders">
        <id column="id" property="id"></id>
        <result column="ordertime" property="ordertime"></result>
        <result column="total" property="total"></result>
        <!--一对一（多对一）使用association标签关联  
			property="user" 封装实体的属性名  
			javaType="user" 封装实体的属性类型  -->
        <association property="user" javaType="User">
            <id column="id" property="id"></id>
            <result column="username" property="username"></result>
            <result column="birthday" property="birthday"></result>
            <result column="sex" property="sex"></result>
            <result column="address" property="address"></result>
        </association>

    </resultMap>

    <select id="findAllWithUser" resultMap="OrdersMap">
        SELECT * FROM orders o LEFT JOIN USER u ON o.uid = u.id
    </select>
</mapper>
```

配置映射 在sqlMapconfig.xml中

```xml
<!--加载映射配置-->
    <mappers>
<!--        <mapper resource="com/example/mapper/UserMapper.xml"></mapper>-->
<!--        <mapper resource="com/example/mapper/OedersMapper.xml"></mapper>-->
        <!--批量加载映射-->
        <package name="com.example.mapper"/>
    </mappers>
```

测试代码

```java
	@Test
    public void testOrderWithUser() throws Exception {
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        OrdersMapper orderMapper = sqlSession.getMapper(OrdersMapper.class);
        List<Orders> list = orderMapper.findAllWithUser();
        for (Orders order : list) {
            System.out.println(order);
        }
    }
```

### 一对多

一对多查询语句

```sql
SELECT *,o.id oid FROM user u LEFT JOIN orders o ON u.id = o.uid;
```

User实体

```java
@Data
@ToString
public class User {
    private Integer id;
    private String username;
    private Date birthday;
    private String sex;
    private String address;
    // 代表当前用户具备的订单列表
    private List<Orders> orderList;
}
```

UserMapper接口

```java
public interface UserMapper {
    public List<User> findAllWithOrder();
}
```

UserMapper.xml映射

```xml
<resultMap id="userMap" type="User">
        <id column="id" property="id"></id>
        <result column="username" property="username"></result>
        <result column="birthday" property="birthday"></result>
        <result column="sex" property="sex"></result>
        <result column="address" property="address"></result>
        <!--
        一对多使用collection标签关联
        property="orderList" 封装到集合的属性名
        ofType="order" 封装集合的泛型类型
        -->
        <collection property="orderList" ofType="Orders">
            <id column="oid" property="id"></id>
            <result column="ordertime" property="ordertime"></result>
            <result column="total" property="total"></result>
        </collection>
    </resultMap>
    <select id="findAllWithOrder" resultMap="userMap">
        SELECT *,o.id oid FROM USER u LEFT JOIN orders o ON u.`id` = o.`uid`;
    </select>
```

测试代码

```java
	@Test
    public void testUserWithOrder() throws Exception {
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        List<User> list = userMapper.findAllWithOrder();
        for (User user : list) {
            System.out.println(user);
        }
    }
```

### 多对多

多对多查询的模型 用户表和角色表的关系为，一个用户有多个角色，一个角色被多个用户使用 多对多查询的需求：查询所有用户同时查询出该用户的所有角色 

多对多查询语句

```sql
SELECT * FROM user u -- 用户表
LEFT JOIN user_role ur -- 左外连接中间表
ON u.id = ur.userid
LEFT JOIN role r -- 左外连接中间表
ON ur.roleid = r.id;
```

User和Role 实体

```java
@Data
@ToString
public class User {
    private Integer id;
    private String username;
    private Date birthday;
    private String sex;
    private String address;
    // 代表当前用户关联的角色列表
    private List<Role> roleList;
}
```

```java
@Data
@ToString
public class Role {
    private Integer id;
    private String roleName;
    private String roleDesc;
}
```

UserMapper接口

```java
public interface UserMapper {
	public List<User> findAllWithRole();
}
```

UserMapper.xml映射

```xml
	<resultMap id="userAndRoleMap" type="com.example.demo2.entity.User">
        <id column="id" property="id"></id>
        <result column="username" property="username"></result>
        <result column="birthday" property="birthday"></result>
        <result column="sex" property="sex"></result>
        <result column="address" property="address"></result>

        <collection property="roleList" ofType="com.example.demo2.entity.Role">
            <id column="id" property="id"></id>
            <result column="roleName" property="roleName"></result>
            <result column="roleDesc" property="roleDesc"></result>
        </collection>
    </resultMap>

    <select id="findAllWithRole" resultMap="userAndRoleMap">
        SELECT * FROM user u
            LEFT JOIN user_role ur
            ON u.id = ur.userid
            LEFT JOIN role r
            ON ur.roleid = r.id;
    </select>
```

测试代码

```java
	@Test
    public void testUserWithRole() throws Exception {
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        List<User> list = userMapper.findAllWithRole();
        for (User user : list) {
            System.out.println(user);
        }
    }
```

## 日志配置

pom.xml

```xml
		<!-- 添加slf4j日志api -->
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>1.7.20</version>
        </dependency>
        <!-- 添加logback-classic依赖 -->
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>1.2.3</version>
        </dependency>
        <!-- 添加logback-core依赖 -->
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-core</artifactId>
            <version>1.2.3</version>
        </dependency>
```

resource 下新建 logback.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <!--CONSOLE ：表示当前的日志信息是可以输出到控制台的。-->
    <appender name="Console" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>[%level]  %cyan([%thread]) %boldGreen(%logger{15}) - %msg %n</pattern>
        </encoder>
    </appender>
    <logger name="com.aaa" level="DEBUG" additivity="false">
        <appender-ref ref="Console"/>
    </logger>

    <!--level:用来设置打印级别，大小写无关：TRACE, DEBUG, INFO, WARN, ERROR, ALL 和 OFF默认debug-->
    <root level="DEBUG">
        <appender-ref ref="Console"/>
    </root>
</configuration>
```

## MyBatis嵌套查询

嵌套查询就是将原来多表查询中的联合查询语句拆成单个表的查询，再使用mybatis的语法嵌套在一 起

优点：简化多表查询操作 缺点：执行多次sql语句，浪费数据库性能

### 一对一嵌套查询

需求：查询一个订单，与此同时查询出该订单所属的用户

```sql
SELECT * FROM orders o LEFT JOIN user u ON o.uid = u.id;
```

一对一查询语句 

```sql
-- 先查询订单
SELECT * FROM orders;
-- 再根据订单uid外键，查询用户
SELECT * FROM user WHERE id = #{订单的uid};
```

**代码实现** 

OrderMapper接口

```java
public interface OrdersMapper {
	 public List<Orders> findAllUser();
}
```

OrderMapper.xml映射

```xml
	<!--一对一嵌套查询-->
    <resultMap id="orderMap" type="orders">
        <id column="id" property="id"></id>
        <result column="ordertime" property="ordertime"></result>
        <result column="total" property="total"></result>
        <!--根据订单中uid外键，查询用户表-->
        <association property="user" javaType="user" column="uid"
                     select="com.example.mapper.UserMapper.findById"></association>
    </resultMap>
    <select id="findAllUser" resultMap="orderMap" >
        SELECT * FROM orders
    </select>
```

UserMapper接口

```java
public interface UserMapper {
    public User findById(Integer id);
}
```

UserMapper.xml映射

```xml
	<select id="findById" parameterType="int" resultType="user">
        SELECT * FROM `user` where id = #{uid}
    </select>
```

测试代码

```java
 	@Test
    public void testOrderWithAllUser() throws Exception {
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        OrdersMapper orderMapper = sqlSession.getMapper(OrdersMapper.class);
        List<Orders> list = orderMapper.findAllUser();
        for (Orders order : list) {
            System.out.println(order);
        }
    }
```

### 一对多嵌套查询

需求：查询所有用户，与此同时查询出该用户具有的订单

一对多查询语句

```sql
-- 先查询用户
SELECT * FROM `user`;
-- 再根据用户id主键，查询订单列表
SELECT * FROM orders where uid = #{用户id};
```

**代码实现** 

UserMapper接口

```java
public interface UserMapper {
	public List<User> findAllWith();
}
```

UserMapper.xml映射

```xml
	<!--一对多嵌套查询-->
    <resultMap id="userAllMap" type="user">
        <id column="id" property="id"></id>
        <result column="username" property="username"></result>
        <result column="birthday" property="birthday"></result>
        <result column="sex" property="sex"></result>
        <result column="address" property="address"></result>
        <!--根据用户id，查询订单表-->
        <collection property="orderList" column="id" ofType="orders"
                    select="com.example.mapper.OrdersMapper.findByUid"></collection>
    </resultMap>
    <select id="findAllWith" resultMap="userAllMap">
        SELECT * FROM `user`
    </select>
```

OrderMapper接口

```java
public interface OrdersMapper { 
	public List<Orders> findByUid(Integer uid);
}
```

OrderMapper.xml映射

```xml
	<select id="findByUid" parameterType="int" resultType="orders">
        SELECT * FROM orders where uid = #{uid}
    </select>
```

测试代码

```java
	@Test
    public void testUserWithAllOrder() throws Exception {
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        List<User> list = userMapper.findAllWith();
        for (User user : list) {
            System.out.println(user);
        }
    }
```

### 多对多嵌套查询

需求：查询用户 同时查询出该用户的所有角色

多对多查询语句

```sql
-- 先查询用户
SELECT * FROM `user`;
-- 再根据用户id主键，查询角色列表
SELECT * FROM role r INNER JOIN user_role ur 
ON r.`id` = ur.`rid` WHERE ur.`uid` = #{用户id};
```

**代码实现**

UserMapper接口

```java
public interface UserMapper { 
	public List<User> findWithRole();
}
```

UserMapper.xml映射

```xml
	<!--多对多嵌套查询-->
    <resultMap id="userAndRole" type="user">
        <id column="id" property="id"></id>
        <result column="username" property="username"></result>
        <result column="birthday" property="birthday"></result>
        <result column="sex" property="sex"></result>
        <result column="adress" property="address"></result>
        <!--根据用户id，查询角色列表-->
        <collection property="roleList" column="id" ofType="role"
                    select="com.example.mapper.RoleMapper.findByUid"></collection>
    </resultMap>
    <select id="findWithRole" resultMap="userAndRole">
        SELECT * FROM `user`
    </select>
```

RoleMapper接口

```java
public interface RoleMapper {
    public List<Role> findByUid(Integer uid);
}
```

RoleMapper.xml映射

```xml
	<select id="findByUid" parameterType="int" resultType="role">
        SELECT r.id,r.rolename roleName,r.roleDesc roleDesc FROM role r
        INNER JOIN user_role ur ON r.id = ur.roleid WHERE ur.userid = #{uid}
    </select>
```

测试代码

```java
	@Test
    public void testUserRole() throws Exception {
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        List<User> list = userMapper.findWithRole();
        for (User user : list) {
            System.out.println(user);
        }
    }
```

## MyBatis加载策略

**什么是延迟加载** 

问题 通过前面的学习，我们已经掌握了Mybatis中一对一，一对多，多对多关系的配置及实现，可以实现 对象的关联查询。实际开发过程中很多时候我们并不需要总是在加载用户信息时就一定要加载他的订单 信息。此时就是我们所说的延迟加载。

**延迟加载**

就是在需要用到数据时才进行加载，不需要用到数据时就不加载数据。延迟加载也称懒加载。

优点： 先从单表查询，需要时再从关联表去关联查询，大大提高数据库性能，因为查询单表要比关联查询多张表 速度要快。 

缺点： 因为只有当需要用到数据时，才会进行数据库查询，这样在大批量数据查询时，因为查询工作也要消耗时 间，所以可能造成用户等待时间变长，造成用户体验下降。 

在多表中： 一对多，多对多：通常情况下采用延迟加载，一对一（多对一）：通常情况下采用立即加载 

注意： 延迟加载是基于嵌套查询来实现的

### 局部延迟加载

在association和collection标签中都有一个fetchType属性，通过修改它的值，可以修改局部的加载策略。

```xml
	<!-- 开启一对多 延迟加载 -->
    <resultMap id="userMap" type="user">
        <id column="id" property="id"></id>
        <result column="username" property="username"></result>
        <result column="password" property="password"></result>
        <result column="birthday" property="birthday"></result>
        <!--
        fetchType="lazy" 懒加载策略
        fetchType="eager" 立即加载策略
        -->
        <collection property="orderList" ofType="orders" column="id"
                    select="com.aaa.dao.OrderMapper.findByUid" fetchType="lazy">
        </collection>
    </resultMap>
    <select id="findAll" resultMap="userMap">
        SELECT * FROM `user`
    </select>
```

### 设置触发延迟加载的方法

大家在配置了延迟加载策略后，发现即使没有调用关联对象的任何方法，但是在你调用当前对象的 equals、clone、hashCode、toString方法时也会触发关联对象的查询。

我们可以在配置文件 sqlMapConfig.xml 中使用lazyLoadTriggerMethods配置项覆盖掉上面四个方法。

```xml
<settings>
    <!--所有方法都会延迟加载-->
    <setting name="lazyLoadTriggerMethods" value="toString()"/>
</settings>
```

全局延迟加载

```xml
<settings>
    <!--开启全局延迟加载功能-->
    <setting name="lazyLoadingEnabled" value="true"/>
</settings>
```

**注意: 局部的加载策略优先级高于全局的加载策略。**

## MyBatis缓存

**为什么使用缓存**

当用户频繁查询某些固定的数据时,第一次将这些数据从数据库中查询出来,保存在缓存中。当用户再 次查询这些数据时,不用再通过数据库查询,而是去缓存里面查询。减少网络连接和数据库查询带来的损耗,从而提高我们的查询效率,减少高并发访问带来的系统性能问题。一句话概括：经常查询一些不经常发生变化的数据，使用缓存来提高查询效率。 像大多数的持久化框架一样，Mybatis也提供了缓存策略，通过缓存策略来减少数据库的查询次数， 从而提高性能。 Mybatis中缓存分为一级缓存，二级缓存。

### 一级缓存

一级缓存是SqlSession级别的缓存，是默认开启的，所以在参数和SQL完全一样的情况下，我们使用同一个SqlSession对象调用一个Mapper方法，往往只执行一次SQL，因为使用SelSession第一次查询后，MyBatis会将其放在缓存中，以后再查询的时候，如果没有声明需要刷新，并且缓存没有超时的情况下，SqlSession都会取出当前缓存的数据，而不会再次发送SQL到数据库。

**验证**

```java
	@Test
    public void testOneCache() throws Exception {
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        User user1 = userMapper.findById(1);
        System.out.println("第一次查询的用户：" + user1);
        System.out.println("----------------------------");
        User user2 = userMapper.findById(1);
        System.out.println("第二次查询的用户：" + user2);
        sqlSession.close();
    }
```

我们可以发现，虽然在上面的代码中我们查询了两次，但最后只执行了一次数据库操作，这就是 Mybatis提供给我们的一级缓存在起作用了。因为一级缓存的存在，导致第二次查询id为1的记录时，并没有发出sql语句从数据库中查询数据，而是从一级缓存中查询。 

**分析** 

 一级缓存是SqlSession范围的缓存，执行SqlSession的C（增加）U（更新）D（删除）操作，或者调 用clearCache()、commit()、close()方法，都会清空缓存。

这样做的目的为了让缓存中存储的是最新的信息，避免脏读。

**清除缓存**

```java
	@Test
    public void testOneCache() throws Exception {
        SqlSession sqlSession = new GetSqlSession().getSqlSession();
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        User user1 = userMapper.findById(1);
        System.out.println("第一次查询的用户：" + user1);
        System.out.println("----------------------------");
        //调用sqlSession清除缓存 方法一
        sqlSession.clearCache();
        User user2 = userMapper.findById(1);
        System.out.println("第二次查询的用户：" + user2);
        sqlSession.close();
    }
```

```xml
<!-- 每次查询时，都会清除缓存 方法二 -->
<select id="id" parameterType="x" resultType="x" flushCache="true" useCache="false"></select>
```

**当为select语句时：**
flushCache默认为false，表示任何时候语句被调用，都不会去清空本地缓存和二级缓存。
useCache默认为true，表示会将本条语句的结果进行二级缓存。
**当为insert、update、delete语句时：**

flushCache默认为true，表示任何时候语句被调用，都会导致本地缓存和二级缓存被清空。

useCache属性在该情况下没有。

当为select语句的时候，如果没有去配置flushCache、useCache，那么默认是启用缓存的，所以，如果有必要，那么就需要人工修改配置，

update 的时候如果 flushCache="false"，则当你更新后，查询的数据数据还是老的数据。

### 二级缓存

二级缓存是namspace级别（跨sqlSession）的缓存，是默认不开启的

二级缓存的开启需要进行配置，实现二级缓存的时候，MyBatis要求返回的POJO必须是可序列化的。 也就是要求实现Serializable接口，配置方法很简单，只需要在映射XML文件配置  就可以开启 二级缓存了。

**验证**

```java
	@Test
    public void testOneCacheall() throws Exception {
        SqlSession sqlSession1 = MyBatisUtil.getSqlSession();
        UserMapper userMapper1 = sqlSession1.getMapper(UserMapper.class);
        User user1 = userMapper1.findById(1);
        System.out.println("第一次查询的用户：" + user1);
        sqlSession1.close();
        System.out.println("----------------------------");
        //sqlSession1 和sqlSession2 缓存不共享 独立缓存区
        SqlSession sqlSession2 = MyBatisUtil.getSqlSession();
        UserMapper userMapper2 = sqlSession2.getMapper(UserMapper.class);
        User user2 = userMapper2.findById(1);
        System.out.println("第二次查询的用户：" + user2);
        sqlSession2.close();
    }
```

**配置核心配置文件**

```xml
	<settings>
        <!--开启二级缓存-->
        <setting name="cacheEnabled" value="true"/>
    </settings>
```

配置UserMapper.xml映射 

```xml
    <!--当前映射文件开启二级缓存-->
    <cache></cache>
    <!--
    <select>标签中设置useCache=”true”代表当前这个statement要使用二级缓存。
    如果不使用二级缓存可以设置为false
    注意：针对每次查询都需要最新的数据sql，要设置成useCache="false"，禁用二级缓存。-->
	<select id="findById" parameterType="int" resultType="user" useCache="true">
        SELECT * FROM `user` where id = #{id}
    </select>
```

MyBatisUtil

```java
public class MyBatisUtil {
    
    static SqlSessionFactory sqlSessionFactory;

    static {
        /* 加载核心配置文件 */
        InputStream is = null;
        try {
            is = Resources.getResourceAsStream("SqlMapConfig.xml");
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
        /* 获取SqlSessionFactory工厂对象 */
        sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);
    }

    public static SqlSession getSqlSession() throws IOException {
        /* 获取SqlSession会话对象 true 自动提交事务 */
        SqlSession sqlSession = sqlSessionFactory.openSession(true);
        return sqlSession;
    }
}
```

修改User实体

```java
public class User implements Serializable {
    
}
```

测试

```java
	@Test
    public void testOneCacheall() throws Exception {
        SqlSession sqlSession1 = MyBatisUtil.getSqlSession();
        UserMapper userMapper1 = sqlSession1.getMapper(UserMapper.class);
        User user1 = userMapper1.findById(1);
        System.out.println("第一次查询的用户：" + user1);
        sqlSession1.close();
        System.out.println("----------------------------");
        SqlSession sqlSession2 = MyBatisUtil.getSqlSession();
        UserMapper userMapper2 = sqlSession2.getMapper(UserMapper.class);
        User user2 = userMapper2.findById(1);
        System.out.println("第二次查询的用户：" + user2);
        sqlSession2.close();
    }
```

**分析**

二级缓存是mapper映射级别的缓存，多个SqlSession去操作同一个Mapper映射的sql语句，多个 SqlSession可以共用二级缓存，二级缓存是跨SqlSession的。

映射语句文件中的所有select语句将会被缓存。 

映射语句文件中的所有insert、update和delete语句会刷新缓存。

**注意问题（脏读）** 

mybatis的二级缓存因为是namespace级别，所以在进行多表查询时会产生脏读问题

**小结** 

mybatis的缓存，都不需要我们手动存储和获取数据。mybatis自动维护的。 

mybatis开启了二级缓存后，那么查询顺序：二级缓存-->一级缓存-->数据库 

注意：mybatis的二级缓存会存在脏读问题，需要使用第三方的缓存技术解决问题。

## MyBatis注解

### MyBatis常用注解

这几年来注解开发越来越流行，Mybatis也可以使用注解开发方式，这样我们就可以减少编写 Mapper映射文件了。我们先围绕一些基本的CRUD来学习，再学习复杂映射多表操作

```xml
@Insert：实现新增，代替了<insert></insert>
@Delete：实现删除，代替了<delete></delete>
@Update：实现更新，代替了<update></update>
@Select：实现查询，代替了<select></select>
@Result：实现结果集封装，代替了<result></result>
@Results：可以与@Result 一起使用，封装多个结果集，代替了<resultMap></resultMap>
@One：实现一对一结果集封装，代替了<association></association>
@Many：实现一对多结果集封装，代替了<collection></collection>
```

### MyBatis注解的增删改查

创建UserMapper接口

```java
public interface UserMapper {
   	@Select("SELECT * FROM `user`")
    public List<User> findAll();
    @Insert("INSERT INTO user(username,birthday,sex,address)VALUES(#{username},#{birthday},#{sex},#{address})")
            public void save(User user);
    @Update("UPDATE `user` SET username = #{username},birthday = #{birthday},sex = #{sex},address = #{address} WHERE id = #{id}")
            public void update(User user);
    @Delete("DELETE FROM `user` where id = #{id}")
    public void delete(Integer id);
}
```

编写核心配置文件 sqlMapConfig.xml

```xml
	<!--我们使用了注解替代的映射文件，所以我们只需要加载使用了注解的Mapper接口即可-->
        <mappers>
            <!--扫描使用注解的Mapper类-->
            <mapper class="com.aaa.mapper.UserMapper"></mapper>
        </mappers>
```

```xml
	<!--或者指定扫描包含映射关系的接口所在的包也可以-->
        <mappers>
            <!--扫描使用注解的Mapper类所在的包-->
            <package name="com.aaa.mapper"></package>
        </mappers>
```

测试代码

```java
	//查询
    @Test
    public void testFindAll() throws Exception {
        SqlSession sqlSession = MyBatisUtil.getSqlSession();
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        List<User> list = userMapper.findAll();
        for (User user : list) {
            System.out.println(user);
        }
    }
	//添加
    @Test
    public void testSave() throws Exception {
        SqlSession sqlSession = MyBatisUtil.getSqlSession();
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        User user = new User();
        user.setUsername("于谦");
        user.setBirthday(new Date());
        user.setSex("男");
        user.setAddress("德云社");
        userMapper.save(user);
    }
    //更新
    @Test
    public void testUpdate() throws Exception {
        SqlSession sqlSession = MyBatisUtil.getSqlSession();
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        User user = new User();
        user.setId(14);
        user.setUsername("郭德纲");
        user.setBirthday(new Date());
        user.setSex("男");
        user.setAddress("德云社");
        userMapper.update(user);
    }
    //删除
    @Test
    public void testDelete() throws Exception {
        SqlSession sqlSession = MyBatisUtil.getSqlSession();
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        userMapper.delete(4);
    }
```

### 使用注解实现复杂映射开发

之前我们在映射文件中通过配置 resultMap、association、collection 来实现复杂关系映射。

使用注解开发后，我们可以使用 @Results、@Result，@One、@Many 注解组合完成复杂关系的配置。

![](https://image.aobayu.cn/images/Results.jpg)

![](https://image.aobayu.cn/images/OneMany.jpg)

### 一对一查询

需求：查询一个订单，与此同时查询出该订单所属的用户

一对一查询语句：

SELECT * FROM orders;

SELECT * FROM user WHERE id = #{订单的uid};

**代码实现**

OrderMapper1接口

```java
public interface OrderMapper1 {
    @Select("select * from orders")
    @Results({
            @Result(id = true,column = "id",property = "id"),
            @Result(column = "ordertime",property = "ordertime"),
            @Result(column = "total",property = "total"),
            @Result(property = "user",javaType = User.class,column = "uid",one = @One(
                    select ="com.example.mapper.UserMapper1.findById",fetchType = FetchType.EAGER))
    })
    public List<Orders> findAllWithUser();
}
```

UserMapper1接口

```java
public interface UserMapper1 {
	@Select("SELECT * FROM `user` WHERE id = #{id}")
    public User findById(Integer id);
}
```

sqlMapConfig.xml 配置

```xml
	<mappers>
        <!--扫描使用注解的Mapper类-->
        <mapper class="com.example.mapper.UserMapper1"></mapper>
        <mapper class="com.example.mapper.OrderMapper1"></mapper>
    </mappers>
```

测试代码

```java
	@Test
    public void testOrderWithUser1() throws Exception {
        SqlSession sqlSession = MyBatisUtil.getSqlSession();
        OrderMapper1 orderMapper = sqlSession.getMapper(OrderMapper1.class);
        List<Orders> list = orderMapper.findAllWithUser();
        for (Orders order : list) {
            System.out.println(orders);
        }
    }
```

### 一对多查询

需求：查询一个用户，与此同时查询出该用户具有的订单

一对多查询语句：

SELECT * FROM user;

SELECT * FROM orders where uid = #{用户id};

**代码实现**

UserMapper1接口

```java
public interface UserMapper1 {
    @Select("select *from user")
    @Results({
            @Result(id = true,column = "id",property = "id"),
            @Result(column = "brithday",property = "brithday"),
            @Result(column = "sex",property = "sex"),
            @Result(column = "address",property = "address"),
            @Result(property = "orderList",javaType = List.class,column = "id",
                    many = @Many(select = "com.example.mapper.OrderMapper1.findById",fetchType= FetchType.EAGER))
    })
    public List<User> findAllWithOrder();
}
```

OrderMapper1接口

```java
public interface OrderMapper1 {
    @Select("select *from orders")
    public List<Orders> findById();
}
```

测试代码

```java
	@Test
    public void testUserWithOrder() throws Exception {
        SqlSession sqlSession = MyBatisUtil.getSqlSession();
        UserMapper1 userMapper = sqlSession.getMapper(UserMapper1.class);
        List<User> list = userMapper.findAllWithOrder();
        for (User user : list) {
            System.out.println(user);
        }
    }
```

### 多对多查询

需求：查询所有用户，同时查询出该用户的所有角色 多对多查询语句

SELECT * FROM user;

SELECT * FROM role r INNER JOIN user_role ur ON r.`id` = ur.`rid` WHERE ur.`uid` = #{用户id};

**代码实现**

UserMapper1接口

```java
public interface UserMapper1 {	
	@Select("SELECT * FROM `user`")
    @Results({
            @Result(id = true, column = "id", property = "id"),
            @Result(column = "brithday", property = "brithday"),
            @Result(column = "sex", property = "sex"),
            @Result(column = "address", property = "address"),
            @Result(property = "roleList", javaType = List.class,
                    column = "id" ,
                    many = @Many(select = "com.example.mapper.RoleMapper1.findByUid",fetchType = FetchType.EAGER))
    })
    public List<User> findAllWithRole();
}
```

RoleMapper1接口

```java
public interface RoleMapper1 {
    @Select("SELECT * FROM role r INNER JOIN user_role ur ON r.id = ur.roleid WHERE ur.userid = #{uid}")
    public List<Role> findByUid(Integer uid);
}
```

sqlMapConfig.xml 配置

```xml
	<mappers>
        <!--扫描使用注解的Mapper类-->
        <mapper class="com.example.mapper.UserMapper1"></mapper>
        <mapper class="com.example.mapper.OrderMapper1"></mapper>
        <mapper class="com.example.mapper.RoleMapper1"></mapper>
    </mappers>
```

测试代码

```java
	@Test
    public void testUserWithRole() throws Exception {
        SqlSession sqlSession = MyBatisUtil.getSqlSession();
        UserMapper1 userMapper = sqlSession.getMapper(UserMapper1.class);
        List<User> list = userMapper.findAllWithRole();
        for (User user : list) {
            System.out.println(user);
        }
    }
```

### 基于注解的二级缓存

**配置SqlMapConfig.xml文件开启二级缓存的支持**

```xml
	<settings>
        <!--
        因为cacheEnabled的取值默认就为true，所以这一步可以省略不配置。
        为true代表开启二级缓存；为false代表不开启二级缓存。
        -->
        <setting name="cacheEnabled" value="true"/>
    </settings>
```

**在Mapper接口中使用注解配置二级缓存**

```java
@CacheNamespace
public interface UserMapper {...}
```

**注解延迟加载**

不管是一对一还是一对多 ，在注解配置中都有fetchType的属性

```
fetchType = FetchType.LAZY 表示懒加载
fetchType = FetchType.EAGER 表示立即加载
fetchType = FetchType.DEFAULT 表示使用全局配置 
```

**小结**

 注解开发和xml配置优劣分析 

1.注解开发和xml配置相比，从开发效率来说，注解编写更简单，效率更高。 

2.从可维护性来说，注解如果要修改，必须修改源码，会导致维护成本增加。xml维护性更强。