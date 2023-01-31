---
title: SpringMVC
copyright_url: https://www.aobayu.cn/2022/11/23/SpringMVC/
tags: 
    - SpringMVC
categories: 学习之路
date: 2022-11-23
keywords: SpringMVC
description: SpringMVC 是一种基于 Java 的实现 MVC 设计模式的轻量级 Web 框架，它通过一套注解，让一个简单的 Java 类成为处理请求的控制器，而无须实现任何接口。同时它还支持 RESTful 编程风格的请求。--本文为自己学习中所写。
---

## SpringMVC

**MVC模式**

MVC是软件工程中的一种软件架构模式，它是一种分离业务逻辑与显示界面的开发思想。

M（model）模型：处理业务逻辑，封装实体 

V（view） 视图：展示内容 

C（controller）控制器：负责调度分发（1.接收请求、2.调用模型、3.转发到视图） 

**SpringMVC概述**

SpringMVC 是一种基于 Java 的实现 MVC 设计模式的轻量级 Web 框架，属于SpringFrameWork 的 后续产品，已经融合在 Spring Web Flow 中。

SpringMVC 已经成为目前最主流的MVC框架之一，并且随着Spring3.0 的发布，全面超越 Struts2， 成为最优秀的 MVC 框架。它通过一套注解，让一个简单的 Java 类成为处理请求的控制器，而无须实现任何接口。同时它还支持 RESTful 编程风格的请求。

SpringMVC的框架就是封装了原来Servlet中的共有行为；例如：参数封装，视图转发等。

## SpringMVC快速入门

需求 客户端发起请求，服务器接收请求，执行逻辑并进行视图跳转。

步骤分析：

1. 创建web项目，导入SpringMVC相关坐标 

2. 配置SpringMVC前端控制器 DispathcerServlet 

3. 编写Controller类和视图页面 
4. 配置SpringMVC核心文件 spring-mvc.xml 

> 创建web项目，导入SpringMVC相关坐标

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.aaa</groupId>
    <artifactId>SpringMvc</artifactId>
    <version>1.0-SNAPSHOT</version>
    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    <!-- 设置为web工程 -->
    <packaging>war</packaging>
    <dependencies>
        <!--springMVC坐标-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
        <!--servlet坐标-->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.1.0</version>
            <scope>provided</scope>
        </dependency>
        <!--jsp坐标-->
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>jsp-api</artifactId>
            <version>2.2</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
</project>
```

> 配置SpringMVC前端控制器DispathcerServlet  web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--前端控制器-->
    <servlet>
        <servlet-name>dispatcherServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:spring-mvc.xml</param-value>
        </init-param>
        <load-on-startup>2</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>dispatcherServlet</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>
```

> 编写Controller类和视图页面 com.aaa.controller.

```java
@Controller
public class UserController {
    @RequestMapping("/quick")
    public String quick() {
        System.out.println("quick running.....");
        return "/WEB-INF/pages/success.jsp";
    }
}
```

webapp/WEB-INF/pages/ success.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>success</title>
</head>
<body>
    <h3>请求成功！</h3>
</body>
</html>
```

> 配置SpringMVC核心文件spring-mvc.xml

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans.xsd
http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context.xsd">
    <!--配置注解扫描-->
    <context:component-scan base-package="com.aaa.controller"/>
</beans>
```

> 访问web项目

如果报错：Cannot access defaults field of Properties

在pom文件中配置

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-war-plugin</artifactId>
            <version>3.3.1</version>
        </plugin>
    </plugins>
</build>
```

## SpringMVC组件概述

**SpringMVC的执行流程**

1. 用户发送请求至前端控制器DispatcherServlet。

2. DispatcherServlet收到请求调用HandlerMapping处理器映射器。 

3. 处理器映射器找到具体的处理器(可以根据xml配置、注解进行查找)，生成处理器对象及处理器拦截器(如果有则生成)一并返回给DispatcherServlet。 

4. DispatcherServlet调用HandlerAdapter处理器适配器。

5. HandlerAdapter经过适配调用具体的处理器(Controller，也叫后端控制器)。 

6. Controller执行完成返回ModelAndView。 

7. HandlerAdapter将controller执行结果ModelAndView返回给DispatcherServlet。 

8. DispatcherServlet将ModelAndView传给ViewReslover视图解析器。 

9. ViewReslover解析后返回具体View。 

10. DispatcherServlet根据View进行渲染视图（即将模型数据填充至视图中）。 

11. DispatcherServlet将渲染后的视图响应响应用户。

**SpringMVC组件解析**

1. 前端控制器：DispatcherServlet 

   用户请求到达前端控制器，它就相当于 MVC 模式中的 C，DispatcherServlet 是整个流程控制的 中心，由它调用其它组件处理用户的请求，DispatcherServlet 的存在降低了组件之间的耦合性。 

2. 处理器映射器：HandlerMapping 

   HandlerMapping 负责根据用户请求找到 Handler 即处理器，SpringMVC 提供了不同的映射器 实现不同的映射方式，例如：配置文件方式，实现接口方式，注解方式等。 

3. 处理器适配器：HandlerAdapter 

   通过 HandlerAdapter 对处理器进行执行，这是适配器模式的应用，通过扩展适配器可以对更多类型的处理器进行执行。 

4. 处理器：Handler【**开发者编写**】

   它就是我们开发中要编写的具体业务控制器。由 DispatcherServlet 把用户请求转发到 Handler。由Handler 对具体的用户请求进行处理。 

5. 视图解析器：ViewResolver 

   View Resolver 负责将处理结果生成 View 视图，View Resolver 首先根据逻辑视图名解析成物理视图名，即具体的页面地址，再生成 View 视图对象，最后对 View 进行渲染将处理结果通过页面展示给 用户。 

6. 视图：View 【**开发者编写**】 

   SpringMVC 框架提供了很多的 View 视图类型的支持，包括：jstlView、freemarkerView、 pdfView等。最常用的视图就是 jsp。一般情况下需要通过页面标签或页面模版技术将模型数据通过页面展 示给用户，需要由程序员根据业务需求开发具体的页面。 

> 在controller中的返回值 ，只需要写上success就可以访问

> spring-mvc.xml

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans.xsd
http://www.springframework.org/schema/mvc
http://www.springframework.org/schema/mvc/spring-mvc.xsd
http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context.xsd">
    <!--配置注解扫描-->
    <context:component-scan base-package="com.aaa.controller"/>
    <!--处理器映射器和处理器适配器功能增强-->
    <mvc:annotation-driven></mvc:annotation-driven>
    <!--视图解析器-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/pages/"></property>
        <property name="suffix" value=".jsp"></property>
    </bean>
</beans>
```

