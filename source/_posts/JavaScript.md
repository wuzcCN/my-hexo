---
title: JavaScript
copyright_url: https://www.aobayu.cn/2022/08/29/JavaScript/
tags: 
    - JavaScript
    - JQuery
categories: 学习之路
date: 2022-8-29
keywords: JavaScript
description: JavaScript（简称“JS”）是一种具有函数优先的轻量级，解释型的编程语言。基于原型编程、多范式的动态脚本语言，并且支持面向对象、命令式和声明式风格。--本文为自己学习中所写，包括JavaScript~jQuery，jQuery在本文最后，附带中文在线手册速查。
---

## 快速入门

### 引入JavaScript

1. script标签内，写与javascript代码

   ```html
   <script type="text/javascript"> 
       alwrt('hello,world');
   </script>
   ```

2. 外部引入

   ```html
   <script src="./index.js"> </script>
   ```

### 基本语法入门

```html
<script>
    // 1．定义变量 变量类型 变量名=变量值;
    var score = 71;
    // alert(score);
    //2．条件控制
    if (score>60 && score<70){
    	alert("60~70")
    }else if(score>70 && score<80){
    	alert("70~80")
    }else{
    	alert("other")
    }
	//console.log(score）在浏览器的控制台打印变量!system.out.println();
</script>
```

## 数据类型

### 字符串

1. number    

   js不区分小数和整数

2. 字符  "abc"

3. 布尔值  2>1 true

   true false

4. **逻辑运算  &&     ||   !**

- &&两边都是真，结果才是真: true

- 或 ||有一个是真  结果就是真

- 非 ！取反

5. **比较运算符**

- = =等于（类型不一样，值一样，也会判断为true)

- === 绝对等于

- NaN===NaN，这个与所有的数值都不相等，包括自己
-  只能通过isNaN(NaN)来判断这个数是否是NaN
   
6. null和undefined
- null空 
- undefined未定义

7. Java的数组必须是相同类型的对象~，JS中不需要这样!

   ```javascript
   var arr = [1,2,3,4,5 , 'hello ' ,null,true];
   
   //取数组下标:如果越界了，就会undefined   console.log(arr[7]）
   ```

8. 对象是大括号，数组是中括号

   每个属性之间使用逗号隔开，最后一个不需要添加

   ``` javascript
   var person = {
       name: "wzc",
       age: "12",
       tage: ['js','java','web']
   }
   //person.name
   ```

### 数组

 **Array可以包含任意的数据类型**

```javascript
  var arr = [1,2,3,4,5,6];
  arr[0]
//arr[0] = 1
```

1、长度

```javascript
//arr.length
```

注意:加入给arr.length赋值，数组大小就会发生变化~，如果赋值过小，元素就会丢失

2、indexOf,通过元素获得下标索引   

```javascript
  arr.indexOf(2)
//1
```

字符串的“1”和数字1是不同的

3、**slice () **截取Array的一部分，返回一个新数组，类似于String中的substring

4、push(),pop() 尾部

```javascript
arr.push(元素)//压入到尾部
arr.pop(元素)//弹出尾部的一个元素
```

5、unshift(),shift() 头部

```javascript
arr.unshift(元素)//压入到头部
arr.shift(元素)//弹出头部的一个元素
```

6、排序sort()

```javascript
arr.sort(元素)
```

7、includes 查找字符串是否包含

```html
<script>
        var arr = new Array()
        for( var i =0;i<50;i++){
            //Math.ceil(Math.random( )*100)1到100的随机数
            // arr[i] = Math.ceil(Math.random( )*100)
            var anyNum = Math.ceil(Math.random()*100)
            if(arr.includes(anyNum)){
                i--
                continue
            }
            arr.push(anyNum)
        }
        console.log(arr)
</script>
```



8、元素反转reverse()

```javascript
  arr.reverse()
//['1','2','3']
//['3','2','1']
```

9、concat()

```javascript
//[1,2,3]
  arr.concat(["A","B","C"])
//[1,2,3,"A",'B','C']
  arr
//[1,2,3]
```

注意: concat ()并没有修改数组，只是会返回一个新的数组

10、连接符join

打印拼接数组，使用特定的字符串连接

```javascript
//["C","B","A"]
  arr.join('-')
//"C-B-A"
```

