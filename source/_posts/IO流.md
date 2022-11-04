---
title: IO流
copyright_url: https://www.aobayu.cn/2022/09/15/IO流/
tags: 
    - IO流
categories: 学习之路
date: 2022-9-15
keywords: IO流
description: 当你编辑一个文本文件，忘记了ctrl+s，可能文件就白白编辑了。当你电脑上插入一个U盘，可以把一个视频，拷贝到你的电脑硬盘里。那么数据都是在哪些设备上的呢？ --本文为自己学习中所写，IO流详解！
---

## IO流

### IO流简介

当你编辑一个文本文件，忘记了`ctrl+s` ，可能文件就白白编辑了。当你电脑上插入一个U盘，可以把一个视频，拷贝到你的电脑硬盘里。那么数据都是在哪些设备上的呢？键盘、内存、硬盘、外接设备等等。

我们把这种数据的传输，可以看做是一种数据的流动，按照流动的方向，以内存为基准，分为`输入input` 和`输出output` ，即流向内存是输入流，流出内存的输出流。

Java中I/O操作主要是指使用`java.io`包下的内容，进行输入、输出操作。**输入**也叫做**读取**数据，**输出**也叫做作**写出**数据。

流的定义：流是指一连串流动的字符,是以先进先出方式发送信息的通道。

按流向分：

- 输出流：OutputStream和Writer为基类
- 输入流：InputStream和Reader为基类

按处理数据单元划分：

- 字节流：字节输入流：InputStream基类
- 字节输出流：OutputStream基类
- 字符流：字符输入流：Reader基类
- 字节输出流：Writer基类

（字节流是 8 位通用字节流，字符流是16位Unicode字符流）

### File字节流

#### File类概述

- java.io.File类主要用于描述文件或目录路径的抽象表示信息，可以获取文件或目录的特征信息， 如：大小等

- `public File (String pathname)` ：通过将给定的**路径名字符串**转换为抽象路径名来创建新的 File实例。  

- `public File (String parent, String child)` ：从**父路径名字符串和子路径名字符串**创建新的 File实例。

- `public File (File parent, String child)` ：从**父抽象路径名和子路径名字符串**创建新的 File实例。  

```java
// 文件路径名
String pathname = "D:\\aaa.txt";
File file1 = new File(pathname);
// 文件路径名
String pathname2 = "D:\\aaa\\bbb.txt";
File file2 = new File(pathname2);
// 通过父路径和子路径字符串
String parent = "d:\\aaa";
String child = "bbb.txt";
File file3 = new File(parent,child);
// 通过父级File对象和子路径字符串
File parentDir = new File("d:\\aaa");
String child = "bbb.txt";
File file4 = new File(parentDir,child);
```

**tips:**

1. 一个File对象代表硬盘中实际存在的一个文件或者目录。
1. 无论该路径下是否存在文件或者目录，都不影响File对象的创建。

#### 常用方法

- `public String getAbsolutePath()` ：返回此File的绝对路径名字符串。

- `public String getPath()` ：将此File转换为路径名字符串。 

- `public String getName()`  ：返回由此File表示的文件或目录的名称。  

- `public long length()`  ：返回由此File表示的文件的长度。 

```java
public static void main(String[] args) {
    File f = new File("d:/aaa/bbb.java");
    System.out.println("文件绝对路径:"+f.getAbsolutePath());
    System.out.println("文件构造路径:"+f.getPath());
    System.out.println("文件名称:"+f.getName());
    System.out.println("文件长度:"+f.length()+"字节");
    File f2 = new File("d:/aaa");
    System.out.println("目录绝对路径:"+f2.getAbsolutePath());
    System.out.println("目录构造路径:"+f2.getPath());
    System.out.println("目录名称:"+f2.getName());
    System.out.println("目录长度:"+f2.length());
}
```

#### 绝对路径和相对路径

- **绝对路径**：从盘符开始的路径，这是一个完整的路径。

- **相对路径**：相对于项目目录的路径，这是一个便捷的路径，开发中经常使用。