> Controller类

```java
@Controller
public class UserController {
    @RequestMapping("/quick")
    public String quick() {
        System.out.println("quick running.....");
        return "success";
    }
}
```

**SpringMVC注解解析**

SpringMVC基于Spring容器，所以在进行SpringMVC操作时，需要将Controller存储到Spring容器 中，如果使用@Controller注解标注的话，就需要使用：

```xml
<!--配置注解扫描-->
<context:component-scan base-package="com.aaa.controller"/>
```

```java
@Controller
@RequestMapping("/user") //一级访问目录
public class UserController {
    /*
        /一级访问目录/二级访问目录
        http://localhost:8080/springmvc_war/user/quick    
        path : 或者写value 都可以,同样是设置方法的映射地址
        method：用来限定请求的方式 RequestMethod.POST:
        只能以post的请求方式访问该访问，其他请求方式会报错
        params：用来限定请求参数的条件 
        params={"accountName"} 表示请求参数中必须有accountName
     */
    @RequestMapping(path = "/quick",method = RequestMethod.GET,params = {"accountName"})
    public String quick() {
        System.out.println("quick running.....");
        return "success";
    }
}
```

@RequestMapping 作用：用于建立请求 URL 和处理请求方法之间的对应关系

位置：

- 类上：请求URL的第一级访问目录。此处不写的话，就相当于应用的根目录。写的话需要以/开头。它出现的目的是为了使我们的URL可以按照模块化管理:
  - 用户模块
    - /user/add
    - /user/update
    - /user/delete
  - 账户模块
    - /account/add
    - /account/update
    - /account/delete
- 方法上：请求URL的第二级访问目录，和一级目录组成一个完整的 URL 路径。
  - 属性：
    - value：用于指定请求的URL。它和path属性的作用是一样的
    - method：用来限定请求的方式
    - params：用来限定请求参数的条件

例如：params={"accountName"} 表示请求参数中必须有accountName

params={"money!=100"} 表示请求参数中money不能是100

## SpringMVC的请求

**请求参数类型介绍**

客户端请求参数的格式是： name=value&name=value……

服务器要获取请求的参数的时候要进行类型转换，有时还需要进行数据的封装

SpringMVC可以接收如下类型的参数：

- 基本类型参数

- 对象类型参数 

- 数组类型参数  

- 集合类型参数

### 获取基本类型参数

Controller中的业务方法的参数名称要与请求参数的name一致，参数值会自动映射匹配。并且能自动做类型转换；自动的类型转换是指从String向其他类型的转换。

> 创建文件 requestParam.jsp

> 注：创建在 WEB-INF 下，这里是安全目录 只可以通过controller转发访问，不可以直接访问

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<%--${pageContext.request.contextPath}动态的来获取当前的项目路径 springmvc_war  a标签的请求方式：get请求--%>
<a href="${pageContext.request.contextPath}/user/simpleParam?id=1&username=fyh">
    基本类型
</a>
</body>
</html>
```

> 在controller 中，写上接口

> 注意：参数名字和请求一样

```java
public interface UserControllerDao {
	@RequestMapping("/simpleParam")
    public String simpleParam(Integer id,String username) {
        System.out.println(id);
        System.out.println(username);
        return "requestParam";
    }
}
```

### 获取对象类型参数

Controller中的业务方法参数的POJO属性名与请求参数的name一致，参数值会自动映射匹配。

```jsp
	<form action="${pageContext.request.contextPath}/user/pojoParam" method="post">
        编号：<input type="text" name="id"> <br>
        用户名：<input type="text" name="username"> <br>
        <input type="submit" value="对象类型">
    </form>
```

```java
public class User {
    private int id;
    private String username;

    @Override
    public String 
    toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                '}';
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }
}
```

```java
	@RequestMapping("/pojoParam")
    public String pojoParam(User user) {
        System.out.println(user);
        return "requestParam";
    }
```

### 中文乱码过滤器

当post请求时，数据会出现乱码，我们可以设置一个过滤器来进行编码的过滤，web.xml中加上过滤器的配置

```xml
<!--配置全局过滤的filter-->
    <filter>
        <filter-name>CharacterEncodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>CharacterEncodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
```

### 获取数组类型参数

Controller中的业务方法数组名称与请求参数的name一致，参数值会自动映射匹配。

```java
	@RequestMapping("/arrayParam")
    public String arrayParam(Integer[] ids) {
        System.out.println(Arrays.toString(ids));
        return "requestParam";
    }
```

```jsp
	<form action="${pageContext.request.contextPath}/user/arrayParam">
        编号：<br>
        <input type="checkbox" name="ids" value="1">1<br>
        <input type="checkbox" name="ids" value="2">2<br>
        <input type="checkbox" name="ids" value="3">3<br>
        <input type="checkbox" name="ids" value="4">4<br>
        <input type="checkbox" name="ids" value="5">5<br>
        <input type="submit" value="数组类型">
    </form>
```

### 获取集合（复杂）类型参数

获得集合参数时，要将集合参数包装到一个POJO中才可以。

```jsp
	<form action="${pageContext.request.contextPath}/user/queryParam" method="post">
        搜索关键字：<input type="text" name="keyword"> <br>
        user对象：
        <input type="text" name="user.id" placeholder="编号">
        <input type="text" name="user.username" placeholder="姓名"><br>
        list集合<br>
        第一个元素：
        <input type="text" name="userList[0].id" placeholder="编号">
        <input type="text" name="userList[0].username" placeholder="姓名"><br>
        第二个元素：
        <input type="text" name="userList[1].id" placeholder="编号">
        <input type="text" name="userList[1].username" placeholder="姓名"><br>
        map集合<br>
        第一个元素：
        <input type="text" name="userMap['u1'].id" placeholder="编号">
        <input type="text" name="userMap['u1'].username" placeholder="姓名"><br>
        第二个元素：
        <input type="text" name="userMap['u2'].id" placeholder="编号">
        <input type="text" name="userMap['u2'].username" placeholder="姓名"><br>
        <input type="submit" value="复杂类型">
    </form>
```

```java
public class QueryVo {
    private String keyword;
    private User user;
    private List<User> userList;
    private Map<String, User> userMap;
   	//get/set toString
}
```

```java
	@RequestMapping("/queryParam")
    public String queryParam(QueryVo queryVo) {
        System.out.println(queryVo);
        return "requestParam";
    }