11、多维数组

```javascript
  arr = [[1,2],[3,4],["5","6"]];
  arr[1][0]
//3
```

数组:存储数据(如何存，如和取，方法都可以自己实现!)

### 对象

```javascript
var 对象名= {
    属性名:属性值,
	属性名:属性值,
}

var person = {
    name: "wzc",
    age: 22,
    email: "3285458564"
}
```

Js中对象，{..…}表示一个对象，键值对描述属性xxx: xx，多个属性之间使用逗号隔开，最后一个属性不加逗号!

JavaScript中的所有的键都是字符串，值是任意对象!

1、对象赋值

```javascript
person.name = "www"
```

2、使用一个不存在的对象属性，不会报错!

```javascript
  person.haha
//undefined
```

3、动态的删减属性

```javascript
  delete person.name
//true
//person
```

4、动态的添加

```javascript
  person.fafa = "fafa"
//"fafa"
  person
```

5、判断属性值是否在这个对象中!xxx in xxx!

```javascript
  'age' in person
//true
//继承
  'toString' in person
//true
```

6、判断一个属性是否是这个对象自身拥有的hasOwnProperty()

```javascript
  person.hasOwnProperty('toString')
//false
  person.hasOwnProperty('age')
//true
```

### 流程控制

1、if判断

```javascript
var age = 3;
if(age>3){
    alert("haha");
}else if(age<5){
    alert("kuku");     
}else{
    alert("yuyu");
}

let money = prompt("你有钱吗?")
//						true	false
let ren = money > 100 ? "有钱" : "没钱"
```

2、while循环，避免程序死循环

```javascript
while(age<10){
    age = age++;
    console.log(age)
}
```

3、for循环

```javascript
for(let i = 0; i < 100; i++){
    console.log(i)
}
```

4、forEach循环

```javascript
var age = [22,54,52,12,6,23]
age.forEach(function (value){
    console.log(value)
})
```

5、for....in

```javascript
//for(var index in object){}
//for in 下标
for(var num in age){
    if(age.hasOwnProperty(num)){
        console.log(num)//console.log(age[num])
    }
}
//for of 数值
for(var x of age){
    console.log(x)
}   
```

6、switch

```javascript
age = 10;
switch(age){
    case 10:
        console.log("pbq")
    break;
    case 9:
        console.log("p")
    break;
    case 8:
        console.log("b")
    break;
    default:
        console.log("q")
    break;
}
```

7、 break和continue

**break** :在循环的过程中，在满足某些条件的情况下，中断循环的执行。

注意: switch 中的break用于结束某个分支。而循环中的 break 是中断循环的。

```javascript
for (var i = 1; i <= 10; i++) {
            if (i == 5) {
                //中断循环 
                break;
            }
        document.write(i + "<br/>");
    }
document.write("循环结束");
```



**continue** :在循环的过程中，在满足某些条件的情况下，跳过循环中的部分代码不执行，直接进入下次循环。

```javascript
for (var i = 1; i <= 10; i++) {
            if (i == 5) {
                //跳过continue后面的代码，进入循环的下一步 
                continue;
            } 
    	document.write(i + "<br/>");
	}
document.write("循环结束");
```



### Map和Set

1、map

```javascript
var map = new Map([['www',63],['qqq',87],['eee',89]]);
var name = map.get('www');//通过key获得value
map.set('rrr'.36);//新增或修改
map.delete("qqq")////删除
console.log(name);
```

2、Set:无序不重复的集合

```javascript
var set = new Set([3,1,1,1,1]); //set可以去重
set.add (2);//增加
set.delete("1");//删除
console.log(set.has(3));//true ||false
```

### iterator

1、遍历数组

```javascript
var arr = [3,4,5];
for(var x of arr){
    console.log(x)
}
```

2、遍历map

```javascript
var map = new Map([["tom",100],["jack",90],["haha",80]]);
for(let x of map){
    console.log(x)
}
```

3、遍历set

```javascript
var set = new Set([5,6,7]);
for(let x of set){
    console.log(x)
}
```

## 函数

### 定义函数

```javascript
public 返回值类型 方法名(){
	return 返回值;
}
```

**绝对值函数**

> 定义方式一