#### 判断功能的方法

- `public boolean exists()` ：此File表示的文件或目录是否实际存在。

- `public boolean isDirectory()` ：此File表示的是否为目录。

- `public boolean isFile()` ：此File表示的是否为文件。

```java
public static void main(String[] args) {
    File f = new File("d:\\aaa\\bbb.java");
    File f2 = new File("d:\\aaa");
    // 判断是否存在
    System.out.println("d:\\aaa\\bbb.java 是否存在:"+f.exists());
    System.out.println("d:\\aaa 是否存在:"+f2.exists());
    // 判断是文件还是目录
    System.out.println("d:\\aaa 文件?:"+f2.isFile());
    System.out.println("d:\\aaa 目录?:"+f2.isDirectory());
}
```

#### 创建删除功能的方法

- `public boolean createNewFile()` ：当且仅当具有该名称的文件尚不存在时，创建一个新的空文件。 
- `public boolean delete()` ：删除由此File表示的文件或目录。  
- `public boolean mkdir()` ：创建由此File表示的目录。
- `public boolean mkdirs()` ：创建由此File表示的目录，包括任何必需但不存在的父目录。

```java
//文件的创建
File f = new File("aaa.txt");
System.out.println("是否存在:"+f.exists());//false
System.out.println("是否创建:"+f.createNewFile());//true
System.out.println("是否存在:"+f.exists());//true
//目录的创建
File f2= new File("newDir");
System.out.println("是否存在:"+f2.exists());//false
System.out.println("是否创建:"+f2.mkdir());//true
System.out.println("是否存在:"+f2.exists());//true
//创建多级目录
File f3= new File("newDira\\newDirb");
System.out.println(f3.mkdir());//false
File f4= new File("newDira\\newDirb");
System.out.println(f4.mkdirs());//true
//文件的删除
System.out.println(f.delete());//true
//目录的删除
System.out.println(f2.delete());//true
System.out.println(f4.delete());//false
```

> API中说明：delete方法，如果此File表示目录，则目录必须为空才能删除。

#### 目录的遍历

- `public String[] list()` ：返回一个String数组，表示该File目录中的所有子文件或目录。

- `public File[] listFiles()` ：返回一个File数组，表示该File目录中的所有的子文件或目录。

```java
public static void main(String[] args) {
    File dir = new File("d:\\java_code");
    //获取当前目录下的文件以及文件夹的名称。
    String[] names = dir.list();
    for(String name : names){
        System.out.println(name);
    }
    //获取当前目录下的文件以及文件夹对象，只要拿到了文件对象，那么就可以获取更多信息  
    File[] files = dir.listFiles();
    for (File file : files) {
        System.out.println(file);
    }
}
```

### 字节输出流(OutputStream)

java.io.OutputStream抽象类是表示字节输出流的所有类的超类，将指定的字节信息写出到目的地。它定义了字节输出流的基本共性功能方法。

- public void close() ：关闭此输出流并释放与此流相关联的任何系统资源。 

- public void flush() ：刷新此输出流并强制任何缓冲的输出字节被写出。 

- public void write(byte[] b)：将 b.length字节从指定的字节数组写入此输出流。 

- public void write(byte[] b, int off, int len) ：从指定的字节数组写入 len字节，从偏移量 off开始输出到此输出流。 

-  public abstract void write(int b) ：将指定的字节输出流。

tips：close方法，当完成流的操作时，必须调用此方法，释放系统资源。

> FileOutputStream类

```java
public static void main(String[] args) {
    //使用File对象创建流对象
    File file = new File("a.txt");
    FileOutputStream fos = new FileOutputStream(file);
    //使用文件名称创建流对象
    FileOutputStream fos = new FileOutputStream("b.txt");
}
```

> `write(int b)` 方法，每次可以写出一个字节数据