```

### 自定义类型转换器

SpringMVC 默认已经提供了一些常用的类型转换器；例如：客户端提交的字符串转换成int型进行参数设置，日期格式类型要求为：yyyy/MM/dd 不然的话会报错，对于特有的行为，SpringMVC提供了自定义类型转换器方便开发者自定义处理。

```jsp
	<form action="${pageContext.request.contextPath}/user/converterParam">
        生日：<input type="text" name="birthday">
        <input type="submit" value="自定义类型转换器">
    </form>
```

```java
public class DateConverter implements Converter<String , Date> {

    @Override
    public Date convert(String dateStr) {
        //将日期字符串转换成日期对象返回
        SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd");
        Date date = null;
        try {
            date = format.parse(dateStr);
        } catch (ParseException e) {
            e.printStackTrace();
        }
        return date;
    }
}
```

> 在spring-mvc.xml中配置

```xml
<!--处理器映射器和适配器增强-->
    <mvc:annotation-driven conversion-service="conversionService"></mvc:annotation-driven>
    <!--自定义转换器配置-->
    <bean id="conversionService"
          class="org.springframework.context.support.ConversionServiceFactoryBean">
        <property name="converters">
            <set>
                <bean class="com.aaa.converter.DateConverter"></bean>
            </set>
        </property>
    </bean>
```

```java
	@RequestMapping("/converterParam")
    public String converterParam(Date birthday) {
        System.out.println(birthday);
        return "requestParam";
    }
```

### 相关注解

当请求的参数name名称与Controller的业务方法参数名称不一致时,就需要通过@RequestParam注解显示的绑定

```xml
<a href="${pageContext.request.contextPath}/user/findByPage?pageNo=2">分页查询</a>
```

```java
	/* @RequestParam() 注解
    defaultValue 设置参数默认值
    name 匹配页面传递参数的名称
    required 设置是否必须传递参数，默认值为true；如果设置了默认值，值自动改为false*/
    @RequestMapping("/findByPage")
    public String findByPage(@RequestParam(name = "pageNo", defaultValue = "1")Integer pageNum, @RequestParam(defaultValue = "5") Integer pageSize) {
        System.out.println(pageNum);
        System.out.println(pageSize);
        return "requestParam";
    }
```

> @RequestHeader 获取请求头的数据

```java
	@RequestMapping("/requestHead")
    public String requestHead(@RequestHeader("cookie") String cookie) {
        System.out.println(cookie);
        return "requestParam";
    }
```

> @CookieValue 获取cookie中的数据

```java
	@RequestMapping("/cookieValue")
    public String cookieValue(@CookieValue("JSESSIONID") String jesessionId) {
        System.out.println(jesessionId);
        return "requestParam";
    }
```

### 获取Servlet相关API

SpringMVC支持使用原始ServletAPI对象作为控制器方法的参数进行注入，常用的对象

```java
@RequestMapping("/servletAPI")
    public String servletAPI(HttpServletRequest request, HttpServletResponse response, HttpSession session) {
        System.out.println(request);
        System.out.println(response);
        System.out.println(session);
        return "requestParam";
    }
```

## SpringMVC的响应

### 返回字符串逻辑视图

直接返回字符串：此种方式会将返回的字符串与视图解析器的前后缀拼接后跳转到指定页面

```java
	@RequestMapping("/returnString")
    public String returnString(){
        return "requestParam";
    }
```

### 原始ServletAPI

我们可以通过request、response对象实现响应

```java
@RequestMapping("/returnString")
    public void returnString(HttpServletResponse response) throws IOException {
        //通过response直接响应数据
        response.setContentType("text/html;charset=utf-8");
        response.getWriter().write("xiao");
    }
```

```java
@RequestMapping("/returnVoid")
    public void returnVoid(HttpServletRequest request, HttpServletResponse response)
            throws Exception {
    //通过request实现转发
    request.getRequestDispatcher("/WEB-INF/pages/success.jsp").forward(request,response);
    }
```

```java
@RequestMapping("/returnVoid")
    public void returnVoid(HttpServletRequest request, HttpServletResponse response)
            throws Exception {
	//通过response实现重定向
    response.sendRedirect(request.getContextPath() + "/index.jsp");
    }
```

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <h3>Hello ......</h3>
</body>
</html>
```

### 转发和重定向

企业开发我们一般使用返回字符串逻辑视图实现页面的跳转，这种方式其实就是请求转发。

> 我们也可以写成，forward转发，如果用了forward，则路径必须写成实际视图url，不能写逻辑视图，相当于

```java
request.getRequestDispatcher("url").forward(request,response)
```

使用请求转发，既可以转发到jsp，也可以转发到其他的控制器方法。

```java
	@RequestMapping("/forward")
    public String forward() {
        System.out.println("forward...");
        return "forward:/WEB-INF/pages/success.jsp";
    }
```

> Redirect重定向

我们可以不写虚拟目录，springMVC框架会自动拼接，并且将Model中的数据拼接到url地址上

```java
	@RequestMapping("/redirect")
    public String redirect() {
        System.out.println("redirect...");
        return "redirect:/index.jsp";
    }
```

> 跳转页面时 携带数据

```java

```

> 在 success.jsp 页面中 加入

```jsp
<h3>请求成功！ ${username}</h3>
```

### ModelAndView

> 方式一：在Controller中方法创建并返回ModelAndView对象，并且设置视图名称

```java
@RequestMapping("/returnModelAndView1")
    public ModelAndView returnModelAndView1() {
      /*
      Model:模型 作用封装数据
      View：视图 作用展示数据
      */
        ModelAndView modelAndView = new ModelAndView();
        //设置模型数据
        modelAndView.addObject("username", "fyh");
        //设置视图名称
        modelAndView.setViewName("success");
        return modelAndView;
    }
```

> 方式二：在Controller中方法形参上直接声明ModelAndView，无需在方法中自己创建，在方法中直接使用该对象设置视图，同样可以跳转页面

```java
	@RequestMapping("/returnModelAndView2")
    public ModelAndView returnModelAndView2(ModelAndView modelAndView) {
        //设置模型数据
        modelAndView.addObject("username", "fly");
        //设置视图名称
        modelAndView.setViewName("success");
        return modelAndView;
    }
```

### @SessionAttributes

如果在多个请求之间共用数据，则可以在控制器类上标注一个 @SessionAttributes,配置需要在 session中存放的数据范围，Spring MVC将存放在model中对应的数据暂存到 HttpSession 中。

> 注意：@SessionAttributes只能定义在类上