```javascript
function abs(x){
    if(x>=0){
		return x;
    }else{
        return -x;
    }
}
```

一旦执行到return代表函数结束，返回结果!

如果没有执行return，函数执行完也会返回结果，结果就是undefined

> 定义方式二

```javascript
var abs = function(x){
    if(x>=0){
		return x;
    }else{
        return -x;
    }
}
```

> 定义方式三

```javascript
var abs = (x)=>{
    if(x>=0){
		return x;
    }else{
        return -x;
    }
}
```

常规函数，**this** 表示调用该函数的对象：

```javascript
// 常规函数：
hello = function() {
  document.getElementById("demo").innerHTML += this;
}

// window 对象调用该函数：
window.addEventListener("load", hello);

// button 对象调用该函数：
document.getElementById("btn").addEventListener("click", hello);
```

箭头函数， **this** 则表示函数的拥有者：

```javascript
// 箭头函数：
hello = () => {
  document.getElementById("demo").innerHTML += this;
}

// window 对象调用该函数：
window.addEventListener("load", hello);

// button 对象调用该函数：
document.getElementById("btn").addEventListener("click", hello);
```

function(x) {...}这是一个匿名函数。但是可以把结果赋值给abs，通过abs就可以调用函数!

> 调用函数

```javascript
abs(10)
abs(-10)
```

> 假设不存在参数，如果规避?

```javascript
var abs = function(x){
    //手动抛出异常来判断
    if (typeof x !== 'number'){
    	throw "Not a Number';
	}
    if(x>=0){
		return x;
    }else{
        return -x;
    }
}
```

> arguments是一个JS免费赠送的关键字;
> 代表，传递进来的所有的参数，是一个数组!

```javascript
var abs = function(x){
    
    console.log("x=>"+x);
    for(var i = 0; i < arguments.length; i++){
        console.log(arguments[i]);
    }
    
    if (typeof x !=  'number'){
    	throw "Not a Number';
	}
    
}
```

问题: arguments包含所有的参数，我们有时候想使用多余的参数来进行附加操作。需要排除已有参数

> rest ES6引入的新特性 arguments 升级版，获取除了已经定义的参数之外的所有参数...

```javascript
function aaa(a,b, ...rest) {
	console.log( "a=>"+a);
    console.log( "b=>"+b);
    console.log(rest);
}
```

rest参数只能写在最后面，**必须用...标识**。

### 变量的作用域

在javascript中, var定义变量实际是有作用域的。

1、假设在函数体中声明，则在函数体外不可以使用

```javascript
function qi(){
    var x =1;
    x = x+1;
}
x = x+2;//Uncaught ReferenceError: x is not defined
```

2、如果两个函数使用了相同的变量名，只要在函数内部，就不冲突

```javascript
function qi(){
    var x = 1;
    x = x + 1;
}
function qi2(){
    var x = 'A';
    x = x +1 ;
}
```

3、内部函数可以访问外部函数的成员，反之则不行

```javascript
function qj() {
	var x= 1;
	//内部函数可以访问外部的成员，反之则不行
    function qj2(){
		var y = x + 1;// 2
	}
	var z = y + 1; // Uncaught ReferenceError: y is not defined
}

```

假设，内部函数变量和外部函数的变量，重名!

假设在JavaScript中函数查找变量从自身函数开始，由“内”向“外”查找

```javascript
function qj() {
	var x= 1;
    function qj2(){
		var x = 'A';
        console.log('a'+x);
	}
	console.log('1'+x);
    qj2()
}
```

> 提升变量的作用域

```javascript
function qi(){
    var x = "x" + y;
    console.log(x);
    var y = 'y';
}
```

结果: xundefined
说明: js执行引擎，自动提升了y的声明，但是不会提升变量y的赋值;

```javascript
function qi(){
    var x = "x",
        y = 2,
        z,v;
    z = 5;
}
```

这个是在JavaScript建立之初就存在的特性。

养成规范:所有的变量定义都放在函数的头部，不要乱放，便于代码维护;

> 全局函数

```javascript
//全局函数
x = 1;
function qi(){
    console.log(x);
}
qi();
console.log(x);
```

全局对象 window

```javascript
var x = 'xxx';
alert(x);
alert(window.x);//默认所有的全局变量，都会自动绑定在 window对象下;
```