```java
public static void main(String[] args) throws IOException {
    //使用文件名称创建流对象
    FileOutputStream fos = new FileOutputStream("fos.txt");
    //写出数据
    fos.write(97);//写出第1个字节
    fos.write(98);//写出第2个字节
    fos.write(99);//写出第3个字节
    //关闭资源
    fos.close();
}
```

> 写出字节数组：`write(byte[] b)`，每次可以写出数组中的数据

```java
public static void main(String[] args) throws IOException {
    //使用文件名称创建流对象
    FileOutputStream fos = new FileOutputStream("fos.txt");
    //字符串转换为字节数组
    byte[] b = "我爱学习".getBytes();
    //写出字节数组数据
    fos.write(b);
    //关闭资源
    fos.close();
}
```

> 写出指定长度字节数组：`write(byte[] b, int off, int len)` ,每次写出从off索引开始，len个字节

```java
public static void main(String[] args) throws IOException {
    //使用文件名称创建流对象
    FileOutputStream fos = new FileOutputStream("fos.txt");
    //字符串转换为字节数组
    byte[] b = "abcde".getBytes();
    //写出从索引2开始，2个字节。索引2是c，两个字节，也就是cd.
    fos.write(b,2,2);
    //关闭资源 
    fos.close();
}
```

> 数据追加续写

```java
public static void main(String[] args) throws IOException {
    //使用文件名称创建流对象
    FileOutputStream fos = new FileOutputStream("fos.txt",true);
    //字符串转换为字节数组
    byte[] b = "abcde".getBytes();
    //写出从索引2开始，2个字节。索引2是c，两个字节，也就是cd。
    fos.write(b);
    //关闭资源
    fos.close();
}
```

> Windows系统里，换行符号是`\r\n` 。

```java
public static void main(String[] args) throws IOException {
    FileOutputStream fos = new FileOutputStream("fos.txt");
    byte[] words = {97,98,99,100,101};
    //遍历数组
    for (int i = 0; i < words.length; i++) {
        //写出一个字节
        fos.write(words[i]);
        //写出一个换行, 换行符号转成数组写出
        fos.write("\r\n".getBytes());
    }
    fos.close();
}
```

### 字节输入流(InputStream)

`java.io.InputStream`抽象类是表示字节输入流的所有类的超类，可以读取字节信息到内存中。它定义了字节输入流的基本共性功能方法。

- `public void close()` ：关闭此输入流并释放与此流相关联的任何系统资源。    

- `public abstract int read()`： 从输入流读取数据的下一个字节。 

- `public int read(byte[] b)`： 从输入流中读取一些字节数，并将它们存储到字节数组 b中 。

> FileInputStream类

```java
public static void main(String[] args) {
    //使用File对象创建流对象
    File file = new File("a.txt");
    FileInputStream fos = new FileInputStream(file);
    //使用文件名称创建流对象
    FileInputStream fos = new FileInputStream("b.txt");
}
```

> 读取字节数据

> read方法，每次可以读取一个字节的数据，提升为int类型，读取到文件末尾，返回 -1

```java
public static void main(String[] args) throws IOException{
    //使用文件名称创建流对象
    FileInputStream fis = new FileInputStream("read.txt");
    //读取数据，返回一个字节
    int read = fis.read();
    System.out.println((char) read);
    read = fis.read();
    System.out.println((char) read);
    read = fis.read();
    System.out.println((char) read);
    read = fis.read();
    System.out.println((char) read);
    read = fis.read();
    System.out.println((char) read);
    //读取到末尾,返回-1
    read = fis.read();
    System.out.println(read);
   	fis.close();
}
```

> 循环读取方式

```java
public static void main(String[] args) throws IOException{
    //使用文件名称创建流对象
    FileInputStream fis = new FileInputStream("read.txt");
    //定义变量，保存数据
    int b;
    //循环读取
    while ((b = fis.read())!=-1) {
        System.out.println((char)b);
    }
    fis.close();
}
```

> 字节数组读取：read(byte[] b)