```java
@Controller
@SessionAttributes("username") //向request域存入的key为username时，同步到session域中
@RequestMapping("/user")
public class UserController {	
		@RequestMapping("/forward1")
        public String forward1(Model model) {
            model.addAttribute("username", "fly");
            return "forward:/WEB-INF/pages/success.jsp";
        }
}
```

### 静态资源访问的开启

当有静态资源需要加载时，比如jquery文件，通过谷歌开发者工具抓包发现，没有加载到jquery文 件，原因是SpringMVC的前端控制器DispatcherServlet的url-pattern配置的是 /（缺省）,代表对所有的 静态资源都进行处理操作，这样就不会执行Tomcat内置的DefaultServlet处理，我们可以通过以下两种 方式指定放行静态资源

> 在requestParam.jsp 中添加对jquery的引用

```jsp
<%--引入jquery.js--%>
<script src="${pageContext.request.contextPath}/js/jquery-3.6.1.js"/>
```

> 方式一

```xml
<!--在springmvc配置文件中指定放行资源-->
<mvc:resources mapping="/js/**" location="/js/"/>
<mvc:resources mapping="/css/**" location="/css/"/>
<mvc:resources mapping="/img/**" location="/img/"/>
```

> 方式二

```xml
<!--在springmvc配置文件中开启DefaultServlet处理静态资源-->
<mvc:default-servlet-handler/>
```

## ajax异步交互

Springmvc默认用MappingJackson2HttpMessageConverter对json数据进行转换，需要加入jackson的包；同时使用 <mvc:annotation-driven />

```xml
		<dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.9.8</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-core</artifactId>
            <version>2.9.8</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-annotations</artifactId>
            <version>2.9.0</version>
        </dependency>
```

### @RequestBody

该注解用于Controller的方法的形参声明，当使用ajax提交并指定contentType为json形式时，通过HttpMessageConverter接口转换为对应的POJO对象。

> 新建ajax.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
  <script src="${pageContext.request.contextPath}/js/jquery-3.6.1.js"></script>
</head>
<body>

  <button id="btn1">ajax异步提交</button>
  <script>
    $("#btn1").click(function () {
      let url = '${pageContext.request.contextPath}/ajaxRequest';
      let data = '[{"id":1,"username":"张三"},{"id":2,"username":"李四"}]';
      $.ajax({
        type: 'POST',//请求方式
        url: url,//请求后端的URL地址
        data: data,//我要携带的数据
        contentType: 'application/json;charset=utf-8',//请求数据类型 json
        success: function (resp) {
          alert(JSON.stringify(resp))//后端返回数据
        }
      })
    })
  </script>

</body>
</html>
```

> 新建AjaxController,注意给类加controller注解

```java
@Controller
public class AjaxController {
    @RequestMapping(value = "/ajaxRequest")
    public void ajaxRequest(@RequestBody List<User> list) {
        System.out.println(list);
    }
}
```

### @ResponseBody

该注解用于将Controller的方法返回的对象，通过HttpMessageConverter接口转换为指定格式的数据如：json,xml等，通过Response响应给客户端。

```java
@Controller
public class AjaxController {
    /*@RequestMapping
    produces = "application/json;charset=utf-8" 
    响应返回数据的mime类型和编码，默认为json*/
    @RequestMapping(value = "/ajaxRequest")
    @ResponseBody
    public List<User> ajaxRequest(@RequestBody List<User> list) {
        System.out.println(list);
        return list;
    }
}
```

## RESTful

**什么是RESTful**

Restful是一种软件架构风格、设计风格，而不是标准，只是提供了一组设计原则和约束条件。主要用于客户端和服务器交互类的软件，基于这个风格设计的软件可以更简洁，更有层次，更易于实现缓存机制等。

Restful风格的请求是使用“url+请求方式”表示一次请求目的的，HTTP 协议里面四个表示操作方式的动词如下：

- GET：读取（Read）

- POST：新建（Create）

- PUT：更新（Update）

- DELETE：删除（Delete）

| 客户端请求 | 原来风格URL地址     | RESTful风格URL地址 |
| ---------- | ------------------- | ------------------ |
| 查询所有   | /user/findAll       | GET /user          |
| 根据ID查询 | /user/findById?id=1 | GET /user/{1}      |
| 新增       | /user/save          | POST /user         |
| 修改       | /user/update        | PUT /user          |
| 删除       | /user/delete?id=1   | DELETE /user/{1}   |

### 代码实现

**@PathVariable**

用来接收RESTful风格请求地址中占位符的值

**@RestController**

RESTful风格多用于前后端分离项目开发，前端通过ajax与服务器进行异步交互，我们处理器通常返回的是json数据所以使用@RestController来替代@Controller和@ResponseBody两个注解。

```java
@RestController//替代@Controller和@ResponseBody
//@Controller
public class RestFulController {
    @GetMapping(value = "/user/{id}")
    //相当于 @RequestMapping(value = "/user/{id}",method = RequestMethod.GET)
    //@ResponseBody 返回数据
    public String get(@PathVariable Integer id) {
        System.out.println("get：" + id);
        return "get:" + id;
    }
    @PostMapping(value = "/user")
    public String post() {
        return "post";
    }
    @PutMapping(value = "/user")
    public String put() {
        return "put";
    }
    @DeleteMapping(value = "/user/{id}")
    public String delete(@PathVariable Integer id) {
        return "delete："+ id;
    }
}
```

> @RequestParam用于接收url地址传参或表单传参
>
> @RequestBody用于接收json数据
>
> @PathVariable用于接收路径参数，使用{参数名称}描述路径参数

> 使用 postman 软件对接口进行测试

## 文件上传

**文件上传三要素**

- 表单项 type="file"

- 表单的提交方式 method="POST"

- 表单的enctype属性是多部分表单形式 enctype=“multipart/form-data"

**文件上传原理**

1. 当form表单修改为多部分表单时，request.getParameter()将失效

2. 当form表单的enctype取值为 application/x-www-form-urlencoded 时，form表单的正文内容格式是name=value&name=value

3. 当form表单的enctype取值为 mutilpart/form-data 时，请求正文内容就变成多部分形式

### 单文件上传

> 导入fileupload和io坐标

```xml
		<dependency>
            <groupId>commons-fileupload</groupId>
            <artifactId>commons-fileupload</artifactId>
            <version>1.3.3</version>
        </dependency>
        <dependency>
            <groupId>commons-io</groupId>
            <artifactId>commons-io</artifactId>
            <version>2.6</version>
        </dependency>