alert()这个函数本身也是一个 window 变量

```javascript
var x='XXX';
window. alert(x);
var o1d_alert = window.alert;
//o1d_alert(x);
window.alert = function(){
    
};
//发现alert(失效了
window.alert(123);
//恢复
window.alert = o1d_alert;window.alert(456);
```

Javascript实际上只有一个全局作用域，任何变量（函数也可以视为变量)，假设没有在函数作用范围内找到，就会向外查找，如果在全局作用域都没有找到，报错RefrenceError

> 由于我们所有的全局变量都会绑定到我们的window 上。如果不同的js文件，使用了相同的全局变量，冲突~>如果能够减少冲突?

```javascript
//唯一全局变量
var App = {};
//定义全局变量
App.name = ' haha ' ;
App.add = function (a,b) {
	return a + b;
}
```

减少冲突: 把自己的代码全部放入自己定义的唯一空间名字中，降低全局命名冲突的问题~

> 局部作用域let 

```javascript
function aaa(){
	for (var i = 0; i < 100;i++) {
		console.log(i)
	}
console.log(i+1);//问题 i 出了这个作用域还可以使用
}
```

let关键字，解决局部作用域冲突问题!

```javascript
function aa(){
	for (let i = 0; i < 100; i++) {
		console.log(i)
	}
conso1e.log(i+1);//uncaught ReferenceError: i is not defined
}
```

建议大家都是用let去定义局部作用域的变量;

> 常量const

在ES6之前，怎么定义常量: 只有用全部大写字母命名的变量就是常量;建议不要修改这样的值?

```javascript
var PI = '3.14';
console.log(PI);
PI = '213'; //可以改变这个值conso1e.log(PI);
console.log(PI);
```
在ES6后用常量const
```javascript
const PI = '3.14'; //只读变量
console.log(PI);
PI = '123';
```

### 方法

> 定义方法

方法就是把函数放在对象的里面，对象只有两个东西: 属性和方法

```javascript
var haha = {
	name: '哈哈哈',
	bitrh: 2000,
	//方法
	age: function(){
		//今年 –出生的年
		var now = new Date().getFullYear();
        return now-this.bitrh;
	}
}
//属性
////方法一定要带()
alert(haha.age())
```

this. 代表什么?

```javascript
function getAge(){
		//今年 –出生的年
		var now = new Date().getFullYear();
        return now-this.bitrh;
	}
var haha = {
	name: '哈哈哈',
	bitrh: 2000,
	age: getAge
}
alert(haha.age())
```

this是无法指向的，是默认指向调用它的那个对象;

>apply

在js中可以控制this指向

```javascript
function getAge() {
    //今年 –出生的年
    var now = new Date().getFullYear();
    return now - this.bitrh;
}
var haha = {
    name: '哈哈哈',
    bitrh: 2000,
    age: getAge
};
  	getAge.apply(haha, []); //this，指向了haha，参数为空
    alert(haha.age())
```

onclick :元素的单击事件

```html
<div id="dl">

</div>
<script>
dl.onclick = function(){
    alert("111")
}
</script>
```

onload :页面加载完成事件

```html
<script>
dl.onload = function(){
    alert("222")
}
</script>
<div id="dl">

</div>
```

## 内部对象

> 标椎对象  object

### Date

基本使用

````javascript
var now = new Date();
console.log(now)//Thu Aug 18 2022 17:00:52 GMT+0800 (中国标准时间)
now.getFullYear();//年
now.getMonth();//月
now.getDate();//日
now.getDay();//星期
now.getHours();//时
now.getMinutes();//分
now.getSeconds();//秒
now.getTime();//时间戳
console.log(new Date(1578106175991))//时间戳转为时间
````

转换

```javascript
now.toLocalesString(); 注意，调用是一个方式，不是一个属性!
now.toGMTString();
```

### JSON

> jsonjson是什么

早期，所有数据传输习惯使用XML文件!

- <u>JSON</u>(JavaScript Object Notation, JS对象简谱)是一种轻量级的数据交换格式。
- 简洁和清晰的**层次结构**使得JSON成为理想的数据交换语言。
- 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。

在JavaScript一切皆为对象、任何js支持的类型都可以用JSON来表示格式

- 对象都用{}
- 数组都用[]
- 所有的键值对都是用 key:value

