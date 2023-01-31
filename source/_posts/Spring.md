---
title: Spring
copyright_url: https://www.aobayu.cn/2022/11/16/Spring/
tags: 
    - Spring
categories: 学习之路
date: 2022-11-16
keywords: Spring
description: Spring是分层的 Java SE/EE应用 full-stack(全栈式) 轻量级开源框架。提供了表现层SpringMVC和持久层 Spring JDBC Template以及业务层事务管理等众多的企业级应用技术，还能整合开源世界众多著名的第三方框架和类库，逐渐成为使用最多的Java EE 企业应用开源框架。--本文为自己学习中所写。
---

## Spring

Spring是分层的 Java SE/EE应用 full-stack(全栈式) 轻量级开源框架。

提供了表现层 SpringMVC和持久层 Spring JDBC Template以及 业务层 事务管理等众多的企业级应用 技术，还能整合开源世界众多著名的第三方框架和类库，逐渐成为使用最多的Java EE 企业应用开源框架。

**两大核心**：以 IOC（Inverse Of Control：控制反转）和 AOP（Aspect Oriented Programming：面向 切面编程）为内核。

**Spring优势**

- 方便解耦，简化开发
  - Spring就是一个容器，可以将所有对象创建和关系维护交给Spring管理
  - 什么是耦合度？对象之间的关系，通常说当一个模块(对象)更改时也需要更改其他模块(对象)，这就是耦合，耦合度过高会使代码的维护成本增加。要尽量解耦

- AOP编程的支持
  - Spring提供面向切面编程，方便实现程序进行权限拦截，运行监控等功能。

- 声明式事务的支持
  - 通过配置完成事务的管理，无需手动编程

- 方便测试，降低JavaEE API的使用
  - Spring对Junit4支持，可以使用注解测试

- 方便集成各种优秀框架
  - 不排除各种优秀的开源框架，内部提供了对各种优秀框架的直接支持

## 初识IOC

**控制反转（Inverse Of Control）**不是什么技术，而是一种设计思想。它的目的是指导我们设计出更 加松耦合的程序。

> 控制：在java中指的是对象的控制权限（创建、销毁）
>
> 反转：指的是对象控制权由原来 由开发者在类中手动控制 反转到 由Spring容器控制 

**自定义IOC容器**

需求：

实现service层与dao层代码解耦合

步骤分析：

1. 创建java项目，导入自定义IOC相关坐标

2. 编写Dao接口和实现类

3. 编写Service接口和实现类

4. 编写测试代码

**实现**

创建java项目，导入自定义IOC相关坐标

pom.xml

```xml
	<dependencies>
        <dependency>
            <groupId>dom4j</groupId>
            <artifactId>dom4j</artifactId>
            <version>1.6.1</version>
        </dependency>
        <dependency>
            <groupId>jaxen</groupId>
            <artifactId>jaxen</artifactId>
            <version>1.1.6</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
    </dependencies>
```

编写Dao接口和实现类 com.aaa.dao.

```java
public interface UserDao {
    public void save();
}
```

```java
public class UserImpl implements UserDao {
    @Override
    public void save() {
        System.out.println("保存成功....");
    }
}
```

编写Service接口和实现类 com.aaa.service.

```java
public interface UserService {
    public void save();
}
```

```java
public class UserServiceImpl implements UserService{
    private UserDao userDao;
    public void save(){
        userDao = new UserImpl();
        userDao.save();
    }
}
```

编写测试代码

```java
public class UserTest {
    @Test
    public void testSave() throws Exception {
        UserService userService = new UserServiceImpl();
        userService.save();
    }
}
```

当前service对象和dao对象耦合度太高，而且每次new的都是一个新的对象，导致服务器压力过大。

> 解耦合的原则是编译期不依赖，而运行期依赖就行了。

把所有需要创建对象的信息定义在配置文件中 resources.beans.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<beans>
    <bean id="userDao" class="com.aaa.dao.impl.UserImpl"></bean>
</beans>
```

编写BeanFactory工具类 com.aaa.utils.

```java
public class BeanFactory {
    /* 声明集合用来保存bean  */
    private static Map<String, Object> ioc = new HashMap<>();