```

> 配置文件上传解析器

```xml
	<!--文件上传解析器-->
    <bean id="multipartResolver"
          class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
        <!-- 设定文件上传的最大值为5MB，5*1024*1024 -->
        <property name="maxUploadSize" value="5242880"></property>
        <!-- 设定文件上传时写入内存的最大值，如果小于这个参数不会生成临时文件，默认为10240 -->
        <property name="maxInMemorySize" value="40960"></property>
    </bean>
```

> 编写文件上传代码

新建fileupload.jsp页面

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <form action="${pageContext.request.contextPath}/fileUpload" method="post" enctype="multipart/form-data">
        名称：<input type="text" name="username"> <br>
        文件：<input type="file" name="filePic"> <br>
        <input type="submit" value="单文件上传">
    </form>
</body>
</html>
```

新建  FileUploadController

```java
@Controller
public class FileUploadController {
    @RequestMapping("/fileUpload")
    public String fileUpload(String username, MultipartFile filePic) throws IOException {
        //上传文件后端需要用MultipartFile接受
        System.out.println(username);
        // 获取文件名
        String originalFilename = filePic.getOriginalFilename();
        //保存文件
        filePic.transferTo(new File("E:/aaa/"+originalFilename));
        //跳转到成功页面
        return "success";
    }
}
```

### 多文件上传

> 修改上传文件 为多文件

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
	<form action="${pageContext.request.contextPath}/filesUploads" method="post" enctype="multipart/form-data">
        名称：<input type="text" name="username"> <br>
        文件1：<input type="file" name="filePic"> <br>
        文件2：<input type="file" name="filePic"> <br>
        <input type="submit" value="多文件上传">
    </form>
</body>
</html>
```

```java
	@RequestMapping("/filesUploads")
    public String filesUpload(String username, MultipartFile[] filePic) throws IOException {
        System.out.println(username);
        for (MultipartFile multipartFile : filePic) {
            // 获取文件名
            String originalFilename = multipartFile.getOriginalFilename();
            // 保存到服务器
            multipartFile.transferTo(new File("E:/aaa/" + originalFilename));
        }
        return "success";
    }
```

## 异常处理

**异常处理的思路**

在Java中，对于异常的处理一般有两种方式:

一种是当前方法捕获处理（try-catch），这种处理方式会造成业务代码和异常处理代码的耦合。

另一种是自己不处理，而是抛给调用者处理（throws），调用者再抛给它的调用者，也就是一直向上抛。

在这种方法的基础上，衍生出了SpringMVC的异常处理机制。系统的dao、service、controller出现都通过throws Exception向上抛出，最后由springmvc前端控制器交由异常处理器进行异常处理。

### 自定义异常处理器

> 创建异常处理器类实现HandlerExceptionResolver

```java
@Component
public class GlobalExceptionResolver implements HandlerExceptionResolver {
    @Override
    public ModelAndView resolveException(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, Exception e) {
            ModelAndView modelAndView = new ModelAndView();
            modelAndView.addObject("error", e.getMessage());
            modelAndView.setViewName("error");
            return modelAndView;
    }
}
```

> 新建error.jsp页面，在WEB-INF->pages下

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    error ----> ${error}
</body>
</html>
```

> 配置异常处理器，使用注解或者xml配置
>
> 配置注解记得增加扫描包

```xml
<context:component-scan base-package="com.aaa.controller,com.aaa.exception"/>
```

### web的处理异常机制

> 新建404页面

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
	<h3>未能找到目标资源 </h3>
</body>
</html>
```

> 新建500.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <h3>服务器内部错误</h3>
</body>
</html>
```

> 在web.xml 中配置 

```xl
	<!--处理404异常-->
    <error-page>
        <error-code>404</error-code>
        <location>/404.jsp</location>
    </error-page>
    <!--处理500异常-->
    <error-page>
        <error-code>500</error-code>
        <location>/500.jsp</location>
    </error-page>
```

## 拦截器

**拦截器（interceptor）的作用**

Spring MVC 的拦截器类似于 Servlet 开发中的过滤器 Filter，用于对处理器进行预处理和后处理。

将拦截器按一定的顺序联结成一条链，这条链称为拦截器链（InterceptorChain）。在访问被拦截的方法或字段时，拦截器链中的拦截器就会按其之前定义的顺序被调用。

**拦截器和过滤器区别**