> JSON字符串和JS对象的转化

```javascript
var user = {
            name: "xiaoming",
            age: 3,
            sex: '男'
  }
//对象转化为json字符串 { "name" : "xiaoming" , "age" : 3, "sex":"男"}
var jsonuser = JSON.stringify(user);
//json字符串转化为对象参数为json字符串
var obj = JSON.parse('{"name" : "xiaoming" , "age" : 3, "sex" :"男"}');
```

### Ajax

- 原生的js写法  xhr异步请求
- jQuey封装好的方法 $("#name").ajax("")
- axios请求

## 面向对象编程

> 什么是面向对象

javascript、Java、c#......面向对象;javascript有些区别!·

- 类:模板

- 对象:具体的实例

在JavaScript这个需要大家换一下思维方式!

> 面向对象原型继承

```javascript
var student = {
            name: "xiaoming",
            age: 3,
            run: function () {
                console.log(this.name + " run. . ..");
            }
        };

        student.run();

        var xiao = {
            name: "xiao"
        };
		//原型对象
        xiao.__proto__ = student;
        
        xiao.run();

		var Bird = {
            f1y: function () {
                console.log(this.name + " f1y.. .. ");
            }
        };
        //小的原型是student
        xiaoming.__proto__ = Bird;

        xiaoming.f1y();
```

```javascript
function student(name) {
            this.name = name;
        }
        //给student新增一个方法
        student.prototype.hello = function (){
            alert('Hello')
        };
```



> 面向对象class继承

class关健字，是在ES6引入的
1、定义一个类，属性，方法

```javascript
//ES6之后=========EEEE
//定义一个学生的类
        class student {
            constructor(name) {
                this.name = name
            }
            hello() {
                alert(" hello")
            }
        }
	var xiaoming = new student("xiaoming");
    var xiaohong = new student("xiaohong");
xiaoming.hello()
```

2、继承

```javascript
class student {
            constructor(name) {
                this.name = name
            }
            hello() {
                alert(" hello")
            }
        }
        class xiaostudent extends student {
            constructor(name, grade) {
                super(name);
                this.grade = grade;
            }
            myGrade() {
                alert('我是一名小学生')
            }
        }

        var xiaoming = new student("xiaoming");
        var xiaohong = new xiaostudent("xiaohong",1);
```

本质:查看对象原型  __ proto__

> 原型链

简单的回顾一下构造函数、原型和实例的关系:每个构造函数都有一个原型对象，原型对象都包含一个指向构造函数的指针，而实例都包含一个指向原型对象的内部指针。那么假如我们让原型对象等于另一个类型的实例，结果会怎样?显然，此时的原型对象将包含一个指向另一个原型的指针，相应地，另一个原型中也包含着一个指向另一个构造函数的指针。假如另一个原型又是另一个类型的实例，那么上述关系依然成立。如此层层递进，就构成了实例与原型的链条。这就是所谓的原型链的基本概念。——摘自《javascript高级程序设计》

## 操作BOM对象(重点)
> 浏览器介绍

JavaScript和浏览器关系?

javaScript 诞生就是为了能够让他在浏览器中运行!

BOM:浏览器对象模型

- IE 6~12
- Chrome
- Safai
- FireFox

>window

window代表浏览器窗口
```javascript
//大家可以调整浏览器窗口
window.alert(1)
undefined
window.innerHeight
258
window.innerwidth
919
window.outerHeight
994
window.outerwidth
919
win = window.open("https: / / cn.bing.com" , "" , "width=300 , height=300")
//打开子窗口
win.close()//关闭窗口
```

> Navigator

Navigator 封装了浏览器的信息

```javascript
navigator.appName
"Netscape"
navigator.appversion
"5.o"
navigator.userAgent
"Mozi11a/5.o (windowsGecko) chrome/63.0.32:"
navigator.platform
"win32"
```

大多数时候，我们不会使用navigator对象，因为会被人为修改!
不建议使用这些属性来判断和编写代码

> screen

代表屏幕尺寸

```javascript
screen.width
1920
screen.height
1080
```

> location(重要)

location代表当前页面的URL信息)

```javascript
host: "www.baidu. com"
href: "https : / /www.baidu. com/"
protocol : "https : "
reload:f reload() //刷新网页//设置新的地址
location.assign('https: //b1og.kuangstudy. com/ ')
```