```java
public static void main(String[] args) throws IOException{
    //使用文件名称创建流对象
    FileInputStream fis = new FileInputStream("read.txt");
    // 定义变量，作为有效个数
    int b;
    //定义字节数组，作为装字节数据的容器
    byte[] by = new byte[2];
    //循环读取
    while ((b = fis.read(by))!=-1) {
        System.out.println(new String(by,0,b));
        //b每次读取的有效字节个数
    }
    fis.close();
}
```

### 字节缓冲流

缓冲流的基本原理，是在创建流对象时，会创建一个内置的默认大小的缓冲区数组，通过缓冲区读写，减少系统IO次数，从而提高读写的效率。

**构造方法**

- `public BufferedInputStream(InputStream in)` ：创建一个 新的缓冲输入流。 

- `public BufferedOutputStream(OutputStream out)`： 创建一个新的缓冲输出流。

```java
//创建字节缓冲输入流
BufferedInputStream bis = new BufferedInputStream(new FileInputStream("bis.txt"));
//创建字节缓冲输出流
BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("bos.txt"));
```

```java
public static void main(String[] args) {
        //获取当前系统时间距离1970年1月1日0时0分0秒的毫秒数
        long g1 = System.currentTimeMillis();
        BufferedInputStream bis = null;
        BufferedOutputStream bos = null;
        try {
            //1.创建BufferedInputStream类型的对象与d:/视频文件1.mp4文件关联
            bis = new BufferedInputStream(new FileInputStream("d:/视频文件1.mp4"));
            //2.创建BufferedOuputStream类型的对象与d:/视频文件2.mp4文件关联
            bos = new BufferedOutputStream(new FileOutputStream("d:/视频文件2.mp4"));
            //3.不断地从输入流中读取数据并写入到输出流中
            System.out.println("正在玩命地拷贝...");
            byte[] bArr = new byte[1024];
            int res = 0;
            while ((res = bis.read(bArr)) != -1) {
                bos.write(bArr, 0, res);
            }
            System.out.println("拷贝文件成功！");
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            //4.关闭流对象并释放有关的资源
            if (null != bos) {
                try {
                    bos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
                if (null != bis) {
                    try {
                        bis.close();
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                    long g2 = System.currentTimeMillis();
                    System.out.println("使用缓冲区拷贝视频文件消耗的时间为：" + (g2 - g1));
                }
            }
        }
}
```

## 字符流

字符 --->1010101 + 编码表  

计算机中储存的信息都是用二进制数表示的，而我们在屏幕上看到的数字、英文、标点符号、汉字等字符是二进制数转换之后的结果。按照某种规则，将字符存储到计算机中，称为**编码** 。反之，将存储在计算机中的二进制数按照某种规则解析显示出来，称为**解码** 。比如说，按照A规则存储，同样按照A规则解析，那么就能显示正确的文本符号。反之，按照A规则存储，再按照B规则解析，就会导致乱码现象。

编码:字符(能看懂的)--字节(看不懂的)

解码:字节(看不懂的)-->字符(能看懂的)

**字符编码**`Character Encoding` : 就是一套自然语言的字符与二进制数之间的对应规则。

- 编码表:生活中文字和计算机中二进制的对应规则

### 字符集

- **字符集** `Charset`：也叫编码表。是一个系统支持的所有字符的集合，包括各国家文字、标点符号、图形符号、数字等。

- 计算机要准确的存储和识别各种字符集符号，需要进行字符编码，一套字符集必然至少有一套字符编码。常见字符集有ASCII字符集、GBK字符集、Unicode字符集等。

- **ASCII字符集** ：

- ASCII（American Standard Code for Information Interchange，美国信息交换标准代码）是基于拉丁字母的一套电脑编码系统，用于显示现代英语，主要包括控制字符（回车键、退格、换行键等）和可显示字符（英文大小写字符、阿拉伯数字和西文符号）。

- 基本的ASCII字符集，使用7位（bits）表示一个字符，共128字符。ASCII的扩展字符集使用8位（bits）表示一个字符，共256字符，方便支持欧洲常用字符。

