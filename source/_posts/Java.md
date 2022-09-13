---
title: Java
copyright_url: https://www.aobayu.cn/2022/09/13/Java/
tags: 
    - java
categories: 学习之路
date: 2022-8-29
keywords: Java
description: Java是一门面向对象的编程语言，不仅吸收了C++语言的各种优点，还摒弃了C++里难以理解的多继承、指针等概念，因此Java语言具有功能强大和简单易用两个特征。--本文为自己学习中所写，主要为JavaSE基础！
---

## Java简介

### Java特性和优势

- 简单性 

  Java就是C++语法的简化版，我们也可以将Java称之为“C++-”。跟我念“C加加减”，指的就是将C++的一些内容去掉；比如：头文件，指针运算，结构，联合，操作符重载，虚基类等等。

  同时，由于语法基于C语言，因此学习起来完全不费力。

- 面向对象 

  面向对象是一种程序设计技术，非常适合大型软件的设计和开发。由于C++为了照顾大量C语言使用者而兼容了C，使得自身仅仅成为了带类的C语言，多少影响了其面向对象的彻底性！

  Java则是完全的面向对象语言。

- 可移植性 

  这是Java的核心优势。Java在设计时就很注重移植和跨平台性。比如：Java的int永远都是32位。不像C++可能是16，32，可能是根据编译器厂商规定的变化。这样的话程序的移植就会非常麻烦。

- 高性能 

  Java最初发展阶段，总是被人诟病“性能低”；客观上，高级语言运行效率总是低于低级语言的，这个无法避免。Java语言本身发展中通过虚拟机的优化提升了几十倍运行效率。

  比如，通过JIT(JUST IN TIME)即时编译技术提高运行效率。 将一些“热点”字节码编译成本地机器码，并将结果缓存起来，在需要的时候重新调用。这样的话，使Java程序的执行效率大大提高，

  某些代码甚至接待C++的效率。因此，Java低性能的短腿，已经被完全解决了。业界发展上，我们也看到很多C++应用转到Java开发，很多C++程序员转型为Java程序员。

- 分布式 

  Java是为Internet的分布式环境设计的，因为它能够处理TCP/IP协议。事实上，通过URL访问一个网络资源和访问本地文件是一样简单的。Java还支持远程方法调用(RMI,Remote Method Invocation)，

  使程序能够通过网络调用方法。

- 多线程 

  多线程的使用可以带来更好的交互响应和实时行为。 Java多线程的简单性是Java成为主流服务器端开发语言的主要原因之一。

- 安全性 

  Java适合于网络/分布式环境，为了达到这个目标，在安全性方面投入了很大的精力，使Java可以很容易构建防病毒，防篡改的系统。

- 健壮性

  Java是一种健壮的语言，吸收了C/C++ 语言的优点，但去掉了其影响程序健壮性的部分（如：指针、内存的申请与释放等）。Java程序不可能造成计算机崩溃。即使Java程序也可能有错误。

  如果出现某种出乎意料之事，程序也不会崩溃，而是把该异常抛出，再通过异常处理机制加以处理。

### Java三大版本

- Write Once、Run Anywhere
- JavaSE: 标准版(桌面程序,控制台开发......)
- JavaME:嵌入式开发(手机,小家电...)
- JavaEE :E企业级开发(web端，服务器开发...)

### Java学习路线

- 首先要学习Java SE，掌握Java语言本身、Java核心开发技术以及Java标准库的使用；
- 如果继续学习Java EE，那么Spring框架、数据库开发、分布式架构就是需要学习的；
- 如果要学习大数据开发，那么Hadoop、Spark、Flink这些大数据平台就是需要学习的，他们都基于Java或Scala开发；
- 如果想要学习移动开发，那么就深入Android平台，掌握Android App开发。

## Java环境配置

### 下载jdk8