    static {
        try {
            /* 1.读取配置文件 */
            InputStream in =
                    BeanFactory.class.getClassLoader().getResourceAsStream("beans.xml");
            /* 2.解析xml */
            SAXReader saxReader = new SAXReader();
            Document document = saxReader.read(in);
            /* 3.编写xpath表达式 */
            String xpath = "//bean";
            /* 4.获取所有的bean标签 */
            List<Element> list = document.selectNodes(xpath);
            /* 5.遍历并创建对象实例，设置到map集合中 */
            for (Element element : list) {
                String id = element.attributeValue("id");
                String className = element.attributeValue("class");
                Object object = Class.forName(className).newInstance();
                ioc.put(id, object);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    // 获取指定id的对象实例
    public static Object getBean(String beandId) {
        return ioc.get(beandId);
    }
}
```

修改UserServiceImpl实现类

```java
public class UserServiceImpl implements UserService{
    private UserDao userDao;
    public void save(){
        userDao = (UserDao) BeanFactory.getBean("userDao");
        userDao.save();
    }
}
```

**知识小结**

其实升级后的BeanFactory就是一个简单的Spring的IOC容器所具备的功能。

之前我们需要一个userDao实例，需要开发者自己手动创建 new UserDao();

现在我们需要一个userdao实例，直接从spring的IOC容器获得，对象的创建权交给了spring控制

最终目标：代码解耦合

## Spring快速入门

需求：借助spring的IOC实现service层与dao层代码解耦合

步骤分析：

1. 创建java项目，导入spring开发基本坐标

2. 编写Dao接口和实现类

3. 创建spring核心配置文件

4. 在spring配置文件中配置 UserImpl

5. 使用spring相关API获得Bean实例

**实现**

创建java项目，导入spring开发基本坐标

```xml
	<dependencies>
        <dependency>
            <groupId>dom4j</groupId>
            <artifactId>dom4j</artifactId>
            <version>1.6.1</version>
        </dependency>
        <dependency>
            <groupId>jaxen</groupId>
            <artifactId>jaxen</artifactId>
            <version>1.1.6</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
        <!--spring开发-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
    </dependencies>
```

编写Dao接口和实现类 com.aaa.dao.

```java
public interface UserDao {
    public void save();
}
```

```java
public class UserImpl implements UserDao {
    @Override
    public void save() {
        System.out.println("保存成功....");
    }
}
```

创建spring核心配置文件 resources.applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--在spring配置文件中配置 UserDaoImpl-->
    <bean id="userDao" class="com.aaa.dao.impl.UserImpl"></bean>
</beans>
```

使用spring相关API获得Bean实例

```java
	@Test
    public void testSave() throws Exception {
        /* 配置文件一加载直接创建出来对象 */
        /* 加载同时保存bean到容器中 */
        ApplicationContext applicationContext =
                new ClassPathXmlApplicationContext("applicationContext.xml");
        /* 直接从容器中获取 */
        UserDao userDao = (UserDao) applicationContext.getBean("userDao");
        userDao.save();
    }
	@Test
    public void testSave2() throws Exception {
        XmlBeanFactory xmlBeanFactory = new XmlBeanFactory(new 		ClassPathResource("applicationContext.xml"));
        /* 使用时才会去初始化创建出来 */
        UserDao userDao = (UserDao) xmlBeanFactory.getBean("userDao");
        userDao.save();
    }
```

## Spring相关API

Spring的API体系异常庞大，我们现在只关注两个BeanFactory和ApplicationContext

### BeanFactory

BeanFactory是 IOC 容器的核心接口，它定义了IOC的基本功能

> 特点：在第一次调用getBean()方法时，创建指定对象的实例

```java
	@Test
    public void testSave2() throws Exception {
        /*  核心接口，不会创建bean对象存到容器中 */
        XmlBeanFactory xmlBeanFactory = new XmlBeanFactory(new ClassPathResource("applicationContext.xml"));
        /* getBean的时候才真正创建bean对象 */
        UserDao userDao = (UserDao) xmlBeanFactory.getBean("userDao");
        userDao.save();
    }
```

### ApplicationContext

代表应用上下文对象，可以获得spring中IOC容器的Bean对象

> 特点：在spring容器启动时，加载并创建所有对象的实例

**常用实现类** 

1. ClassPathXmlApplicationContext 它是从类的根路径下加载配置文件 推荐使用这种。 

2. FileSystemXmlApplicationContext 它是从磁盘路径上加载配置文件，配置文件可以在磁盘的任意位置。 

3. AnnotationConfigApplicationContext 当使用注解配置容器对象时，需要使用此类来创建 spring 容器。它用来读取注解。

```java
	@Test
    public void test(){
        /* 获取到了spring上下文对象，借助上下文对象可以获取到IOC容器中的bean对象,
        加载的同时就创建了bean对象存到容器中 */
        ApplicationContext classPathXmlApplicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
        
        //ApplicationContext fileSystemXmlApplicationContext = new FileSystemXmlApplicationContext("D:\\xxx\\xxx\\src\\main\\resources\\applicationContext.xml");
		/*使用上下文对象从IOC容器中获取到了bean对象
		根据beanid在容器中找对应的bean对象 */
        //UserDao userDao = (UserDao) fileSystemXmlApplicationContext.getBean("userDao");
        
        /*根据类型在容器中进行查询：有可能报错的情况：根据当前类型匹配到多个实例 */
        UserDao userDao = classPathXmlApplicationContext.getBean("userDao",UserDao.class);
        /* 调用方法 */
        userDao.save();
    }
```

**常用方法** 

1. Object getBean(String name)：根据Bean的id从容器中获得Bean实例，返回是Object，需要强转。

2. <> T getBean(Class<> requiredType)：根据类型从容器中匹配Bean实例，当容器中相同类型的Bean有多个时，则此方法会报错。

3. <> T getBean(String name,Class<> requiredType)：根据Bean的id和类型获得Bean实例，解决容器中相同类型Bean有多个情况。

## Spring配置文件

### Bean标签基本配置 

```xml
<bean id="" class="" scope=""></bean>
<!--用于配置对象交由Spring来创建。
	基本属性：
  	id：Bean实例在Spring容器中的唯一标识
  	class：Bean的全限定名
	默认情况下它调用的是类中的无参构造函数，如果没有无参构造函数则不能创建成功-->
```

**Bean标签范围配置**

scope属性指对象的作用范围，取值如下：

| 取值范围  | 说明                                                         |
| --------- | ------------------------------------------------------------ |
| singleton | 默认值，单例的                                               |
| prototype | 多例的，生成一个新的对象，占内存空间                         |
| request   | WEB项目中，Spring创建一个Bean的对象，将对象存入到request域中 |
| session   | WEB项目中，Spring创建一个Bean的对象，将对象存入到session域中 |

- 当scope的取值为singleton时
  - Bean的实例化个数：1个
  - Bean的实例化时机：当Spring核心文件被加载时，实例化配置的Bean实例

- Bean的生命周期：
  - 对象创建：当应用加载，创建容器时，对象就被创建了
  - 对象运行：只要容器在，对象一直活着
  - 对象销毁：当应用卸载，销毁容器时，对象就被销毁了

- 当scope的取值为prototype时
  - Bean的实例化个数：多个
  - Bean的实例化时机：当调用getBean()方法时实例化Bean
- Bean的生命周期：
  - 对象创建：当使用对象时，创建新的对象实例
  - 对象运行：只要对象在使用中，就一直活着
  - 对象销毁：当对象长时间不用时，被 Java 的垃圾回收器回收了

### Bean生命周期配置

```xml
<bean id="" class="" scope="" init-method="" destroy-method=""></bean>
<!-- init-method：指定类中的初始化方法名称 -->
<!-- destroy-method：指定类中销毁方法名称 -->
```

```xml
<bean id="userDao" class="com.aaa.dao.impl.UserImpl" init-method="init" destroy-method="destroy"></bean>
```

```java
public class UserImpl implements UserDao {
    @Override
    public void save() {
        System.out.println("保存成功....");
    }
    public void init(){
        System.out.println("init");
    }
    public void destroy(){
        System.out.println("destroy");
    }
}
```

### Bean实例化三种方式

**无参构造方法实例化**

默认无参构造方法来创建类对象，如果bean中没有默认无参构造函数，将会创建失败

```xml
<bean id="userDao" class="com.aaa.dao.impl.UserImpl"/>
```

**工厂静态方法实例化**
用静态方法，去创建出来一个bean，手动创建一个bean，不用Spring去创建 com.aaa.utils.StaticFactoryBean

```java
public class StaticFactoryBean {
    public static UserDao createUserDao(){
        return new UserImpl();
    }
}
```

```xml
<bean id="userDao" class="com.aaa.utils.StaticFactoryBean" factory-method="createUserDao" />
```

**工厂普通方法实例化**

com.aaa.utils.DynamicFactoryBean

```java
public class DynamicFactoryBean {
    public UserDao createUserDao(){
        return new UserImpl();
    }
}
```

```xml
<bean id="dynamicFactoryBean" class="com.aaa.utils.DynamicFactoryBean"/>
<!--FactoryBean 用来创建一类bean id="dynamicFactoryBean"-->
<bean id="userDao2" factory-bean="dynamicFactoryBean" factory-method="createUserDao"/>
```

### Bean依赖注入方式

**构造方法**

在UserServiceImpl中创建有参构造

```java
public class UserServiceImpl implements UserService{
    private UserDao userDao;
    public UserServiceImpl(UserDao userDao) {
        this.userDao = userDao;
    }
    @Override
    public void save() {
        userDao.save();
    }
}
```

配置Spring容器调用有参构造时进行注入

```xml
	<bean id="userDao" class="com.aaa.dao.impl.UserImpl"/>
    <bean id="userService" class="com.aaa.service.UserServiceImpl">
        <!-- <constructor-arg index="0" type="com.aaa.dao.UserDao" ref="userDao"/> -->
        <constructor-arg name="userDao" ref="userDao"/>
    </bean>
```

标签 constructor-arg

- name属性对应的值为构造函数中方法形参的参数名，必须要保持一致。
- ref属性指向的是spring的IOC容器中其他bean对象。

测试

```java
	@Test
    public void testSave() throws Exception {
        ApplicationContext classPathXmlApplicationContext =
            new ClassPathXmlApplicationContext("applicationContext.xml");
    	UserService userService =
            (UserService) classPathXmlApplicationContext.getBean("userService");
		userService.save();
    }
```

**set方法**

在UserServiceImpl中创建set方法

```java
public class UserServiceImpl implements UserService{
    private UserDao userDao;
    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }
    @Override
    public void save() {
        userDao.save();
    }
}
```

配置Spring容器调用set方法进行注入

```xml
	<bean id="userDao" class="com.aaa.dao.impl.UserImpl"/>
    <bean id="userService" class="com.aaa.service.UserServiceImpl">
        <constructor-arg name="userDao" ref="userDao"/>
    </bean>
```

**P命名空间注入(了解)**

P命名空间注入本质也是set方法注入，但比起上述的set方法注入更加方便，主要体现在配置文件中

需要引入P命名空间

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd"
       <!--P命名空间-->
       xmlns:p="http://www.springframework.org/schema/p">
```

修改注入方式

```xml
<bean id="userDao" class="com.aaa.dao.impl.UserImpl"/>
<bean id="userService" class="com.aaa.service.UserServiceImpl" p:userDao-ref="userDao"/>
```

### Bean依赖注入的数据类型

除了对象的引用可以注入，普通数据类型和集合都可以在容器中进行注入。 以set方法注入为例，演示普通数据类型和集合数据类型的注入。

**注入普通数据类型**

```java
public class User {
    private String username;
    private String age;
    
    public void setUsername(String username) {
        this.username = username;
    }
    public void setAge(String age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "User{" +
                "username='" + username + '\'' +
                ", age='" + age + '\'' +
                '}';
    }
}
```

```xml
<!--    注入普通数据类型-->
    <bean id="user" class="com.aaa.domain.User">
        <property name="username" value="fly"/>
        <property name="age" value="19"/>
    </bean>
```

```java
	@Test
    public void Save(){
        ApplicationContext classPathXmlApplicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
        User user = classPathXmlApplicationContext.getBean("user", User.class);
        System.out.println(user);
    }
```

**注入集合数据类型**

List集合注入

```java
public class UserDaoImpl{
    private List<Object> list;
    public void setList(List<Object> list) {
        this.list=list;
    }
    public void save1(){
        System.out.println(list);
    }
}
```

```xml
<!--    注入普通数据类型-->
    <bean id="user" class="com.aaa.domain.User">
        <property name="username" value="fly"/>
        <property name="age" value="19"/>
    </bean>
<!--    List集合注入-->
    <bean id="userList" class="com.aaa.dao.impl.UserDaoImpl">
        <property name="list">
            <list>
                <value>fly</value>
                <!--调用 bean id="user" 数据 -->
                <ref bean="user"></ref>
            </list>
        </property>
    </bean>
```

```java
	@Test
    public void Save1(){
        ApplicationContext classPathXmlApplicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
        UserDaoImpl user = classPathXmlApplicationContext.getBean("userList", UserDaoImpl.class);
        user.save1();
    }
```

Set集合注入

```java
public class UserDaoImpl{
	private Set<Object> set;
    public void setSet(Set<Object> set) {
        this.set = set;
    }
    public void save2() {
        System.out.println(set);
        System.out.println("保存成功了...");
    }
}
```

```xml
	<bean id="userSet" class="com.aaa.dao.impl.UserDaoImpl">
        <property name="set">
            <set>
                <value>bbb</value>
            </set>
        </property>
    </bean>
```

```java
@Test
    public void Save2(){
        ApplicationContext classPathXmlApplicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
        UserDaoImpl user = classPathXmlApplicationContext.getBean("userSet", UserDaoImpl.class);
        user.save2();
    }
```

Array数组注入

```java
public class UserDaoImpl{
	private Object[] array;
    public void setArray(Object[] array) {
        this.array = array;
    }
    public void save() {
        System.out.println(Arrays.toString(array));
        System.out.println("保存成功了...");
    }
}
```

```xml
<bean id="userArray" class="com.aaa.dao.impl.UserDaoImpl">
        <property name="array">
            <array>
                <value>ccc</value>
            </array>
        </property>
    </bean>
```

Map集合注入

```java
public class UserDaoImpl{
	private Map<String, Object> map;
    public void setMap(Map<String, Object> map) {
        this.map = map;
    }
    public void save() {
        System.out.println(map);
        System.out.println("保存成功了...");
    }
}
```

```xml
	<bean id="userMap" class="com.aaa.dao.impl.UserDaoImpl">
        <property name="map">
            <map>
                <entry key="k1" value="ddd"/>
                <entry key="k2" value-ref="user"></entry>
            </map>
        </property>
    </bean>
```

Properties配置注入

```java
public class UserDaoImpl{
	private Properties properties;
        public void setProperties(Properties properties) {
            this.properties = properties;
        }
        public void save() {
            System.out.println(properties);
            System.out.println("保存成功了...");
        }
}
```

```xml
	<bean id="userProperties" class="com.aaa.dao.impl.UserDaoImpl">
        <property name="properties">
            <props>
                <prop key="k1">v1</prop>
                <prop key="k2">v2</prop>
                <prop key="k3">v3</prop>
            </props>
        </property>
    </bean>
```

### 配置文件模块化

实际开发中，Spring的配置内容非常多，这就导致Spring配置很繁杂且体积很大，所以，可以将部分 配置拆解到其他配置文件中，也就是所谓的配置文件模块化。

主从配置文件

```xml
	<!-- import 标签导入 applicationContext-into.xml 配置文件-->
    <import resource="applicationContext-into.xml"/>
```

applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="userDao" class="com.aaa.dao.impl.UserImpl"/>

    <bean id="userDaos" class="com.aaa.dao.impl.UserImpl" init-method="init" destroy-method="destroy" />
	<!-- 导入 applicationContext-into.xml 配置文件-->
    <import resource="applicationContext-into.xml"/>
</beans>
```

applicationContext-into.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--    注入普通数据类型-->
    <bean id="user" class="com.aaa.domain.User">
        <property name="username" value="fly"/>
        <property name="age" value="19"/>
    </bean>
    <!--    List集合注入-->
    <bean id="userList" class="com.aaa.dao.impl.UserDaoImpl">
        <property name="list">
            <list>
                <value>fly</value>
            </list>
        </property>
    </bean>
</beans>
```

并列的多个配置文件

```java
ApplicationContext act = new ClassPathXmlApplicationContext("beans1.xml","beans2.xml","...");
```

```java
ApplicationContext classPathXmlApplicationContext = new ClassPathXmlApplicationContext("applicationContext.xml","applicationContext-into.xml");
```

> 注意： 同一个xml中不能出现相同名称的bean,如果出现会报错 多个xml如果出现相同名称的bean，不会报错，但是后加载的会覆盖前加载的bean

## IOC实战案例

**DbUtils**

DbUtils是Apache的一款用于简化Dao代码的工具类，它底层封装了JDBC技术。

核心对象

```java
QueryRunner queryRunner = new QueryRunner(DataSource dataSource)
```

查询数据库所有账户信息到Account实体中

```java
public class DbUtilsTest {
        @Test
        public void findAllTest() throws Exception {
            /* 创建DBUtils工具类，传入连接池 */
            QueryRunner queryRunner = new QueryRunner(JdbcUtils.getDataSource());
            /* 编写sql */
            String sql = "select * from account";
            /* 执行sql */
            List<Account> list = queryRunner.query(sql,
                    new BeanListHandler<Account>(Account.class));
            /* 打印结果 */
            for (Account account : list) {
                System.out.println(account);
            }
        }
}
```

**Spring的DbUtils**

基于Spring的xml配置实现账户的CRUD案例 

步骤分析：

1. 准备数据库环境 

2. 创建java项目，导入坐标 

3. 编写Account实体类 

4. 编写AccountDao接口和实现类 

5. 编写AccountService接口和实现类 

6. 编写spring核心配置文件 

7. 编写测试代码

**准备数据库环境**

```sql
CREATE DATABASE `spring_db`;
USE `spring_db`;
CREATE TABLE `account` (
                           `id` int(11) NOT NULL AUTO_INCREMENT,
                           `name` varchar(32) DEFAULT NULL,
                           `money` double DEFAULT NULL,
                           PRIMARY KEY (`id`)
) ;
insert into `account`(`id`,`name`,`money`)
values (1,'tom',1000),
        (2,'jerry',1000);
```

**创建java项目，导入坐标**

```xml
<dependencies>
		<dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>


        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.38</version>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.2.8</version>
        </dependency>
        <dependency>
            <groupId>commons-dbutils</groupId>
            <artifactId>commons-dbutils</artifactId>
            <version>1.6</version>
        </dependency>
</dependencies>
```

**编写Account实体类**

```java
public class Account {
    private Integer id;
    private String name;
    private Double money;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Double getMoney() {
        return money;
    }

    public void setMoney(Double money) {
        this.money = money;
    }

    @Override
    public String toString() {
        return "Account{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", money=" + money +
                '}';
    }
}

```

**编写AccountDao接口和实现类**

```java
public interface AccountDao {
    public List<Account> findAll();
    public Account findById(Integer id);
    public void save(Account account);
    public void update(Account account);
    public void delete(Integer id);
}
```

```java
public class AccountDaoImpl implements AccountDao {
    private QueryRunner queryRunner;
    public void setQueryRunner(QueryRunner queryRunner) {
        this.queryRunner = queryRunner;
    }
    @Override
    public List<Account> findAll() {
        List<Account> list = null;
        /* 编写sql */
        String sql = "select * from account";
        try {
            /* 执行sql */
            list = queryRunner.query(sql,
                    new BeanListHandler<Account>(Account.class));
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return list;
    }

    @Override
    public Account findById(Integer id) {
        Account account = null;
        /* 编写sql */
        String sql = "select * from account where id = ?";
        try {
            /* 执行sql */
            account = queryRunner.query(sql,
                    new BeanHandler<Account>(Account.class), id);
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return account;
    }
    @Override
    public void save(Account account) {
        /* 编写sql */
        String sql = "insert into account values(null,?,?)";
        /* 执行sql */
        try {
            queryRunner.update(sql, account.getName(), account.getMoney());
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    @Override
    public void update(Account account) {
        /* 编写sql */
        String sql = "update account set name = ?,money = ? where id = ?";
        /* 执行sql */
        try {
            queryRunner.update(sql, account.getName(),
                    account.getMoney(),account.getId());
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    @Override
    public void delete(Integer id) {
        /* 编写sql */
        String sql = "delete from account where id = ?";
        /* 执行sql */
        try {
            queryRunner.update(sql, id);
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

**编写AccountService接口和实现类**

```java
public interface AccountService {
    public List<Account> findAll();
    public Account findById(Integer id);
    public void save(Account account);
    public void update(Account account);
    public void delete(Integer id);
}
```

```java
public class AccountServiceImpl implements AccountService {

    private AccountDao accountDao;
    public void setAccountDao(AccountDao accountDao) {
        this.accountDao = accountDao;
    }
    @Override
    public List<Account> findAll() {
        return accountDao.findAll();
    }
    @Override
    public Account findById(Integer id) {
        return accountDao.findById(id);
    }
    @Override
    public void save(Account account) {
        accountDao.save(account);
    }
    @Override
    public void update(Account account) {
        accountDao.update(account);
    }
    @Override
    public void delete(Integer id) {
        accountDao.delete(id);
    }
}
```

**编写spring核心配置文件 applicationContext-db.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--把数据库连接池交给IOC容器-->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="com.mysql.jdbc.Driver" />
        <property name="url" value="jdbc:mysql://localhost:3306/spring_db?useSSL=false&amp;useServerPrepStmts=true&amp;characterEncoding=utf-8&amp;serverTimezone=Asia/Shanghai" />
        <property name="username" value="root" />
        <property name="password" value="123456" />
    </bean>
    <!--把QueryRunner交给IOC容器-->
    <bean id="queryRunner" class="org.apache.commons.dbutils.QueryRunner">
        <constructor-arg name="ds" ref="dataSource"></constructor-arg>
    </bean>
    <!--把AccountDao交给IOC容器-->
    <bean id="accountDao" class="com.aaa.dao.impl.AccountDaoImpl">
        <property name="queryRunner" ref="queryRunner"></property>
    </bean>
    <!--把AccountService交给IOC容器-->
    <bean id="accountService" class="com.aaa.service.impl.AccountServiceImpl">
        <property name="accountDao" ref="accountDao"></property>
    </bean>
</beans>
```

**编写测试代码**

```java
public class AccountTest {
    ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext-db.xml");
    AccountService accountService = applicationContext.getBean(AccountService.class);
    /* 测试保存 */
    @Test
    public void testSave() {
        Account account = new Account();
        account.setName("lucy");
        account.setMoney(100d);
        accountService.save(account);
    }
    /* 测试查询 */
    @Test
    public void testFindById() {
        Account account = accountService.findById(3);
        System.out.println(account);
    }
    /* 测试查询所有 */
    @Test
    public void testFindAll() {
        List<Account> accountList = accountService.findAll();
        for (Account account : accountList) {
            System.out.println(account);
        }
    }
    /* 测试修改 */
    @Test
    public void testUpdate() {
        Account account = new Account();
        account.setId(3);
        account.setName("jack");
        account.setMoney(2000d);
        accountService.update(account);
    }
    /* 测试删除 */
    @Test
    public void testDelete() {
        accountService.delete(3);
    }
}
```

**抽取jdbc配置文件**

applicationContext.xml加载jdbc.properties配置文件获得连接信息。 首先，需要引入context命名空间和约束路径

```
	* 命名空间：
    xmlns:context="http://www.springframework.org/schema/context"
    * 约束路径：
    http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context.xsd
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
    <context:property-placeholder location="classpath:jdbc.properties"/>
    <!--把数据库连接池交给IOC容器-->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${jdbc.driver}" />
        <property name="url" value="${jdbc.url}" />
        <property name="username" value="${jdbc.username}" />
        <property name="password" value="${jdbc.password}" />
    </bean>
```

jdbc.properties配置文件

```properties
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql:///spring_db?useSSL=false&useServerPrepStmts=true&characterEncoding=utf-8&serverTimezone=Asia/Shanghai
jdbc.username=root
jdbc.password=123456
```

## Spring注解开发

Spring是轻代码而重配置的框架，配置比较繁重，影响开发效率，所以注解开发是一种趋势，注解代 替xml配置文件可以简化配置，提高开发效率。 

### Spring常用注解

| 注解            | 说明                                                         |
| --------------- | ------------------------------------------------------------ |
| @component      | 使用在类上用于实例化Bean                                     |
| @Controller     | 使用在web层类上用于实例化Bean                                |
| @Service        | 使用在service层类上用于实例化Bean                            |
| @Repository     | 使用在dao层类上用于实例化Bean                                |
| @Autowired      | 使用在字段上用于根据类型依赖注入                             |
| @Qualifier      | 结合@Autowired一起使用,根据名称进行依赖注入                  |
| @Resource       | 相当于@Autowired+@Qualifier，按照名称进行注入                |
| @value          | 注入普通属性                                                 |
| @scope          | 标注Bean的作用范围                                           |
| @PostConstruct  | 使用在方法上标注该方法是Bean的初始化方法                     |
| @PreDestroy     | 使用在方法上标注该方法是Bean的销毁方法                       |
| @Configuration  | 用于指定当前类是一个Spring配置类，当创建容器时会从该类上加载注解 |
| @Bean           | 使用在方法上，标注将该方法的返回值存储到Spring容器中         |
| @PropertySource | 用于加载properties文件中的配置                               |
| @ComponentScan  | 用于指定Spring在初始化容器时要扫描的包                       |
| @lmport         | 用于导入其他配置类                                           |

说明：JDK11以后完全移除了javax扩展导致不能使用@resource注解

**maven引入依赖**

```xml
		<!--  引入注解依赖-->
        <dependency>
            <groupId>javax.annotation</groupId>
            <artifactId>javax.annotation-api</artifactId>
            <version>1.3.2</version>
        </dependency>
```

使用注解进行开发时，需要在applicationContext.xml中配置组件扫描，作用是指定哪个包及其子包 下的Bean需要进行扫描以便识别使用注解配置的类、字段和方法。

```xml
<!--注解的组件扫描-->
<context:component-scan base-package="com.aaa" />
```

**Bean实例化（IOC）**

使用@Compont或@Repository标识UserDaoImpl需要Spring进行实例化 AccountDaoImpl

```xml
<bean id="userDao" class="com.aaa.dao.impl.AccountDaoImpl"></bean>
```

```java
//@Component(value = "userDao")   如果没有写value属性值，Bean的id为：类名首字母小
@Repository
public class AccountDaoImpl implements AccountDao {}
```

**属性依赖注入（DI）**

使用@Autowired或者@Autowired+@Qulifier或者@Resource进行AccountDaoImpl的注入 不在使用Set方法

```xml
<bean id="userService" class="com.aaa.service.impl.AccountDaoImpl">
    <property name="queryRunner" ref="queryRunner"/>
</bean>
```

```java
@Repository
public class AccountDaoImpl implements AccountDao {
    /* <property name="userDao" ref="userDaoImpl"/>
    	@Autowired
    	@Qualifier("userDaoImpl")
    	@Resource(name = "userDaoImpl") */
       	@Autowired
    	private QueryRunner queryRunner;
}
```

**@Value**

使用@Value进行字符串的注入，结合SPEL表达式获得配置参数

```java
@Service
public class jdbcServiceTest implements Service {
    @Value("注入普通数据")
    private String str;
    @Value("${jdbc.driver}")
    private String driver;
}
```

@Scope

使用@Scope标注Bean的范围

```JAVA
@Service
@Scope("singleton")
public class ServiceImpl implements Service {}
```

**Bean生命周期**

使用@PostConstruct标注初始化方法，使用@PreDestroy标注销毁方法

```java
@PostConstruct
public void init(){System.out.println("初始化方法....");}
@PreDestroy
public void destroy(){System.out.println("销毁方法.....");}
```

### Spring注解整合DbUtils

修改AccountDaoImpl实现类

```java
//bean实例化
@Repository
public class AccountDaoImpl implements AccountDao {
    //注入
    @Autowired
    private QueryRunner queryRunner;
    
    @Override
    public List<Account> findAll() {
        List<Account> list = null;
        /* 编写sql */
        String sql = "select * from account";
        try {
            /* 执行sql */
            list = queryRunner.query(sql,
                    new BeanListHandler<Account>(Account.class));
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return list;
    }

    @Override
    public Account findById(Integer id) {
        Account account = null;
        /* 编写sql */
        String sql = "select * from account where id = ?";
        try {
            /* 执行sql */
            account = queryRunner.query(sql,
                    new BeanHandler<Account>(Account.class), id);
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return account;
    }
    @Override
    public void save(Account account) {
        /* 编写sql */
        String sql = "insert into account values(null,?,?)";
        /* 执行sql */
        try {
            queryRunner.update(sql, account.getName(), account.getMoney());
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    @Override
    public void update(Account account) {
        /* 编写sql */
        String sql = "update account set name = ?,money = ? where id = ?";
        /* 执行sql */
        try {
            queryRunner.update(sql, account.getName(),
                    account.getMoney(),account.getId());
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    @Override
    public void delete(Integer id) {
        /* 编写sql */
        String sql = "delete from account where id = ?";
        /* 执行sql */
        try {
            queryRunner.update(sql, id);
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

修改AccountServiceImpl实现类

```java
//bean实例化
@Service
public class AccountServiceImpl implements AccountService {
    //注入
    @Autowired
    private AccountDao accountDao;
    
    @Override
    public List<Account> findAll() {
        return accountDao.findAll();
    }
    @Override
    public Account findById(Integer id) {
        return accountDao.findById(id);
    }
    @Override
    public void save(Account account) {
        accountDao.save(account);
    }
    @Override
    public void update(Account account) {
        accountDao.update(account);
    }
    @Override
    public void delete(Integer id) {
        accountDao.delete(id);
    }
}
```

编写Spring核心配置类 com.aaa.springdao.SpringConfig

```java
@Configuration
@ComponentScan("com.aaa")
@Import(DataSourceConfig.class)
public class SpringConfig {
    @Autowired
    DataSource dataSource;
    @Bean("queryRunner")
    public QueryRunner getQueryRunner() {
        return new QueryRunner(dataSource);
    }
}
```

编写数据库配置信息类

```java
@PropertySource("classpath:jdbc.properties")
public class DataSourceConfig {
    @Value("${jdbc.driver}")
    private String driver;
    @Value("${jdbc.url}")
    private String url;
    @Value("${jdbc.username}")
    private String username;
    @Value("${jdbc.password}")
    private String password;

    @Bean("dataSource")
    public DataSource getDataSource() {
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setDriverClassName(driver);
        dataSource.setUrl(url);
        dataSource.setUsername(username);
        dataSource.setPassword(password);
        return dataSource;
    }
}
```

编写测试代码

```java
public class TestConfig {
    ApplicationContext applicationContext =
            new AnnotationConfigApplicationContext(SpringConfig.class);
    AccountService accountService =
            applicationContext.getBean(AccountService.class);
    /* 测试查询所有 */
    @Test
    public void testFindAll1() {
        List<Account> all = accountService.findAll();
        System.out.println(all);
    }
}
```

### Spring整合Junit

**普通Junit测试问题**

在普通的测试类中，需要开发者手动加载配置文件并创建Spring容器，然后通过Spring相关API获得 Bean实例；如果不这么做，那么无法从容器中获得对象。 

```java
ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml"); 
AccountService accountService = applicationContext.getBean(AccountService.class)
```

我们可以让SpringJunit负责创建Spring容器来简化这个操作，开发者可以直接在测试类注入Bean实 例；但是需要将配置文件的名称告诉它。

步骤分析：

1. 导入spring集成Junit的坐标

2. 使用@Runwith注解替换原来的运行器

3. 使用@ContextConfiguration指定配置文件或配置类

4. 使用@Autowired注入需要测试的对象

5. 创建测试方法进行测试 

导入spring集成Junit的坐标

```xml
<!--此处需要注意的是，spring5 及以上版本要求 junit 的版本必须是 4.12 及以上-->	
		<dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
```

使用@Runwith注解替换原来的运行器

```java
@RunWith(SpringJUnit4ClassRunner.class)
public class JnitTest {}
```

使用@ContextConfiguration指定配置文件或配置类

```java
@RunWith(SpringJUnit4ClassRunner.class)
/* 加载spring核心配置类 */
@ContextConfiguration(classes = {SpringConfig.class})
public class JnitTest {}
```

使用@Autowired注入需要测试的对象

```java
@RunWith(SpringJUnit4ClassRunner.class)
/* 加载spring核心配置类 */
@ContextConfiguration(classes = {SpringConfig.class})
public class JnitTest {
    @Autowired
    private AccountService accountService;
}
```

创建测试方法进行测试

```java
@RunWith(SpringJUnit4ClassRunner.class)
/* 加载spring核心配置类 */
@ContextConfiguration(classes = {SpringConfig.class})
public class JnitTest {
    @Autowired
    private AccountService accountService;
    /* 测试查询所有 */
    @Test
    public void testFindAll1() {
        List<Account> all = accountService.findAll();
        System.out.println(all);
    }
}
```

## Spring转账案例

### 转账案例

需求 使用spring框架整合DBUtils技术，实现用户转账功能 

步骤分析：

1. 创建java项目，导入坐标

2. 编写Account实体类

3. 编写AccountDao接口和实现类

4. 编写AccountService接口和实现类

5. 编写spring核心配置文件

6. 编写测试代码

创建java项目，导入坐标 

```xml
<dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.38</version>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.2.8</version>
        </dependency>
        <dependency>
            <groupId>commons-dbutils</groupId>
            <artifactId>commons-dbutils</artifactId>
            <version>1.6</version>
        </dependency>
</dependencies>
```

编写Account实体类 com.aaa.domain.

```java
public class Account {
    private Integer id;
    private String name;
    private Double money;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Double getMoney() {
        return money;
    }

    public void setMoney(Double money) {
        this.money = money;
    }

    @Override
    public String toString() {
        return "Account{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", money=" + money +
                '}';
    }
}
```

编写AccountDao接口和实现类 com.aaa.dao.

```java
public interface AccountDao {
    /* 转出操作 */
    public void out(String outUser, Double money);
    /* 转入操作 */
    public void in(String inUser, Double money);
}
```

```java
@Repository
public class AccountDaoImpl implements AccountDao {

    @Autowired
    private QueryRunner queryRunner;
    @Override
    public void out(String outUser, Double money) {
        try {
            queryRunner.update("update account set money=money-? where name=?", money, outUser);
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    @Override
    public void in(String inUser, Double money) {
        try {
            queryRunner.update("update account set money=money+? where name=?",money, inUser);
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

}
```

编写AccountService接口和实现类

```java
public interface AccountService {
    public void transfer(String outUser, String inUser, Double money);
}
```

```java
@Service
public class AccountServiceImpl implements AccountService {
    @Autowired
    private AccountDao accountDao;
    @Override
    public void transfer(String outUser, String inUser, Double money) {
        accountDao.out(outUser, money);
        accountDao.in(inUser, money);
    }
}
```

编写spring核心配置文件

jdbc.properties

```properties
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql:///spring_db?useSSL=false&useServerPrepStmts=true&characterEncoding=utf-8&serverTimezone=Asia/Shanghai
jdbc.username=root
jdbc.password=123456
```

applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
    <!--开启组件扫描-->
    <context:component-scan base-package="com.aaa"/>
    <!--加载jdbc配置文件-->
    <context:property-placeholder location="classpath:jdbc.properties"/>
    <!--把数据库连接池交给IOC容器-->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${jdbc.driver}"></property>
        <property name="url" value="${jdbc.url}"></property>
        <property name="username" value="${jdbc.username}"></property>
        <property name="password" value="${jdbc.password}"></property>
    </bean>
    <!--把QueryRunner交给IOC容器-->
    <bean id="queryRunner" class="org.apache.commons.dbutils.QueryRunner">
        <constructor-arg name="ds" ref="dataSource"></constructor-arg>
    </bean>
</beans>
```

编写测试代码

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:applicationContext.xml")
public class AccountTest {
    @Autowired
    private AccountService accountService;
    @Test
    public void testTransfer() throws Exception {
        accountService.transfer("tom", "jerry", 100d);
    }
}
```

问题分析：

上面的代码事务在dao层，转出转入操作都是一个独立的事务，但实际开发，应该把业务逻辑控制在 一个事务中，所以应该将事务挪到service层。

### 传统事务

编写线程绑定工具类

```java
/* 接工具类，从数据源中获取一个连接，并将实现和线程的绑定 */
@Component
public class ConnectionUtils {
    private ThreadLocal threadLocal = new ThreadLocal<>();
    @Autowired
    private DataSource dataSource;

    /*获取当前线程上的连接 return Connection*/
    public Connection getThreadConnection() {
        // 1.先从ThreadLocal上获取
        Connection connection = (Connection) threadLocal.get();
        // 2.判断当前线程是否有连接
        if (connection == null) {
            try {
                // 3.从数据源中获取一个连接，并存入到ThreadLocal中
                connection = dataSource.getConnection();
                threadLocal.set(connection);
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        return connection;
    }
    /*解除当前线程的连接绑定*/
    public void removeThreadConnection() {
        threadLocal.remove();
    }
}
```

编写事务管理器

```java
/* 事务管理器工具类，包含：开启事务、提交事务、回滚事务、释放资源*/
@Component
public class TransactionManager {
    @Autowired
    private ConnectionUtils connectionUtils;
    public void beginTransaction() {
        try {
            connectionUtils.getThreadConnection().setAutoCommit(false);
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    public void commit() {
        try {
            connectionUtils.getThreadConnection().commit();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    public void rollback() {
        try {
            connectionUtils.getThreadConnection().rollback();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    public void release() {
        try {
            /* 改回自动提交事务 */
            connectionUtils.getThreadConnection().setAutoCommit(true);
            /* 归还到连接池 */
            connectionUtils.getThreadConnection().close();
            /* 解除线程绑定 */
            connectionUtils.removeThreadConnection();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

修改service层代码

```java
@Service
public class AccountServiceImpl implements AccountService {
    @Autowired
    private AccountDao accountDao;
    @Autowired
    private TransactionManager transactionManager;
    @Override
    public void transfer(String outUser, String inUser, Double money) {
        try {
            /* 1.开启事务 */
            transactionManager.beginTransaction();
            /* 2.业务操作 */
            accountDao.out(outUser, money);
            //int i = 1 / 0;
            accountDao.in(inUser, money);
            /* 3.提交事务 */
            transactionManager.commit();
        } catch (Exception e) {
            e.printStackTrace();
            /* 4.回滚事务 */
            transactionManager.rollback();
        } finally {
            /* 5.释放资源 */
            transactionManager.release();
        }
    }
}
```

修改dao层代码

```java
@Repository
public class AccountDaoImpl implements AccountDao {

    @Autowired
    private QueryRunner queryRunner;
    @Autowired
    private ConnectionUtils connectionUtils;
    @Override
    public void out(String outUser, Double money) {
        try {
            queryRunner.update(connectionUtils.getThreadConnection(),"update account set money=money-? where name=?", money, outUser);
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    @Override
    public void in(String inUser, Double money) {
        try {
            queryRunner.update(connectionUtils.getThreadConnection(),"update account set money=money+? where name=?",money, inUser);
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

问题分析：

上面代码，通过对业务层改造，已经可以实现事务控制了，但是由于我们添加了事务控制，也产生了 一个新的问题： 业务层方法变得臃肿了，里面充斥着很多重复代码。并且业务层方法和事务控制方法耦 合了，违背了面向对象的开发思想。

## Proxy优化转账案例

我们可以将业务代码和事务代码进行拆分，通过动态代理的方式，对业务方法进行事务的增强。这样 就不会对业务层产生影响，解决了耦合性的问题啦！

常用的动态代理技术 

- JDK 代理：基于接口的动态代理技术·：利用拦截器（必须实现invocationHandler）加上反射机制生成 一个代理接口的匿名类，在调用具体方法前调用InvokeHandler来处理，从而实现方法增强

- CGLIB代理：基于父类的动态代理技术：动态生成一个要代理的子类，子类重写要代理的类的所有不是 final的方法。在子类中采用方法拦截技术拦截所有的父类方法的调用，顺势织入横切逻辑，对方法进行增强 ASM 

### JDK动态代理方式

Jdk工厂类

```java
@Component
public class JdkProxyFactory {
    @Autowired
    private AccountService accountService;
    @Autowired
    private TransactionManager transactionManager;
    public AccountService createAccountServiceJdkProxy() {
        AccountService accountServiceProxy = null;

        accountServiceProxy = (AccountService)
                Proxy.newProxyInstance(accountService.getClass().getClassLoader(),
                        accountService.getClass().getInterfaces(), new InvocationHandler(){
                                    @Override
                                    public Object invoke(Object proxy, Method method, Object[] args)throws Throwable {
                                        Object result = null;
                                        try {
                                            /* 1.开启事务 */
                                            transactionManager.beginTransaction();
                                            /* 2.业务操作 */
                                            result = method.invoke(accountService, args);
                                            // 3.提交事务
                                            transactionManager.commit();
                                        } catch (Exception e) {
                                            e.printStackTrace();
                                            // 4.回滚事务
                                            transactionManager.rollback();
                                        } finally {
                                            // 5.释放资源
                                            transactionManager.release();
                                        }
                                        return result;
                                    }
                                });
        return accountServiceProxy;
    }
}
```

修改service层代码

```java
@Service
public class AccountServiceImpl implements AccountService {
    @Autowired
    private AccountDao accountDao;
    @Override
    public void transfer(String outUser, String inUser, Double money) {
        accountDao.out(outUser, money);
        accountDao.in(inUser, money);
    }
}
```

编写测试代码

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:applicationContext.xml")
public class AccountTest {
    @Autowired
    private JdkProxyFactory jdkProxyFactory;
    @Test
    public void testTransfer() throws Exception {
        AccountService accountService = jdkProxyFactory.createAccountServiceJdkProxy();
        accountService.transfer("tom", "jerry", 100d);
    }
}
```

### CGLIB动态代理方式

Cglib工厂类

```java
@Component
public class CglibProxyFactory {
    @Autowired
    private AccountService accountService;
    @Autowired
    private TransactionManager transactionManager;
    public AccountService createAccountServiceCglibProxy() {
        AccountService accountServiceProxy = null;
        /*
         * 参数一：目标对象的字节码对象
         * 参数二：动作类，实现增强功能
         * */
        accountServiceProxy = (AccountService)
                Enhancer.create(accountService.getClass(), new MethodInterceptor() {
                    @Override
                    public Object intercept(Object o, Method method, Object[] objects,
                                            MethodProxy methodProxy) throws Throwable {
                        Object result = null;
                        try {
                            // 1.开启事务
                            transactionManager.beginTransaction();
                            // 2.业务操作
                            result = method.invoke(accountService, objects);
                            // 3.提交事务
                            transactionManager.commit();
                        } catch (Exception e) {
                            e.printStackTrace();
                            // 4.回滚事务
                            transactionManager.rollback();
                        } finally {
                            // 5.释放资源
                            transactionManager.release();
                        }
                        return result;
                    }
                });
        return accountServiceProxy;
    }
}
```

编写测试代码

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:applicationContext.xml")
public class AccountTest {
    @Autowired
    private CglibProxyFactory cglibProxyFactory;
    @Test
    public void testTransfer() throws Exception {
        AccountService accountService = cglibProxyFactory.createAccountServiceCglibProxy();
        accountService.transfer("tom", "jerry", 100d);
    }
}
```

## 初识AOP

### 什么是AOP

AOP 为 Aspect Oriented Programming 的缩写，意思为面向切面编程

AOP 是 OOP（面向对象编程） 的延续，是软件开发中的一个热点，也是Spring框架中的一个重要内容，利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率。

这样做的好处是：

1. 在程序运行期间，在不修改源码的情况下对方法进行功能增强

2. 逻辑清晰，开发核心业务的时候，不必关注增强业务的代码

3. 减少重复代码，提高开发效率，便于后期维护

**AOP底层实现**

实际上，AOP 的底层是通过 Spring 提供的的动态代理技术实现的。在运行期间，Spring通过动态代理技术动态的生成代理对象，代理对象方法执行时进行增强功能的介入，在去调用目标对象的方法，从而完成功能的增强。

**AOP相关术语**

Spring 的 AOP 实现底层就是对上面的动态代理的代码进行了封装，封装后我们只需要对需要关注的部分进行代码编写，并通过配置的方式完成指定目标的方法增强。

在正式讲解 AOP 的操作之前，我们必须理解 AOP 的相关术语，常用的术语如下：

```
\* Target（目标对象）：代理的目标对象 //accountServiceiml
\* Proxy （代理）：一个类被 AOP 织入增强后，就产生一个结果代理类 //兄弟类或者子类
\* Joinpoint（连接点）：所谓连接点是指那些可以被拦截到的点。在spring中,这些点指的是方法，因为 spring只支持方法类型的连接点 //transfer
\* Pointcut（切入点）：所谓切入点是指我们要对哪些 Joinpoint 进行拦截的定义
\* Advice（通知/增强）：所谓通知是指拦截到 Joinpoint 之后所要做的事情就是通知 分类：前置通知、后置通知、异常通知、最终通知、环绕通知 // 开启事务 提交事务
\* Aspect（切面）：是切入点和通知（引介）的结合
\* Weaving（织入）：是指把增强应用到目标对象来创建新的代理对象的过程。spring采用动态代理织入，而AspectJ采用编译期织入和类装载期织入
```

### AOP开发明确事项

**开发阶段（我们做的）**

1. 编写核心业务代码（目标类的目标方法） 切入点

2. 把公用代码抽取出来，制作成通知（增强功能方法） 通知

3. 在配置文件中，声明切入点与通知间的关系，即切面

**运行阶段（Spring框架完成的）**

Spring 框架监控切入点方法的执行。一旦监控到切入点方法被运行，使用代理机制，动态创建目标对象的代理对象，根据通知类别，在代理对象的对应位置，将通知对应的功能织入，完成完整的代码逻辑运行。

**底层代理实现** 

在 Spring 中，框架会根据目标类是否实现了接口来决定采用哪种动态代理的方式。

当bean实现接口时，会用JDK代理模式

当bean没有实现接口，用cglib实现（ 可以强制使用cglib（在spring配置中加入<aop:aspectjautoproxy proxyt-target-class=“true”/>）

**知识小结**

aop：面向切面编程 

aop底层实现：基于JDK的动态代理 和 基于Cglib的动态代理 

aop的重点概念： 

Pointcut（切入点）：真正被增强的方法 

Advice（通知/ 增强）：封装增强业务逻辑的方法 

Aspect（切面）：切点+通知 

Weaving（织入）：将切点与通知结合，产生代理对象的过程

## 基于XML的AOP开发

### 快速入门

步骤分析：

1. 创建java项目，导入AOP相关坐标 

2. 创建目标接口和目标实现类（定义切入点） 

3. 创建通知类及方法（定义通知） 

4. 将目标类和通知类对象创建权交给spring 
5. 在核心配置文件中配置织入关系，及切面 

6. 编写测试代码

创建java项目，导入AOP相关坐标

```xml
<dependencies>
        <!--导入spring的context坐标，context依赖aop-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
        <!-- aspectj的织入（切点表达式需要用到该jar包） -->
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.8.13</version>
        </dependency>
        <!--spring整合junit-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
</dependencies>
```

创建目标接口和目标实现类

```java
public interface AccountService {
    public void transfer();
}
```

```java
public class AccountServiceImpl implements AccountService {
	@Override
    public void transfer() {
        System.out.println("转账业务...");
    }
}
```

创建通知类

```java
public class MyAdvice {
    public void before() {
        System.out.println("前置通知...");
    }
}
```

将目标类和通知类对象创建权交给spring 创建applicationContext.xml 在核心配置文件中配置织入关系，及切面

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans 
	http://www.springframework.org/schema/beans/spring-beans.xsd 
	http://www.springframework.org/schema/aop 
	http://www.springframework.org/schema/aop/spring-aop.xsd">

    <!--目标类交给IOC容器-->
    <bean id="accountService" class="com.aaa.service.impl.AccountServiceImpl"> </bean>
    <!--通知类交给IOC容器-->
    <bean id="myAdvice" class="com.aaa.advice.MyAdvice"></bean>
    
    <aop:config>
        <!--引入通知类-->
        <aop:aspect ref="myAdvice">
            <!--配置目标类的transfer方法执行时，使用通知类的before方法进行前置增强-->
            <aop:before method="before" pointcut="execution(public void com.aaa.service.impl.AccountServiceImpl.transfer())"></aop:before>
        </aop:aspect>
    </aop:config>
</beans>
```

编写测试代码

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:applicationContext.xml")
public class AopTest {
    @Autowired
    private AccountService accountService;

    @Test
    public void testTransfer() throws Exception {
        accountService.transfer();
    }
}
```

### XML配置AOP详解

**切点表达式**

表达式语法：

- execution([修饰符] 返回值类型 包名.类名.方法名(参数))
- 访问修饰符可以省略
- 返回值类型、包名、类名、方法名可以使用星号 * 代替，代表任意
- 包名与类名之间一个点 . 代表当前包下的类，两个点 .. 表示当前包及其子包下的类
- 参数列表可以使用两个点 .. 表示任意个数，任意类型的参数列表

例如：

```xml
execution(public void com.aaa.service.impl.AccountServiceImpl.transfer()) 
execution(void com.aaa.service.impl.AccountServiceImpl.*(..)) 
execution(* com.aaa.service.impl.*.*(..)) 
execution(* com.aaa.service..*.*(..))
```

**切点表达式抽取**

当多个增强的切点表达式相同时，可以将切点表达式进行抽取，在增强中使用 pointcut-ref 属性代替pointcut 属性来引用抽取后的切点表达式。

```xml
<aop:config>
    <!--抽取的切点表达式-->
    <aop:pointcut id="myPointcut" expression="execution(* com.aaa.service..*.*(..))"> 		</aop:pointcut>
    <aop:aspect ref="myAdvice">
        <aop:before method="before" pointcut-ref="myPointcut"></aop:before>
    </aop:aspect>
</aop:config>
```

**通知类型**

通知的配置语法：

```
<aop:通知类型 method="通知类中方法名" pointcut="切点表达式"></aop:通知类型>
```

| 名称     | 标签                   | 说明                                                       |
| -------- | ---------------------- | ---------------------------------------------------------- |
| 前置通知 | <aop:before >          | 用于配置前置通知。指定增强的方法在切入点方法之前执行       |
| 后置通知 | <aop:after-returning > | 用于配置后置通知。指定增强的方法在切入点方法之后执行       |
| 异常通知 | <aop:after-throwing >  | 用于配置异常通知。指定增强的方法出现异常后执行             |
| 最终通知 | <aop:after >           | 用于配置最终通知。无论切入点方法执行时是否有异常，都会执行 |
| 环绕通知 | <aop:around >          | 用于配置环绕通知。开发者可以手动控制增强代码在什么时候执行 |

注意：通常情况下，环绕通知都是独立使用的

## 基于注解的AOP开发

创建java项目，导入AOP相关坐标

```xml
<dependencies>
        <!--导入spring的context坐标，context依赖aop-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
        <!-- aspectj的织入（切点表达式需要用到该jar包） -->
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.8.13</version>
        </dependency>
        <!--spring整合junit-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
</dependencies>
```

创建目标接口和目标实现类

```java
public interface AccountService {
    public void transfer();
}
```

```java
@Service
public class AccountServiceImpl implements AccountService {
    @Override
    public void transfer() {
        System.out.println("转账业务...");
    }
} 
```

创建通知类

```java
@Component
@Aspect
public class MyAdvice {
    @Before("execution(* com.aaa.aop.*.*())")
    public void before() {
        System.out.println("前置通知...");
    }
}
```

在配置文件中开启组件扫描和 AOP 的自动代理

```xml
<!--组件扫描-->
<context:component-scan base-package="com.aaa"/>
<!--aop的自动代理-->
<aop:aspectj-autoproxy></aop:aspectj-autoproxy>
```

```java
//纯注解配置
@Configuration
@ComponentScan("com.aaa.aop")
@EnableAspectJAutoProxy//替代<aop:aspectj-autoproxy />
public class SpringConfig {}
```

测试类

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(classes = Spring.class)
public class AopTest {
    @Autowired
    private AccountService accountService;

    @Test
    public void testTransfer() throws Exception {
        accountService.transfer();
    }
}
```

切点表达式抽取

```java
public class MyAdvice {

    @Pointcut("execution(* com.aaa..*.*(..))")
    public void myPoint(){}

    @Before("MyAdvice.myPoint()")
    public void before() {
        System.out.println("前置通知...");
    }
}
```

**注意：**当前四个通知组合在一起时，执行顺序如下：

@Before -> @After -> @AfterReturning（如果有异常：@AfterThrowing）

## AOP优化转账案例

依然使用前面的转账案例，将两个代理工厂对象直接删除！改为spring的aop思想来实现

### xml配置实现

配置文件 applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation=" http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans.xsd
http://www.springframework.org/schema/aop
http://www.springframework.org/schema/aop/spring-aop.xsd
http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context.xsd">

    <!--开启组件扫描-->
    <context:component-scan base-package="com.aaa"/>
    <!--加载jdbc配置文件-->
    <context:property-placeholder location="classpath:jdbc.properties"/>
    <!--把数据库连接池交给IOC容器-->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${jdbc.driver}"></property>
        <property name="url" value="${jdbc.url}"></property>
        <property name="username" value="${jdbc.username}"></property>
        <property name="password" value="${jdbc.password}"></property>
    </bean>
    <!--把QueryRunner交给IOC容器-->
    <bean id="queryRunner" class="org.apache.commons.dbutils.QueryRunner">
        <constructor-arg name="ds" ref="dataSource"></constructor-arg>
    </bean>
    <!--AOP配置-->
    <aop:config>
        <!--切点表达式-->
        <aop:pointcut id="myPointcut" expression="execution(* com.aaa.service..*.*(..))"/>
        <!-- 切面配置 -->
        <aop:aspect ref="transactionManager">
            <aop:before method="beginTransaction" pointcut-ref="myPointcut"/>
            <aop:after-returning method="commit" pointcut-ref="myPointcut"/>
            <aop:after-throwing method="rollback" pointcut-ref="myPointcut"/>
            <aop:after method="release" pointcut-ref="myPointcut"/>
        </aop:aspect>
    </aop:config>
</beans>
```

事务管理器（通知）

```java
/* 事务管理器工具类，包含：开启事务、提交事务、回滚事务、释放资源*/
@Component
public class TransactionManager {
    @Autowired
    private ConnectionUtils connectionUtils;
    public void beginTransaction() {
        try {
            connectionUtils.getThreadConnection().setAutoCommit(false);
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    public void commit() {
        try {
            connectionUtils.getThreadConnection().commit();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    public void rollback() {
        try {
            connectionUtils.getThreadConnection().rollback();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    public void release() {
        try {
            /* 改回自动提交事务 */
            connectionUtils.getThreadConnection().setAutoCommit(true);
            /* 归还到连接池 */
            connectionUtils.getThreadConnection().close();
            /* 解除线程绑定 */
            connectionUtils.removeThreadConnection();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

测试类

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:applicationContext.xml")
public class AccountTest {
    @Autowired
    private AccountService accountService;

    @Test
    public void testTransfer() throws Exception {
        accountService.transfer("tom", "jerry", 100d);
    }
}
```

### 注解配置实现

开启注解支持 <aop:aspectj-autoproxy /> 配置文件 applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation=" http://www.springframework.org/schema/beans
		http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/aop
		http://www.springframework.org/schema/aop/spring-aop.xsd
		http://www.springframework.org/schema/context
		http://www.springframework.org/schema/context/spring-context.xsd">

    <!--开启组件扫描-->
    <context:component-scan base-package="com.aaa"/>
    <!--开启AOP注解支持-->
    <aop:aspectj-autoproxy/>
    <!--加载jdbc配置文件-->
    <context:property-placeholder location="classpath:jdbc.properties"/>
    <!--把数据库连接池交给IOC容器-->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${jdbc.driver}"></property>
        <property name="url" value="${jdbc.url}"></property>
        <property name="username" value="${jdbc.username}"></property>
        <property name="password" value="${jdbc.password}"></property>
    </bean>

    <!--把QueryRunner交给IOC容器-->
    <bean id="queryRunner" class="org.apache.commons.dbutils.QueryRunner">
        <constructor-arg name="ds" ref="dataSource"></constructor-arg>
    </bean>
</beans>
```

事务管理器（通知）

```java
@Component
@Aspect
public class TransactionManager {
    @Autowired
    ConnectionUtils connectionUtils;

    @Around("execution(* com.aaa.service..*.*(..))")
    public Object around(ProceedingJoinPoint pjp) {
        Object object = null;
        try {
            // 开启事务
            connectionUtils.getThreadConnection().setAutoCommit(false);
            // 业务逻辑
            pjp.proceed();
            // 提交事务
            connectionUtils.getThreadConnection().commit();
        } catch (Throwable throwable) {
            throwable.printStackTrace();
            // 回滚事务
            try {
                connectionUtils.getThreadConnection().rollback();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        } finally {
            try {
                connectionUtils.getThreadConnection().setAutoCommit(true);
                connectionUtils.getThreadConnection().close();
                connectionUtils.removeThreadConnection();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        return object;
    }
}
```

> spring 环绕通知 ProceedingJoinPoint 执行 proceed 方法的作用是让目标方法执行
>
> 环绕通知=前置+目标方法执行+后置通知，proceed方法就是用于启动目标方法执行的.

测试类

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:applicationContext.xml")
public class AccountTest {
    @Autowired
    private AccountService accountService;

    @Test
    public void testTransfer() throws Exception {
        accountService.transfer("tom", "jerry", 100d);
    }
}
```

## JdbcTemplate

JdbcTemplate是spring框架中提供的一个模板对象，是对原始繁琐的Jdbc API对象的简单封装。

核心对象 dataSource --->驱动 url username

```java
JdbcTemplate jdbcTemplate = new JdbcTemplate(DataSource dataSource);
```

### 整合JdbcTemplate

需求：基于Spring的xml配置实现账户的CRUD案例

创建java项目，导入坐标

```xml
<dependencies>
        <!--导入spring的context坐标，context依赖aop-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
        <!-- aspectj的织入（切点表达式需要用到该jar包） -->
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.8.13</version>
        </dependency>
        <!--spring整合junit-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
        <!--在spring 框架 中实现事务管理功能-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-tx</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
        <!--JDBC API-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>

        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.38</version>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.2.8</version>
        </dependency>
    </dependencies>
```

编写Account实体类

```java
public class Account {
    private Integer id;
    private String name;
    private Double money;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Double getMoney() {
        return money;
    }

    public void setMoney(Double money) {
        this.money = money;
    }

    @Override
    public String toString() {
        return "Account{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", money=" + money +
                '}';
    }
}
```

编写AccountDao接口和实现类

```java
public interface AccountDao {
    public List<Account> findAll();
    public Account findById(Integer id);
    public void save(Account account);
    public void update(Account account);
    public void delete(Integer id);
}
```

```java
@Repository
public class AccountDaoImpl implements AccountDao{
    @Autowired
    private JdbcTemplate jdbcTemplate;
    @Override
    public List<Account> findAll() {
        // 编写sql 
        String sql = "select * from account";
        // 执行sql 
        return jdbcTemplate.query(sql, new BeanPropertyRowMapper<>(Account.class));
    }

    @Override
    public Account findById(Integer id) {
        // 编写sql 
        String sql = "select * from account where id = ?";
        // 执行sql 
        return jdbcTemplate.queryForObject(sql, new BeanPropertyRowMapper<> (Account.class),id);
    }

    @Override
    public void save(Account account) {
        // 编写sql 
        String sql = "insert into account values(null,?,?)";
        // 执行sql 
        jdbcTemplate.update(sql, account.getName(), account.getMoney());

    }

    @Override
    public void update(Account account) {
        // 编写sql 
        String sql = "update account set name = ?,money = ? where id = ?";
        // 执行sql 
        jdbcTemplate.update(sql, account.getName(), account.getMoney(),account.getId());
    }

    @Override
    public void delete(Integer id) {
        // 编写sql 
        String sql = "delete from account where id = ?";
        // 执行sql 
        jdbcTemplate.update(sql, id);
    }
}
```

编写AccountService接口和实现类

```java
public interface AccountService {
    public List<Account> findAll();
    public Account findById(Integer id);
    public void save(Account account);
    public void update(Account account);
    public void delete(Integer id);
}
```

```java
@Service
public class AccountServiceImpl implements AccountService{
    @Autowired
    private AccountDao accountDao;

    @Override
    public List<Account> findAll() {
        return accountDao.findAll();
    }

    @Override
    public Account findById(Integer id) {
        return accountDao.findById(id);
    }

    @Override
    public void save(Account account) {
        accountDao.save(account);
    }

    @Override
    public void update(Account account) {
        accountDao.update(account);
    }

    @Override
    public void delete(Integer id) {
        accountDao.delete(id);
    }
}
```

编写spring核心配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
		http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/context
		http://www.springframework.org/schema/context/spring-context.xsd">


    <context:component-scan base-package="com.aaa.crud"/>
    <context:property-placeholder location="classpath:jdbc.properties"/>

    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${jdbc.driver}"></property>
        <property name="url" value="${jdbc.url}"></property>
        <property name="username" value="${jdbc.username}"></property>
        <property name="password" value="${jdbc.password}"></property>
    </bean>

    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        <constructor-arg name="dataSource" ref="dataSource"></constructor-arg>
    </bean>
</beans>
```

编写测试代码

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:applicationContext-crud.xml")
public class CrudTest {
    @Autowired
    private AccountService accountService;
    //测试保存
    @Test
    public void testSave() {
        Account account = new Account();
        account.setName("lucy");
        account.setMoney(100d);
        accountService.save(account);
    }
    //测试查询
    @Test
    public void testFindById() {
        Account account = accountService.findById(3);
        System.out.println(account);
    }

    //测试查询所有
    @Test
    public void testFindAll() {
        List<Account> accountList = accountService.findAll();
        for (Account account : accountList) {
            System.out.println(account);
        }
    }

    //测试修改
    @Test
    public void testUpdate() {
        Account account = new Account();
        account.setId(3);
        account.setName("rose");
        account.setMoney(2000d);
        accountService.update(account);
    }

    //测试删除
    @Test
    public void testDelete() {
        accountService.delete(3);
    }
}
```

### 实现转账案例

创建java项目，导入坐标

```xml
	<dependencies>
        <!--导入spring的context坐标，context依赖aop-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
        <!-- aspectj的织入（切点表达式需要用到该jar包） -->
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.8.13</version>
        </dependency>
        <!--spring整合junit-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
        <!--在spring 框架 中实现事务管理功能-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-tx</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
        <!--JDBC API-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>

        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.38</version>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.2.8</version>
        </dependency>
    </dependencies>
```

编写Account实体类

```java
public class Account {
    private Integer id;
    private String name;
    private Double money;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Double getMoney() {
        return money;
    }

    public void setMoney(Double money) {
        this.money = money;
    }

    @Override
    public String toString() {
        return "Account{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", money=" + money +
                '}';
    }
}
```

编写AccountDao接口和实现类

```java
public interface AccountDao {
    /* 转出操作 */
    public void out(String outUser, Double money);
    /* 转入操作 */
    public void in(String inUser, Double money);
}
```

```java
@Repository
public class AccountDaoImpl implements AccountDao {

    @Autowired
    private JdbcTemplate jdbcTemplate;
    @Override
    public void out(String outUser, Double money) {
        jdbcTemplate.update("update account set money = money - ? where name = ?", money, outUser);
    }
    @Override
    public void in(String inUser, Double money) {
        jdbcTemplate.update("update account set money = money + ? where name = ?", money, inUser);
    }
}
```

编写AccountService接口和实现类

```java
public interface AccountService {
    public void transfer(String outUser, String inUser, Double money);
}
```

```java
@Service
public class AccountServiceImpl implements AccountService {
    @Autowired
    private AccountDao accountDao;
    @Override
    public void transfer(String outUser, String inUser, Double money) {
            accountDao.out(outUser, money);
            accountDao.in(inUser, money);
    }
}
```

编写spring核心配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation=" http://www.springframework.org/schema/beans
		http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/context
		http://www.springframework.org/schema/context/spring-context.xsd">

    <!--开启组件扫描-->
    <context:component-scan base-package="com.aaa"/>
    <!--加载jdbc配置文件-->
    <context:property-placeholder location="classpath:jdbc.properties"/>
    <!--把数据库连接池交给IOC容器-->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${jdbc.driver}"></property>
        <property name="url" value="${jdbc.url}"></property>
        <property name="username" value="${jdbc.username}"></property>
        <property name="password" value="${jdbc.password}"></property>
    </bean>
    <!--把JdbcTemplate交给IOC容器-->
    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        <constructor-arg name="dataSource" ref="dataSource"></constructor-arg>
    </bean>
</beans>
```

编写测试代码

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:applicationContext.xml")
public class AccountTest {
    @Autowired
    private AccountService accountService;

    @Test
    public void testTransfer() throws Exception {
        accountService.transfer("tom", "jerry", 100d);
    }
}
```

## Spring的事务

Spring的事务控制可以分为编程式事务控制和声明式事务控制。 

**编程式**：开发者直接把事务的代码和业务代码耦合到一起，在实际开发中不用。 

**声明式**：开发者采用配置的方式来实现的事务控制，业务代码与事务代码实现解耦合，使用的AOP思想。 

### 编程式事务控制（了解）

> PlatformTransactionManager接口，是spring的事务管理器，里面提供了我们常用的操作事务的方法

| 方法                                                         | 说明               |
| ------------------------------------------------------------ | ------------------ |
| TransactionStatus getTransaction(TransactionDefinition definition); | 获取事务的状态信息 |
| void commit(TransactionStatus status);                       | 提交事务           |
| void rollback(TransactionStatus status);                     | 回滚事务           |

> PlatformTransactionManager 是接口类型，不同的 Dao 层技术则有不同的实现类

Dao层技术是jdbcTemplate或mybatis时： DataSourceTransactionManager 

Dao层技术是hibernate时： HibernateTransactionManager 

Dao层技术是JPA时： JpaTransactionManager

> TransactionDefinition接口提供事务的定义信息（事务隔离级别、事务传播行为等等）

| 方法                         | 说明               |
| ---------------------------- | ------------------ |
| int getlsolationLevel()      | 获得事务的隔离级别 |
| int getPropogationBehavior() | 获得事务的传播行为 |
| int getTimeout()             | 获得超时时间       |
| boolean isReadOnly()         | 是否只读           |

**事务隔离级别**

设置隔离级别，可以解决事务并发产生的问题，如脏读、不可重复读和虚读（幻读）

```sql
* ISOLATION_DEFAULT 使用数据库默认级别
* ISOLATION_READ_UNCOMMITTED 读未提交 
* ISOLATION_READ_COMMITTED 读已提交
* ISOLATION_REPEATABLE_READ 可重复读 
* ISOLATION_SERIALIZABLE 串行化
```

**事务传播行为** 

事务传播行为指的就是当一个业务方法【被】另一个业务方法调用时，应该如何进行事务控制。

| 参数          | 说明                                                         |
| ------------- | ------------------------------------------------------------ |
| REQUIRED      | 如果当前没有事务，就新建一个事务，如果已经存在一个事务中<br>加入到这个事务中。一般的选择（默认值) |
| SUPPORTS      | 新建事务，如果当前在事务中，把当前事务挂起                   |
| MANDATORY     | 使用当前的事务，如果当前没有事务，就抛出异常                 |
| REQUERS_NEW   | 新建事务，如果当前在事务中，把当前事务挂起                   |
| NOT_SUPPORTED | 以非事务方式执行操作，如果当前存在事务，就把当前事务挂起     |
| NEVER         | 以非事务方式运行，如果当前存在事务，抛出异常                 |
| NESTED        | 如果当前存在事务，则在嵌套事务内执行。如果当前没有事务<br>则执行REQUIRED类似的操作 |

read-only（是否只读）：建议查询时设置为只读

timeout（超时时间）：默认值是-1，没有超时限制。如果有，以秒为单位进行设置

> TransactionStatus 接口提供的是事务具体的运行状态

| 方法                       | 说明         |
| -------------------------- | ------------ |
| boolean isNewTransaction() | 是否是新事务 |
| boolean hasSavepoint()     | 是否是回滚点 |
| boolean isRollbackOnly()   | 事务是否回滚 |
| boolean isCompleted()      | 事务是否完成 |

**实现代码**

配置文件

```xml
<!--事务管理器交给IOC-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"/>
    </bean>
```

业务层代码

```java
@Service
public class AccountServiceImpl implements AccountService {
    @Autowired
    private AccountDao accountDao;
    @Autowired
    private PlatformTransactionManager transactionManager;
    @Override
    public void transfer(String outUser, String inUser, Double money) {
        // 创建事务定义对象 
        DefaultTransactionDefinition def = new DefaultTransactionDefinition();
        // 设置是否只读，false支持事务 
        def.setReadOnly(false);
        // 设置事务隔离级别，可重复读mysql默认级别 
        def.setIsolationLevel(TransactionDefinition.ISOLATION_REPEATABLE_READ);
        // 设置事务传播行为，必须有事务 
        def.setPropagationBehavior(TransactionDefinition.PROPAGATION_REQUIRED);
        // 配置事务管理器 
        TransactionStatus status = transactionManager.getTransaction(def);
        try {
            // 转账 
            accountDao.out(outUser, money);
            accountDao.in(inUser, money);
            // 提交事务 
            transactionManager.commit(status);
        } catch (Exception e) {
            e.printStackTrace();
            // 回滚事务 
            transactionManager.rollback(status);
        }
    }
}
```

PlatformTransactionManager 负责事务的管理，它是个接口，其子类负责具体工作 

TransactionDefinition 定义了事务的一些相关参数 

TransactionStatus 代表事务运行的一个实时状态

可以简单理解三者的关系：事务管理器通过读取事务定义参数进行事务管理，然后会产生一系列的事务状态。

### 基于XML的声明式事务控制

在 Spring 配置文件中声明式的处理事务来代替代码式的处理事务。底层采用AOP思想来实现的。

需求：使用spring声明式事务控制转账业务。

引入tx命名空间 aop命名空间

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="
http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans.xsd
http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context.xsd
http://www.springframework.org/schema/aop
http://www.springframework.org/schema/aop/spring-aop.xsd
http://www.springframework.org/schema/tx
http://www.springframework.org/schema/tx/spring-tx.xsd
http://www.w3.org/2001/XMLSchema-instance
http://www.w3.org/2001/XMLSchema-instance ">
    <context:component-scan base-package="com.aaa"/>
    <context:property-placeholder location="classpath:jdbc.properties"/>
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${jdbc.driver}"></property>
        <property name="url" value="${jdbc.url}"></property>
        <property name="username" value="${jdbc.username}"></property>
        <property name="password" value="${jdbc.password}"></property>
    </bean>
    <!--把JdbcTemplate交给IOC容器-->
    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        <constructor-arg name="dataSource" ref="dataSource"></constructor-arg>
    </bean>
</beans>
```

事务管理器通知配置

```xml
<!--事务管理器-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"></property>
    </bean>
    <!--通知增强-->
    <tx:advice id="txAdvice" transaction-manager="transactionManager">
        <!--定义事务的属性-->
        <tx:attributes>
            <tx:method name="*"/>
        </tx:attributes>
    </tx:advice>
```

事务管理器AOP配置

```xml
	<!--aop配置-->
    <aop:config>
        <!--切面配置-->
        <aop:advisor advice-ref="txAdvice"pointcut="execution(* com.aaa.service..*.*(..))"/>
    </aop:config>
```

事务控制转账业务代码

```java
@Service
public class AccountServiceImpl implements AccountService {
    @Autowired
    private AccountDao accountDao;
    @Override
    public void transfer(String outUser, String inUser, Double money) {
            accountDao.out(outUser, money);
            accountDao.in(inUser, money);
    }
}
```

测试类

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:applicationContext.xml")
public class AccountTest {
    @Autowired
    private AccountService accountService;

    @Test
    public void testTransfer() throws Exception {
        accountService.transfer("tom", "jerry", 100d);
    }
}
```

**事务参数的配置详解**

```
<tx:method name="transfer" isolation="REPEATABLE_READ" 	propagation="REQUIRED" timeout="-1" read-only="false"/> 
* name：切点方法名称
* isolation:事务的隔离级别
* propogation：事务的传播行为
* timeout：超时时间
* read-only：是否只读
```

CRUD常用配置

```xml
<tx:attributes>
    <tx:method name="save*" propagation="REQUIRED"/>
    <tx:method name="delete*" propagation="REQUIRED"/>
    <tx:method name="update*" propagation="REQUIRED"/>
    <tx:method name="find*" read-only="true"/>
    <tx:method name="*"/>
</tx:attributes>
```

### 基于注解的声明式事务控制

修改service层，增加事务注解

```java
@Service
public class AccountServiceImpl implements AccountService {
    @Autowired
    private AccountDao accountDao;
    @Transactional(propagation = Propagation.REQUIRED, isolation = Isolation.REPEATABLE_READ, timeout = -1, readOnly = false)
    @Override
    public void transfer(String outUser, String inUser, Double money) {

            accountDao.out(outUser, money);
            accountDao.in(inUser, money);
    }
}
```

修改spring核心配置文件，开启事务注解支持（可由 SpringConfig 替代）

```xml
<!--省略之前datsSource、jdbcTemplate、组件扫描配置-->
    <!--事务管理器-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"></property>
    </bean>
	<!--事务的注解支持--> 
    <tx:annotation-driven/>
```

核心配置类

```java
@Configuration // 声明为spring配置类
@ComponentScan("com.aaa") // 扫描包
@Import(DataSourceConfig.class) // 导入其他配置类
@EnableTransactionManagement // 事务的注解驱动
public class SpringConfig {
    @Bean
    public JdbcTemplate getJdbcTemplate(@Autowired DataSource dataSource) {
        return new JdbcTemplate(dataSource);
    }

    @Bean("transactionManager")
    public PlatformTransactionManager getPlatformTransactionManager(@Autowired 	DataSource dataSource) {
        return new DataSourceTransactionManager(dataSource);
    }
}
```

数据源配置类

```java
@PropertySource("classpath:jdbc.properties")
public class DataSourceConfig {
    @Value("${jdbc.driver}")
    private String driver;
    @Value("${jdbc.url}")
    private String url;
    @Value("${jdbc.username}")
    private String username;
    @Value("${jdbc.password}")
    private String password;

    @Bean
    public DataSource getDataSource() {
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setDriverClassName(driver);
        dataSource.setUrl(url);
        dataSource.setUsername(username);
        dataSource.setPassword(password);
        return dataSource;
    }
}
```

测试类

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(classes = SpringConfig.class)
//@ContextConfiguration("classpath:applicationContext-crud.xml")
public class AccountTest {
    @Autowired
    private AccountService accountService;

    @Test
    public void testTransfer() throws Exception {
        accountService.transfer("tom", "jerry", 100d);
    }
}
```