- **ISO-8859-1字符集**：

- 拉丁码表，别名Latin-1，用于显示欧洲使用的语言，包括荷兰、丹麦、德语、意大利语、西班牙语等。

- ISO-8859-1使用单字节编码，兼容ASCII编码。

- **GBxxx字符集**：

- GB就是国标的意思，是为了显示中文而设计的一套字符集。

- **GB2312**：简体中文码表。一个小于127的字符的意义与原来相同。但两个大于127的字符连在一起时，就表示一个汉字，这样大约可以组合了包含7000多个简体汉字，此外数学符号、罗马希腊的字母、日文的假名们都编进去了，连在ASCII里本来就有的数字、标点、字母都统统重新编了两个字节长的编码，这就是常说的"全角"字符，而原来在127号以下的那些就叫"半角"字符了。

- **GBK**：最常用的中文码表。是在GB2312标准基础上的扩展规范，使用了双字节编码方案，共收录了21003个汉字，完全兼容GB2312标准，同时支持繁体汉字以及日韩汉字等。

- **GB18030**：最新的中文码表。收录汉字70244个，采用多字节编码，每个字可以由1个、2个或4个字节组成。支持中国国内少数民族的文字，同时支持繁体汉字以及日韩汉字等。

- **Unicode字符集** ：

- Unicode编码系统为表达任意语言的任意字符而设计，是业界的一种标准，也称为统一码、标准万国码。

- 它最多使用4个字节的数字来表达每个字母、符号，或者文字。有三种编码方案，UTF-8、UTF-16和UTF-32。最为常用的UTF-8编码。

- UTF-8编码，可以用来表示Unicode标准中任何字符，它是电子邮件、网页及其他存储或传送文字的应用中，优先采用的编码。互联网工程工作小组（IETF）要求所有互联网协议都必须支持UTF-8编码。所以，我们开发Web应用，也要使用UTF-8编码。它使用一至四个字节为每个字符编码，编码规则：

- 128个US-ASCII字符，只需一个字节编码。

- 拉丁文等字符，需要二个字节编码。 

- 大部分常用字（含中文），使用三个字节编码。

- 其他极少使用的Unicode辅助字符，使用四字节编码。

### 字符输入流(Reader)

`java.io.Reader`抽象类是表示用于读取字符流的所有类的超类，可以读取字符信息到内存中。它定义了字符输入流的基本共性功能方法。

- `public void close()` ：关闭此流并释放与此流相关联的任何系统资源。    

- `public int read()`： 从输入流读取一个字符。 

- `public int read(char[] cbuf)`： 从输入流中读取一些字符，并将它们存储到字符数组 cbuf中 。

> FileReader类  

```java
//当你创建一个流对象时，必须传入一个文件路径。类似于FileInputStream
public static void main(String[] args) {
    //使用File对象创建流对象
    File file = new File("a.txt");
    FileReader fr = new FileReader(file);
    //使用文件名称创建流对象
    FileReader fr = new FileReader("b.txt");
}
```

> 读取字符数据

```java
public static void main(String[] args) throws IOException {
    //使用文件名称创建流对象
    FileReader fr = new FileReader("read.txt");
    //定义变量，保存数据
    int b;
    //循环读取
    while ((b = fr.read())!=-1) {
        System.out.println((char)b);
    }
    fr.close();
}
```

> 使用字符数组读取：read(char[] cbuf)

```java
public static void main(String[] args) throws IOException {
    //使用文件名称创建流对象
    FileReader fr = new FileReader("read.txt");
    //定义变量，保存有效字符个数
    int len;
    //定义字符数组，作为装字符数据的容器
    char[] cbuf = new char[2];
    //循环读取
    while ((len = fr.read(cbuf))!=-1) {
        System.out.println(new String(cbuf,0,len));
    }
    fr.close();
}
```

### 字符输出流(Writer)

`java.io.Writer`抽象类是表示用于写出字符流的所有类的超类，将指定的字符信息写出到目的地。它定义了字节输出流的基本共性功能方法。