[神谕|Java 8 (oracle.com)](https://www.oracle.com/java/technologies/downloads/)

> 下载时需要同意协议，注册账号

### Java 开发环境配置

[Java 开发环境配置 | 菜鸟教程 (runoob.com)](https://www.runoob.com/java/java-environment-setup.html)

> 跟着教程走

 **测试JDK是否安装成功**

1、"开始"->"运行"，键入"cmd"；

2、键入命令: **java -version**、**java**、**javac** 几个命令，出现信息，说明环境变量配置成功；

### 下载IDEA

[IntelliJ IDEA: The Capable & Ergonomic Java IDE by JetBrains](https://www.jetbrains.com/idea/)

> 注：正版收费，破解教程如下查找

[IDE激活网 (idejihuo.com)](http://blog.idejihuo.com/)

### IDEA常用快捷鍵

- 快速生成main方法和输出语句
  - main方法：main或者psvm，回车
  - 输出语句：sout，回车

- 常用快捷键
  - Ctrl+D：复制数据到下一行
  - Ctrl+X：剪切数据，可以用来删除所在行
  - Ctrl+Alt+L：格式化代码，建议自己写代码的时候就注意格式
  - Ctrl+/：对选中的代码添加单行注释，如果想取消注释，再来一次即可
  - Ctrl+Shift+/：对选中的代码添加多行注释，如果想取消注释，再来一次即可

### 第一个Java程序

这个定义被称为**class**（类），这里的类名是**Hello**，大小写敏感，class用来定义一个类，**public**表示这个类是公开的，public、class都是Java的**关键字**，必须小写，**Hello**是类的名字，按照习惯，首字母**H**要大写。而花括号**{}**中间则是类的定义。

定义了一个名为**main**的方法：方法的代码每一行用**;**结束

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
```

我们把代码保存为文件时，文件名必须是`Hello.java`，而且文件名也要注意大小写，因为要和我们定义的类名`Hello`完全保持一致。

一个Java源码只能定义一个`public`类型的class，并且class名称和文件名要完全一致。

## Java基础语法

### 注释

> 平时我们编写代码，在代码量比较少的时候，我们还可以看懂自己写的，但是当项目结构一旦复杂起来，我们就需要用到注释了。
> 注释并不会被执行，是给我们写代码的人看的,书写注释是一个非常好的习惯平时写代码一定要注意规范。

Java中的注释有三种:

```java
单行注释：//我是单行注释

多行注释：/*我是多行注释*/

文档注释：/**
		*我是文档注释
		*文档注释不可以随意使用
		*/
```

### 标识符

- 所有的标识符都应该以字母(A-Z或者a-z),美元符($)、或者下划线(_）开始
- 首字符之后可以是字母(A-Z或者a-z),美元符（$）、下划线（_）或数字的任何字符组合
- 不能使用关键字作为变量名或方法名。
- 标识符是大小写敏感的
- 合法标识符举例: age、$salary._value、__1_value
- 非法标识符举例:123abc、-salary、#abc
- 可以使用中文命名，但是一般不建议这样去使用，也不建议使用拼音，很Low

### 命名的规范

**文件命名规范**

①包名:所有字母都小写。如: xxx.yyy.zzz
②类名、接名:若出现多个单词，每个单词首字母都大写。如: XxxYyyZzz
③方法名、变量名:若出现多个单词，第一个单词的首字母小写，其余单词首字母都大写。如: xxxYyyZzz
④常量名:所有字母都大写，每个单词之间以"_”分隔。如:XXX_YYY_ZZZ

**变量的命名规范**

- 所有变量、方法、类名:见名知意
- 类成员变量:首字母小写和驼峰原则
- monthSalary局部变量:首字母小写和驼峰原则
- 常量:大写字母和下划线:MAX_VALUE
- 类名:首字母大写和驼峰原则: Man, GoodMan
- 方法名:首字母小写和驼峰原则: run(), runRun()

### 关键字

| **关键字**   | **含义**                                                     |
| ------------ | ------------------------------------------------------------ |
| abstract     | 表明类或者成员方法具有抽象属性                               |
| assert       | 断言，用来进行程序调试                                       |
| boolean      | 基本数据类型之一，声明布尔类型的关键字                       |
| break        | 提前跳出一个块                                               |
| byte         | 基本数据类型之一，字节类型                                   |
| case         | 用在switch语句之中，表示其中的一个分支                       |
| catch        | 用在异常处理中，用来捕捉异常                                 |
| char         | 基本数据类型之一，字符类型                                   |
| class        | 声明一个类                                                   |
| const        | 保留关键字，没有具体含义                                     |
| continue     | 回到一个块的开始处                                           |
| default      | 默认，例如，用在switch语句中，表明一个默认的分支。Java8 中也作用于声明接口函数的默认实现 |
| do           | 用在do-while循环结构中                                       |
| double       | 基本数据类型之一，双精度浮点数类型                           |
| else         | 用在条件语句中，表明当条件不成立时的分支                     |
| enum         | 枚举                                                         |
| extends      | 表明一个类型是另一个类型的子类型。对于类，可以是另一个类或者抽象类；对于接口，可以是另一个接口 |
| final        | 用来说明最终属性，表明一个类不能派生出子类，或者成员方法不能被覆盖，或者成员域的值不能被改变，用来定义常量 |
| finally      | 用于处理异常情况，用来声明一个基本肯定会被执行到的语句块     |
| float        | 基本数据类型之一，单精度浮点数类型                           |
| for          | 一种循环结构的引导词                                         |
| goto         | 保留关键字，没有具体含义                                     |
| if           | 条件语句的引导词                                             |
| implements   | 表明一个类实现了给定的接口                                   |
| import       | 表明要访问指定的类或包                                       |
| instanceof   | 用来测试一个对象是否是指定类型的实例对象                     |
| int          | 基本数据类型之一，整数类型                                   |
| interface    | 接口                                                         |
| long         | 基本数据类型之一，长整数类型                                 |
| native       | 用来声明一个方法是由与计算机相关的语言（如C/C++/FORTRAN语言）实现的 |
| new          | 用来创建新实例对象                                           |
| package      | 包                                                           |
| private      | 一种访问控制方式：私用模式                                   |
| protected    | 一种访问控制方式：保护模式                                   |
| public       | 一种访问控制方式：共用模式                                   |
| return       | 从成员方法中返回数据                                         |
| short        | 基本数据类型之一,短整数类型                                  |
| static       | 表明具有静态属性                                             |
| strictfp     | 用来声明FP_strict（单精度或双精度浮点数）表达式遵循[IEEE 754](https://baike.baidu.com/item/IEEE 754?accessToken=eyJhbGciOiJIUzI1NiIsImtpZCI6ImRlZmF1bHQiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE2NjE5NDgwMjAsImZpbGVHVUlEIjoiMzREVEdzTVd4THcwQ1JXNyIsImlhdCI6MTY2MTk0NzcyMCwiaXNzIjoidXBsb2FkZXJfYWNjZXNzX3Jlc291cmNlIiwidXNlcklkIjotNzExNDMyMTI5MH0.RHTMzQaOrUYxo_1wsxydlUk7Z0NakbUt6qBexRcDsdw)算术规范 |
| super        | 表明当前对象的父类型的引用或者父类型的构造方法               |
| switch       | 分支语句结构的引导词                                         |
| synchronized | 表明一段代码需要同步执行                                     |
| this         | 指向当前实例对象的引用                                       |
| throw        | 抛出一个异常                                                 |
| throws       | 声明在当前定义的成员方法中所有需要抛出的异常                 |
| transient    | 声明不用序列化的成员域                                       |
| try          | 尝试一个可能抛出异常的程序块                                 |
| void         | 声明当前成员方法没有返回值                                   |
| volatile     | 表明两个或者多个变量必须同步地发生变化                       |
| while        | 用在循环结构中                                               |

### 变量

> 变量：用于保存数据（局部变量 & 成员变量）

变量的格式：数据类型  变量名  =  值;

```java
声明一个变量;
数据类型 变量名; 如 int a
    
为变量赋值;
变量名 = 值；  如： a= 10;

声明一个变量并赋值
int var = 10;
```

> 变量的概念：

①在内存中开辟一块内存空间

②该空间有名称（变量名）有类型（数据类型）

③变量可以在指定的范围内不断的变化

> 变量的注意：

①作用域：变量作用在所属的那对 {} 内

②局部变量在使用前必须赋初始值

③先声明，后使用


### 数据类型

> Java为强类型语言：要求变量的使用要严格符合规定，所有变量都必须先定义后才能使用

Java 的两大数据类型:

- 内置数据类型
  - **byte** 数据类型是8位、有符号的，以二进制补码表示的整数；byte 类型用在大型数组中节约空间，主要代替整数
  - **short** 数据类型是16位、有符号的以二进制补码表示的整数;
  - **int** 数据类型是32位、有符号的以二进制补码表示的整数; 一般地整型变量默认为 int 类型；
  - **long** 数据类型是 64 位、有符号的以二进制补码表示的整数；这种类型主要使用在需要比较大整数的系统上
  - **float** 数据类型是单精度、32位、符合IEEE 754标准的浮点数；float 在储存大型浮点数组的时候可节省内存空间；
  - **double** 数据类型是双精度、64 位、符合 IEEE 754 标准的浮点数；浮点数的默认类型为 double 类型；
  - **char** 类型是一个单一的 16 位 Unicode 字符；char 数据类型可以储存任何字符；
  - **boolean**数据类型表示一位的信息; 这种类型只作为一种标志来记录 true/false 情况；

- 引用数据类型
  - 在Java中，引用类型的变量非常类似于C/C++的指针。引用类型指向一个对象，指向对象的变量是引用变量。这些变量在声明时被指定为一个特定的类型，比如 Employee、Puppy 等。变量一旦声明后，类型就不能被改变了。
  - 对象、数组都是引用数据类型。
  - 所有引用类型的默认值都是null。
  - 一个引用变量可以用来引用任何与之兼容的类型。

#### 自动类型转换

整型、实型（常量）、字符型数据可以混合运算。运算中，不同类型的数据先转化为同一类型，然后进行运算。

```java
转换从低级到高级
byte,short,char —> int —> long —> float —> double 
```

数据类型转换必须满足如下规则：

- 不能对**boolean**类型进行类型转换。

- 不能把**对象类型**转换成不相关类的对象。

- 在把容量大的类型转换为容量小的类型时必须使用**强制类型转换**。

- 转换过程中可能导致溢出或损失精度。

- 浮点数到整数的转换是通过舍弃小数得到，而不是四舍五入。

```java
  public class Zhuan{
        public static void main(String[] args){
            char c1='a';//定义一个char类型
            int i1 = c1;//char自动类型转换为int
            System.out.println("char自动类型转换为int后的值等于"+i1);
            char c2 = 'A';//定义一个char类型
            int i2 = c2+1;//char 类型和 int 类型计算
            System.out.println("char类型和int计算后的值等于"+i2);
        }
}
```

#### 强制类型转换

- 条件是转换的数据类型必须是兼容的。
  - 高级到低级用强制类型转换
  - 不能对布尔值进行转换
  - 不能把对象类型转换为不相干的类型,
  - 转换的时候可能存在内存溢出，或者精度问题!
- 格式：(type)value   type是要强制类型转换后的数据类型。

```java
public class Huan{
    public static void main(String[] args){
        int i1 = 123;
        byte b = (byte)i1;//强制类型转换为byte
        System.out.println("int强制类型转换为byte后的值等于"+b);
    }
}
```

### 转义字符

| 转义字符 | 意义                                | ASCII码值（十进制） |
| -------- | ----------------------------------- | ------------------- |
| \a       | 响铃(BEL)                           | 007                 |
| \b       | 退格(BS) ，将当前位置移到前一列     | 008                 |
| \f       | 换页(FF)，将当前位置移到下页开头    | 012                 |
| \n       | 换行(LF) ，将当前位置移到下一行开头 | 010                 |
| \r       | 回车(CR) ，将当前位置移到本行开头   | 013                 |
| \t       | 水平制表(HT) （跳到下一个TAB位置）  | 009                 |
| \v       | 垂直制表(VT)                        | 011                 |
| \\       | 代表一个反斜线字符''\'              | 092                 |
| \'       | 代表一个单引号（撇号）字符          | 039                 |
| \"       | 代表一个双引号字符                  | 034                 |
| \?       | 代表一个问号                        | 063                 |
| \0       | 空字符(NUL)                         | 000                 |
| \ddd     | 1到3位八进制数所代表的任意字符      | 三位八进制          |
| \xhh     | 十六进制所代表的任意字符            | 十六进制            |

**注意：**

1. 区分，斜杠："/" 与 反斜杠："\" ,此处不可互换

2. \xhh 十六进制转义不限制字符个数 '\x000000000000F' == '\xF'

### 运算符
- 算术运算符:+， -，*，l， %，++， --*
- 赋值运算符:=
- 关系运算符:>，<，>=，<=，==，!= instanceof
- 逻辑运算符: &&，||，!
- 位运算符: &，|，^，~，>>，<<，>>>(了解! ! ! )
- 条件运算符:?∶
- 扩展赋值运算符:+=，-=，*=，/=

#### 算术运算符

在数学表达式中的使用方式与在代数中使用的方式相同。下表列出了算术运算符的使用示例

假设整数类型变量`A`的值为：`10`，变量`B`的值为：`20`

| 运算符 | 描述                                      | 示例                     |
| ------ | ----------------------------------------- | ------------------------ |
| `+`    | 加法运算符,第一个操作数加上第二个数操作数 | `A + B`结果为：`30`      |
| `-`    | 减法运算符,从第一个操作数减去第二个操作数 | `A - B`结果为：`-10`     |
| `*`    | 两个操作数相乘                            | `A * B`结果为：`200`     |
| `/`    | 左操作数除以右操作数返回模值              | `B / A`结果为：`2`       |
| `%`    | 左操作数除以右操作数返回余数              | `B / A`结果为：`0`       |
| `++`   | 将操作数的值增加`1`                       | `A++`，则`A`的值为：`11` |
| `--`   | 将操作数的值减`1`                         | `A--`，则`A`的值为：`9`  |

#### 关系运算符

Java语言支持以下关系运算符。假设变量`A`的值是`10`，变量`B`的值是`20`

| 运算符 | 描述                                                         | 示例             |
| ------ | ------------------------------------------------------------ | ---------------- |
| `==`   | 等于运算符，检查两个操作数的值是否相等，如果相等，则条件变为真。 | `A==B`结果为假。 |
| `!=`   | 不等于运算符，检查两个操作数的值是否不相等，如果不相等，则条件变为真。 | `A!=B`结果为真。 |
| `>`    | 大于运算符，检查左操作数的值是否大于右操作数的值，如果大于，则条件变为真。 | `A>B`结果为假。  |
| `<`    | 小于运算符，检查左操作数的值是否小于右操作数的值，如果小于，则条件变为真。 | `A<B`结果为真。  |
| `>=`   | 大于或等于运算符，检查左操作数的值是否大于等于右操作数的值，如果大于或等于，则条件变为真。 | `A>=B`结果为假。 |
| `<=`   | 小于或等于运算符，检查左操作数的值是否小于或等于右操作数的值，如果小于或等于，则条件变为真。 | `A<=B`结果为真。 |

#### 逻辑运算符

下表列出了逻辑运算符

假设布尔变量`A`的值为：`true`，变量`B` 的值为：`false`

| 运算符 | 描述                                                         | 示例                      |
| ------ | ------------------------------------------------------------ | ------------------------- |
| `&&`   | 逻辑AND运算符。 如果两个操作数都不为零，则条件成立。         | `(A && B)`结果为：`false` |
| ΙΙ     | 逻辑OR运算符。 如果两个操作数中的任何一个非零，则条件变为真。 | (A ΙΙ B)结果为：`true`    |
| `!`    | 逻辑非运算符。用于反转其操作数的逻辑状态。 如果条件为真，则口逻辑NOT运算符将为`false`。 | `!(A && B)`结果为：`true` |

#### 赋值运算符

以下是Java语言支持的赋值运算符 

| 运算符 | 描述                                                         | 示例                                |
| ------ | ------------------------------------------------------------ | ----------------------------------- |
| `=`    | 简单赋值运算符。 将右侧操作数的值分配给左侧操作数。          | `C = A + B`将`A + B`的值分配给`C`。 |
| `+=`   | 相加与赋值运算符。 它将右操作数相加到左操作数并将结果分配给左操作数。 | `C += A`等于`C = C + A`。           |
| `-=`   | 减去与赋值运算符。 它从左操作数中减去右操作数，并将结果赋给左操作数。 | `C -= A`等于`C = C - A`。           |
| `*=`   | 乘以与赋值运算符。 它将右操作数与左操作数相乘，并将结果赋给左操作数。 | `C *= A`等于`C = C * A`。           |
| `/=`   | 除以与赋值运算符。 它将左操作数除以右操作数，并将结果赋给左操作数。 | `C /= A`等于`C = C / A`。           |
| `%=`   | 模数与赋值运算符。 它使用两个操作数来计算获取模数，并将结果赋给左操作数。 | `C %= A`等于`C = C % A`。           |
| `<<=`  | 左移与赋值运算符。                                           | `C <<= 2`与`C = C << 2`相同         |
| `>>=`  | 右移与赋值运算符。                                           | `C >>= 2`与`C = C >> 2`相同         |
| `&=`   | 按位与赋值运算符。                                           | `C &= 2`与`C = C & 2`相同           |
| `^=`   | 按位异或和赋值运算符。                                       | `C ^= 2`与`C = C ^ 2`相同           |
| Ι=     | 按位包含或与赋值运算符。                                     | C Ι= 2与C = C Ι=2相同               |

#### 三元运算符

```java
(关系表达式)?表达式1:表达式2;
int x = 10;
int y = 5;
int z;
如果x大于y则是true，将x赋值给z;
如果x不大于y则是false，将y赋值给z;
z =(x >y)?x : y;
system.out.println( "x =" + x);
```

## Java流程控制

### Scanner类

之前我们学的基本语法中我们并没有实现程序和人的交互，但是Java给我们提供了这样一个工具类，我们可以获取用户的输入。我们可以通过Scanner类来获取用户的输入
基本语法:

```java
Scanner s = new Scanner(System.in);
```

通过Scanner类的`next()`与`nextLine()`方法获取输入的字符串，在读取前我们一般需要使`hasNext()`与`hasNextLine()`判断是否还有输入的数据。

```java
		//创建一个扫描器对象，用于接收键盘数据
        Scanner scanner = new Scanner(System.in);
        System.out.println("使用next方式接收: ");
        //判断用户有没有输入字符串
        if (scanner.hasNext()){
            //使用next方式接收
            String str = scanner.next();
            System.out.println("输出的内容为:"+str);
        }
		scanner.close();//关闭资源(scanner) 同时释放内存
```

> next():

1、一定要读取到有效字符后才可以结束输入。

2、对输入有效字符之前遇到的空白，next()方法会自动将其去掉。

3、只有输入有效字符后才将其后面输入的空白作为分隔符或者结束符。

4、next()不能得到带有空格的字符串。

> nextLine():

1、以Enter为结束符,也就是说nextLine()方法返回的是输入回车之前的所有字符。

2、可以获得空白。

### 顺序结构

> JAVA的基本结构就是顺序结构除非特别指明，否则就按照顺序一句一句执行。
>
> 顺序结构是最简单的算法结构。

> 语句与语句之间，框与框之间是按从上到下的顺序进行的，它是由若干个依次执行的处理步骤组成的，它是任何一个算法都离不开的一种基本算法结构。

### 选择结构

#### if单选择结构

```java
public static void main(String[] args) {
        //创建一个扫描器对象，用于接收键盘数据
        Scanner scanner = new Scanner(System.in);
        System.out.println("输出考试分数");
        int sum = scanner.nextInt();
        ///考试分数小于60分就不及格。
        if (sum<60){

            System.out.println("不及格:"+sum);
        }
   
        scanner.close();
  }
```

#### if双选择结构

```java
public static void main(String[] args) {
        //创建一个扫描器对象，用于接收键盘数据
        Scanner scanner = new Scanner(System.in);
        System.out.println("输出考试分数");
        int sum = scanner.nextInt();
        ///考试分数小于60分就不及格，考试分数大于60就是及格
        if (sum<60){
            System.out.println("不及格:"+sum);
        }else{
            System.out.println("及格:"+sum);
        }
        
        scanner.close();
      
    }
```

#### 嵌套的if结构

```java
public static void main(String[] args) {
        //创建一个扫描器对象，用于接收键盘数据
        Scanner scanner = new Scanner(System.in);
        System.out.println("输入考试分数");
        int sum = scanner.nextInt();
        ///考试分数小于60分就不及格。
        if (sum<60){
            System.out.println("不及格:"+sum);
        }else if (sum<=70 && sum>=60){
            System.out.println("及格:" + sum);
        } else if (sum<=80 && sum>70) {
            System.out.println("良好:" + sum);
        }else if (sum<=90 && sum>80){
            System.out.println("优:" + sum);
        }else {
            System.out.println("完美:" + sum);
        }
        scanner.close();
      
    }
```

#### switch多选择结构

````java
public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("输入一个数");
        int age = scanner.nextInt();
        switch(age){
            case 10:
                System.out.println("10");
                break;
            case 9:
                System.out.println("9");
                break;
            case 8:
                System.out.println("8");
                break;
            //除上述条件，执行default:
            default:
                System.out.println("数");
                break;
        }
        scanner.close();

    }
````

> **break** :在循环的过程中，在满足某些条件的情况下，中断循环的执行。
>
> 注意: switch 中的break用于结束某个分支。而循环中的 break 是中断循环的。

```java
for (int i = 1; i <= 10; i++) {
            if (i == 5) {
                //中断循环 
                break;
            }
        System.out.println(i);
    }
System.out.println("循环结束");
```

> **continue** :在循环的过程中，在满足某些条件的情况下，跳过循环中的部分代码不执行，直接进入下次循环。

```java
for (int i = 1; i <= 10; i++) {
            if (i == 5) {
                //跳过continue后面的代码，进入循环的下一步 
                continue;
            } 
    	System.out.println(i);
	}
System.out.println("循环结束");
```

### 循环结构

> 只要布尔表达式为true，循环就会一直执行下去。
> 我们大多数情况是会让循环停止下来的，我们需要一个让表达式失效的方式来结束循环。少部分情况需要循环一直执行，比如服务器的请求响应监听等。
> 循环条件一直为true就会造成无限循环【死循环】，我们正常的业务编程中应该尽量避免死循环。会影响程序性能或者造成程序卡死奔溃!

#### while

```java
int age=0;
while(age<10){
    age++;
    System.out.println(age);
}
```

#### do while

> 对于while语句而言，如果不满足条件，则不能进入循环。但有时候我们需要即使不满足条件，也至少执行一次。
> do...while循环和while循环相似，不同的是，do...while循环至少会执行一次。

```java
public static void main(String[] args) {
        int age =0;
        do{
            age++;
            System.out.println(age);
        }
        while(age<10);
}
```

> **While和do-While的区别:**
> while先判断后执行。dowhile是先执行后判断!
> Do...while总是保证循环体会被至少执行一次!这是他们的主要差别。

### for循环

> 虽然所有循环结构都可以用while或者do...while表示，但Java提供了另一种语句—— for循环，使一些循环结构变得更加简单。
> for循环语句是支持迭代的一种通用结构，是最有效、最灵活的循环结构。

```java
public static void main(String[] args) {
        int a = 1; //初始化条件
        while (a<=100){//条件判断
            System.out.println(a); //循环体
            a+=2; //迭代
        }
        System.out.println( "while循环结束!");//初始化I/条件判断//迭代
        for (int i=1;i<=100;i++){
            System.out.println(i) ;
        }
        System.out.println( "for循环结束! ");

}
```

> **关于for循环有以下几点说明;**
> 最先执行初始化步骤。可以声明一种类型，但可初始化一个或多个循环控制变量，也可以是空语句。
> 然后，检测布乐表达式的值。如果为 true，循环体被执行。如果为false，循环终止，开始执行循环体后面的语句。执行一次循环后，更新循环控制变量(迭代因子控制循环变量的增减)。
> 再次检测布尔表达式。循环执行上面的过程。

Java**增强for循环语法**格式如下:

```java
for(声明语句:表达式){
{
	//代码句子
}
```

**声明语句:**声明新的局部变量，该变量的类型必须和数组元素的类型匹配。其作用域限定在循环语句块，其值与此时数组元素的值相等。
**表达式:**表达式是要访问的数组名，或者是返回值为数组的方法。

```java
public static void main(String[] args) {
        int[] numbers = {10,20,30,40,50}; //定义了一个数组
        //遍历数组的元素
        for (int x :numbers){
            System.out.println(x);
        }
    	System.out.println("--------------");
        //等于for(i)循环
        for (int i = 0;i<5;i++){
            System.out.println( numbers[i]);
        }

}
```

### goto关键字

goto关键字很早就在程序设计语言中出现。尽管goto仍是Java的一个保留字，但并未在语言中得到正式使用;Java没有goto。然而，在break和continue这两个关键字的身上，我们仍然能看出一些goto的影子---带标签的break和continue。
“标签”是指后面跟一个冒号的标识符，例如: label:
对Java来说唯一用到标签的地方是在循环语句之前。而在循环之前设置标签的唯一理由是:我们希望在其中嵌套另个循环，由于break和continue关键字通常只中断当前循环，但若随同标签使用，它们就会中断到存在标签的地方。**很少使用！**

> 说白了，就是跳转到指定的循环继续执行;

## Java方法

> **Java方法是语句的集合**，它们在一起执行一个功能。
> 方法是解决一类问题的步骤的有序组合
> **方法包含**于类或对象中
> 方法在程序中被创建，在其他地方被引用
> **设计方法的原则:**方法的本意是功能块，就是实现某个功能的语句块的集合。
> 我们设计方法的时候，最好保持方法的原子性，就是一个方法只完成1个功能，这样利于我们后期的扩展。

```java
public static void main(String[] args) {
    	//main方法
        int sum = add(1,2);
        System.out.println(sum);
    	//调用test()
        test();
    }
	//创建add()方法 static关键字
    public static int add(int a,int b){
        return a+b;//return 返回值（a+b）
    }
	//创建test()方法
	public static void test() {
    for (int i=0;i<=1000;i++){
        if (i%5==0) {
            System.out.println(i+"\t");
        }
        if (i%(5*3)==0) {
            System.out.println("");
            //System.out.println("\n");
        }
        //println输出完会换行
        //print输出完不会换行
    }
```

#### 方法的定义

Java的方法类似于其它语言的函数，是一段用来完成特定功能的代码片段，一般情况下，定义
一个方法包含以下语法:

```java
修饰符 返回值类型 方法名(参数类型 参数名){
   
	//方法体
	return返回值;
}
```



**方法包含一个方法头和一个方法体**。下面是一个方法的所有部分:
**修饰符: ** 这是可选的，告诉编译器如何调用该方法。定义了该方法的访问类型。
**返回值类型︰**方法可能会返回值。returnValueType是方法返回值的数据类型。有些方法执行所需的操作，但没有返回值。在这种情况下，returnValueType是关键字void。
**方法名: ** 是方法的实际名称。方法名和参数表共同构成方法签名。
**参数类型:**  参数像是一个占位符。当方法被调用时，传递值给参数。这个值被称为实参或变量。参数列表是指方法的参数类型、顺序和参数的个数。参数是可选的，方法可以不包含任何参数。

- 形式参数:在方法被调用时用于接收外界输入的数据。
- 实参:调用方法时实际传给方法的数据。

**方法体:**方法体包含具体的语句，定义该方法的功能。

#### 方法调用

**调用方法:** 对象名.方法名(实参列表)
Java支持两种调用方法的方式，根据方法是否返回值来选择。

- 当方法返回一个值的时候，方法调用通常被当做一个值。例如:
  int larger = max( 30，40);
- 如果方法返回值是void，方法调用一定是一条语句。
  system.out.print1n("Hello,kuangshen ! ");

```java
public class TextDemo {
    public static void main(String[] args) {
            Demo sum = new Demo();//调用class Demo内的方法
            sum.haha();
            sum.add(1,2);
            System.out.println(sum.adds(1,2));
    }
}
//两个class类,为两个独立的class文件
public class Demo {
	public void haha() {
        System.out.println("哈哈哈");
    }
    public void add(int a, int b) {
        System.out.println(a+b);
    }
    public int adds(int a, int b) {
        return a+b;
    }
}
```

#### 方法的重载

重载就是在一个类中，有相同的函数名称，但形参不同的函数。
**方法的重载的规则:**

- 方法名称必须相同。

- 数列表必须不同（个数不同、或类型不同、参数排列顺序不同等)。

- 方法的返回类型可以相同也可以不相同。

- 仅仅返回类型不同不足以成为方法的重载。

**实现理论**:

方法名称相同时，编译器会根据调用方法的参数个数、参数类型等去逐个匹配，以选择对应的方法，如果匹配失败，则编译器报错。

```java
public class Demo {

    public String Demo(){
        String sc="哈哈哈";
        return sc;
    }

    public void Demo(int b) {
        System.out.println(b);
    }
    public void Demo(int a, int b) {
        System.out.println(a+b);
    }
    //调用Demo()
   	public static void main(String[] args) {
      Demo sum =  new Demo();
      System.out.println(sum.Demo());
      sum.Demo(2);
      sum.Demo(1,2);
    }
}
```

#### 可变参数

JDK 1.5开始,Java支持传递同类型的可变参数给一个方法。
在方法声明中，在指定参数类型后加一个省略岁(.….)。
一个方法中只能指定一个可变参数它必须是方法的`最后一个参数` ，任何普通的参数必须在它之前声明。

```java
public static void main(String[] args) {
        Demo demo = new Demo();
        Demo.test(1,2,3,4);

    }
    public void test(int ...i){
        System.out.println(i[2]);
    }
```

#### 递归

- A方法调用B方法，我们很容易理解

- 递归就是:A方法调用A方法!就是自己调用自己

  递归结构包括两个部分:

- 递归头:什么时候不调用自身方法。如果没有头，将陷入死循环。
- 递归体:什么时候需要调用自身方法。

利用递归可以用简单的程序来解决一些复杂的问题。它通常把一个大型复杂的问题层层转化为一个与原问题相似的规模较小的问题来求解，递归策略只需少量的程序就可描述出解题过程所需要的多次重复计算，大大地减少了程序的代码量。递归的能力在于用有限的语句来定义对象的无限集合。

```java
public static void main(String[] args) {
        System.out.println(text(5));
    }
	//5*4*3*2*1 =120;
    public static int text(int n){
        if (n==1){
            return 1;
        }else {
            return n*text(n-1);
        }
    }
```

## Java数组

### 数组的定义

- 数组是相同类型数据的有序集合.
- 数组描述的是相同类型的若干个数据,按照一定的先后次序排列组合而成。
- 其中,每一个数据称作一个数组元素,每个数组元素可以通过一个下标来访问它们

**三种初始化**
静态初始化

```java
int[] a = {1,2,3};
Man[] mans = {new Man(1,1),new Man(2,2)};
```

动态初始化

```java
int[] a = new int[2];
a[0]=1;
a[1]=2;
```

数组的默认初始化

数组是引用类型，它的元素相当于类的实例变量，因此数组一经分配空间，其中的每个元素也被按照实例变量同样的方式被隐式初始化。

### 数组声明创建

首先必须声明数组变量，才能在程序中使用数组。下面是声明数组变量的语法:

```java
dataType[] arrayRefVar;//首选的方法
//或
dataType arrayRefVar[];//效果相同，但不是首选方法
```
Java语言使用new操作符来创建数组，语法如下:

```java
dataType[] arrayRefVar = new dataType[arraySize];
//数组的元素是通过索引访问的，数组索引从0开始。
//获取数组长度: arrayRefVar.length
```

> for循环遍历数组

```java
public static void main(String[] args) {
    	//声明数组变量
        int[] arr = new int[10];
        int num =0;
    	////数组赋值
        arr[0] = 1;
        arr[1] = 2;
        arr[2] = 3;
        arr[3] = 4;
        arr[4] = 5;
        arr[5] = 6;
        arr[6] = 7;
        arr[7] = 8;
        arr[8] = 9;
        arr[9] = 10;
    	//for循环遍历数组
    	//1+2+3+4+...+10;
        for (int i =0 ;i<arr.length;i++) {
          num += arr[i];
        }
        System.out.println(num);
    }
```

> for each遍历数组

```java
public static void main(String[] args) {
    	//声明数组变量和赋值
    	int num =0;
        int[] arr = {12,5,324,6,3,2};
        for (int i:arr) {
            num +=i;
            System.out.println(i);
        }
    	System.out.println(num);
    }
```

### 数组的特点

- 其长度是确定的数组一旦被创建，它的大小就是不可以改变的
- 其元素必须是相同类型,不允许出现混合类型。
- 数组中的元素可以是任何数据类型，包括基本类型和引用类型。
- 数组变量属引用类型，数组也可以看成是对象，数组中的每个元素相当于该对象的成员变量。数组本身就是对象，Java中对象是在堆中的，因此数组无论保存原始类型还是其他对象类型,数组对象本身是在堆中的。

### 数组边界

下标的合法区间:[0, length-1]，如果越界就会报错;

```java
public static void main(String[ ] args) {
	int[] a=new int[2];
	system.out.println(a[2]);
}
```

ArraylndexOutOfBoundsException:数组下标越界异常!
**小结:**

- 数组是相同数据类型(数据类型可以为任意类型)的有序集合数组也是对象。
- 数组元素相当于对象的成员变量
- 数组长度的确定的，不可变的。如果越界，则报:ArrayllndexOutofBounds

### 数组使用

> 数组for循环的简单使用

```java
public static void main(String[] args) {

        int[] arr = {2,43,1,5,3};
        //打印全部的数组元素
        for (int i = 0 ; i < arr.length;i++ ){
            System.out.println(arr[i]);
        }
        System.out.println("------");
        //计算所有元素的和
        int num = 0;
        for (int i = 0 ; i < arr.length;i++ ){
            num +=arr[i];
        }
        System.out.println(num);
        System.out.println("------");
        //查找最大元素
        int max = arr[0];
        for (int i = 1; i < arr.length ; i++) {
            if (arr[i]>max){
                max = arr[i];
            }
        }
        System.out.println( "max="+max );

    }
```

> 数组for each循环的简单使用

```java
//没有下标
public static void main(String[] args) {

        int[] arr = {2,43,1,5,3};
        //打印全部的数组元素
        for (int arrs:arr) {
            System.out.println(arrs);
        }
        System.out.print("---------");
        printArray(arr);
        System.out.print("---------");
        printArray(reverse(arr));
    }
//打印数组元素
    public static void printArray(int[ ]arrays){
        for (int i = 0; i < arrays. length; i++) {
            System.out.print(arrays[i]+" ");
        }
    }
//反转数组
    public static int[] reverse(int[] arrays) {
        int[] result = new int[arrays.length];
        //反转的操作
        for (int i = 0,j = result.length-1; i < arrays.length; i++,j--) {
            result[j] = arrays[i];
        }
        return result;
    }
```

### 多维数组

多维数组可以看成是数组的数组，比如二维数组就是一个特殊的一维数组，其每一个元素都是一个一维数组。
二维数组

```java
int a[][] = new int[2][5];
```

解析:以上二维数组a可以看成一个两行五列的数组。

```java
public static void main(String[] args) {
    int[][] array = {{1,2},{3,4},{5,6}}
    
    System.out.println(array.length);
    System.out.println(array[0].length);
    
    for (int i = 0; i < array . length ; i++) {
            for (int j =0; j <array[i].length ; j++){
                System.out.println(array[i][j]);
            }

    }
}
```

### Arrays类

- 数组的工具类java.util.Arrays
- 由于数组对象本身并没有什么方法可以供我们调用,但API中提供了一个工具类Arrays供我们使用,从而可以对数据对象进行一些基本的操作。
- Arrays类中的方法都是static修饰的静态方法,在使用的时候可以直接使用类名进行调用,而"不用"使用对象来调用(注意:是"不用”而不是"不能")
- 具有以下常用功能:
  - 给数组赋值:通过fill方法。
  - 对数组排序:通过sort方法,按升序。
  - 比较数组:通过equals方法比较数组中元素值是否相等。
  - 查找数组元素:通过binarySearch方法能对排序好的数组进行二分查找法操作。

> **Arrays.toString**()

```java
public static void main(String[] args) {
        int[] a = {1,2,3,4,9090,31231,543,21,3,23};
        System.out.println(a); //[I@1b6d3586
    	//打印数组元素Arrays.toString
        //数组进行排序:升序Arrays.sort()
        Arrays.sort(a);
        System.out.println(Arrays.toString(a));
		Arrays.fill(a,0);
        System.out.println(Arrays.toString(a));
    }
```

> **Arrays.fill();**

**参数：**

- a - 要填充的数组
- fromIndex - 要使用指定值填充的第一个元素的索引（包括）
- toIndex - 要使用指定值填充的最后一个元素的索引（不包括）
- val - 要存储在数组的所有元素中的值

**抛出：**

- IllegalArgumentException - 如果 fromIndex > toIndex
- ArrayIndexOutOfBoundsException - 如果 fromIndex < 0 或 toIndex > a.length
- ArrayStoreException - 如果指定值不是可存储在指定数组中的运行时类型

### 冒泡排序

冒泡排序无疑是最为出名的排序算法之一，总共有八大排序!

冒泡的代码还是相当简单的，两层循环，外层冒泡轮数，里层依次比较。

```java
public static void main(String[] args) {
        //冒泡排序
        //1．比较数组中两个相邻的元素，如果第一个数比第二个数大，我们就交换他们的位置
        //2.每一次比较，都会产生出一个最大，或者最小的数字;
        //3.下一轮可以少一次排序!
        //4、依次循环，直到结束!
        int[] a ={23,53,5,15,34,27,35,23};
        int[] arr = sort(a);
        System.out.println(Arrays.toString(arr));

    }
    public static int[] sort(int[] array) {
        //临时变量
        int temp = 0;
        //外层循环，判断我们这个要走多少次;
        for (int i = 0; i < array.length - 1; i++) {
            //内层循环，判断两个数，如果第一个数，比第二个数大，则交换位置
            for (int j = 0; j < array.length - 1; j++) {
                if (array[j + 1] < array[j]) {
                    temp = array[j];
                    array[j] = array[j + 1];
                    array[j + 1] = temp;
                }
            }
        }
        return array;
    }
```

### 稀疏数组

> 当一个数组中大部分元素为0，或者为同一值的数组时，可以使用稀疏数组来保存该数组。

稀疏数组的处理方式是:

- 记录数组一共有几行几列，有多少个不同值
- 把具有不同值的元素和行列及值记录在一个小规模的数组中，从而缩小程序的规模

```java
public static void main(String[] args) {
        //1.创建一个二维数组11*11:没有棋子，1:黑棋2:白棋
        int[][] arr1 = new int[11][11];
        arr1[1][2] =1;
        arr1[2][3] =2;
        //1.1输出原始的数组
        for (int[] ints : arr1){
            for (int intes : ints) {
                System.out.print(intes+"\t");
            }
            System.out.println();
        }
        //1.2转换为稀疏数组保存
        //1.3获取有效值的个数
        int num =0;
        for (int i =0; i<11; i++){
            for (int j = 0; j < 11; j++) {
                if (arr1[i][j] != 0){
                    num++;
                }
            }
        }
        System.out.println("有效值的个数:"+num);
        System.out.println( "=====================");
        //2.创建一个稀疏数组的数组
        int[][] arr2 = new int[num+1][3];
        arr2[0][0] = 11;
        arr2[0][1] = 11;
        arr2[0][2] = num;
        //2.1遍历二维数组，将非零的值，存放稀疏数组中
        int count = 0;
        for (int i = 0; i < arr1.length ; i++) {
            for (int j = 0; j < arr1[i].length; j++) {
                if (arr1[i][j]!=0){
                    count++;
                    arr2[count][0] =i;
                    arr2[count][1] =j;
                    arr2[count][2] =arr1[i][j];
                }
            }
        }
        //2.2输出稀疏数组
        System.out.println("稀疏数组");
        for (int i = 0; i < arr2.length ; i++) {
            System.out.println( arr2[i][0]+"\t"+
                                arr2[i][1]+"\t"+
                                arr2[i][2]+"\t");
        }
        System.out.println( "=====================");
        System.out.println("还原");
        //3.读取稀疏数组
        int[][] arr3 = new int[arr2[0][0]][arr2[0][1]];
        //3.1给其中的元素还原它的值
        for (int i = 1; i < arr2.length; i++) {
            arr3[arr2[i][0]][arr2[i][1]] = arr2[i][2];
        }
        //3.2打印
        System.out.println("输出还原的数组"+"\n");
        for (int[] ints : arr3){
            for (int intes : ints) {
                System.out.print(intes+"\t");
            }
            System.out.println();
        }

    }
```

## Java面向对象

### 什么是面向对象

**面向过程&面向对象**

面向过程思想

- 步骤清晰简单，第一步做什么，第二步做什么...
- 面对过程适合处理一些较为简单的问题

面向对象思想

- 物以类聚，分类的思维模式，思考问题首先会解决问题需要哪些分类，然后对这些分类进行单独思考。最后，才对某个分类下的细节进行面向过程的思索。
- 面向对象适合处理复杂的问题，适合处理需要多人协作的问题!

对于描述复杂的事物，为了从宏观上把握、从整体上合理分析,我们需要使用面向对象的思路来分析整个系统。但是，具体到微观操作，仍然需要面向过程的思路去处理。

**什么是面向对象**
面向对象编程(Object-Oriented Programming, OOP)
面向对象编程的**本质**就是: 以类的方式组织代码，以对象的组织(封装)数据。

抽象

三大特性:

- 封装
- 继承
- 多态

从认识论角度考虑是先有对象后有类。对象，是具体的事物。类，是抽象的，是对对象的抽象

从代码运行角度考虑是先有类后有对象。类是对象的模板。

### 对象的创建

**类与对象的关系**
类是一种抽象的数据类型,它是对某一类事物整体描述/定义,但是并不能代表某一个具体的事物

- 动物、植物、手机、电脑.....
- Person类、Pet类、Car类等，这些类都是用来描述/定义某一类具体的事物应该具备的特点和行为

对象是抽象概念的具体实例

- 张三就是人的一个具体实例,张三家里的旺财就是狗的一个具体实例
- 能够体现出特点,展现出功能的是具体的实例,而不是一个抽象的概念

**创建与初始化对象**
使用new关键字创建对象
使用new关键字创建的时候，除了分配内存空间之外，还会给创建好的对象进行默认的初始化以及对类中构造器的调用。
类中的构造器也称为构造方法，是在进行创建对象的时候必须要调用的。并且构造器有以下俩个特点:

- 必须和类的名字相同
- 必须没有返回类型,也不能写void

构造器必须要掌握

```java
//一个项目应该只存一个main方法
public class Demo {
    public static void main( String[] args) {
		//类:抽象的，实例化
        //类实例化后会返回一个自己的对象!
        //student对象就是一个Student类的具体实例!
        Student xiaoming = new Student();
        Student xh = new Student();
        xiaoming.name = "小明";
        xiaoming.age = 3;
        System.out.println(xiaoming.name);
        System.out.println(xiaoming.age);
        xh.name ="小红";
        xh.age = 3;
        System.out.println(xh.name);
        System.out.println(xh.age);
    }
}
```

```java
//学生类
    public class Student {
        //属性:字段
        String name;//NULL
        int age;//0

        //方法
        public void study() {
            System.out.println(this.name + "在学习");
        }

    }
```

### 构造器

> 无参构造


```java
public class Student {
      
		//一个类即使什么都不写，它也会存在一个方法
        public Student(){
            
        }

}
```

```java
public class Demo {
        //类实例化后会返回一个自己的对象!
        Student xiaoming = new Student();
    }
}
```

> 有参构造

```java
public class Student {
      	String name;
		//一个类即使什么都不写，它也会存在一个方法
        public Student(String name){
            this.name = name;
        	System.out.println("我是："+name);    
        }

}
```

```java
public class Demo {
    public static void main( String[] args) {
        //类实例化后会返回一个自己的对象!
        Student xiaoming = new Student("xiaoming");
    }
}
```

构造器:

- 和类名相同
- 没有返回值

作用:

- new本质在调用构造方法
- 初始化对象的值

注意点: 定义有参构造之后，如果想使用无参构造，显示的定义一个无参的构造

### 封装

该露的露，该藏的藏
我们程序设计要追求“高内聚，低耦合”。
高内聚: 类的内部数据操作细节自己完成，不允许外部干涉;
低耦合: 仅暴露少量的方法给外部使用。

封装（数据的隐藏)
通常，应禁止直接访问一个对象中数据的实际表示，而应通过操作接口来访问，这称为信息隐藏。

> 记住这句话就够了:属性私有，get/set

```java
public class Student {
    //private 私有
    private String name;
    private int id;

    public void setName(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setId(int id) {
        //封装可以加判断
        if (id>120||id<0) {
            System.out.println("不合法");
        }else {
            this.id = id;
        }
    }

    public int getId() {
        return id;
    }
}
```

```java
public class Demo {
    public static void main( String[] args) {
        /*1.提高程序的安全性，保护数据
          2.隐藏代码的实现细节
          3.统一接口
          4.系统可维护增加了*/
      Student student =  new Student();
        
      student.setName("xiaoming");
      System.out.println(student.getName());
      student.setId(38);
      System.out.println(student.getId());
    }
}
```

### 继承

继承的本质是对某一批类的抽象，从而实现对现实世界更好的建模。

extands的意思是“扩展”。子类是父类的扩展。

JAVA中类只有单继承，没有多继承!

继承是类和类之间的一种关系。除此之外,类和类之间的关系还有依赖、组合、聚合等。
继承关系的俩个类，一个为子类(派生类).一个为父类(基类)。
子类继承父类,使用关键字extends来表示。子类和父类之间,从意义上讲应该具有"is a"的关系.

```java
//在Java中，所有的类，都默认直接或者间接继承object
public class Person {
    public void say(){
        System.out.println("说了一句话");
    }
}
```

```java
///学生 is 人
public class Student extends Person{
   	//子类继承了父类，就会拥有父类的全部方法!
	//ctrl+h Idea继承树
}
```

```java
public class Demo {
    public static void main( String[] args) {
      Student student =  new Student();
      student.say();
    }
}
```

> **super**

**super注意点:**

- super调用父类的构造方法，必须在构造方法的第一个
- super必须只能出现在子类的方法或者构造方法中!
- super和 this不能同时调用构造方法!

```java
//父类
public class Person {
    //private  私有的东西无法被继承!
    public String name = "xiaoming";
    public Person(){
        System.out.println("Person无参执行了");
    }
    public void print(){
        System.out.println("Person");
    }
}
```

```java
///学生 is 人
//子类继承了父类，就会拥有父类的全部方法!
public class Student extends Person{
    public String name = "zhengzi";
    //隐藏代码;调用了父类的无参构选
    //super()调用父类的构选器，必须要在子类构造器的第一行
    public Student(){
        System.out.println("Student无参执行了");
    }
    public void print(){
        System.out.println("Students");
    }
    public void test1(){
        print();
        this.print();
        super.print();
    }
    public void test(String name){
        System.out.println(name);
        System.out.println(this.name);
        System.out.println(super.name);
    }

}
```

```java
public class Demo {
    public static void main( String[] args) {
        //类实例化后会返回一个自己的对象!
        Student student =  new Student();
        System.out.println("========");
        student.test1();
        System.out.println("========");
        student.test("wulin");
    }
}
```

**vs this:**

代表的对象不同:

- this: 本身调用者这个对象
- super: 代表父类对象的应用

前提

- this: 没哟继承也可以使用
- super: 只能在继承条件才可以使用

构造方法

- this(); 本类的构造
- super(): 父类的构造!

### 方法重写

> 静态的方法

```java
//重写都是方法的重写,和属性无关
public class B {
    //static
    public static void test(){
        System.out.println("B=>test()");
    }
}
```

```java
//继承
public class A extends B{
    //static
    public static void test(){
        System.out.println("A=>test()");
    }
}
```

```java
public class Demo {
    public static void main( String[] args) {
        //方法的调用只和左边，定义的数据类里有关
        A a = new A();
        a.test();//A

        //父类的引用指向了子类
        B b = new A();
        b.test();//B
    }
}
```

> 非静态的方法(重写)

```java
public class B {
    public void test(){
        System.out.println("B=>test()");
    }
}
```

```java
//继承
public class A extends B{
    //Override 重写
    //A|t + Insert 选中 Override
    @Override//注解:有功能的注释!
    public void test(){
        System.out.println("A=>test()");
    }
}
```

```java
public class Demo {
    public static void main( String[] args) {
        //静态的方法和非静态的方法区别很大!
        //方法的调用只和左边，定义的数据类里有关
        A a = new A();
        a.test();//A

        //父类的引用指向了子类
        B b = new A();
        //子类重写了父类的方法
        //子类重写了父类的方法，执行子类的方法
        b.test();//B
    }

```

**重写:**需要有继承关系，子类重写父类的方法!

- 方法名必须相同
- 参数列表列表必须相同
- 修饰符:范围可以扩大但不能缩小:public>Protected>Default>private
- 抛出的异常:范围，可以被缩小，但不能扩大;ClassNotFoundException --> Exception(大)重写异常抛出范围不能大于父类

重写，子类的方法和父类必要一致;方法体不同!

为什么需要重写: 父类的功能，子类不一定需要，或者不一定满足!

### 多态

即同一方法可以根据发送对象的不同而采用多种不同的行为方式。

一个对象的实际类型是确定的，但可以指向对象的引用的类型有很多

多态存在的条件

- 有继承关系
- 子类重写父类方法
- 父类引用指向子类对象

注意:多态是方法的多态，属性没有多态性。

```java
//父类
public class Person {
    public void run(){
        System.out.println("run");
    }
}
```

```java
//学生 is 人
//子类继承了父类，就会拥有父类的全部方法!
public class Student extends Person{
    @Override
    public void run() {
        System.out.println("son");
    }
    public void eat(){
        System.out.println("eat");
    }
}

```

```java
public class Demo {
    //静态的方法和非静态的方法区别很大!
    public static void main( String[] args) {
        //一个对象的实际类型是确定的
        //new Student();
        //new Person();
        //可以指向的引用类型就不确定了:父类的引用指向子类
        //student能调用的方法都是自已的或者继承父类的!
        Student s1 = new Student();
        //Person父类型，可以指向子类，但是不能调用子类独有的方法
        Person s2 = new Student();
        Object s3 = new Student();
        s2.run();
        s1.run();
        //对象能执行哪些方法，主要看对象左边的类型，和右边关系不大!
        //类重写了父类的方法，执行子类的方法
        //(Student(s2)).eat();
        s1.eat();

    }
}
```

多态注意事项:

1. 多态是方法的多态，属性没有多态
2. 父类和子类，有联系   类型转换异常: cLasscastException !
3. .存在条件:继承关系，方法需要重写，父类引用指向子类对象!

不能重写：static方法，属于类，它属于实例 ;  final 常量;  private方法;

> instanceof 判断一个对象是什么类型(俗称亲子鉴定)
>
> 父类-子类 A instance B B的prototype是否在A的原型链上

类型之间的转化:  子类转换为父类，可能丢失自己的本来的一些方法!

- 把子类转换为父类,  向上转型;
- 把父类转换为子类，向下转型;强制转换 B b = (B)A
- 方便方法的调用，减少重复的代码

### 抽象类

`abstract`修饰符可以用来修饰方法也可以修饰类,如果修饰方法,那么该方法就是抽象方法;如果修饰类,那么该类就是抽象类。
抽象类中可以没有抽象方法,但是有抽象方法的类一定要声明为抽象类。

抽象类,不能使用new关键字来创建对象,它是用来让子类继承的。
抽象方法,只有方法的声明,没有方法的实现,它是用来让子类实现的。

子类继承抽象类,那么就必须要实现抽象类没有实现的抽象方法,否则该子类也要声明为抽象类。

```java
// abstract 抽象类: 类extends:单继承~ (接口可以多继承)
public abstract class Action {
    //约束~有人帮我们实现~
    //abstract ，抽象方法，只有方法名字，没有方法的实现!
    public abstract void something();
    //正常方法
    public void text(){
        
    }
}
```

```java
//抽象类的所有方法，然承了它的子类，都必须要实现,除非加abstract 让子子类实现
public class A extends Action{
    @Override
    public void something() {

    }
}
```

- 不能new这个抽象类，只能靠子类去实现它;约束!
- 抽象类中可以写普通的方法
- 抽象方法必须在抽象类中

### 接口

普通类: 只有具体实现
抽象类: 具体实现和规范(抽象方法)都有!
接口: 只有规范!

接口就是规范，定义的是一组规则，体现了现实世界中“如果你是...则必须能..”的思想。如果你是天使，则必须能飞。如果你是汽车，则必须能跑。如果你好人，则必须干掉坏人;如果你是坏人，则必须欺负好人。
**接口的本质是契约**，就像我们人间的法律一样。制定好后大家都遵守。
OO的精髓，是对对象的抽象，最能体现这一点的就是接口。为什么我们讨论设计模式都只针对具备了抽象能力的语言(比如c++、java、c#等)，就是因为设计模式所研究的，实际上就是如何合理的去抽象。

> 声明类的关键字是class, 声明接口的关键字是interface

```java
//interface定义的关键字
public interface UsersService {
    //按口中的所有定义其实都是抽象的public abstract
    void add(String name);
    void delete(String name);
    void update(String name);
    void query(String name);
/*作用:
约束定义一些方法，让不同的人实现
 public abstract void add(String name)
 public static final int i =99;
接口不能被实例化心，接口中没有构造方法~
implements可以实现多个接口
必须要重写接口中的方法*/
}
```

```java
public interface TimeService {
    void timer();
}
```

```java
//类可以实现接口 implements接口
//实现了按口的类，就需要重写按口中的方法~
//多继承~利用接口实现多继承~
public class UserServiceImpl implements UsersService,TimeService {

    @Override
    public void add(String name) {

    }

    @Override
    public void delete(String name) {

    }

    @Override
    public void update(String name) {

    }

    @Override
    public void query(String name) {

    }

    @Override
    public void timer() {

    }
}
```

### 内部类

> 一个Java类中可以有多个class类，但是只能有一个public class
>
> 没有名字初始化类,不用把实例保存到变量中~new Apple().eat();

```java
public class Person {
    private static int id=10;
    
    public void out(){
        System.out.println("这是外部类的方法");
    }
    
    public static class Inner{
        public void in(){
            System.out.println("这是内部类的方法");
        }
        //获得外部类的私有属性~static
        public void getID(){
            System.out.println(id);
        }
    }
}
```

```java
public class Demo {

    public static void main(String[] args) {
        Person person = new Person();
        //通过这个外部类来实例化内部类~
        Person.Inner inner = new Person.Inner();
        inner.in();
        inner.getID();
    }
}
```

## java异常

**什么是异常**

实际工作中，遇到的情况不可能是非常完美的。比如:你写的某个模块，用户输入不一定符合你的要求、你的程序要打开某个文件，这个文件可能不存在或者文件格式不对，你要读取数据库的数据，数据可能是空的等。我们的程序再跑着，内存或硬盘可能满了。等等。

软件程序在运行过程中，非常可能遇到刚刚提到的这些异常问题，我们叫异常，英文是:`Exception`，意思是例外。这些，例外情况，或者叫异常，怎么让我们写的程序做出合理的处理。而不至于程序崩溃。

异常指程序运行中出现的不期而至的各种状况,如:文件找不到、网络连接失败、非法参数等。
异常发生在程序运行期间,它影响了正常的程序执行流程。

**简单分类**
要理解Java异常处理是如何工作的，你需要掌握以下三种类型的异常:

检查性异常: 最具代表的检查性异常是用户错误或问题引起的异常，这是程序员无法预见的。例如要打开一个不存在文件时，一个异常就发生了，这些异常在编译时不能被简单地忽略。

运行时异常: 运行时异常是可能被程序员避免的异常。与检查性异常相反，运行时异常可以在编译时被忽略。

错误: 错误不是异常，而是脱离程序员控制的问题。错误在代码中通常被忽略。例如，当栈溢出时，一个错误就发生了，它们在编译也检查不到的。

> Error

Error类对象由Java意拟机生成并抛出大多数错误与代码编写者所执行的操作无关。

Java虚拟机运行错误(Virtual MachineError) ，当JVM不下再有继续执行操作所需的内存资源时，将出现 OutOfMemoryError。这些异常发生时、Java虚拟机(JV)一般会选择线程终止;

还有发生在虚拟机试图执行应用时，如类定义错误(NoClass8DefFoundError)、链接错误(LinkageError)，这些错误是不可查的，因为它们在应用程序的控制和处理能力之外，而且绝大多数是程序运行时不允许出现的状况。

> Exception

在Exception分支中有一个重要的子类RuntimeException(运行时异常)

- ArraylndexOutOfBoundsException(数组下标越界)
- NullPointerException(空指针异常)
- ArithmeticException(算术异常)
- MissingResourceException(丢失资源)
- ClassNotFoundException(找不到类)等异常，这些异常是不检查异常，程序中可以选择捕获处理，也可以不处理。

这些异常一般是由程序逻辑错误引起的，程序应该从逻辑角度尽可能避免这类异常的发生;

Error和Exception的区别: Error通常是灾难性的致命的错误,是程序无法控制和处理的，当出现这些异常时，Java虚拟机(JVM)一般会选择终止线程;Exception通常情况下是可以被程序处理的，并且在程序中应该尽可能的去处理这些异常。

### 异常处理机制
- 抛出异常
- 捕获异常

异常处理五个关键字：try、catch、finally、throw、throws

```java
public static void main(String[] args) {
        int a = 1;
        int b = 0;
		//ctrl + Alt + T
		//Idea 快捷键
        try {
            //try监控区域T
            System.out.println(a/b);
        }catch (ArithmeticException e){
            //catch(想要捕获的异常类型!)捕获异常
            System.out.println("程序出现异常，变量b不能为0");
        } finally {
            //处理善后工作
            System.out.println( "finally") ;
        }
        //finally 可以不finally，假设Io，资源，关闭!
}
```

> 捕获多个异常

```java
//假设要捕获多个异常:从小到大!
		try {
            //try监控区域T
            System.out.println(a/b);
        }catch (ArithmeticException e){
            //catch(想要捕获的异常类型!)捕获异常
            System.out.println("程序出现异常，变量b不能为0");
        }catch(Exception e){
            System.out.println("Exception");
        }catch(Throwable e){
            System.out.println("Throwable");
        }finally {
            //处理善后工作
            System.out.println( "finally") ;
        }
```

> 主动的抛出异常-throw

```java
	public static void main(String[] args){	
		in(120);
    }
	//假设这方法中，处理不了这个异常。方法上抛出异常
	public static void in(int age){
        if (age>100){
            throw new ArithmeExcepption("异常");
            //主动的抛出异常，一殷在方法中使用
        }else {
            System.out.println(age);
        }
    }
```

> 假设这方法中，处理不了这个异常。方法上抛出异常-throws

```java
	public static void main(String[] args){	
		try{
           in(120);
        }catch (ArithmeExcepption e){
            e.printStackTrace();
       	}
    }
	//假设这方法中，处理不了这个异常。方法上抛出异常
	public static void in(int age) throw ArithmeExcepption{
        if (age>100){
            throw new ArithmeExcepption("异常");
            //主动的抛出异常，一殷在方法中使用
        }else {
            System.out.println(age);
        }
    }
```

### 自定义异常

使用Java内置的异常类可以描述在编程时出现的大部分异常情况。除此之外，用户还可以自定义异常。用户自定义异常类，只需继承Exception类即可。

在程序中使用自定义异常类，大体可分为以下几个步骤:
1．创建自定义异常类。
2．在方法中通过throw关键字抛出异常对象。
3．如果在当前抛出异常的方法中处理异常，可以使用try-catch语句捕获并处理;否则在方法的声明处通过throws关键字指明要抛出给方法调用者的异常，继续进行下一步操作。
4．在出现异常方法的调用者中捕获并处理异常。

```java
//自定义的异常类
public class ArithmeException extends Exception{
    private int num ;
    public ArithmeException(){}
    public ArithmeException(int i){
        this.num =i;
    }
    //tostring:异常的打印信息
    @Override
    public String toString() {
        return "ArithmeException{"+num+"}";
    }
}
```

```java
//可能会存在异常的方法
public class Runtime {
    public static void main(String[] args) {
        try {
            test(11);
        }catch (ArithmeException e){
            e.printStackTrace();//打印异常
            System.out.println("ArithmeException=>"+e);
        }
    }
    public static void test(int i) throws ArithmeException {
        if (i>10){
            throw new ArithmeException(i);
        }
        System.out.println("ok");
    }

}
```

**实际应用中的经验总结**

处理运行时异常时，采用逻辑去合理规避同时辅助try-catch处理
在多重catch块后面，可以加一个catch(Exceptior）来处理可能会被遗漏的异常
对于不确定的代码，也可以加上 try-catch，处理潜在的异常
尽量去处理异常，切忌只是简单地调用printStackTrace()去打印输出
具体如何处理异常，要根据不同的业务需求和异常类型去决定
尽量添加finally语句块去释放占用的资源