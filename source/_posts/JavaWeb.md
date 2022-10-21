---
title: JavaWeb
copyright_url: https://www.aobayu.cn/2022/10/08/JavaWeb/
tags: 
    - JavaWeb
categories: 学习之路
date: 2022-10-8
keywords: JavaWeb
description: Java Web，是用Java技术来解决相关web互联网领域的技术栈。web包括：web服务端和web客户端两部分。Java在客户端的应用有Java Applet，不过使用得很少，Java在服务器端的应用非常的丰富。--本文为自己学习中所写
---

## 基本概念

### 前言

web开发：

- web，网页的意思，www.baidu.com
- 静态web
  - html，css
  - 提供给所有人看的数据始终不会发生变化！
- 动态web
  - 淘宝，几乎是所有的网站；
  - 提供给所有人看的数据始终会发生变化，每个人在不同的时间，不同的地点看到的信息各不相同！
  - 技术栈：Servlet/JSP，ASP，PHP；

在Java中，动态web资源开发的技术统称为JavaWeb；

### C/S架构的概念

C/S架构（Client/Server，客户端/服务器模式），是一种比较早的软件体系结构，也是生活中很常见的结构。这种结构将需要处理的业务合理地分配到客户端和服务器端，客户端通常负责完成与用户的交互任务，服务器通常负责数据的管理。

**C/S架构的主要优点如下：**

客户端的界面和功能可以很丰富。

应用服务器的负荷较轻。

响应速度较快。

**C/S架构的主要缺点如下：**

适用面窄，用户群固定。

维护和升级的成本高，所有的客户端都需要更新版本。

### B/S架构的概念

B/S架构（Browser/Server，浏览器/服务器模式），是互联网兴起后的软件体系结构，该结构将系统功能实现的主要业务逻辑集中到服务器端，极少数业务逻辑在浏览器实现，浏览器通常负责完成与用户的交互任务，服务器通常负责数据的管理。

**B/S架构的主要优点如下：**

无需安装客户端，只要有浏览器即可。

适用面广，用户群不固定。

通过权限控制实现多客户访问的目的，交互性较强。

维护和升级的成本低，无需更新所有客户端版本。

**B/S架构的主要缺点如下：**

应用服务器的负荷较重。

浏览器的界面和功能想要达到客户端的丰富程度需要花费大量的成本。

在跨浏览器上不尽如人意，适配比较麻烦。

### web应用程序

web应用程序：可以提供浏览器访问的程序；

- a.html、b.html......多个web资源，这些web资源可以被外界访问，对外界提供服务；
- 你们能访问到的任何一个页面或者资源，都存在于这个世界的某一个角落的计算机上。
- URL
- 这个统一的web资源会被放在同一个文件夹下，web应用程序-->Tomcat：服务器
- 一个web应用由多部分组成 （静态web，动态web）
  - html，css，js
  - jsp，servlet
  - Java程序
  - jar包
  - 配置文件 （Properties）

web应用程序编写完毕后，若想提供给外界访问：需要一个服务器来统一管理；

### 静态web

- *.htm, *.html,这些都是网页的后缀，如果服务器上一直存在这些东西，我们就可以直接进行读取。通络；