> document

document代表当前的页面，HTML  DOM文档树

```javascript
  document.title
//"百度一下，你就知道"
  document.title='Aobayu'
//"Aobayu"
```

获取具体的文档树节点

```html
<dl id="app">
    <dt>Java</dt>
    <dd>JavasE</dd>
    <dd>JavaEE</dd>
</dl>
<script>
	var dl = document.getElementById( 'app');
</script>
```

获取cookie

```javascript
  document.cookie
//"__guid=111872281.88375976493059340.1578110638877.133;monitor_count=1"
```

劫持cookie原理

```html
<script src="aa.js"></script>
<!--恶意人员;获取你的cookie上传到他的服务器-->
```

服务器端可以设置cookie: httpOnly

> history  (不建议使用)

history代表浏览器的历史记录

```javascript
history.back()//后退
history.forward()//前进
history.go(1)
```

> window.open 用于打开一个新的浏览器窗口或查找一个已命名的窗口

```html
 <!--history历史记录对象  -->
    <div>
        <h1>春天</h1>
        <a href="summer.html">访问夏天</a>
        <a href="javascript:history.forward()">下一页</a>
    </div>

<!--summer.html-->
	<h1>夏天</h1>
    <a href="javascript:history.back()">上一页</a>
<!-- location地址栏对象 -->
    <div>
        <select id="we" onchange="goWe()">
            <option value="">请选择</option>
            <option value="http://www.baidu.com">百度</option>
            <option value="http://www.taobao.com">淘宝</option>
            <option value="http://www.jd.com">京东</option>
        </select>
    </div>
    <script type="text/javascript">

        function goWe() {
            var site = document.getElementById("we").value;
            if (site != "") {
                window.location.href = site
            }

        }

    </script>
<!--window.open('新窗口的页面路径','新窗口的名称','新窗口的属性设置')  -->
    <button type="button" onclick="openWin()">打开窗口</button>
    <button type="button" onclick="closeWin()">关闭窗口</button>
    <script>
        var subWin;
        let openWin = () => {
            subWin = window.open("http://www.baidu.com", "","width=650,height=400")
        }

        let closeWin = () => {
            subWin.close();
        }
    </script>
    <!-- 
        setTimeout(函数名,延时时间) :延迟指定的时间后，执行一次函数
        var t = setInterval(函数名,延迟时间) :每隔指定的延迟时间，就执行一次函数
		将定时器对象清除，结束定时器效果
		clearTimeout(t);
    -->
```

> event 绑定函数

```html
	//当鼠标移动时，显示鼠标的坐标位置 
    //event:封装了事件发生时相关信息的事件对象 
    //		:这个对象有浏览器在事件发生时自动创建出来。
    // 		:并通过函数参数的方式，传给函数。
    <script type="text/javascript">
        let eve = (e) => {
            let div = document.getElementById("dl");
            //通过事件对象可以获取事件中存储的鼠标位置：x,y
            div.innerHTML=e.clientX +" "+ e.clientY;
            //通过事件对象可以获取事件中存储的鼠标位置：x,y
            div.style.left = e.clientX + "px";
            div.style.top = e.clientY + "px";
        }
        document.onmousemove = eve;
		//绑定鼠标移动事件
    </script>

    <div id="dl" style="position:absolute; border: 1px solid red;">
    </div>
```



## 操作DOM对象(重点)

DOM:文档对象模型

> 核心

浏览器网页就是一个Dom树形结构!

- 更新:更新Dom节点
- 遍历dom节点:得到Dom节点
- 删除:删除一个Dom节点
- 添加:添加一个新的节点

要操作一个Dom节点，就必须要先获得这个Dom节点

```html
<div id="father">
	<h1>标题一</ h1>
	<p id="p1">p1</p>
    <p class="p2">p2</p>
</div>

//对应 css选择器
<script>
var h1 = document.getElementsByTagName( 'h1');
var p1 = document.getElementById( 'p1');
var p2 = document.getElementsByc1assName( 'p2 ');
var father = document.getElementById( 'father ');
var childrens = father.children;
//获取父节点下的所有子节点
// father.firstchild
// father.lastchild
</script>
```