- `void write(int c)` 写入单个字符。

- `void write(char[] cbuf)`写入字符数组。 

- `abstract  void write(char[] cbuf, int off, int len)`写入字符数组的某一部分,off数组的开始索引,len写的字符个数。 

- `void write(String str)`写入字符串。 

- `void write(String str, int off, int len)` 写入字符串的某一部分,off字符串的开始索引,len写的字符个数。

- `void flush()`刷新该流的缓冲。  

- `void close()` 关闭此流，但要先刷新它。

> FileWriter类

```java
public static void main(String[] args) throws IOException {
    //使用File对象创建流对象
    File file = new File("a.txt");
    FileWriter fw = new FileWriter(file);
    //使用文件名称创建流对象
    FileWriter fw = new FileWriter("b.txt");
}
```

> write(int b) 方法，每次可以写出一个字符数据

```java
public static void main(String[] args) throws IOException {
    //使用文件名称创建流对象
    FileWriter fw = new FileWriter("fw.txt");
    //写出数据
    fw.write(97);//写出第1个字符
    fw.write('b');//写出第2个字符
    fw.write('C');//写出第3个字符
    fw.write(30000);//写出第4个字符，中文编码表中30000对应一个汉字。
    /*【注意】关闭资源时,与FileOutputStream不同。
    如果不关闭,数据只是保存到缓冲区，并未保存到文件。 */
    // fw.close();
}
```

> 关闭和刷新

关闭的流对象，是无法继续写出数据的。如果我们既想写出数据，又想继续使用流，就需要`flush` 方法了。

- `flush` ：刷新缓冲区，流对象可以继续使用。

- `close`:先刷新缓冲区，然后通知系统释放资源。流对象不可以再被使用了。

> 字符数组 

```java
public static void main(String[] args) throws IOException {
        //使用文件名称创建流对象
        FileWriter fw = new FileWriter("fw.txt");
        //字符串转换为字节数组
        char[] chars = "中秋节快乐".toCharArray();
        //写出字符数组
        fw.write(chars);
        //关闭资源
        fw.close();
}
```

> 字符串

```java
public static void main(String[] args) throws IOException {
        //使用文件名称创建流对象
        FileWriter fw = new FileWriter("fw.txt");
        //字符串转换为字节数组
        String msg = "中秋节快乐";
        //写出字符数组
        fw.write(msg);
    	fw.write(msg,2,2);
        //关闭资源
        fw.close();
}
```

> 续写和换行

```java
public static void main(String[] args) throws IOException {
        //使用文件名称创建流对象，可以续写数据
        FileWriter fw = new FileWriter("fw.txt",true);
        //写出字符串
        fw.write("中秋节");
        //写出换行
        fw.write("\r\n");
        //写出字符串
        fw.write("快乐");
        //关闭资源
        fw.close();
}
```

>字符流，只能操作文本文件，不能操作图片，视频等非文本文件。
>
>当我们单纯读或者写文本文件时 ,使用字符流 ,其他情况使用字节流

### 字符缓冲流

**构造方法**

- `public BufferedReader(Reader in)` ：创建一个 新的缓冲输入流。 

- `public BufferedWriter(Writer out)`： 创建一个新的缓冲输出流。

```java
//创建字符缓冲输入流
BufferedReader br = new BufferedReader(new FileReader("br.txt"));
//创建字符缓冲输出流
BufferedWriter bw = new BufferedWriter(new FileWriter("bw.txt"));
```

**特有方法**

字符缓冲流的基本方法与普通字符流调用方式一致，不再阐述，我们来看它们具备的特有方法。

> BufferedReader：`public String readLine()`: 读一行文字。 

```java
public static void main(String[] args) throws IOException {
    //创建流对象
    BufferedReader br = new BufferedReader(new FileReader("in.txt"));
    //定义字符串,保存读取的一行文字
    String line = null;
    //循环读取,读取到最后返回null
    while ((line = br.readLine())!=null) {
        System.out.print(line);
        System.out.println("------");
    }
    br.close();
}
```

