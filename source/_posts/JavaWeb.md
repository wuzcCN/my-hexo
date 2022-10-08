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

- web，网页的意思 ， www.baidu.com
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