这是原生代码，之后我们尽量都是用jQuery();

> 更新节点

操作文本

- id.innerText='456'  修改文本的值
- id.innerHTML='<strong>123</strong>'  可以解析HTML文本

操作js

```javascript
id.style.color = 'red' //属性使用字符串包裹
id.style.fontSize = '20px'
```

> 删除节点

删除节点的步骤:  先获取父节点，在通过父节点删除自己

```html
<div id="father">
	<h1>标题一</ h1>
	<p id="p1">p1</p>
    <p class="p2">p2</p>
</div>
<script>
    var self = document.getElementById( 'p1');
    var father = self.parentElement;
	father. removechild(self)
    //删除是一个动态的过程;
	father.removechild(father.children[0])
</script>
```

注意: 删除多个节点的时候，children是在时刻变化的，删除节点的时候一定要注意!

>插入节点

我们获得了某个Dom节点,假设这个dom节点是空的，我们通过innerHTML 就可以增加一个元素了，但是这个DOM节点已经存在元素了，我们就不能这么干了

追加

```html
<p id="js">Javascript</p>
<div id="list">
	<p id="se">avaSE</p>
    <p id="ee">avaEE</p>
    <p id="me">avaME</p>
</div>
<script>
	var js = document.getE1ementById('js');
    var list = document.getE1ementById('list');
    list.appendchild(js);//追加到后面
</script>

```
创建节点

```html
<p id="newP"></p>
<div id="list">
	<p id="se">avaSE</p>
    <p id="ee">avaEE</p>
    <p id="me">avaME</p>
</div>
<script>
//通过js创建一个新的节点
var newP = document.createElement('p');//创建一个p标签
    newP.id = 'newP' ;
	newP.innerText = 'Hello,Kuangshen' ;
    List.appendchild(newP);//把创建好的p添加List上

</script>
```

创建一个标签节点

```html
<style>
    
</style>
<script type="text/javascript" src="">
    
</script>

<script>
//创建一个标签节点
var myscript = document.createElement('script');
    myScript.setAttribute( 'type','text/javascript')
    
//可以创建一个Style标签
var myStyle= document.createElement( 'style');//创建了一个空styLe标签
    myStyle.setAttribute( 'type' ,'text/css' );
myStyLe.innerHTML = 'body{ background-color: chartreuse;}';//设置标签内容
    document.getElementsByTagName( 'head')[0].appendChild(myStyle)

</script>
```

> insert 向某个标签中添加数据行

```html
<p id="js">javaScript</p>
	<div id="list">
		<p id="se">JavaSE</p>
        <p id="ee" >avaEE</p>
        <p id="me" >avaME</p>
	</div>
<script>
	var ee = document.getElementById( 'ee' ) ;
    var js = document.getElementById( 'js' );
    var list = document.getElementById( 'list ' );
    //要包含的节点.insertBefore(newNode,targetNode)
    list.insertBefore(js,ee);
</script>
```

## 操作表单(验证)

> 表单是什么form DOM树

- 文本框text
- 下拉框< select >
- 单选框radio
- 多选框checkbox
- 隐藏域hidden
- 密码框password

表单的目的:提交信息

> 获得要提交的信息

```html
</p>
    <input type="text" id="username" value="hahaha">
    绑定同一个
    <p>
        <span>性别: </span>
        <!--多选框的值，就是定义好的value -->
        <input type="radio" name="sex" value="man" id="boy">男
        <input type="radio" name="sex" value="women" id="gir1">女
    </P>
    </form>
    <script>
        var input_text = document.getElementById("username");
        var boy_radio = document.getElementById("boy");
        var gir1_radio = document.getElementById("gir1");
        //得到输入框的值
        input_text.value
        //修改输入框的值
        input_text.value = '123'
        //对于单选框，多选框等等固定的值，boy_radio.value只能取到当前的值
        boy_radio.checked;
        //查看返回的结果，是否为true，如果为true，则被选中~
        //赋值
        boy_radio.checked = 'true'
    </script>
```

> 提交表单