![](https://s1.328888.xyz/2022/09/29/MLZRm.png)

- 静态web存在的缺点
  - Web页面无法动态更新，所有用户看到都是同一个页面
    - 轮播图，点击特效：伪动态
    - JavaScript [实际开发中，它用的最多]
    - VBScript
  - 它无法和数据库交互（数据无法持久化，用户无法交互）

### 动态web

页面会动态展示： “Web的页面展示的效果因人而异”；

![](https://s1.328888.xyz/2022/09/29/MLR8K.png)

缺点：

- 加入服务器的动态web资源出现了错误，我们需要重新编写我们的

  - 后台程序
  - 重新发布
  - 停机维护

优点：

- Web页面可以动态更新，所有用户看到都不是同一个页面
- 它可以与数据库交互 （数据持久化：注册，商品信息，用户信息........）

![](https://s1.328888.xyz/2022/09/29/MLAwr.png)

## web服务器

**ASP:**

- 微软：国内最早流行的就是ASP；

- 在HTML中嵌入了VB的脚本， ASP + COM；

- 在ASP开发中，基本一个页面都有几千行的业务代码，页面极其乱；

- 维护成本高！

- C#

- IIS

  ```html
  <h1>
      <h1><h1>
          <h1>
              <h1>
                  <h1>
          <h1>
              <%
              System.out.println("hello")
              %>
              <h1>
                  <h1>
     <h1><h1>
  <h1>
  ```

**php：**

- PHP开发速度很快，功能很强大，跨平台，代码很简单 （70% , WP）
- 无法承载大访问量的情况（局限性）

**JSP/Servlet : **

B/S：浏览和服务器

C/S: 客户端和服务器

- sun公司主推的B/S架构
- 基于Java语言的 (所有的大公司，或者一些开源的组件，都是用Java写的)
- 可以承载三高问题带来的影响
- 语法像ASP ， ASP-->JSP , 加强市场强度

**Web Server**

服务器是一种被动的操作，用来处理用户的一些请求和给用户一些响应信息

**IIS**

微软的； ASP...,Windows中自带的

**Tomcat**

面向百度编程

Tomcat是Apache 软件基金会（Apache Software Foundation）的Jakarta 项目中的一个核心项目，最新的Servlet 和JSP 规范总是能在Tomcat 中得到体现，因为Tomcat 技术先进、性能稳定，而且**免费**，因而深受Java 爱好者的喜爱并得到了部分软件开发商的认可，成为目前比较流行的Web 应用服务器。

Tomcat 服务器是一个免费的开放源代码的Web 应用服务器，属于轻量级应用服务器，在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试JSP 程序的首选。对于一个Java初学web的人来说，它是最佳的选择

Tomcat 实际上运行JSP 页面和Servlet。

## HTTP协议

HTTP协议（HyperText Transfer Protocol，超文本传输协议）是由W3C（万维网联盟）组织制定的一种应用层协议，是用来规范浏览器与Web服务器之间如何通讯的数据格式，主要涉及浏览器的发请求格式和服务器的响应格式。

HTTP协议通常承载于TCP协议之上，而承载于TLS或SSL协议层之上的协议就是常说的HTTPS协议。

HTTP默认的端口号为80，HTTPS默认的端口号为443。

**两个时代**

- http1.0
  - HTTP/1.0：客户端可以与web服务器连接后，只能获得一个web资源，断开连接
- http2.0
  - HTTP/1.1：客户端可以与web服务器连接后，可以获得多个web资源。

**HTTP请求格式**

客户端发送一个HTTP请求到服务器的请求消息主要包括：请求行、请求头、空白行和请求体。

**HTTP响应格式**

通常情况下服务器接收并处理客户端发过来的请求后会返回一个HTTP的响应消息，主要包括：响应行、响应头、空白行和响应体。

- 客户端---发请求（Request）---服务器

百度：

```java
Request URL:https://www.baidu.com/   请求地址
Request Method:GET    get方法/post方法
Status Code:200 OK    状态码：200
Remote（远程） Address:14.215.177.39:443
    
Accept:text/html  
Accept-Encoding:gzip, deflate, br
Accept-Language:zh-CN,zh;q=0.9    语言
Cache-Control:max-age=0
Connection:keep-alive
```

**请求行**

- 请求行中的请求方式：GET

- 请求方式：

  Get，Post,HEAD,DELETE,PUT,TRACT…

  - get：请求能够携带的参数比较少，大小有限制，会在浏览器的URL地址栏显示数据内容，不安全，但高效
  - post：请求能够携带的参数没有限制，大小没有限制，不会在浏览器的URL地址栏显示数据内容，安全，但不高效。

**消息头**

```java
Accept：告诉浏览器，它所支持的数据类型
Accept-Encoding：支持哪种编码格式  GBK   UTF-8   GB2312  ISO8859-1
Accept-Language：告诉浏览器，它的语言环境
Cache-Control：缓存控制
Connection：告诉浏览器，请求完成是断开还是保持连接
HOST：主机..../.
```

**Http响应**

- 服务器---响应-----客户端

百度：

```java
Cache-Control:private    缓存控制
Connection:Keep-Alive    连接
Content-Encoding:gzip    编码
Content-Type:text/html   类型
```

**响应体**

```java
Accept：告诉浏览器，它所支持的数据类型
Accept-Encoding：支持哪种编码格式  GBK   UTF-8   GB2312  ISO8859-1
Accept-Language：告诉浏览器，它的语言环境
Cache-Control：缓存控制
Connection：告诉浏览器，请求完成是断开还是保持连接
HOST：主机..../.
Refresh：告诉客户端，多久刷新一次；
Location：让网页重新定位；
```

**响应状态码**

200：请求响应成功 200

3xx：请求重定向

- 重定向：你重新到我给你新位置去；

4xx：找不到资源 404

- 资源不存在；

5xx：服务器代码错误 500 502:网关错误

## tomcat

**安装tomcat**

tomcat官网：http://tomcat.apache.org/

**Tomcat启动和配置**

bin: 主要存放二进制可执行文件和脚本。

conf: 主要存放各种配置文件。

lib: 主要用来存放Tomcat运行需要加载的jar包。

logs: 主要存放Tomcat在运行过程中产生的日志文件。

temp: 主要存放Tomcat在运行过程中产生的临时文件。

webapps: 主要存放应用程序，当Tomcat启动时会去加载该目录下的应用程序。

work: 主要存放tomcat在运行时的编译后文件，例如JSP编译后的文件。

**启动-关闭Tomcat**

startup.bat: 启动

shutdown.bat: 关闭

**可能遇到的问题：**

1. Java环境变量没有配置
2. 闪退问题：需要配置兼容性
3. 乱码问题：配置文件中设置

**启动信息乱码的处理方式**

apache-tomcat-8.5.68\conf下

logging.properties文件修改为

java.util.logging.ConsoleHandler.encoding = GBK

## 在IDEA中使用tomcat

1.添加新配置

![](https://s1.328888.xyz/2022/10/08/fRqTk.png)

2. 添加Tomact Server

![](https://s1.328888.xyz/2022/10/08/fRXsE.png)

3. 选择 tomcat 路径

![](https://s1.328888.xyz/2022/10/08/fRYpJ.png)

4. 添加 Artifact

![](https://s1.328888.xyz/2022/10/08/fRAOw.png)

5. 添加 :war exploded

![](https://s1.328888.xyz/2022/10/08/fRR9i.png)

6. 启动

![](https://s1.328888.xyz/2022/10/08/fRHR7.png)

## maven

**我为什么要学习这个技术？**

1. 在Javaweb开发中，需要使用大量的jar包，我们手动去导入；

2. 如何能够让一个东西自动帮我导入和配置这个jar包。

   由此，Maven诞生了！

**Maven项目架构管理工具**

我们目前用来就是方便导入jar包的！

Maven的核心思想：约定大于配置

- 有约束，不要去违反。

Maven会规定好你该如何去编写我们的Java代码，必须要按照这个规范来；

**Maven的作用**

- 依赖管理
  - 依赖指的就是是 我们项目中需要使用的第三方Jar包, 一个大一点的工程往往需要几十上百个 Jar包,按照我们之前的方式,每使用一种Jar,就需要导入到工程中,还要解决各种Jar冲突的问题.
  - Maven可以对Jar包进行统一的管理,包括快速引入Jar包,以及对使用的 Jar包进行统一的版本控制

- 一键构建项目
  - 之前我们创建项目,需要确定项目的目录结构,比如 src 存放Java源码, resources 存放配置文件,还要配置环境比如JDK的版本等等,如果有多个项目 那么就需要每次自己搞一套配置,十分麻烦
  - Maven为我们提供了一个标准化的Java项目结构,我们可以通过Maven快速创建一个标准的 Java项目.

**下载安装Maven**

官网;https://maven.apache.org/

下载完成后，解压即可；

解压后目录结构:

bin:存放了 maven 的命令 

boot:存放了一些 maven 本身的引导程序，如类加载器等 

conf:存放了 maven 的一些配置文件，如 setting.xml 文件 

lib:存放了 maven 本身运行所需的一些 jar 包

**配置环境变量**

在我们的系统环境变量中

配置如下配置：

- MAVEN_HOME maven的目录
- 在系统的path中配置 %MAVEN_HOME%\bin

**Maven 软件版本测试**

打开命令行，输入 mvn –v命令，看到版本号，即为执行成功

**Maven中的仓库是用来存放maven构建的项目和各种依赖的(Jar包)**

**本地仓库**: 位于自己计算机中的仓库, 用来存储从远程仓库或中央仓库下载的插件和 jar 包，

**远程仓库**: 需要联网才可以使用的仓库，阿里提供了一个免费的maven 远程仓库。 

**中央仓库**: 在 maven 软件中内置一个远程仓库地址 [http://repo1.maven.org/maven2](http://repo1.maven.org/maven2?accessToken=eyJhbGciOiJIUzI1NiIsImtpZCI6ImRlZmF1bHQiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE2NjUyMjA1MzksImZpbGVHVUlEIjoiV2xBcnoxN0phWXM3dkdBMiIsImlhdCI6MTY2NTIyMDIzOSwiaXNzIjoidXBsb2FkZXJfYWNjZXNzX3Jlc291cmNlIiwidXNlcklkIjotNzIzMTQ0NTA2MX0.B5LqHwI3o8MwvpNDgo_YTD1c7l2WhsinqEF5Xeh4a-c) ，它是中央仓库，服务于整个互联网，它是由 Maven 团队自己维护，里面存储了非常全的 jar 包，它包 含 了世界上大部分流行的开源项目构件

**Maven 本地仓库的配置**

maven仓库默认是在 C盘 .m2 目录下,如果怕C盘满，可以在设置中配置

在maven安装目录中,进入 conf文件夹, 可以看到一个 settings.xml 文件中, 我们在这个文件中, 进行 本地仓库的配置打开 settings.xml文件，进行如下配置：

**Maven 本地仓库的配置**  打开 settings.xml找到 localRepository 标签,下面的内容复制到其中即可

```
<localRepository>D:\Environment\apache-maven-3.6.2\maven-repo</localRepository>
```

 **配置阿里云远程仓库**  打开 settings.xml,找到<mirrors> 标签 , 下面的内容复制到其中即可

```
<mirror>
    <id>alimaven</id>
    <name>aliyun maven</name>
    <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
    <mirrorOf>central</mirrorOf>
</mirror>
```

## 在IDEA中使用Maven

1. 打开IDEA，新建项目

![](https://s1.328888.xyz/2022/10/08/fRb5g.png)

2. 选择Jakarta EE ，Web appLication，下一步

![](https://s1.328888.xyz/2022/10/08/fRBDi.png)

3. 选择Java EE 8，勾选 Web Profile，创建项目

![](https://s1.328888.xyz/2022/10/08/fRwzh.png)

4. 项目创建完成，目录如下

![](https://s1.328888.xyz/2022/10/08/fRPwd.png)

5. IDEA中的Maven设置，仓库位置，更改路径

![](https://s1.328888.xyz/2022/10/08/fR77j.png)

**pom核心配置文件**

一个 maven 工程都有一个 pom.xml 文件，通过 pom.xml 文件定义项目的信息、项目依赖、引入插 件等等。

创建一个Servlet, 缺少jar包报错, 要解决问题，就是要将 servlet-api-xxx.jar 包放进来，作为 maven 工程应当添加 servlet的坐标，从而导入它的 jar

 pom.xml 文件中引入依赖包的坐标 

```
<!--引入Servlet依赖-->
<dependencies>
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>4.0.1</version>
      <scope>provided</scope>
    </dependency>
</dependencies>
```

使用插件,可以由插件启动tomcat

```
<build>
    <plugins>
        <!--Tomcat插件 -->
        <plugin>
            <groupId>org.apache.tomcat.maven</groupId>
            <artifactId>tomcat7-maven-plugin</artifactId>
            <version>2.2</version>
            <!--修改Tomcat的端口和访问路径-->
            <configuration>
                <port>80</port><!--访问端口号 -->
                <path>/</path>
            </configuration>
        </plugin>
    </plugins>
</build>
```

**Maven的常用命令** 

| 命令        | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| mvn compile | 完成编译操作，执行完毕后，会生成target目录，该目录中存放了编译后的字节码文件 |
| mvn clean   | 执行完毕后，会将target目录删除                               |
| mvn clean   | 执行完毕后，会在target目录中生成三个文件夹:<br>surefire、surefire-reports(测试报告)、test-classes(测试的字节码文件) |
| mvn package | 完成打包操作,执行完毕后，会在target目录中生成一个文件，该文件可能是jar、war |
| mvn install | 执行mvn install命令，完成将打好的jar包安装到本地仓库的操作，执行完毕后<br>会在本地仓库中出现安装后的jar包，方便其他工程引用 |

## Servlet

Servlet（Server Applet）是Java Servlet的简称，称为小服务程序或服务连接器，是Java语言编写的服务器端程序，换句话说，Servlet就是运行在服务器上的Java类。

Servlet用来完成B/S架构下客户端请求的响应处理，也就是交互式地浏览和生成数据，生成动态Web内容。

### Servlet的编程步骤

- 建立一个Java Web Application项目并配置Tomcat服务器。
- 自定义类实现Servlet接口或继承 HttpServlet类（推荐） 并重写service方法。
- 将自定义类的信息配置到 web.xml文件并启动项目，配置方式如下

```java
//@WebServlet("/hello1") web.xml中不配置 使用注解
public class HelloServlet  implements Servlet {
        @Override
        public void init(ServletConfig servletConfig) throws ServletException {

        }

        @Override
        public ServletConfig getServletConfig() {
        	return null;
        }

        @Override
        public void service(ServletRequest servletRequest,ServletResponse servletResponse) throws ServletException, IOException {
        	System.out.println("接收到了浏览器的请求并做出了响应！");
        }

        @Override
        public String getServletInfo() {
        	return null;
        }

        @Override
        public void destroy() {

        }
}
```

> src.main.webapp.WEB-INF 下的 web.xml 中添加

```java
<!-- 配置Servlet -->
<servlet>
    <!-- HelloServlet是Servlet类的别名 -->
    <servlet-name>HelloServlet</servlet-name>
    <!-- com.aaa.test1.HelloServlet是包含路径的真实的Servlet类名 -->
    <servlet-class>com.aaa.test1.HelloServlet</servlet-class>
</servlet>
<!-- 映射Servlet -->
<servlet-mapping>
    <!-- HelloServlet是Servlet类的别名，与上述名称必须相同 -->
    <servlet-name>HelloServlet</servlet-name>
    <!-- /hello是供浏览器使用的地址 -->
    <url-pattern>/hello</url-pattern>
</servlet-mapping>
```

在浏览器上访问的方式为：http://localhost:8080/工程路径/url-pattern的内容

###  Servlet接口

基本概念

- javax.servlet.Servlet接口用于定义所有servlet必须实现的方法。

常用的方法

方法介绍

**void init(ServletConfig config)**	由servlet容器调用，以向servlet指示servlet正在被放入服务中

**void service(ServletRequest req,ServletResponse res)**	由servlet容器调用，以允许servlet响应请求

**ServletConfig getServletConfig()**	返回ServletConfig对象，该对象包含此servlet的初始化和启动参数

**String getServletInfo()**	返回有关servlet的信息，如作者、版本和版权

**void destroy()**	由servlet容器调用，以向servlet指示该servlet正在退出服务

### Servlet的生命周期

- 构造方法只被调用一次，当第一次请求Servlet时调用构造方法来创建Servlet的实例。 

- init方法只被调用一次，当创建好Servlet实例后立即调用该方法实现Servlet的初始化。  

- service方法被多次调用，每当有请求时都会调用service方法来用于请求的响应。 

- destroy方法只被调用一次，当该Servlet实例所在的Web应用被卸载前调用该方法来释放当前占用的资源。

### GenericServlet类

基本概念

- javax.servlet.GenericServlet类主要用于定义一个通用的、与协议无关的servlet，该类实现了Servlet接口。

- 若编写通用servlet，只需重写service抽象方法即可。

**常用的方法**

| 方法声明                                                     | 功能介绍                             |
| ------------------------------------------------------------ | ------------------------------------ |
| abstract void service(ServletRequest req,ServletResponse res) | 由servlet容器调用允许servlet响应请求 |

### HttpServlet类

基本概念

- javax.servlet.http.HttpServlet类是个抽象类并继承了GenericServlet类。

- 用于创建适用于网站的HTTP Servlet，该类的子类必须至少重写一个方法。

**常用的方法**

**void doGet(HttpServletRequest req,HttpServletResponse resp)**	处理客户端的GET请求

**void doPost(HttpServletRequest req,HttpServletResponse resp)**	处理客户端的POST请求

**void init()**	进行初始化操作

**void service(HttpServletRequest req,HttpServletResponse resp)** 根据请求决定调用doGet还是doPost方法

**void destroy()**	删除实例时释放资源

**GET请求**

发出GET请求的主要方式： 

​	（1）在浏览器输入URL按回车 

​	（2）点击<a>超链接 </a>

​	（3）点击submit按钮，提交 <form method="get">表单 GET请求特点：会将请求数据添加到请求URL地址的后面，只能提交少量的数据、不安全

**POST请求**

发出POST请求的方法如下： 

​	点击submit按钮，提交 <form method="post">表单 

POST请求的特点： 

​	请求数据添加到HTTP协议体中，可提交大量数据、安全性好

> 实现Servlet接口，这里我们直接继承HttpServlet

```java
@WebServlet("/thind")
public class ThindServlet extends HttpServlet {
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("Post");
    }

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("Get");
    }
}
```

> 编写Servlet的映射(有Servlet依赖则不用)

```xml
    <!--注册Servlet-->
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.kuang.servlet.HelloServlet</servlet-class>
    </servlet>
    <!--Servlet的请求路径-->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
```

> 映射问题

1. 一个Servlet可以指定一个映射路径

   ```xml
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/hello</url-pattern>
       </servlet-mapping>
   ```

2. 一个Servlet可以指定多个映射路径

   ```xml
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/hello</url-pattern>
       </servlet-mapping>
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/hello2</url-pattern>
       </servlet-mapping>
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/hello3</url-pattern>
       </servlet-mapping>
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/hello4</url-pattern>
       </servlet-mapping>
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/hello5</url-pattern>
       </servlet-mapping>
   ```

3. 一个Servlet可以指定通用映射路径

   ```xml
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/hello/*</url-pattern>
       </servlet-mapping>
   ```

4. 默认请求路径

   ```xml
       <!--默认请求路径-->
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/*</url-pattern>
       </servlet-mapping>
   ```

5. 指定一些后缀或者前缀等等….

   ```xml
   <!--可以自定义后缀实现请求映射
       注意点，*前面不能加项目映射的路径
       hello/sajdlkajda.qinjiang
       -->
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>*.qinjiang</url-pattern>
   </servlet-mapping>
   ```

6. 优先级问题
   指定了固有的映射路径优先级最高，如果找不到就会走默认的处理请求；

   ```xml
   <!--404-->
   <servlet>
       <servlet-name>error</servlet-name>
       <servlet-class>com.kuang.servlet.ErrorServlet</servlet-class>
   </servlet>
   <servlet-mapping>
       <servlet-name>error</servlet-name>
       <url-pattern>/*</url-pattern>
   </servlet-mapping>
   ```

### ServletRequest接口

基本概念 

- javax.servlet.ServletRequest接口主要用于向servlet提供客户端请求信息，可以从中获取到任何 请求信息。 

- Servlet容器创建一个ServletRequest对象，并将其作为参数传递给Servlet的service方法。

**常用的方法**

**String getParameter(String name)**	以字符串形式返回请求参数的值，如果该参数不存在，则返回空值

**String[] getParameterValues(String name)**	返回一个字符串对象数组，其中包含给定请求参数所具有的所有值，如果该参数不存在，则返回空值

**Map<String, String[]> getParameterMap()**	返回请求参数的键值对，一个键可以对应多个值

**String getRemoteAddr()**	返回发送请求的客户端或最后一个代理的IP地址

**int getRemotePort()**	返回发送请求的客户端或最后一个代理的端口号

```html
<html>
<head>
    <meta charset="UTF-8">
    <title>请求参数的获取和测试</title>
</head>
<body>
    <form action="parameter" method="post">
      姓名：<input type="text" name="name"/><br/>
      年龄：<input type="text" name="age"/><br/>
      爱好：<input type="checkbox" name="hobby" value="Java"/>Java
      <input type="checkbox" name="hobby" value="C"/>C
      <input type="checkbox" name="hobby" value="C++"/>C++<br/>
      <input type="submit" value="提交"/>
    </form>
</body>
</html>
```

```java
@WebServlet("/parameter")
public class ParameterServlet extends HelloServlet{
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException, UnsupportedEncodingException {
        // 6.设置请求信息中的编码方式为utf-8来解决乱码问题
        request.setCharacterEncoding("utf-8");
        // 1.获取指定参数名称对应的参数值并打印
        String name = request.getParameter("name");
        System.out.println("获取到的姓名为：" + name);
        String[] hobbies = request.getParameterValues("hobby");
        System.out.print("获取到的爱好有：");
        for (String ts : hobbies) {
            System.out.print(ts + " ");
        }
        System.out.println();
        System.out.println("----------------------------");

        // 2.获取请求参数名和对应值的第二种方式
        Map<String, String[]> parameterMap = request.getParameterMap();
        // 使用Map集合中所有的键值对组成Set集合
        Set<Map.Entry<String, String[]>> entries = parameterMap.entrySet();
        // 遍历Set集合
        for (Map.Entry<String, String[]> me : entries) {
            System.out.print(me.getKey() + "对应的数值有：");
            for (String ts : me.getValue()) {
                System.out.print(ts + " ");
            }
            System.out.println();
        }
        System.out.println("----------------------");
        // 4.获取客户端请求的其它信息
        System.out.println("发送请求的客户端IP地址为：" + request.getRemoteAddr());
        System.out.println("发送请求的客户端端口号为：" + request.getRemotePort());
    }
}
```

### HttpServletRequest接口

web服务器接收到客户端的http请求，针对这个请求，分别创建一个代表请求的HttpServletRequest对象，代表响应的一个HttpServletResponse；

- 如果要获取客户端请求过来的参数：找HttpServletRequest
- 如果要给客户端响应一些信息：找HttpServletResponse

基本概念

- javax.servlet.http.HttpServletRequest接口是ServletRequest接口的子接口，主要用于提供HTTP 请求信息的功能。 

- 不同于表单数据，在发送HTTP请求时，HTTP请求头直接由浏览器设置。 

- 可直接通过HttpServletRequest对象提供的一系列get方法获取请求头数据。 

**常用的方法**

**String getRequestURI()**	返回此请求的资源路径信息

**StringBuffer getRequestURL()**	返回此请求的完整路径信息

**String getMethod()**	返回发出此请求的HTTP方法的名称，例如GET、POST

**String getQueryString()**	返回路径后面请求中附带的参数

**String getServletPath()**	返回此请求中调用servlet的路径部分

```java
System.out.println("发送请求的客户端IP地址为：" +request.getRemoteAddr());
System.out.println("发送请求的客户端端口号为：" + request.getRemotePort());
System.out.println("请求资源的路径为：" + request.getRequestURI());
System.out.println("请求资源的完整路径为：" + request.getRequestURL());
System.out.println("请求方式为：" + request.getMethod());
System.out.println("请求的附带参数为：" + request.getQueryString());
System.out.println("请求的Servlet路径为：" + request.getServletPath());
```

### ServletResponse接口

基本概念

- javax.servlet.ServletResponse接口用于定义一个对象来帮助Servlet向客户端发送响应。 

- Servlet容器创建ServletResponse对象，并将其作为参数传递给servlet的service方法。

**常用方法**

**PrintWriter getWriter()**	返回可向客户端发送字符文本的PrintWriter对象

**String getCharacterEncoding()**	获取响应内容的编码方式

**void setContentType(String type)**	如果尚未提交响应，则设置发送到客户端响应的内容类型。内容类型可以包括字符编码规范，例如text/html;charset=UTF-8

```java
@Override
public void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
		// 获取响应数据的默认编码方式
        String characterEncoding = response.getCharacterEncoding();
        System.out.println("服务器响应数据的默认编码方式为：" + characterEncoding);
        // ISO-8859-1
        // 设置服务器和浏览器的编码方式以及文本类型
        response.setContentType("text/html;charset=UTF-8");
        PrintWriter writer = response.getWriter();
        writer.write("我接收到了！");
        writer.write("<h1>" +"名字："+ request.getParameter("name") + "</h1>");
        System.out.println("服务器发送数据成功！");
        writer.close();
}
```

### HttpServletResponse接口

基本概念

javax.servlet.http.HttpServletResponse接口继承ServletResponse接口，以便在发送响应时提供特定于HTTP的功能。

**常用方法**

void sendRedirect(String location)   使用指定的重定向位置URL向客户端发送临时重定向响应

### 重定向和转发

**重定向的概述** 

重定向的概念

首先客户浏览器发送http请求，当web服务器接受后发送302状态码响应及对应新的location给客户浏览器，客户浏览器发现是302响应，则自动再发送一个新的http请求，请求url是新的location 地址，服务器根据此请求寻找资源并发送给客户。 

重定向的实现

实现重定向需要借助javax.servlet.http.HttpServletResponse接口中的以下方法：

void sendRedirect(String location)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>重定向的测试</title>
</head>
<body>
<form action="redirectServlet" method="post">
    <input type="submit" value="重定向"/>
</form>
</body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>重定向后的页面</title>
</head>
<body>
<h1>服务器重新指定位置后的页面</h1>
</body>
</html>
```

```java
@WebServlet("/redirectServlet")
public class RedirectServlet extends HttpServlet {
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws IOException {
        System.out.println("接收到了浏览器的请求...");
        // 重定向，也就是给浏览器发送一个新的位置
        resp.sendRedirect("target.html");
        //response.sendRedirect("www.aobayu.cn");
    }

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws IOException {
        this.doPost(req, resp);
    }
}
```

重定向的特点

- 重定向之后，浏览器地址栏的URL会发生改变。 

- 重定向过程中会将前面Request对象销毁，然后创建一个新的Request对象。 

- 重定向的URL可以是其它项目工程。

**转发的概述**

转发的概念

一个Web组件（Servlet/JSP）将未完成的处理通过容器转交给另外一个Web组件继续处理，转发 的各个组件会共享Request和Response对象。

转发的实现

绑定数据到Request对象

**Object getAttribute(String name)** 将指定属性值作为对象返回，若给定名称属性不存在，则返回空值 

**void setAttribute(String name,Object o)**  在此请求中存储属性值

获取转发器对象

**RequestDispatcher getRequestDispatcher(String path)**	返回一个RequestDispatcher对象，该对象充当位于给定路径上的资源的包装器

转发操作

**void forward(ServletRequest request, ServletResponse response)**	将请求从一个servlet转发到服务器上的另一个资源（Servlet、JSP文件或HTML文件）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>转发的测试</title>
</head>
<body>
<form action="forwardServlet" method="post">
    <input type="submit" value="转发"/>
</form>
</body>
</html>
```

```java
@WebServlet("/forwardServlet")
public class ForwardServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("接收到了浏览器的请求...");
        // 向request对象中设置属性信息
        req.setAttribute("key1", "value1");
        // 转发，也就是让Web组件将任务转交给另外一个Web组件
        RequestDispatcher requestDispatcher = req.getRequestDispatcher("/targetServlet");

        requestDispatcher.forward(req, resp);
    }
}
```

```java
@WebServlet("/targetServlet")
public class TargetServlet extends HelloServlet{
    @Override
    public void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        this.doPost(request, response);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws IOException {
        System.out.println("转发过来了...");
        // 获取request对象中的属性值判断是否共享
        Object key1 = req.getAttribute("key1");
        System.out.println("获取到的属性值为：" + key1);// value1
        // 通过打印流向页面写入转发成功的信息
        resp.setContentType("text/html;charset=utf-8");
        resp.getWriter().write("<h1>转发成功！</h1>");
    }
}
```

转发的特点

- 转发之后浏览器地址栏的URL不会发生改变。

- 转发过程中共享Request对象。 

- 转发的URL不可以是其它项目工程。

### Servlet接收中文乱码

**接收乱码原因**

浏览器在提交表单时，会对中文参数值进行自动编码。当Tomcat服务器接收到浏览器请求后自动 解码，当编码与解码方式不一致时,就会导致乱码。 

**解决POST接收乱码**

```Java
//接收之前设置编码方式： 
request.setCharacterEncoding("utf-8") 
//提示：必须在调用request.getParameter("name")之前设置
```

 **解决GET接收乱码**

```Java
// 将接收到的中文乱码重新编码: 
// 接收到get请求的中文字符串 
String name = request.getParameter("name"); 
// 将中文字符重新编码，默认编码为ISO-8859-1 
String userName = new String(name.getBytes("ISO-8859-1"),"utf-8");
```

## Cookie、Session

### 会话

**会话**：用户打开一个浏览器，点击了很多超链接，访问多个web资源，关闭浏览器，这个过程可以称之为会话；

**有状态会话**：一个同学来过教室，下次再来教室，我们会知道这个同学，曾经来过，称之为有状态会话；

**你能怎么证明你是学生？**

1. 学生证书
2. 学校登记，你来过了

**一个网站，怎么证明你来过？**

客户端 服务端

1. 服务端给客户端一个 信件，客户端下次访问服务端带上信件就可以了； cookie
2. 服务器登记你来过了，下次你来的时候我来匹配你； seesion

**状态管理**

Web程序基于HTTP协议通信，而HTTP协议是”无状态”的协议，一旦服务器响应完客户的请求之 后，就断开连接，而同一个客户的下一次请求又会重新建立网络连接。 

服务器程序有时是需要判断是否为同一个客户发出的请求，比如客户的多次选购商品。因此，有必 要跟踪同一个客户发出的一系列请求。

把浏览器与服务器之间多次交互作为一个整体，将多次交互所涉及的数据保存下来，即状态管理。

多次交互的数据状态可以在客户端保存，也可以在服务器端保存。状态管理主要分为以下两类： 

**客户端管理**：将状态保存在客户端。基于Cookie技术实现。

 **服务器管理**：将状态保存在服务器端。基于Session技术实现。

### 保存会话的两种技术

**cookie**

- 客户端技术 （响应，请求）

**session**

- 服务器技术，利用这个技术，可以保存用户的会话信息？ 我们可以把信息或者数据放在Session中！

常见常见：网站登录之后，你下次不用再登录了，第二次访问直接就上去了！

### Cookie技术

- Cookie本意为”饼干“的含义，在这里表示客户端以“名-值”形式进行保存的一种技术。

- 浏览器向服务器发送请求时，服务器将数据以Set-Cookie消息头的方式响应给浏览器，然后浏览器 会将这些数据以文本文件的方式保存起来。

- 当浏览器再次访问服务器时，会将这些数据以Cookie消息头的方式发送给服务器。

### Cookie的方法

使用javax.servlet.http.Cookie类的构造方法实现Cookie的创建。

| 方法声明                          | 功能介绍                 |
| --------------------------------- | ------------------------ |
| Cookie(String name, String value) | 根据参数指定数值构造对象 |

使用javax.servlet.http.HttpServletResponse接口的成员方法实现Cookie的添加。

| 方法声明                      | 功能介绍                 |
| ----------------------------- | ------------------------ |
| void addCookie(Cookie cookie) | 添加参数指定的对象到响应 |

```java
@WebServlet(name = "CookieServlet", urlPatterns = "/cookie")
public class CookieServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 1.测试一下浏览器的请求是否到达
        System.out.println("看看有没有执行到这里哦！");
        // 2.创建Cookie对象并添加到响应信息中
        Cookie cookie = new Cookie("name", "zhangfei");
        response.addCookie(cookie);
        System.out.println("创建Cookie成功！");
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request, response);
    }
}
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>测试</title>
</head>
<body>
<form action="cookie" method="post">
    <input type="submit" value="测试cookie"/>
</form>
</body>
</html>
```

> 使用javax.servlet.http.HttpServletRequest接口的成员方法实现Cookie对象的获取。

| 方法声明              | 功能介绍                         |
| --------------------- | -------------------------------- |
| Cookie[] getCookies() | 返回此请求中包含的所有Cookie对象 |

```java
@WebServlet(name = "CookieServlet2", urlPatterns = "/cookie2")
    public class CookieServlet2 extends HttpServlet {
        protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            // 1.获取客户端发来的Cookie信息并打印出来
            Cookie[] cookies = request.getCookies();
            System.out.println("获取到的Cookie信息有：");
            for (Cookie tc : cookies) {
                System.out.println(tc.getName() + "对应的值为：" + tc.getValue());
            }
        }

        protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            this.doPost(request, response);
        }
```

> 使用javax.servlet.http.Cookie类的构造方法实现Cookie对象中属性的获取和修改。

| 方法声明                       | 功能介绍                 |
| ------------------------------ | ------------------------ |
| String getName()               | 返回此Cookie对象中的名字 |
| String getValue()              | 返回此Cookie对象的数值   |
| void setValue(String newValue) | 设置Cookie的数值         |

```java
@WebServlet(name = "CookieServlet3", urlPatterns = "/cookie3")
public class CookieServlet3 extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            // 1.获取客户端发来的Cookie信息并打印出来
            Cookie[] cookies = request.getCookies();
            for (Cookie tc : cookies) {
                // 2.当获取到的Cookie对象的名字为name时，将对应的数值修改为guanyu并添加到响应信息中
                if ("name".equalsIgnoreCase(tc.getName())) {
                    tc.setValue("guanyu");
                    response.addCookie(tc);
                    break;
                }
            }
            System.out.println("修改Cookie信息成功！");
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            this.doPost(request, response);
        }
	}
```

### Cookie的生命周期

- 默认情况下，浏览器会将Cookie信息保存在内存中，只要浏览器关闭，Cookie信息就会消失。

- 如果希望关闭浏览器后Cookie信息仍有效，可以通过Cookie类的成员方法实现。

| 方法声明                   | 功能介绍                               |
| -------------------------- | -------------------------------------- |
| int getMaxAge()            | 返回cookie的最长使用期限（以秒为单位） |
| void setMaxAge(int expiry) | 设置cookie的最长保留时间（秒）         |

```java
@WebServlet(name = "CookieServlet4", urlPatterns = "/cookie4")
    public class CookieServlet4 extends HttpServlet {
        protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            // 1.创建Cookie信息
            Cookie cookie = new Cookie("name", "liubei");
            // 2.获取Cookie信息的默认使用期限
            int maxAge = cookie.getMaxAge();
            System.out.println("该Cookie的默认使用期限是：" + maxAge);
            // 3.修改Cookie信息的使用期限
            // 正数表示在指定的秒数后失效   负数表示浏览器关闭后失效   0表示马上失效
            //cookie.setMaxAge(0);
            cookie.setMaxAge(60*10);
            // 4.添加到响应信息中
            response.addCookie(cookie);
            System.out.println("设置Cookie的生命周期成功！");
        }

        protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            this.doPost(request, response);
        }
    }
```

> cookie存中文会报错，因此可以使用url编码

```java
@Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //发送Cookie
        String value = "张飞";
        //对中文进行URL编码
        value = URLEncoder.encode(value, "UTF-8");
        System.out.println("存储数据："+value);
        //将编码后的值存入Cookie中
        Cookie cookie = new Cookie("username",value);
        //设置存活时间   ，1周 7天
        cookie.setMaxAge(60*60*24*7);
        //2. 发送Cookie，response
        response.addCookie(cookie);
    }
```

> 解码使用

```java
@Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //获取Cookie
        //1. 获取Cookie数组
        Cookie[] cookies = request.getCookies();
        //2. 遍历数组
        for (Cookie cookie : cookies) {
            //3. 获取数据
            String name = cookie.getName();
            if("username".equals(name)){
                String value = cookie.getValue();//获取的是URL编码后的值 %E5%BC%A0%E4%B8%89
                //URL解码
                value = URLDecoder.decode(value,"UTF-8");
                System.out.println(name+":"+value);//value解码后为 张飞
                break;
            }
        }
    }
```

### Cookie的特点

Cookie技术不适合存储所有数据，程序员只用于存储少量、非敏感信息，原因如下：

- 将状态数据保存在浏览器端，不安全。

- 保存数据量有限制，大约4KB左右。

- 只能保存字符串信息。

- 可以通过浏览器设置为禁止使用。

### Session技术

- Session本意为"会话"的含义，是用来维护一个客户端和服务器关联的一种技术。

- 浏览器访问服务器时，服务器会为每一个浏览器都在服务器端的内存中分配一个空间，用于创建一个Session对象，该对象有一个id属性且该值唯一，我们称为SessionId，并且服务器会将这个SessionId以Cookie方式发送给浏览器存储。

- 浏览器再次访问服务器时会将SessionId发送给服务器，服务器可以依据SessionId查找相对应的Session对象

**什么是Session**

- 服务器会给每一个用户（浏览器）创建一个Seesion对象；
- 一个Seesion独占一个浏览器，只要浏览器没有关闭，这个Session就存在；
- 用户登录之后，整个网站它都可以访问！--> 保存用户的信息；保存购物车的信息…..

### Session的方法

使用javax.servlet.http.HttpServletRequest接口的成员方法实现Session的获取。

| 方法声明                 | 功能介绍                                            |
| ------------------------ | --------------------------------------------------- |
| HttpSession getSession() | 返回此请求关联的当前Session，若此请求没有则创建一个 |

使用javax.servlet.http.HttpSession接口的成员方法实现判断和获取

| 方法声明        | 功能介绍                  |
| --------------- | ------------------------- |
| boolean isNew() | 判断是否为新创建的Session |
| String getId()  | 获取Session的编号         |

```java
@WebServlet(name = "SessionServlet", urlPatterns = "/session")
public class SessionServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 1.调用getSession方法获取或者创建Session对象
        HttpSession session = request.getSession();
        // 2.判断该Session对象是否为新建的对象
        System.out.println(session.isNew()? "新创建的Session对象": "已有的Session对象");
        // 3.获取编号并打印
        String id = session.getId();
        System.out.println("获取到的Session编号为：" + id);
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    	this.doPost(request, response);
    }
}
```

> 使用javax.servlet.http.HttpSession接口的成员方法实现属性的管理。

| 方法声明                                     | 功能介绍                                                     |
| -------------------------------------------- | ------------------------------------------------------------ |
| Object getAttribute(String name)             | 返回在此会话中用指定名称绑定的对象，如果没有对象在该名称下绑定，则返回空值 |
| void setAttribute(String name, Object value) | 使用指定的名称将对象绑定到此会话                             |
| void removeAttribute(String name)            | 从此会话中删除与指定名称绑定的对象                           |

```java
@WebServlet(name = "SessionServlet2", urlPatterns = "/session2")
public class SessionServlet2 extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        HttpSession session = request.getSession();
        // 1.设置属性名和属性值
        session.setAttribute("name", "machao");
        // 2.获取指定属性名对应的属性值
        System.out.println("获取到的属性值为：" + session.getAttribute("name")); // machao
        // 3.删除指定的属性名
        session.removeAttribute("name");
        // 4.获取指定属性名对应的属性值
        System.out.println("获取到的属性值为：" + session.getAttribute("name")); // null
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    	this.doPost(request, response);
    }
}
```

> 可以配置web.xml文件修改失效时间。

```xml
<session-config>
        <session-timeout>30</session-timeout>
</session-config>
```

### Session的特点

- 数据比较安全。
- 能够保存的数据类型丰富，而Cookie只能保存字符串。
- 能够保存更多的数据，而Cookie大约保存4KB。
- 数据保存在服务器端会占用服务器的内存空间，如果存储信息过多、用户量过大，会严重影响服务器的性能。

使用场景：

- 保存一个登录用户的信息；
- 购物车信息；
- 在整个网站中经常会使用的数据，我们将它保存在Session中；

### Session和cookie的区别

- Cookie是把用户的数据写给用户的浏览器，浏览器保存 （可以保存多个）
- Session把用户的数据写到用户独占Session中，服务器端保存 （保存重要的信息，减少服务器资源的浪费）
- Session对象由服务创建；

## JSP

### 什么是JSP

Java Server Pages ： Java服务器端页面，也和Servlet一样，用于动态Web技术！

JSP是Java Server Pages的简称，跟Servlet一样可以动态生成HTML响应， JSP文件命名为xxx.jsp。

与Servlet不同，JSP文件以HTML标记为主，然后内嵌Java代码段，用于处理动态内容。

最大的特点：

- 写JSP就像在写HTML
- 区别：
  - HTML只给用户提供静态的数据
  - JSP页面中可以嵌入JAVA代码，为用户提供动态数据；

**浏览器向服务器发送请求，不管访问什么资源，其实都是在访问Servlet！**

JSP最终也会被转换成为一个Java类！**JSP 本质上就是一个Servlet！**

```jsp
<%@ page import="java.util.Date" %> 

<%@ page contentType="text/html;charset=UTF-8" language="java" %> 

<html> 
<head> 
	<title>Hello Time</title>
</head> 
<body> 
现在的时间是：<%= new Date()%> 
</body> 
</html>
```

只要是 JAVA代码就会原封不动的输出；

如果是HTML代码，就会被转换为：

```java
out.write("<html>\r\n");
```

这样的格式，输出到前端！

### JSP语法

**<%! 程序代码区 %>||<% %>**

```jsp
<%!
    int i; 
	public void setName(){}
%>

<%
    int sum = 0;
	for (int i = 1; i <=100 ; i++) {
      sum+=i;
    }
	out.println("<h1>Sum="+sum+"</h1>");
%>
```

程序代码区：可以定义局部变量以及放入任何的Java程序代码。

**<%= %>**

```jsp
<%="hello world"%> 
```

注意：不需要以;结束，只有一行

可以输出一个变量或一个具体内容，但=后面必须是字符串变量或者可以被转换成字符串的表达式。	

**注释**

```jsp
<!--… …-->HTML文件的注释，浏览器可以查看到
<%--… …--%>JSP文件的注释，浏览器看不到
<%//… …%>Java语言中的单行注释，浏览器看不到
<%/*… …*/%>Java语言中的多行注释，浏览器看不到 注释的内容不会被执行
```

**JSP指令**

**page**指令用于导包和设置一些页面属性，常用属性如下：

import		          导入相应的包，惟一允许在同一文档中多次出现的属性

contentType		设置Content-Type响应报头，标明即将发送到浏览器的文档类型

pageEncoding	 设置页面的编码

language 		     指定页面使用的语言 

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" pageEncoding="utf-8" %>

<%@include file=""%>
<%--@include会将两个页面合二为一--%>

<%@include file="common/header.jsp"%>
<h1>网页主体</h1>

<%@include file="common/footer.jsp"%>

<hr>

<%--jSP标签 jsp:include：拼接页面，本质还是三个 --%>
<jsp:include page="/common/header.jsp"/>
<h1>网页主体</h1>
<jsp:include page="/common/footer.jsp"/>
```

### 内置对象

在JSP程序中有9个内置对象由容器为用户进行实例化，程序员可以不用定义就直接使用这些变量。

在JSP转换成Servlet后，会自动追加这些变量的定义，使用内置对象可以简化JSP的开发。

| 对象变量    | 对象类型            | 作用             |
| ----------- | ------------------- | ---------------- |
| out         | JSPWriter           | 输出流           |
| request     | HttpServletRequest  | 请求信息         |
| response    | HttpServletResponse | 响应信息         |
| session     | HttpSession         | 会话             |
| application | ServletContext      | 全局的上下文对象 |
| pageContext | PageContext         | JSP页面上下文    |
| page        | Object              | JSP页面本身      |
| config      | ServletConfig       | Servlet配管对象  |
| exception   | Throwable           | 捕获网页异常     |

request：客户端向服务器发送请求，产生的数据，用户看完就没用了，比如：新闻，用户看完没用的！

session：客户端向服务器发送请求，产生的数据，用户用完一会还有用，比如：购物车；

application：客户端向服务器发送请求，产生的数据，一个用户用完了，其他用户还可能使用，比如：聊天数据；

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>session内置对象的使用</title>
</head>
    <body>
        <% session.setAttribute("name","hd");%>
        <% session.getAttribute("name");%>
        ${name}
    </body>
</html>
```

### EL表达式

EL（Expression Language）表达式提供了在JSP中简化表达式的方法，可以方便地访问各种数据并输出。

EL表达式： ${ }获取数据、执行运算、获取web开发的常用对象

**JSP标签**

> 依次访问pageContext、request、session和application作用域对象存储的数据。

```jsp
<%=request.getAttribute("varName")%>
用EL实现: ${varName}
```

### **JSTL表达式**

JSTL( JSP Standard Tag Library ) 被称为JSP标准标签库。

开发人员可以利用这些标签取代JSP页面上的Java代码，从而提高程序的可读性，降低程序的维护难度。

JSTL标签库的使用就是为了弥补HTML标签的不足；它自定义许多标签，可以供我们使用，标签的功能和Java代码一样！

**JSTL标签库使用步骤**

- 引入对应的 taglib
- 使用其中的方法
- **在Tomcat 也需要引入 jstl的包，否则会报错：JSTL解析错误**

pom.xml

```xml
<dependency>
    <groupId>jstl</groupId>
    <artifactId>jstl</artifactId>
    <version>1.2</version>
</dependency>
<dependency>
    <groupId>apache-taglibs</groupId>
    <artifactId>standard</artifactId>
    <version>1.1.2</version>
</dependency>
```

在JSP页面中使用taglib指定引入jstl标签库

```jsp
<!-- prefix属性用于指定库前缀 --> 
<!-- uri属性用于指定库的标识 --> 
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
```

> 输出标签

```jsp
<c:out></c:out> 用来将指定内容输出的标签
```

> 设置标签

```jsp
<c:set></c:set> 用来设置属性范围值的标签
```

> 删除标签

```jsp
<c:remove></c:remove> 用来删除指定数据的标签
```

> 单条件判断标签

```jsp
<c:if test ="EL条件表达式"> 

满足条件执行 

</c:if >

<head>
    <title>Title</title>
</head>
<body>


<h4>if测试</h4>

<hr>

<form action="coreif.jsp" method="get">
    <%--
    EL表达式获取表单中的数据
    ${param.参数名}
    --%>
    <input type="text" name="username" value="${param.username}">
    <input type="submit" value="登录">
</form>

<%--判断如果提交的用户名是管理员，则登录成功--%>
<c:if test="${param.username=='admin'}" var="isAdmin">
    <c:out value="管理员欢迎您！"></c:out>
</c:if>

<%--自闭合标签--%>
<c:out value="${isAdmin}"/>

</body>
```

> 多条件判断标签

```jsp
<c:choose > 

	<c:when test ="EL表达式"> 

		满足条件执行 

	</c:when> 

	…

	<c:otherwise>

		不满足上述when条件时执行 

	</c:otherwise>

</c:choose >

<body>

<%--定义一个变量score，值为85--%>
<c:set var="score" value="55"/>

<c:choose>
    <c:when test="${score>=90}">
        你的成绩为优秀
    </c:when>
    <c:when test="${score>=80}">
        你的成绩为一般
    </c:when>
    <c:when test="${score>=70}">
        你的成绩为良好
    </c:when>
    <c:when test="${score>=60}">
        你的成绩为次
    </c:when>
    <c:otherwise>
		<c:out value="成绩不及格"></c:out><br>
	</c:otherwise>
</c:choose>

</body>
```

> 循环标签

```jsp
<c:forEach var="循环变量" items="集合"> 

	… 

</c:forEach>

<%

    ArrayList<String> people = new ArrayList<>();
    people.add(0,"张三");
    people.add(1,"李四");
    people.add(2,"王五");
    people.add(3,"赵六");
    people.add(4,"田六");
    request.setAttribute("list",people);
%>


<%--
var , 每一次遍历出来的变量
items, 要遍历的对象
begin,   哪里开始
end,     到哪里
step,   步长
--%>
<c:forEach var="people" items="${list}">
    <c:out value="${people}"/><br>
</c:forEach>

<hr>
<%-- 指定起始和结尾位置 从下标1开始到3结束，包含1和3 跳跃性遍历 间隔为1--%>
<c:forEach var="people" items="${list}" begin="1" end="3" step="1" >
    <c:out value="${people}"/><br>
</c:forEach>
```

> 实现循环标签的使用

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>实现循环标签的使用</title>
</head>
<body>
<%
  // 准备一个数组并初始化
  String[] sArr = {"11", "22", "33", "44", "55"};
  pageContext.setAttribute("sArr", sArr);
%>

<%-- 使用循环标签遍历数组中的所有元素 --%>
<c:forEach var="ts" items="${sArr}">
  <c:out value="${ts}"></c:out>
</c:forEach>
<hr/>

<%-- 跳跃性遍历 间隔为2  也就是跳过一个遍历一个 --%>
<c:forEach var="ts" items="${sArr}" step="2">
  <c:out value="${ts}"></c:out>
</c:forEach>
<hr/>

<%-- 指定起始和结尾位置 从下标1开始到3结束，包含1和3--%>
<c:forEach var="ts" items="${sArr}" begin="1" end="3">
  <c:out value="${ts}"></c:out>
</c:forEach>

</body>
</html>
```

> 实现choose标签的使用

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>实现choose标签的使用</title>
</head>
<body>
<%-- 设置一个变量代表考试的成绩并指定数值 --%>
<c:set var="score" value="59" scope="page"></c:set>
<c:out value="${score}"></c:out>
<hr/>
<%-- 进行多条件判断和处理 --%>
<c:choose>
  <c:when test="${score > 60}">
    <c:out value="成绩不错，继续加油哦！"></c:out>
  </c:when>
  <c:when test="${score == 60}">
    <c:out value="60分万岁，多一份浪费！"></c:out>
  </c:when>
  <c:otherwise>
    <c:out value="革命尚未成功，同志仍需努力！"></c:out>
  </c:otherwise>
</c:choose>
</body>
</html>
```

> 实现if标签的使用

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>实现if标签的使用</title>
</head>
<body>
<%-- 设置一个变量以及对应的数值 --%>
<c:set var="age" value="17" scope="page"></c:set>
<c:out value="${age}"></c:out>
<hr/>

<%-- 判断该年龄是否成年，若成年则提示已经成年了 --%>
<c:if test="${age >= 18}">
  <c:out value="已经成年了！"></c:out>
</c:if>

</body>
</html>
```

## Filter过滤器

**基本概念**

- Filter本意为”过滤“的含义，是JavaWeb的三大组件之一，三大组件为： Servlet、 Filter、 Listener。

- 过滤器是向 Web 应用程序的请求和响应处理添加功能的 Web 服务组件。

- 过滤器相当于浏览器与Web资源之间的一道过滤网，在访问资源之前通过一系列的过滤器对请求 进行修改、判断以及拦截等，也可以对响应进行修改、判断以及拦截等。

### 使用方式

自定义类实现Filter接口，重写对应的方法即可

```java
public class CharacterEncodingFilter implements Filter {

    //初始化：web服务器启动，就以及初始化了，随时等待过滤对象出现！
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("CharacterEncodingFilter初始化");
    }

    //Chain : 链
    /*
    1. 过滤中的所有代码，在过滤特定请求的时候都会执行
    2. 必须要让过滤器继续同行
        chain.doFilter(request,response);
     */
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        request.setCharacterEncoding("utf-8");
        response.setCharacterEncoding("utf-8");
        response.setContentType("text/html;charset=UTF-8");

        System.out.println("CharacterEncodingFilter执行前....");
        chain.doFilter(request,response); //让我们的请求继续走，如果不写，程序到这里就被拦截停止！
        System.out.println("CharacterEncodingFilter执行后....");
    }

    //销毁：web服务器关闭的时候，过滤会销毁
    public void destroy() {
        System.out.println("CharacterEncodingFilter销毁");
    }
}
```

在web.xml中配置 Filter

```xml
<filter>
    <filter-name>CharacterEncodingFilter</filter-name>
    <filter-class>com.aaa.filter.CharacterEncodingFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>CharacterEncodingFilter</filter-name>
    <!--只要是 /servlet的任何请求，会经过这个过滤器-->
    <url-pattern>/servlet</url-pattern>
    <!--<url-pattern>/*</url-pattern>-->
</filter-mapping>
```

### 登录案例

在web.xml文件中配置过滤器

```xml
	<filter>
        <filter-name>LoginFilter</filter-name>
        <filter-class>com.aobayu.demo.aaa.LoginFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>LoginFilter</filter-name>
        <!--只要是任何请求，会经过这个过滤器-->
        <url-pattern>/*</url-pattern>
        <!--<url-pattern>/*</url-pattern>-->
    </filter-mapping>
```

login.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>登录页面</title>
</head>
<body>

  <form action="login" method="post">
  用户名: <input type="text" name="userName"/><br/>
  密&nbsp;&nbsp;&nbsp;&nbsp;码:<input type="password" name="password"/><br/>
  <input type="submit" value="登录"/>
  </form>

</body>
</html>
```

main.jsp

```jsp
<%@ page import="java.util.Date" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" pageEncoding="utf-8" %>
<html>
<head>
  <title>主页面</title>
</head>
<body>
现在的时间是：<%= new Date()%>

<h1>登录成功，欢迎${sessionScope.userName}使用！</h1>

</body>
</html>
```

点击登录到 LoginServlet

```java
@WebServlet("/login")
public class LoginServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 1.接收前端页面输入的用户名和密码信息并打印
        String userName = req.getParameter("userName");
        System.out.println("接收到的用户名为：" + userName);
        String password = req.getParameter("password");
        System.out.println("接收到的密码为：" + password);
        // 2.使用固定的用户名和密码信息来进行登录的校验
        if ("admin".equals(userName) && "123456".equals(password)) {
            System.out.println("登录成功，欢迎使用！");
            // 存储用户名信息
            req.getSession().setAttribute("userName", userName);
            //跳转到 main.jsp
            resp.sendRedirect("main.jsp");
        } else {
            System.out.println("用户名或密码错误，请重新输入！");
            req.getRequestDispatcher("login.jsp").forward(req, resp);
        }
    }
}
```

登录失败拦截 LoginFilter

```java
@WebFilter("/main.jsp")
public class LoginFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("Filter初始化");
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        // 1.实现对用户访问主页面的过滤操作，也就是只有用户登录后才能访问主页面，否则一律拦截
        //判断session中是否已有用户名信息，若没有则进行拦截，否则放行
        HttpServletRequest httpServletRequest = (HttpServletRequest)servletRequest;
        HttpSession session = httpServletRequest.getSession();
        Object userName = session.getAttribute("userName");
        // 获取Servlet的请求路径
        String servletPath = httpServletRequest.getServletPath();
        // 若没有登录，则回到登录页面
        if (null == userName && !servletPath.contains("login")) {
            servletRequest.getRequestDispatcher("login.jsp").forward(servletRequest, servletResponse);
        } else {
            // 若已经登录，则放行
            filterChain.doFilter(servletRequest, servletResponse);
        }

    }

    @Override
    public void destroy() {
        System.out.println("Filter销毁");
    }
```

## Listener监听器

**概述**

监听你的web应用，监听许多信息的初始化，销毁，增加，修改，删除值等

`Servlet`监听器用于监听一些重要事件的发生，监听器对象可以在事情发生前、发生后可以做一些必要的处理 

**监听器的分类：**

在一个web应用程序的整个运行周期内，web容器会创建和销毁三个重要的对象，`ServletContext`,`HttpSession`,`ServletRequest`

 按监听的对象划分，可以分为

- ServletContext 

- HttpSession 

- ServletRequest  

​    按监听的事件划分

- 对象自身的创建和销毁的监听器

- 对象中属性的创建和消除的监听器

- session中的某个对象的状态变化的监听器

### 创建监听器

> ServletContext 监听

`ServletContext` 代表整个web应用，在服务器启动的时候，tomcat会自动创建该对象。在服务器关闭时会自动销毁该对象

```java
@WebListener
public class MyContextListener implements ServletContextListener {
        @Override
        public void contextInitialized(ServletContextEvent servletContextEvent) {
        //        获取到上下文对象
        ServletContext application = servletContextEvent.getServletContext();
        System.out.println("上下文初始化"+application);
        }
    
        @Override
        public void contextDestroyed(ServletContextEvent servletContextEvent) {
        System.out.println("上下文销毁");
        }
}
```

或在xml中配置

```xml
<listener>

	<listener-class>监听器的全路径</listener-class>

</listener>
```

> session监听

```java
@WebListener
public class MySessionListener implements HttpSessionListener {
    /**
    *
    * @param httpSessionEvent 事件参数，可以获取到被监听对象的数据信息
    */
    @Override
    public void sessionCreated(HttpSessionEvent httpSessionEvent) {
    	System.out.println("session创建"+httpSessionEvent.getSession().getId());
    }

    @Override
    public void sessionDestroyed(HttpSessionEvent httpSessionEvent) {
    	System.out.println("session销毁"+httpSessionEvent.getSession());
    }
}
```

> session中属性监听

```java
@WebListener
public class MySessionAttributeListener implements HttpSessionAttributeListener {
    @Override
    public void attributeAdded(HttpSessionBindingEvent httpSessionBindingEvent) {
    System.out.println("session属性添加："+httpSessionBindingEvent.getName());
    }

    @Override
    public void attributeRemoved(HttpSessionBindingEvent httpSessionBindingEvent) {
    System.out.println("session属性移除："+httpSessionBindingEvent.getName());
    }

    @Override
    public void attributeReplaced(HttpSessionBindingEvent httpSessionBindingEvent) {
    System.out.println("session属性替换："+httpSessionBindingEvent.getName());
    }
}
```

在线人数统计：

1、先获取容器中的数量计数器，如果没有，创建存进去

2、每创建一个session，计数器加1

3、每销毁一个session,计数器减1

```java
@WebListener
public class OnlineListener implements ServletContextListener, HttpSessionListener {
    ServletContext appliction;
    @Override
    public void contextInitialized(ServletContextEvent servletContextEvent) {
        /* 当容器创建就获取上下文对象*/
        appliction = servletContextEvent.getServletContext();
        /* 是否有计数器 */
        if(appliction.getAttribute("count")==null){
            /* 存进去，只执行一次 */
            appliction.setAttribute("count",0);
        }
    }

    @Override
    public void contextDestroyed(ServletContextEvent servletContextEvent) {
    }

    @Override
    public void sessionCreated(HttpSessionEvent httpSessionEvent) {
        /* 获取原来的计数器的值 */
        Integer count=Integer.valueOf(appliction.getAttribute("count").toString());
        count++;
        /* 存进去 */
        appliction.setAttribute("count",count);
    }

    @Override
    public void sessionDestroyed(HttpSessionEvent httpSessionEvent) {
    	Integer count=Integer.valueOf(appliction.getAttribute("count").toString());
        count--;
        appliction.setAttribute("count",count);
    }
}
```

## JQuery异步调用

**同步和异步**

同步：同步请求，客户端发出请求，等待服务器端返回结果，接着进行下一次的请求。

异步：异步请求，客户端发出请求，无需等待服务器端返回结果，接着进行下一次的请求。

**Ajax简介**

Ajax 即“**Asynchronous Javascript And XML**”（异步 JavaScript 和 XML），是指一种创建交互式、快速动态网页应用的网页开发技术，无需重新加载整个网页的情况下，能够更新部分网页的技术。

通过在后台与服务器进行少量数据交换，Ajax 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

原理：

1、客户端发送异步请求

XMLHttpRequest 对象

2、服务器端接收请求，处理数据，通常返回json格式的数据，字符串（文本）

3、客户端获取服务器返回的数据在页面上显示

使用js ,jquery ,dom ,css

### JQuery中的AJAX

**简单使用**

$.get

```xml
$.get(url,[data],[callback],[type])
url:待载入页面的URL地址  @WebServlet("/xxxxxxx") get post
data:待发送 Key/value 参数。
callback:载入成功时回调函数。 接受 后端响应的数据
type:返回内容格式，xml, html, script, json, text, _default。
```

> 在webapp目录下创建static文件夹,在static下创建js,css,image三个文件夹,将jQuery的文件拷贝到js文件夹中

在webapp下新建 webapp/register.jsp

```jsp
<%@ page contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>
<!DOCTYPE html>
<html>
<head>
    <title>JSP - Hello World</title>
    <script src="./static/js/jquery-3.6.0.js"></script>
    <script>
        $(function(){
            $("#dname").on("blur",function(){
                $.get(
                    "/demo1/checkUsername",
                    {username:$("#dname").val()},
                    function(result){
                        if(result==1){
                            $("#usermsg").html("<span style='color:red'>用户已存在<span>");
                        }else{
                            $("#usermsg").html("<span style='color:red'>true<span>");
                        }
                    }
                );
            })
        })
    </script>
</head>
<body>

<form action="/demo1/register" method="post" id="form">
    userName:<input name="username" id="dname" type="text"/> <span id="usermsg"></span><br>
    password:<input name="pass" type="password"/><br>
    <input type="button"  id="btn" value="register">
</form>

</body>
</html>
```

> 服务端Servlet 拿到username 查询数据库，如果可以查到，就返回1

```java
@WebServlet("/checkUsername")
public class CheckUsernameServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String user=req.getParameter("username");

        /*如果存在就返回1 否则0*/
        if("heda".equals(user)){
            resp.getWriter().print(1);
        }else{
            resp.getWriter().print(0);
        }
    }
}
```

### 查询数据库

**前置准备**

pom.xml

```xml
//导入mysql jar包		
<dependency> 
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.38</version>
</dependency>
//导入dbutils jar包		
<dependency>
    <groupId>commons-dbutils</groupId>
    <artifactId>commons-dbutils</artifactId>
    <version>1.6</version>
</dependency>
//导入druid jar包		
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.2.8</version>
</dependency>
```

src/main/resources 编写好的druid.properties

```java
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql:///db5?useSSL=false&useServerPrepStmts=true&characterEncoding=utf-8
username=root
password=123456
initialSize=5
maxActive=10
maxWait=3000
```

在java.com.example.demo1目录下创建controller，dao，pojo，utils文件夹

将DruidUtils 文件拷贝到utils文件夹中

```java
public class DruidUtils {
    public static DataSource dataSource;
    static {
        try {
            Properties p = new Properties();
            InputStream inputStream = DruidUtils.class.getClassLoader().getResourceAsStream("druid.properties");
            p.load(inputStream);
            dataSource = DruidDataSourceFactory.createDataSource(p);
        } catch (Exception e) {
            e.printStackTrace();
            throw new RuntimeException(e);
        }
    }
    public static Connection getConnection(){
        try {
            return dataSource.getConnection();
        } catch (SQLException e) {
            e.printStackTrace();
            return null;
        }
    }
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

    public static void close(ResultSet resultSet,Statement statement,Connection connection){
        close(resultSet);
        close(statement);
        close(connection);
    }

    public  static DataSource getDataSource(){
        return dataSource;
    }
}
```

**实现查询数据库**

新建数据库 cell ,存入用户数据

在webapp下新建 register.jsp

```jsp
<%@ page contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>
<!DOCTYPE html>
<html>
<head>
    <title>JSP</title>
    <script src="./static/js/jquery-3.6.0.js"></script>
    <script>
        $(function(){
            $("#dname").on("blur",function(){
                $.get(
                    "/demo1/checkUsername",
                    {username:$("#dname").val()},
                    function(result){
                        if(result==1){
                            $("#usermsg").html("<span style='color:red'>用户已存在<span>");
                            console.log("用户已存在");
                        }else{
                            $("#usermsg").html("");
                        }
                    }
                );
            })
        })
    </script>
</head>
<body>


<form action="/demo1/register" method="post" id="form">
    userName:<input name="username" id="dname" type="text"/> <span id="usermsg"></span><br>
    password:<input name="pass" type="password"/><br>
    <input type="button"  id="btn" value="register">
</form>

</body>
</html>
```

在pojo下新建 Cell.java

```java
public class Cell {
    private String name;
    private int money;
    private String phone;

    public Cell(){}

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getMoney() {
        return money;
    }

    public void setMoney(int money) {
        this.money = money;
    }

    public String getPhone() {
        return phone;
    }

    public void setPhone(String phone) {
        this.phone = phone;
    }

    @Override
    public String toString() {
        return "Cell{" +
                "name='" + name + '\'' +
                ", money=" + money +
                ", phone='" + phone + '\'' +
                '}';
    }

}
```

在dao下新建 CellDao.java

```java
public interface CellDao {
    long CellServlet(String name) throws SQLException;
}
```

在dao下新建 impl/CellImplement.java

```java
public class CellImplement implements CellDao {
    @Override
    public long CellServlet(String name) throws SQLException {
        
        QueryRunner qr = new QueryRunner(DruidUtils.getDataSource());
        String sql = "select * from cell where name = ?;";
        List<Cell> query = qr.query(sql, new BeanListHandler<>(Cell.class), name);

        if (query.isEmpty()){
            return 0;
        }else {
            return 1;
        }
    }
}
```

在controller下新建 CheckUsernameServlet.java

```java
@WebServlet("/checkUsername")
public class CheckUsernameServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String user=req.getParameter("username");
        /* 通过dao层查询数据库，如果可以查到就通过如下代码返回1 否则返回0  */
        CellDao cell = new CellImplement();
        try {
            long ruelt = cell.CellServlet(user);
            /*如果存在就返回1 否则0*/
            if (ruelt>0) {
                resp.getWriter().print(1);
            } else {
                resp.getWriter().print(0);
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }
}
```

### 插入数据到数据库

在webapp下修改 register.jsp

```jsp
<%@ page contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>
<!DOCTYPE html>
<html>
<head>
    <title>JSP - Hello World</title>
    <script src="./static/js/jquery-3.6.0.js"></script>
    <script>
        $(function(){
            $("#dname").on("blur",function(){
                $.get(
                    "/demo1/checkUsername",
                    {username:$("#dname").val()},
                    function(result){
                        if(result==1){
                            $("#usermsg").html("<span style='color:red'>用户已存在<span>");
                            console.log("用户已存在");
                        }else{
                            $("#usermsg").html("");
                        }
                    }
                );
            })
            $("#btn").click(function () {
                $.post(
                    "/demo1/register",
                    //序列化，拿到所有的表单元素username password
                    $("#form").serialize(),
                    function (result) {
                        if(result==1){
                            alert("插入成功")
                        }else{
                            alert("插入失败")
                        }
                    }
                )
            })
        })
    </script>
</head>
<body>

<form action="/demo1/register" method="post" id="form">
    userName:<input name="username" id="dname" type="text"/> <span id="usermsg"></span><br>
    money:<input name="money" type="text"/><br>
    phone:<input name="phone" type="text"/><br>
    <input type="button"  id="btn" value="register">
</form>

</body>
</html>
```

在dao下修改 CellDao.java

```java
public interface CellDao {
    long CellServlet(String name) throws SQLException;
    long insertServlet(String name,int money,String phone) throws SQLException;
}
```

在dao下修改 impl/CellImplement.java

```java
public class CellImplement implements CellDao {
    @Override
    public long CellServlet(String name) throws SQLException {
        QueryRunner qr = new QueryRunner(DruidUtils.getDataSource());
        String sql = "select * from cell where name = ?;";
        List<Cell> query = qr.query(sql, new BeanListHandler<>(Cell.class), name);

        if (query.isEmpty()){
            return 0;
        }else {
            return 1;
        }
    }
    
    @Override
    public long insertServlet(String name, int money, String phone) throws SQLException {

        QueryRunner qr = new QueryRunner(DruidUtils.getDataSource());
        String sql = "insert into cell(name,money,phone) values (?,?,?)";
        int update = qr.update(sql, name, money, phone);
        System.out.println(update);
        return update;
    }
}
```

在dao下新建 RegisterServlet.java

```java
@WebServlet("/register")
public class RegisterServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String name = req.getParameter("username");
        int money = Integer.parseInt(req.getParameter("money"));
        String phone = req.getParameter("phone");
        CellImplement cell = new CellImplement();
        try {
            long score = cell.insertServlet(name, money, phone);
            if (score>0){
                resp.getWriter().println(1);
            }else{
                resp.getWriter().println(0);
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }
}
```

### 简单封装

在java.com.example.demo1目录下创建service文件夹

在service 下创建 CellService.java

```java
public class CellService {
    public long InsertCell( String name,int money,String phone) throws SQLException {
        Cell cell = new Cell();
        cell.setName(name);
        cell.setMoney(money);
        cell.setPhone(phone);
        long row = new CellImplement().insertServlet(cell);
        return row;
    }
}
```

CellDao 更改

```java
public interface CellDao {
    long CellServlet(String name) throws SQLException;
    // 更改位置
    long insertServlet(Cell cell) throws SQLException;
}
```

CellImplement 更改

```java
public class CellImplement implements CellDao {
    @Override
    public long CellServlet(String name) throws SQLException {
        QueryRunner qr = new QueryRunner(DruidUtils.getDataSource());
        String sql = "select * from cell where name = ?;";
        List<Cell> query = qr.query(sql, new BeanListHandler<>(Cell.class), name);

        if (query.isEmpty()){
            return 0;
        }else {
            return 1;
        }
    }
	// 更改位置
    @Override
    public long insertServlet(Cell cell) throws SQLException {

        QueryRunner qr = new QueryRunner(DruidUtils.getDataSource());
        String sql = "insert into cell(name,money,phone) values (?,?,?)";
        int update = qr.update(sql, cell.getName(), cell.getMoney(), cell.getPhone());
        System.out.println(update);
        return update;
    }
}
```

RegisterServlet.java 更改

```java
@WebServlet("/register")
public class RegisterServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String name = req.getParameter("username");
        int money = Integer.parseInt(req.getParameter("money"));
        String phone = req.getParameter("phone");
        // 更改位置
        CellImplement cell = new CellImplement();
        // 更改位置
        try {
            long score = new CellService().InsertCell(name, money, phone);
            if (score>0){
                resp.getWriter().println(1);
            }else{
                resp.getWriter().println(0);
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }
}
```

## JSON 

JavaScript Object Notation JavaScript 对象表示法 

> JSON的特点: 

JSON 是一种轻量级的数据交换格式。

JSON采用完全独立于语言的文本格式，就是说不同的编程语言JSON数据是一致的。 

JSON易于人阅读和编写，同时也易于机器解析和生成(一般用于提升网络传输速率)。

> XML与JSON的区别

XML : 可扩展标记语言，是一种用于标记电子文件使其具有结构性的标记语言。 

JSON: (JavaScript Object Notation, JS 对象简谱) 是一种轻量级的数据交换格式。 

相同点:  它们都可以作为一种数据交换格式。 

> 二者区别:

XML是重量级的，JSON是轻量级的,XML在传输过程中比较占带宽，JSON占带宽少，易于压 缩。 

XML和json都用在项目交互下，XML多用于做配置文件，JSON用于数据交互 

JSON独立于编程语言存在,任何编程语言都可以去解析json 

### JSON 基础语法

JSON 本质就是一个字符串，但是该字符串内容是有一定的格式要求的。 定义格式 {" key": false }

```json
var 变量名 = '{"key":value,"key":value,...}';
```

`JSON` 串的键要求必须使用双引号括起来，而值根据要表示的类型确定

> 在前端页面中 转换JSON和字符串

```html
<script>
//1. 定义JSON字符串
var jsonStr = '{"name":"zhangsan","age":23,"addr":["北京","郑州","西安"]}'
let jsObject = JSON.parse(jsonStr);
//3. 将 JS 对象转换为 JSON 字符串
let jsonStr2 = JSON.stringify(jsObject);
</script>
```

### JSON串和Java对象的转换

前端发送请求时，如果是复杂的数据就会以 json 提交给后端；而后端如果需要响应一些复杂的数据时，也需要以 json 格式将数据响应回给浏览器

> `Fastjson` 是阿里巴巴提供的一个Java语言编写的高性能功能完善的 `JSON` 库，是目前Java语言中最快的 `JSON` 库，可以实现 `Java` 对象和 `JSON` 字符串的相互转换。

导入依赖 pom.xml

```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.62</version>
</dependency>
```

使用 将 Java 对象转换为 JSON 串，只需要使用 `Fastjson` 提供的 `JSON` 类中的 `toJSONString()` 静态方法

```java
String jsonStr = JSON.toJSONString(obj);
```

将 json 转换为 Java 对象，只需要使用 Fastjson 提供的 JSON 类中的 parseObject() 静态方法

```java
String str = "{'name'':'zhangxuhui','age':18 }";
Student student = JSON.parseObject(jsonStr, Student.class);
```

> lombok插件

在 Idea 中下载 lombok 插件

通过 @JSONField 我们可以自定义字段的名称进行输出，并控制字段的排序，还可以进行序列化 标记。 

指定name属性, 字段的名称 

使用 ordinal属性, 指定字段的顺序 

使用 serialize属性, 指定字段不序列化

```java
//lombok 插件完成set/get方法和toString方法
@Data
@ToString
public class Person {
        //自定义输出的名称, 并且进行输出排序
        @JSONField(name="USERNAME",ordinal = 1)
        private String username;
        @JSONField(name="AGE",ordinal = 2)
        private int age;
        //排除不需要序列化的字段
        @JSONField(serialize = false)
        private String birthday;
}
```

> JSON 字符串转换为 Java 对象

**JSON.parseObject()**

- 可以使用 JSON.parseObject() 将 JSON 字符串转换为 Java 对象。

- 注意反序列化时为对象时，必须要有默认无参的构造函数，否则会报异常

**JSON.parseArray()**

可以使用 JSON.parseArray() 将 JSON 字符串转换为 集合对象。

```java
public void JSONToJavaBean() {
        String json = "{\"age\":15,\"birthday\":\"2022-10-03 19:54:33\",\"username\":\"heda\"}";
        Person person = JSON.parseObject(json, Person.class);
        System.out.println(person);
        //创建Person对象
        String json2 = "[{\"age\":15,\"birthday\":\"2022-10-03 19:59:05\",\"username\":\"heda\"},{\"age\":13,\"birthday\":\"2022-10-03 19:59:05\",\"username\":\"zy\"}]";
        List<Person> list = JSON.parseArray(json2, Person.class);
        System.out.println(list);
}
```

## layui框架

使用流程，在layui官网下载 [Layui - 经典开源模块化前端 UI 组件库(官方开发文档)](http://layui.org.cn/index.html)

将 layui 文件放入 webapp 文件夹中

### layui框架效果

在 webapp 下新建 layui.html

在layui官网粘入框架代码并修改引入的 layui.js  和 layui.css 为自己的路径

更改两处语句 实现点击 menu 1 加载http://cn.bing.com页面

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
  <title>layout 管理系统大布局 - Layui</title>
  <link rel="stylesheet" href="./layui/css/layui.css">
</head>
<body>
<div class="layui-layout layui-layout-admin">
  <div class="layui-header">
    <div class="layui-logo layui-hide-xs layui-bg-black">layout demo</div>
    <!-- 头部区域（可配合layui 已有的水平导航） -->
    <ul class="layui-nav layui-layout-left">
      <!-- 移动端显示 -->
      <li class="layui-nav-item layui-show-xs-inline-block layui-hide-sm" lay-header-event="menuLeft">
        <i class="layui-icon layui-icon-spread-left"></i>
      </li>

      <li class="layui-nav-item layui-hide-xs"><a href="">nav 1</a></li>
      <li class="layui-nav-item layui-hide-xs"><a href="">nav 2</a></li>
      <li class="layui-nav-item layui-hide-xs"><a href="">nav 3</a></li>
      <li class="layui-nav-item">
        <a href="javascript:;">nav groups</a>
        <dl class="layui-nav-child">
          <dd><a href="">menu 11</a></dd>
          <dd><a href="">menu 22</a></dd>
          <dd><a href="">menu 33</a></dd>
        </dl>
      </li>
    </ul>
    <ul class="layui-nav layui-layout-right">
      <li class="layui-nav-item layui-hide layui-show-md-inline-block">
        <a href="javascript:;">
          <img src="//tva1.sinaimg.cn/crop.0.0.118.118.180/5db11ff4gw1e77d3nqrv8j203b03cweg.jpg" class="layui-nav-img">
          tester
        </a>
        <dl class="layui-nav-child">
          <dd><a href="">Your Profile</a></dd>
          <dd><a href="">Settings</a></dd>
          <dd><a href="">Sign out</a></dd>
        </dl>
      </li>
      <li class="layui-nav-item" lay-header-event="menuRight" lay-unselect>
        <a href="javascript:;">
          <i class="layui-icon layui-icon-more-vertical"></i>
        </a>
      </li>
    </ul>
  </div>

  <div class="layui-side layui-bg-black">
    <div class="layui-side-scroll">
      <!-- 左侧导航区域（可配合layui已有的垂直导航） -->
      <ul class="layui-nav layui-nav-tree" lay-filter="test">
        <li class="layui-nav-item layui-nav-itemed">
          <a class="" href="javascript:;">menu group 1</a>
          <dl class="layui-nav-child">
<!--            修改语句-->
            <dd><a href="http://cn.bing.com" target="fm">menu 1</a></dd>
<!--            修改语句-->
            <dd><a href="javascript:;">menu 2</a></dd>
            <dd><a href="javascript:;">menu 3</a></dd>
            <dd><a href="">the links</a></dd>
          </dl>
        </li>
        <li class="layui-nav-item">
          <a href="javascript:;">menu group 2</a>
          <dl class="layui-nav-child">
            <dd><a href="javascript:;">list 1</a></dd>
            <dd><a href="javascript:;">list 2</a></dd>
            <dd><a href="">超链接</a></dd>
          </dl>
        </li>
        <li class="layui-nav-item"><a href="javascript:;">click menu item</a></li>
        <li class="layui-nav-item"><a href="">the links</a></li>
      </ul>
    </div>
  </div>

  <div class="layui-body">
    <!-- 内容主体区域 -->
    <div style="padding: 15px;">内容主体区域。记得修改 layui.css 和 js 的路径</div>
<!--    添加语句-->
    <iframe name="fm" src="" frameborder="0" style="width: 100%;height: 100%"></iframe>
<!--    添加语句-->
  </div>

  <div class="layui-footer">
    <!-- 底部固定区域 -->
    底部固定区域
  </div>
</div>
<script src="./layui/layui.js"></script>
<script>
  //JS
  layui.use(['element', 'layer', 'util'], function(){
    var element = layui.element
            ,layer = layui.layer
            ,util = layui.util
            ,$ = layui.$;

    //头部事件
    util.event('lay-header-event', {
      //左侧菜单事件
      menuLeft: function(othis){
        layer.msg('展开左侧菜单的操作', {icon: 0});
      }
      ,menuRight: function(){
        layer.open({
          type: 1
          ,content: '<div style="padding: 15px;">处理右侧面板的操作</div>'
          ,area: ['260px', '100%']
          ,offset: 'rt' //右上角
          ,anim: 5
          ,shadeClose: true
        });
      }
    });

  });
</script>
</body>
</html>
```

###  表格效果

**前置准备**

导入sql 数据

```sql
-- 删除tb_brand表
drop table if exists tb_brand;
-- 创建tb_brand表
create table tb_brand (
    -- id 主键
                          id  int primary key auto_increment,
    -- 品牌名称
                          brandName   varchar(20),
    -- 企业名称
                          companyName varchar(20),
    -- 排序字段
                          ordered      int,
    -- 描述信息
                          description  varchar(100),
    -- 状态：0：禁用  1：启用
                          status       int
);
-- 添加数据
insert into tb_brand (brandName, companyName, ordered, description, status)
values
    ('华为', '华为技术有限公司', 100, '万物互联', 1),
    ('小米', '小米科技有限公司', 50, 'are you ok', 1),
    ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
    ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
    ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
    ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
    ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
    ('小米', '小米科技有限公司', 50, 'are you ok', 1),
    ('三只松鼠', '三只松鼠股份有限公司', 5, '好吃不上火', 0),
    ('华为', '华为技术有限公司', 100, '万物互联', 1),
    ('小米', '小米科技有限公司', 50, 'are you ok', 1),
    ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
    ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
    ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
    ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
    ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
    ('华为', '华为技术有限公司', 100, '万物互联', 1),
    ('小米', '小米科技有限公司', 50, 'are you ok', 1),
    ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
    ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
    ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
    ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
    ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
    ('小米', '小米科技有限公司', 50, 'are you ok', 1),
    ('三只松鼠', '三只松鼠股份有限公司', 5, '好吃不上火', 0),
    ('华为', '华为技术有限公司', 100, '万物互联', 1),
    ('小米', '小米科技有限公司', 50, 'are you ok', 1),
    ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
    ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
    ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
    ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
    ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
    ('华为', '华为技术有限公司', 100, '万物互联', 1),
    ('小米', '小米科技有限公司', 50, 'are you ok', 1),
    ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
    ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
    ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
    ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
    ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
    ('小米', '小米科技有限公司', 50, 'are you ok', 1),
    ('三只松鼠', '三只松鼠股份有限公司', 5, '好吃不上火', 0),
    ('华为', '华为技术有限公司', 100, '万物互联', 1),
    ('小米', '小米科技有限公司', 50, 'are you ok', 1),
    ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
    ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
    ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
    ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
    ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1);
```

在layui官网下载 layui包，并复制layui文件夹到项目webapp下

pom文件 增加依赖

```XML
<dependency>
   <groupId>mysql</groupId>
   <artifactId>mysql-connector-java</artifactId>
   <version>5.1.38</version>
</dependency>
<dependency>
   <groupId>commons-beanutils</groupId>
   <artifactId>commons-beanutils</artifactId>
   <version>1.9.4</version></dependency>
</dependency>
<dependency>
   <groupId>com.alibaba</groupId>
   <artifactId>druid</artifactId>
   <version>1.2.8</version>
</dependency>
```

在 webapp 下新建文件 table.html

在layui官网粘入数据表格代码并修改引入的 layui.js  和 layui.css 为自己的路径

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Layui</title>
  <meta name="renderer" content="webkit">
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
  <link rel="stylesheet" href="./layui/css/layui.css"    media="all">
  <!-- 注意：如果你直接复制所有代码到本地，上述css路径需要改成你本地的 -->
</head>
<body>
           
<table class="layui-hide" id="test"></table>
              
          
<script src="./layui/layui.js" charset="utf-8"></script>
<!-- 注意：如果你直接复制所有代码到本地，上述 JS 路径需要改成你本地的 -->
 
<script>
layui.use('table', function(){
  var table = layui.table;
  
  table.render({
    elem: '#test'
    ,url: '../demo/table/user/-page=1&limit=20.js'
    ,cellMinWidth: 80 //全局定义常规单元格的最小宽度，layui 2.2.1 新增
    ,cols: [[
      {field:'id', width:80, title: 'ID', sort: true}
      ,{field:'username', width:80, title: '用户名'}
      ,{field:'sex', width:80, title: '性别', sort: true}
      ,{field:'city', width:80, title: '城市'}
      ,{field:'sign', title: '签名', width: '30%', minWidth: 100} //minWidth：局部定义当前单元格的最小宽度，layui 2.2.1 新增
      ,{field:'experience', title: '积分', sort: true}
      ,{field:'score', title: '评分', sort: true}
      ,{field:'classify', title: '职业'}
      ,{field:'wealth', width:137, title: '财富', sort: true}
    ]]
  });
});
</script>

</body>
</html>
```

**实现**

> 编写后端查询代码

在 pojo 下新建文件 Brand.java

````java
@Data
@ToString
public class Brand {
    private int id;
    private String brandName;
    private String companyName;
    private int ordered;
    private String description;
    private int status;
}
````

在 dao 下新建文件 BrandDao.java

```java
public interface BrandDao {
    List<Brand> queryDate() throws SQLException;
}
```

在 dao 下新建文件 BrandImpl.java

```java
public class BrandImpl implements BrandDao {
    @Override
    public List<Brand> queryDate() throws SQLException {
        QueryRunner qr = new QueryRunner(DruidUtils.getDataSource());
        String sql = "select * from tb_brand;";
        List<Brand> query = qr.query(sql, new BeanListHandler<>(Brand.class));
        return query;
    }
}
```

> 拉取数据转化成JSON格式

在 pojo下新建文件 ResultBrean.java

```java
@Data
@ToString
@NoArgsConstructor//空参构造
@AllArgsConstructor//全参构造
public class ResultBrean<T> {
    //编写成JSON模板格式
    private int code;
    private String msg;
    private int count;
    private List<Brand> data;
}
```

在 controller下新建文件 JsonBrand.java

```java
@WebServlet("/static")
public class JsonBrand extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        List<Brand> brands =null;
        try {
            brands = new BrandImpl().queryDate();
            System.out.println(brands);
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }

        ResultBrean<Object> rb = new ResultBrean<>();
        rb.setCode(0);
        rb.setMsg("");
        rb.setCount(50);
        rb.setData(brands);

        String str = JSON.toJSONString(rb);

        System.out.println(str);
        resp.setContentType("test/html;charset = utf-8");

        resp.getWriter().println(str);
    }
}
```

> 收到数据前端获取

更改 table.html

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Layui</title>
  <meta name="renderer" content="webkit">
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
  <link rel="stylesheet" href="./layui/css/layui.css" tppabs="http://res.layui.com/layui/dist/css/layui.css"  media="all">
  <!-- 注意：如果你直接复制所有代码到本地，上述css路径需要改成你本地的 -->
</head>
<body>

<table class="layui-hide" id="test"></table>


<script src="./layui/layui.js" charset="utf-8"></script>
<!-- 注意：如果你直接复制所有代码到本地，上述 JS 路径需要改成你本地的 -->

<script>
  layui.use('table', function(){
    var table = layui.table;

    table.render({
      elem: '#test'
      ,url: '../demo1/static'
      ,cellMinWidth: 80 //全局定义常规单元格的最小宽度，layui 2.2.1 新增
      ,cols: [[
        {field:'id', width:80, title: 'ID', sort: true}
        ,{field:'brandName', width:80, title: '品牌名'}
        ,{field:'companyName', width:200, title: '公司名', sort: true}
        ,{field:'ordered', width:80, title: '排序'}
        ,{field:'description', title: '描述信息', width: '30%', minWidth: 100} //minWidth：局部定义当前单元格的最小宽度，layui 2.2.1 新增
        ,{field:'status', title: '状态', sort: true}
      ]]
    });
  });
</script>

</body>
</html>
```

### 分页

在表格效果中更改

table.html

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Layui</title>
  <meta name="renderer" content="webkit">
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
  <link rel="stylesheet" href="./layui/css/layui.css" tppabs="http://res.layui.com/layui/dist/css/layui.css"  media="all">
  <!-- 注意：如果你直接复制所有代码到本地，上述css路径需要改成你本地的 -->
</head>
<body>

<table class="layui-hide" id="test"></table>


<script src="./layui/layui.js" charset="utf-8"></script>
<!-- 注意：如果你直接复制所有代码到本地，上述 JS 路径需要改成你本地的 -->

<script>
  layui.use('table', function(){
    var table = layui.table;

    table.render({
      elem: '#test'
      ,url: '../demo1/static'
      ,cellMinWidth: 80 //全局定义常规单元格的最小宽度，layui 2.2.1 新增
      ,cols: [[
        {field:'id', width:80, title: 'ID', sort: true}
        ,{field:'brandName', width:80, title: '品牌名'}
        ,{field:'companyName', width:200, title: '公司名', sort: true}
        ,{field:'ordered', width:80, title: '排序'}
        ,{field:'description', title: '描述信息', width: '30%', minWidth: 100} //minWidth：局部定义当前单元格的最小宽度，layui 2.2.1 新增
        ,{field:'status', title: '状态', sort: true}
      ]]
      ,page: true//开启分页
    });
  });
</script>

</body>
</html>
```

JsonBrand.java

```java
@WebServlet("/static")
public class JsonBrand extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //接受前端传过来得分页参数
        Integer page = Integer.valueOf(req.getParameter("page"));
        Integer limit = Integer.valueOf(req.getParameter("limit"));

        List<Brand> brands =null;
        try {
            //计算分页 开始索引 = （当前页码 -  1）*  每页显示条数
            brands = new BrandImpl().queryDate((page-1)*10,limit);
            System.out.println(brands);
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }

        ResultBrean rb = new ResultBrean();
        rb.setCode(0);
        rb.setMsg("");
        rb.setCount(50);
        rb.setData(brands);

        String str = JSON.toJSONString(rb);

        System.out.println(str);
        resp.setContentType("test/html;charset = utf-8");

        resp.getWriter().println(str);
    }
}
```

BrandDao.java

```java
public interface BrandDao {
    List<Brand> queryDate(Integer page, Integer limit) throws SQLException;
}
```

BrandImpl.java

```java
public class BrandImpl implements BrandDao {
    @Override
    public List<Brand> queryDate(Integer page,Integer limit) throws SQLException {
        QueryRunner qr = new QueryRunner(DruidUtils.getDataSource());
        String sql = "select * from tb_brand limit ?,?;";
        List<Brand> query = qr.query(sql, new BeanListHandler<>(Brand.class),page,limit);
        return query;
    }
}
```