| 区别     | 过滤器                                                  | 拦截器                                                       |
| -------- | ------------------------------------------------------- | ------------------------------------------------------------ |
| 使用范围 | 是servlet规范中的一部分，任何Java Web 工程都可以使用    | 是SpringMVC框架自己的，只有使用了SpringMVC框架的工程才能用   |
| 拦截范围 | 在url-pattern中配置了/*之后，可以对所有要访问的资源拦截 | 只会拦截访问的控制器方法，如果访问的是jsp,html.css.image或者is是不会进行拦截的 |

### 快速入门

> 创建拦截器类实现HandlerInterceptor接口

```java
public class MyInterceptor1 implements HandlerInterceptor {
    // 在目标方法(对应的controller方法)执行之前拦截
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) {
        System.out.println("preHendle-1");
        return true;
    }
    // 在目标方法执行之后,视图对象返回之前执行
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse
            response, Object handler, ModelAndView modelAndView) {
        System.out.println("postHandle-11");
    }
    // 在流程都执行完毕后执行
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) {
        System.out.println("afterCompletion1");
    }
}
```

> 在springmvc.xml 中配置拦截器

```xml
	<!--配置拦截器-->
    <mvc:interceptors>
        <mvc:interceptor>
            <!--对哪些资源执行拦截操作-->
            <mvc:mapping path="/**"/>
            <bean class="com.aaa.interceptor.MyInterceptor1"/>
        </mvc:interceptor>
    </mvc:interceptors>
```

>测试拦截器的拦截效果,编写Controller,发请求到controller,跳转页面

```java
@Controller
public class TargetController {
    @RequestMapping("/target")
    public String targetMethod() {
        System.out.println("目标方法执行了...");
        return "success";
    }
}
```

### 拦截器链

开发中拦截器可以单独使用，也可以同时使用多个拦截器形成一条拦截器链。开发步骤和单个拦截器是一样的，只不过注册的时候注册多个，注意这里注册的顺序就代表拦截器执行的顺序。

> 同上，再编写一个MyInterceptor2操作，测试执行顺序：

```xml
	<!--配置拦截器-->
    <mvc:interceptors>
        <mvc:interceptor>
            <!--拦截器路径配置-->
            <mvc:mapping path="/**"/>
            <!--自定义拦截器类-->
            <bean class="com.aaa.interceptor.MyInterceptor1"></bean>
        </mvc:interceptor>
        <mvc:interceptor>
            <!--拦截器路径配置-->
            <mvc:mapping path="/**"/>
            <!--自定义拦截器类-->
            <bean class="com.aaa.interceptor.MyInterceptor2"></bean>
        </mvc:interceptor>
    </mvc:interceptors>
```

| 方法名            | 说明                                                         |
| ----------------- | ------------------------------------------------------------ |
| preHandle()       | 方法将在请求处理之前进行调用，该方法的返回值是布尔值Boolean类型的，当它返回为false时，表示请求结束，后续的Interceptor和Controller都不会再执行;当返回值为true时就会继续调用下一个Interceptor的preHandle方法 |
| postHandle()      | 该方法是在当前请求进行处理之后被调用，前提是preHandle方法的返回值为true时才能被调用，且它会在DispatcherServlet进行视图返回渲染之前被调用，所以我们可以在这个方法中对Controller处理之后的ModelAndView对象进行操作 |
| afterCompletion() | 该方法将在整个请求结束之后，也就是在DispatcherServlet渲染了对应的视图之后执行，前提是preHandle方法的返回值为true时才能被调用 |

## OSS

**OSS是什么**

阿里云对象存储OSS（Object Storage Service）是一款海量、安全、低成本、高可靠的云存储服务，提供99.9999999999%(12个9)的数据持久性，99.995%的数据可用性。多种存储类型供选择，全面优化存储成本

**查看OSS官方文档**

[对象存储OSS 快速入门 (aliyun.com)](https://help.aliyun.com/document_detail/31882.html)

### 快速入门

[OSS SDK JAVA 快速入门](https://help.aliyun.com/document_detail/32008.html?spm=5176.208357.1107607.21.71e6390fBvXVXH)

> 注册AccessKey（按照官网步骤操作）

![AccessKey](https://image.aobayu.cn/images/AccessKey-1.jpg)

![](https://image.aobayu.cn/images/AccessKey-2.jpg)

> 创建bucket（文件存储的桶）

![](https://image.aobayu.cn/images/Bucket-1.jpg)

![](https://image.aobayu.cn/images/Bucket-2.jpg)

![](https://image.aobayu.cn/images/Bucket-3.jpg)

> 根据官网文档编写上传下载工具类

在Maven项目中加入依赖项

```xml
<dependency>
    <groupId>com.aliyun.oss</groupId>
    <artifactId>aliyun-sdk-oss</artifactId>
    <version>3.15.1</version>
</dependency>
```

编写上传功能

```java
import com.aliyun.oss.ClientException;
import com.aliyun.oss.OSS;
import com.aliyun.oss.OSSClientBuilder;
import com.aliyun.oss.OSSException;
import java.io.ByteArrayInputStream;

public class Demo {

    public static void main(String[] args) throws Exception {
        // Endpoint以华东1（杭州）为例，其它Region请按实际情况填写。
        String endpoint = "https://oss-cn-hangzhou.aliyuncs.com";
        // 阿里云账号AccessKey拥有所有API的访问权限，风险很高。强烈建议您创建并使用RAM用户进行API访问或日常运维，请登录RAM控制台创建RAM用户。
        String accessKeyId = "yourAccessKeyId";
        String accessKeySecret = "yourAccessKeySecret";
        // 填写Bucket名称，例如examplebucket。
        String bucketName = "examplebucket";
        // 填写Object完整路径，例如exampledir/exampleobject.txt。Object完整路径中不能包含Bucket名称。
        String objectName = "exampledir/exampleobject.txt";

        // 创建OSSClient实例。
        OSS ossClient = new OSSClientBuilder().build(endpoint, accessKeyId, accessKeySecret);

        try {
            //写入的内容
            String content = "Hello OSS";
            ossClient.putObject(bucketName, objectName, new ByteArrayInputStream(content.getBytes()));
        } catch (OSSException oe) {
            System.out.println("Caught an OSSException, which means your request made it to OSS, "
                    + "but was rejected with an error response for some reason.");
            System.out.println("Error Message:" + oe.getErrorMessage());
            System.out.println("Error Code:" + oe.getErrorCode());
            System.out.println("Request ID:" + oe.getRequestId());
            System.out.println("Host ID:" + oe.getHostId());
        } catch (ClientException ce) {
            System.out.println("Caught an ClientException, which means the client encountered "
                    + "a serious internal problem while trying to communicate with OSS, "
                    + "such as not being able to access the network.");
            System.out.println("Error Message:" + ce.getMessage());
        } finally {
            if (ossClient != null) {
                ossClient.shutdown();
            }
        }
    }
}
```

### 工具类

> 为了防止硬编码，使用了配置 project.properties

```properties
#OSS相关配置
oss.endpoint=https://oss-cn-hangzhou.aliyuncs.com
oss.accessKeyId=LTAI4GEH3ciDi5SVsvFVi6H2
oss.accessKeySecret=l0I6MhbsKPGH1tLmVE25L5naKKO79C
oss.bucketName=demo161
oss.url=https://demo161.oss-cn-hangzhou.aliyuncs.com
```

> springmvc配置

```xml
<!--上传配置-->
    <bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
        <!--支持的最大文件大小 单位是字节-->
        <property name="maxUploadSize" value="10240000000"></property>
        <!--每个文件大小-->
        <!--  <property name="maxUploadSizePerFile" value="1024000000"></property>-->
    </bean>
```

> 编写上传代码（包含加载配置文件）

```java
public class OSSUtil {
    //实例化Map的子类 Properties
    private static Properties properties =new Properties();

    static {
        //任意一个类的Class对象中都存在一个方法getResourceAsStream   可以把properties读成输入字节流
        InputStream inputStream = OSSUtil.class.getResourceAsStream("/project.properties");
        try {
            properties.load(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    /**
     *
     * 外部只需要调用 这个方法，就可以完成文件的上传
     * @param filePath  上传的路径
     * @param multipartFile  上传的文件
     * @return 返回文件的路径
     */
    public static  String uploadFile(String filePath, MultipartFile multipartFile){
        InputStream inputStream = null;
        OSS ossClient = null;
        try {
            //   springmvc中提供文件处理对象   multipartFile获取到上传文件的原始名称 filePath=a/b/c/   aaa.png
            String originalFilename = multipartFile.getOriginalFilename();
            //获取原文件名称的后缀   aaa.png     suffix=.png
            String suffix = originalFilename.substring(originalFilename.
                    lastIndexOf("."));
            //为了防止后上传的请求与先上传请求的文件名称一致，内容不同，被覆盖，所以一定要让保存到服务器上的文件名称不同
            //随机生成一个名字
            String newFileName = UUID.randomUUID()+suffix;
            //springmvc中提供文件处理对象   multipartFile 直接获取上传文件的输入流
            inputStream = multipartFile.getInputStream();
            // 创建OSSClient实例。
            ossClient = new OSSClientBuilder().build(properties.getProperty("oss.endpoint"),properties.getProperty("oss.accessKeyId"),properties.getProperty("oss.accessKeySecret"));
            // InputStream inputStream = new FileInputStream(filePath);
            // 创建PutObject请求。  //filePath+"/"+newFileName = a/b/c/8e3f7b40-41bc-4125-bbcf-97b38dad4a2d.docx
            ossClient.putObject( properties.getProperty("oss.bucketName"), filePath+"/"+newFileName, inputStream);
            //https://testqy1.oss-cn-beijing.aliyuncs.com/a/b/c/8e3f7b40-41bc-4125-bbcf-97b38dad4a2d.docx
            return properties.getProperty("oss.url")+"/"+filePath+"/"+newFileName;
        } catch (Exception oe) {
            oe.printStackTrace();
        }  finally {
            if (ossClient != null) {
                ossClient.shutdown();
            }
            try {
                if(inputStream!=null){
                    inputStream.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        return null;
    }


    public static void downloadFile(String filePath, HttpServletResponse response){
        OSS ossClient = null;
        BufferedInputStream bufferedInputStream = null;
        BufferedOutputStream bufferedOutputStream = null;
        //filePath = https://testqy1.oss-cn-beijing.aliyuncs.com/a/b/c/b57fb665-5619-4aea-8ea9-2da72bbf78df.png
        //按照官网的文档filePath=a/b/c/b57fb665-5619-4aea-8ea9-2da72bbf78df.png
        filePath = filePath.replace(properties.getProperty("oss.url"),"");
        String fileName  =  filePath.substring(filePath.lastIndexOf("/")+1);
        try {
            // 创建OSSClient实例。
            ossClient = new OSSClientBuilder().build(properties.getProperty("oss.endpoint")
                    , properties.getProperty("oss.accessKeyId"),
                    properties.getProperty("oss.accessKeySecret"));
            // ossObject包含文件所在的存储空间名称、文件名称、文件元信息以及一个输入流。
            OSSObject ossObject = ossClient.getObject(properties.getProperty("oss.bucketName"),
                    filePath);
            //得到要下载对象得输入流
            //设置下载文件的头部信息     attachment  附件
            response.setHeader("content-disposition","attachment;filename="+ URLEncoder.encode(fileName,"UTF-8"));//文件名如果包含中文需要指定编码
            //字节输出流  下载的本质把服务上的文件对象变成输入流（内存）   然后把输入流的内容输出到相应对象HttpServletResponse的输出流中
            //套接缓存流，让下载文件速度提高
            bufferedInputStream =new BufferedInputStream(ossObject.getObjectContent());
            bufferedOutputStream =new BufferedOutputStream( response.getOutputStream());
            //定义缓存字节数组
            byte[]  bytes = new byte[2048];
            //定义每次读取字节数
            int readNum = -1;
            //循环读写
            while((readNum=bufferedInputStream.read(bytes))!=-1){
                //System.out.println(readNum+".............................");
                //写入Response输出流
                bufferedOutputStream.write(bytes,0,readNum);
            }
            bufferedOutputStream.flush();
           /* readNum=bufferedInputStream.read(bytes);
            while(readNum!=0){
                readNum=bufferedInputStream.read(bytes);
            }*/
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                ossClient.shutdown();
                if(bufferedOutputStream!=null){
                    bufferedOutputStream.close();
                }
                if(bufferedInputStream!=null){
                    bufferedInputStream.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

## SSM

> 需求:使用ssm框架完成对 account 表的增删改查操作。

步骤分析：

1. 准备数据库和表记录 

2. 创建web项目 

3. 编写mybatis在ssm环境中可以单独使用 

4. 编写spring在ssm环境中可以单独使用 

5. spring整合mybatis 

6. 编写springMVC在ssm环境中可以单独使用 

7. spring整合springMVC

### 环境搭建

> 准备数据库和表记录

```sql
CREATE TABLE `account` (
    `id` int(11) NOT NULL AUTO_INCREMENT,
    `name` varchar(32) DEFAULT NULL,
    `money` double DEFAULT NULL, PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT CHARSET=utf8;

insert into `account`(`id`,`name`,`money`)
values(1,'tom',1000),
    (2,'jerry',1000);
```

### 编写mybatis

> 需求：基于mybatis先来实现对account表的查询

相关 pom.xml 配置

```xml
	<dependencies>
        <!--mybatis坐标-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.47</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.1.15</version>
        </dependency>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.1</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
    </dependencies>
```

Account实体 com.aaa.pojo.

```java
public class Account {
    private Integer id;
    private String name;
    private Double money;
    //get set toString
}
```

AccountDao接口 com.aaa.dao

```java
public interface AccountDao {
    public List<Account> findAll();
}
```

AccountDao.xml映射 resources.com.aaa.dao.

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.aaa.dao.AccountDao">
    <select id="findAll" resultType="com.aaa.pojo.Account">
        select * from account
    </select>
</mapper>
```

mybatis核心配置文件 resources.

jdbc.properties

```properties
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql:///spring_db?useSSL=false&useServerPrepStmts=true&characterEncoding=utf-8&serverTimezone=Asia/Shanghai
jdbc.username=root
jdbc.password=123456
```

SqlMapConfig.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--加载properties-->
    <properties resource="jdbc.properties"></properties>
    <!--类型别名配置-->
    <typeAliases>
        <package name="com.aaa.pojo"/>
    </typeAliases>
    <!--环境配置-->
    <environments default="development">
        <!--使用MySQL环境-->
        <environment id="development">
            <!--使用JDBC类型事务管理器-->
            <transactionManager type="JDBC"></transactionManager>
            <!--使用连接池-->
            <dataSource type="POOLED">
                <property name="driver" value="${jdbc.driver}"></property>
                <property name="url" value="${jdbc.url}"></property>
                <property name="username" value="${jdbc.username}"></property>
                <property name="password" value="${jdbc.password}"></property>
            </dataSource>
        </environment>
    </environments>
    <!--加载映射配置-->
    <mappers>
        <package name="com.aaa.dao"/>
    </mappers>

</configuration>
```

测试代码

```java
public class MyBatisTest {
    @Test
    public void testMybatis() throws Exception {
        // 加载核心配置文件
        InputStream is = Resources.getResourceAsStream("SqlMapConfig.xml");
        // 获得sqlsession工厂对象
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);
        // 获得sqlsession会话对象
        SqlSession sqlSession = sqlSessionFactory.openSession();
        // 获得mapper代理对象
        AccountDao accountDao = sqlSession.getMapper(AccountDao.class);
        // 执行
        List<Account> list = accountDao.findAll();
        for (Account account : list) {
            System.out.println(account);
        }
        // 释放资源
        sqlSession.close();
    }
}
```

### 编写spring

相关 pom.xml 配置

```xml
		<!--spring坐标-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.8.13</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-tx</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
```

AccountService接口 com.aaa.service.

```java
public interface AccountService {
    public List<Account> findAll();
}
```

AccountServiceImpl实现 com.aaa.service.impl.

```java
@Service
public class AccountServiceImpl implements AccountService {
    @Override
    public List<Account> findAll() {
        System.out.println("findAll执行了....");
        return null;
    }
}
```

spring核心配置文件 applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation=" http://www.springframework.org/schema/beans 
http://www.springframework.org/schema/beans/spring-beans.xsd 
http://www.springframework.org/schema/context 
http://www.springframework.org/schema/context/spring-context.xsd 
http://www.springframework.org/schema/tx 
http://www.springframework.org/schema/tx/spring-tx.xsd 
http://www.springframework.org/schema/aop 
http://www.springframework.org/schema/aop/spring-aop.xsd">

    <!--注解组件扫描-->
    <context:component-scan base-package="com.aaa.service"/>
</beans>
```

测试代码

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:applicationContext.xml")
public class SpringTest {
    @Autowired
    private AccountService accountService;

    @Test
    public void testSpring() throws Exception {
        List<Account> list = accountService.findAll();
        System.out.println(list);
    }
}
```

### spring整合mybatis

**整合思想**

将mybatis接口代理对象的创建权交给spring管理，我们就可以把dao的代理对象注入到service中， 此时也就完成了spring与mybatis的整合了。

> 导入整合包

```xml
		<!--mybatis整合spring坐标-->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>1.3.1</version>
        </dependency>
```

spring配置文件applicationContext.xml管理mybatis 注意：此时可以将mybatis主配置文件删除。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation=" http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans.xsd
http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context.xsd
http://www.springframework.org/schema/tx
http://www.springframework.org/schema/tx/spring-tx.xsd
http://www.springframework.org/schema/aop
http://www.springframework.org/schema/aop/spring-aop.xsd">

    <!--注解组件扫描-->
    <context:component-scan base-package="com.aaa.service"/>

    <!--spring整合mybatis-->
    <context:property-placeholder location="classpath:jdbc.properties"/>
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${jdbc.driver}"/>
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>

    <!--SqlSessionFactory创建交给spring的IOC容器-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <!--数据库环境配置-->
        <property name="dataSource" ref="dataSource"/>
        <!--类型别名配置-->
        <property name="typeAliasesPackage" value="com.aaa.pojo"/>
        <!--如果要引入mybatis主配置文件，可以通过如下配置-->
        <!--<property name="configLocation" value="classpath:SqlMapConfig.xml"/>-->
    </bean>
    <!--映射接口扫描配置，由spring创建代理对象，交给IOC容器-->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <property name="basePackage" value="com.aaa.dao"/>
    </bean>
</beans>
```

修改AccountServiceImpl

```java
@Service
public class AccountServiceImpl implements AccountService {
    @Autowired
    private AccountDao accountDao;
    @Override
    public List<Account> findAll() {
        return accountDao.findAll();
    }
}
```

### 编写springMVC在

需求：访问到controller里面的方法查询所有账户，并跳转到list.jsp页面进行列表展示

相关 pom.xml 配置

```xml
<packaging>war</packaging>		

		<!--springMVC坐标-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.1.5.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.1.0</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>jsp-api</artifactId>
            <version>2.2</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>jstl</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>
```

> 新建 list.jsp 页面 webapp.

springMVC核心配置文件 spring-mvc.xml

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans.xsd
http://www.springframework.org/schema/mvc
http://www.springframework.org/schema/mvc/spring-mvc.xsd
http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context.xsd">

    <!--组件扫描-->
    <context:component-scan base-package="com.aaa.controller"/>
    <!--mvc注解增强-->
    <mvc:annotation-driven/>
    <!--视图解析器-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
    <!--实现静态资源映射-->
    <mvc:default-servlet-handler/>
</beans>
```

AccountController类 com.aaa.controller.

```java
@Controller
@RequestMapping("/account")
public class AccountController {
    //记得创建Account有参构造
    @RequestMapping("/findAll")
    public String findAll(Model model) {
        List<Account> list = new ArrayList<>();
        list.add(new Account(1,"张三",1000d));
        list.add(new Account(2,"李四",1000d));
        model.addAttribute("list", list);
        return "list";
    }
}
```

前端控制器DispathcerServlet webapp.WEB-INF.web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!--前端控制器-->
    <servlet>
        <servlet-name>DispatcherServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:spring-mvc.xml</param-value>
        </init-param>
        <load-on-startup>2</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>DispatcherServlet</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
    <!--post中文处理-->
    <filter>
        <filter-name>CharacterEncodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>CharacterEncodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
</web-app>
```

> Tomcat 运行

### spring整合springMVC

**整合思想**

spring和springMVC其实根本就不用整合，本来就是一家。

但是我们需要做到spring和web容器整合，让web容器启动的时候自动加载spring配置文件，web容器销毁的时候spring的ioc容器也销毁。

**spring和web容器整合**

ContextLoaderListener加载【掌握】

可以使用spring-web包中的ContextLoaderListener监听器，可以监听servletContext容器的创建和销毁，来同时创建或销毁IOC容器。

web.xml

```xml
	<!--spring 与 web容器整合-->
    <listener>
        <listener-class>
            org.springframework.web.context.ContextLoaderListener
        </listener-class>
    </listener>
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:applicationContext.xml</param-value>
    </context-param>
```

修改AccountController

```java
@Controller
@RequestMapping("/account")
public class AccountController {
    @Autowired
    private AccountService accountService;

    @RequestMapping("/findAll")
    public String findAll(Model model) {
        List<Account> list = accountService.findAll();
        model.addAttribute("list", list);
        return "list";
    }
}
```

> Tomcat 运行