> BufferedWriter：`public void newLine()`: 写一行行分隔符,由系统属性定义符号。 

```java
public static void main(String[] args) throws IOException  {
    //创建流对象
    BufferedWriter bw = new BufferedWriter(new FileWriter("out.txt"));
    //写出数据
    bw.write("中秋");
    //写出换行
    bw.newLine();
    bw.write("节");
    bw.newLine();
    bw.write("快乐");
    bw.newLine();
    //释放资源
    bw.close();
}
```

## 转换流

### InputStreamReader类  

转换流`java.io.InputStreamReader`，是Reader的子类，是从字节流到字符流的桥梁。它读取字节，并使用指定的字符集将其解码为字符。它的字符集可以由名称指定，也可以接受平台的默认字符集。 

- `InputStreamReader(InputStream in)`: 创建一个使用默认字符集的字符流。 

- `InputStreamReader(InputStream in, String charsetName)`: 创建一个指定字符集的字符流。

```java
InputStreamReader isr = new InputStreamReader(new FileInputStream("in.txt"));
InputStreamReader isr2 = new InputStreamReader(new FileInputStream("in.txt"),"GBK");
```

> 编码读取

```java
public static void main(String[] args) throws IOException {
     //定义文件路径,文件为gbk编码
     String FileName = "E:\\file_gbk.txt";
     //创建流对象,默认UTF8编码
     InputStreamReader isr = new InputStreamReader(new FileInputStream(FileName));
     //创建流对象,指定GBK编码
     InputStreamReader isr2 = new InputStreamReader(new FileInputStream(FileName),"GBK");
     //定义变量,保存字符
     int read;
     //使用默认编码字符流读取,乱码
     while ((read = isr.read()) != -1) {
         System.out.print((char)read);//��Һ�
     }
     isr.close();
     //使用指定编码字符流读取,正常解析
     while ((read = isr2.read()) != -1) {
         System.out.print((char)read);//大家好
     }
     isr2.close();
 }
```

### OutputStreamWriter类

转换流`java.io.OutputStreamWriter` ，是Writer的子类，是从字符流到字节流的桥梁。使用指定的字符集将字符编码为字节。它的字符集可以由名称指定，也可以接受平台的默认字符集。 

- `OutputStreamWriter(OutputStream in)`: 创建一个使用默认字符集的字符流。 

- `OutputStreamWriter(OutputStream in, String charsetName)`: 创建一个指定字符集的字符流。

> 编码写出

```java
public static void main(String[] args) throws IOException {
    //定义文件路径
    String FileName = "E:\\out.txt";
    //创建流对象,默认UTF8编码
    OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream(FileName));
    //写出数据
    osw.write("你好");//保存为6个字节
    osw.close();
    //定义文件路径
    String FileName2 = "E:\\out2.txt";
    //创建流对象,指定GBK编码
 OutputStreamWriter osw2 = new OutputStreamWriter(new FileOutputStream(FileName2),"GBK");
// 写出数据
    osw2.write("你好");//保存为4个字节
    osw2.close();
}
```

## 序列化

###  概述

Java 提供了一种对象序列化的机制。用一个字节序列可以表示一个对象，该字节序列包含该对象的数据、对象的类型和对象中存储的属性等信息。字节序列写出到文件之后，相当于文件中持久保存了一个对象的信息。 

反之，该字节序列还可以从文件中读取回来，重构对象，对它进行反序列化。对象的数据、对象的类型和对象中存储的数据信息，都可以用来在内存中创建对象

### ObjectOutputStream类

`java.io.ObjectOutputStream` 类，将Java对象的原始数据类型写出到文件,实现对象的持久存储。

`public ObjectOutputStream(OutputStream out)`： 创建一个指定OutputStream的ObjectOutputStream。

```java
FileOutputStream fileOut = new FileOutputStream("employee.txt");
ObjectOutputStream out = new ObjectOutputStream(fileOut);
```