```html
<form action="https://fanyi.baidu.com/" method="post" onsubmit="return get()">
<div>
  <span>用户名:</span> <input type="text" id="username"  name="username">
</div>
  
     <div>
          <span>密码:</span> <input type="password" id="password">
      </div>
      <input type="hidden" id="md5-password" name="password">
  
          <!--绑定事件onclick被点击-->
      <input type="submit"  value="提交" >
    <!--<input type="submit"  value="提交" onclick="get()">-->
          
          
      </form>
      <script type="text/javascript">
          function get(){
              let user = document.getElementById("username")
              let pass = document.getElementById("password")
              let md5pwd = document.getElementById("md5-password")
              md5pwd.value = md5(pass.value);//md5加密
              return true
          }
      </script>
	<!--MD5在线链接-->
<script src="https://cdn.bootcss.com/blueimp-md5/2.10.0/js/md5.min.js"></script>
```

> 简单实例

```html
<form action="" method="get" onsubmit="return submits()">
        <input type="text" id="name">账号
        <br>
        <input type="password" name="" id="password">密码
        <br>
        <input type="email" name="" id="email">email
        <br><hr>
        <input type="submit" value="提交" id="submit">
    </form>
<script>
    function $(e){
        return document.getElementById(e)
    }

    function submits(){
        //账号
        let name = $("name").value;
        var nameNode =	/^[a-z0-9_-]{3,16}$/;
        if( nameNode.exec(name) == null ){
            alert("用户名不能为空，必须是字母和数字");
            return false
        }
        //密码
        let password = $("password").value;
        var passwordNode = /^(?![0-9]+$)(?![a-zA-Z]+$)[0-9A-Za-z]{6,18}$/;
        if(passwordNode.exec(password) == null){
            alert("密码必须是大于6位的字母加数字");
            return false
        }
        //email
        let email = $("email").value;
        var emails = /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
        if(emails.exec(email)==null){
            alert("邮箱有误");
            return false
        }
        
    }
</script>
```



## jQuery
JavaScript
jQuery库，里面存在大量的Javascript函数

[Download jQuery | jQuery下载](https://jquery.com/download/)

 [jQuery API 中文文档 | jQuery API 中文在线手册 | jquery api 下载 | jquery api chm (cuishifeng.cn)](https://jquery.cuishifeng.cn/)

> 获取jQuery

```html
<!--cdn引入-->
<script src="https://cdn.bootcss.com/jquery/3.4.1/core.js"></script>
<!--在线引入-->
<script src="lib/jquery-3.4.1.js"></script>
```

>使用:  $ (selector).action()

```html
	<!-- 公式:$ (selector).action() -->

    <a href="" id="test-jquery">点我</a>
	<script>
        //选择器就是css的选择器
        $('#test-jquery').click(function () {
            alert('hello,jQuery');
        })
	</script>
```

>选择器

```javascript
//原生js，选择器少，麻烦不好记
//标签
document.getElementsByTagName();//id
document.getE1ementById();//类
document.getE1ementsByclassName();

//jQuery css中的选择器它全部都能用!
$('p').click(); //标签选择器
$('#id1').click(); //id选择器ssss
$('.c1ass1').click(); //class选择器
```

> jQuery事件

```html
 	<!--要求:获取鼠标当前的一个坐标-->
    mouse : <span id="mouseMove"></span>
    <div id="divMove" style="border:1px solid red ; height: 300px;">
        在这里移动鼠标试试
    </div>

    <script>
    //当网页元素加载完毕之后，响应事件
    $( function () {
        $('#divMove').mousemove(function (e) {
            $('#mouseMove').text( 'x : '+e.pageX + 'y : '+e.pageY)
        })
    });
        // 当网页元素加载完华之后，响应事件
        // 两种写法
        // $(document).ready( function(){

        // });
        
        // $(function(){

        // });
        </script>
    </script>
```

> 操作DOM

节点文本操作

 ```html
<script>
$('#test-ul li[name=python]' ).text();//获得值
$('#test-u1 li[name=python]' ).text('设置值');//设置值
$('#test-ul').html();//获得值
$('#test-ul').html('<strong>123<strong>');//设置值
</script>
 ```

css的操作

```html
<script>$('#test-ul li[name=python]' ).css({"color","red"})</script>
```

元素的显示和隐藏: 本质display : none

```html
<script>
$('#test-ul li[name=python]').show()//显示
$('#test-ul li[name=python]').hide()//隐藏
//$(window).width()
</script>
```