> 序列化操作

```java
public class Employee implements java.io.Serializable {
    public String name;
    public String address;
    public transient int age;//transient瞬态修饰成员,不会被序列化
    public void addressCheck() {
        System.out.println("Address  check : " + name + " -- " + address);
    }
}
```

```java
public class SerializeDemo{
    public static void main(String [] args){
        Employee e = new Employee();
        e.name = "zhangsan";
        e.address = "zhengzhou";
        e.age = 20;
            try {
                //创建序列化流对象
  ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("employee.txt"));
                //写出对象
                out.writeObject(e);
                //释放资源
                out.close();
                fileOut.close();
                System.out.println("Serialized data is saved");
                //姓名，地址被序列化，年龄没有被序列化。
            } catch(IOException i)
            {
                i.printStackTrace();
            }
    }
}
```

### ObjectInputStream类

ObjectInputStream反序列化流，将之前使用ObjectOutputStream序列化的原始数据恢复为对象。 

`public ObjectInputStream(InputStream in)`： 创建一个指定InputStream的ObjectInputStream。

`public final Object readObject ()` : 读取一个对象。

```java
public class DeserializeDemo {
    public static void main(String [] args){
        Employee e = null;
        try{
            //创建反序列化流
            FileInputStream fileIn = new FileInputStream("employee.txt");
            ObjectInputStream in = new ObjectInputStream(fileIn);
            //读取一个对象
            e = (Employee) in.readObject();
            //释放资源
            in.close();
            fileIn.close();
        }catch(IOException i){
            //捕获其他异常
            i.printStackTrace();
            return;
        }catch(ClassNotFoundException c){
            //捕获类找不到异常
            System.out.println("Employee class not found");
            c.printStackTrace();
            return;
        }
        //无异常,直接打印输出
        System.out.println("Name: " + e.name);//zhangsan
        System.out.println("Address: " + e.address);//zhengzhou
        System.out.println("age: " + e.age);//0
    }
}
```

## 属性集

### 概述

`java.util.Properties` 继承于`Hashtable` ，来表示一个持久的属性集。它使用键值结构存储数据，每个键及其对应值都是一个字符串。该类也被许多Java类使用，比如获取系统属性时，`System.getProperties` 方法就是返回一个`Properties`对象。

### Properties类

`public Properties()` :创建一个空的属性列表。

`public Object setProperty(String key, String value)` ： 保存一对属性。  

`public String getProperty(String key)` ：使用此属性列表中指定的键搜索属性值。

`public Set<String> stringPropertyNames()` ：所有键的名称的集合。

```java
 public class ProDemo {
     public static void main(String[] args) throws FileNotFoundException {
         //创建属性集对象
        Properties properties = new Properties();
        //添加键值对元素
        properties.setProperty("filename", "a.txt");
        properties.setProperty("length", "209385038");
        properties.setProperty("location", "D:\\a.txt");
        //打印属性集对象
        System.out.println(properties);
        // 通过键,获取属性值
        System.out.println(properties.getProperty("filename"));
        System.out.println(properties.getProperty("length"));
        System.out.println(properties.getProperty("location"));
        //遍历属性集,获取所有键的集合
        Set<String> strings = properties.stringPropertyNames();//打印键值对
        for (String key : strings ){
            System.out.println(key+"--"+properties.getProperty(key));
        }
     }
 }
```

> 与流相关的方法

`public void load(InputStream inStream)`： 从字节输入流中读取键值对。 

```java
 public class ProDemo2 {
     public static void main(String[] args) throws FileNotFoundException {
         //创建属性集对象
         Properties pro = new Properties();
         //加载文本中信息到属性集
         pro.load(new FileInputStream("read.txt"));
         //遍历集合并打印
         Set<String> strings = pro.stringPropertyNames();
         for (String key : strings ){
             System.out.println(key+" -- "+pro.getProperty(key));
         }
     }
 }
```

> 文本中的数据，必须是键值对形式，可以使用空格、等号、冒号等符号分隔。