---
title: Java基础语法
date: 2018-11-21 10:56:52
tags: 
    - 基础
    - 语法
categories: 
    - Java
---

**目录 start**
 
1. [基础语法](#基础语法)
    1. [代码风格](#代码风格)
    1. [结构](#结构)
        1. [判断](#判断)
        1. [循环](#循环)
    1. [用户输入输出](#用户输入输出)
1. [数据类型](#数据类型)
    1. [基础数据类型](#基础数据类型)
        1. [byte](#byte)
        1. [char](#char)
        1. [boolean](#boolean)
        1. [short](#short)
        1. [int](#int)
        1. [long](#long)
        1. [float](#float)
        1. [double](#double)
    1. [封装类型](#封装类型)
        1. [String](#string)
            1. [StringBuffer和StringBuilder](#stringbuffer和stringbuilder)
        1. [Float](#float)
        1. [Double](#double)
        1. [Integer](#integer)
        1. [Long](#long)
        1. [Boolean](#boolean)
        1. [Void](#void)
    1. [枚举类型](#枚举类型)
    1. [自动拆装箱](#自动拆装箱)
    1. [内部类](#内部类)
    1. [类型强转](#类型强转)
    1. [时间类型](#时间类型)
1. [类的结构](#类的结构)
    1. [修饰符](#修饰符)
        1. [权限修饰符](#权限修饰符)
        1. [其他](#其他)
    1. [成员属性](#成员属性)
    1. [方法](#方法)
1. [Object](#object)
    1. [VO](#vo)
    1. [PO](#po)
    1. [TO](#to)
    1. [BO](#bo)
    1. [POJO](#pojo)
    1. [DAO](#dao)
1. [关键字](#关键字)

**目录 end**|_2019-01-07 23:56_| [码云](https://gitee.com/gin9) | [CSDN](http://blog.csdn.net/kcp606) | [OSChina](https://my.oschina.net/kcp1104) | [cnblogs](http://www.cnblogs.com/kuangcp)
****************************************
# 基础语法

## 代码风格
> [Google Style Guide](https://github.com/google/styleguide) | [阿里巴巴开发手册](/Java/AlibabaJavaStandard.md)

## 结构
### 判断
- if
- switch

### 循环
- while
    - `while(true){}`
    - `do{}while(true);`
- for 循环
    - `for(int a=0; i<10; i++){}`
- for each循环
    - `for(Object item:list){}` 其中list对象如果是通过调用一个对象的方法返回的，那么只会调用一次

## 用户输入输出
- `System.out.println("")` 输出并在末尾追加换行
    - .print() 输出, 行末不换行
    - .printf() 格式化输出, 和C语法类似

***********************
# 数据类型
> [official guide](https://docs.oracle.com/javase/tutorial/java/generics/types.html)

## 基础数据类型
> 八种基本数据类型 byte char boolean short int long float double

> [参考博客: Java 有值类型吗？](http://www.yinwang.org/blog-cn/2016/06/08/java-value-type)

确实, 这样来看Java没有值类型才是更统一的, 不过有没有对程序都是一样的, 因为Java没有解引用, 基本数据类型又没有成员, 所以值还是引用, 没差

### byte
> 字节

Java8以前是使用 char数组 来存放String, Java8开始就是 byte数组 了

### char

### boolean
> [参考 你真的知道Java中boolean类型占用多少个字节吗？](https://www.jianshu.com/p/2f663dc820d0)

### short

### int
> 数值范围 `+- 2147483647` = 2^31-1 也就说明了int是占四个字节 32位 一位是符号位 (操作系统的不同也会有差异)

### long
> 数值范围 `+- 9223372036854775807` = 2^63-1 也就是八个字节 64位 一位是符号位

### float

### double

**************************
## 封装类型
> `wrapper class`基本类型和包装类型不能混为一谈 本质上的 class是不同的, 只不过自动拆装箱才让人感觉没差别

Integer.TYPE == int.class
Byte.TYPE == byte.class
Boolean.TYPE == boolean.class
Double.TYPE == double.class
Void.TYPE == void.class

### String
> 该类是final修饰的, 原因:[知乎问题](https://www.zhihu.com/question/31345592)

- 常量池的实现

- 常见编码转换
    - 一般Windows文件默认编码：`str = new String(str.getBytes("iso8859-1"), "gb2312"); ` 
    - properties文件中获取中文 `str = new String(str.getBytes("utf-8"), "utf-8");`

#### StringBuffer和StringBuilder
> [参考博客](https://blog.csdn.net/rmn190/article/details/1492013)

### Float
### Double
### Integer
### Long
### Boolean

### Void
- void 的包装类型, 常用于反射时对应上 返回值为void的方法(总得有个类型 Void.TYPE) 该类型在 jdk1.1就有了, 1.5出了泛型后, 又多了一个用途(因为泛型不支持原始类型)

> The Void class is an uninstantiable placeholder class to hold a reference to the Class object representing the Java keyword void.

> [参考博客: What is the need of Void class in Java](https://stackoverflow.com/questions/2352447/what-is-the-need-of-void-class-in-java)

> [参考博客: Uses for the Java Void Reference Type?](https://stackoverflow.com/questions/643906/uses-for-the-java-void-reference-type)

1. 在AOP中, 增强根据切点的返回值类型, 做出不同的逻辑, 有可能用到Void
1. Void 强调 the nothing, null 强调 nothing
1. Void 作为方法的返回值时,只能返回 null 

- 案例:  
    - Future<Void>
    - ResponseEntity<Void> 
    - A `Consumer<T>` can be viewed as a `Function<T, Void>`.
    - A `Supplier<T>` can be viewed as a `Function<Void, T>`

> [official api](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletableFuture.html)

> When you use the visitor pattern it can be cleaner to use Void instead of Object when you want to be sure that the return value will be null. Example: 
```java
    public interface LeavesVisitor<OUT>{
    OUT visit(Leaf1 leaf);
    OUT visit(Leaf2 leaf);
    }
```

> When you will implement your visitor you can explicitly set OUT to be Void so that you know your visitor will always return null, instead of using Object

```java
    public class MyVoidVisitor implements LeavesVisitor<Void>{
        Void visit(Leaf1 leaf){
            //...do what you want on your leaf
            return null;
        }
        Void visit(Leaf2 leaf){
            //...do what you want on your leaf
            return null;
        }
    }
```
****************************
## 枚举类型
> [official doc: enum](https://docs.oracle.com/javase/tutorial/java/javaOO/enum.html)

枚举类的构造器必须是private 或者 package private (也就是缺省)

> [参考博客: Java 语言中 Enum 类型的使用介绍](https://www.ibm.com/developerworks/cn/java/j-lo-enum/index.html)
从上面的定义形式来看，似乎 Java 中的枚举类型很简单，但实际上 Java 语言规范赋予枚举类型的功能非常的强大，它不仅是简单地将整形数值转换成对象，而是将枚举类型定义转变成一个完整功能的类定义。

- 简单定义
    - `public enum Color {RED, GREEN, GRAY, BLUE, YELLOW, WHITE, PURPLE, BLACK}`

- 简单单例
```java
    public enum Tool{
        INSTANCE(12); 
        private int num; 
        Tool(int num){
            this.num = num;
        }
        public getNum(){
            return num;
        }
    }
    // 使用的时候
    Tool.INSTANCE.getNum();
```

****************************

## 自动拆装箱
> 基本数据类型和包装类型在Java中是可以视为等价的, 就是因为自动拆装箱的存在

| 基本数据类型 | 封装类型 |
|:----|:----|
| byte | Byte |
| char | Character |
| boolean | Boolean |
| short | Short |
| int | Integer |
| long | Long |
| float | Float |
| double | Double |

> 存在的意义: TODO 

> 实现方式

> 弊端

***************************
## 内部类
> 其域可以和其他常见类型一样, 作为类的成员, 也可作为方法的局部变量, 其中包含的各种变量的域都是按原规则生效的

_但是内部类的属性不能用static修饰_
归根结底，还是类与对象的区别，静态属性不依赖于对象，因为它保存在jvm的静态区，所以访问修改的时候不需要依赖当前有没有存活的对象，在虚拟机加载的时候也是优先于实例生成的。
而实例对象则是保存在jvm的堆内存中，想要访问内部类，必须先实例化外部类，然后通过外部类才能访问内部类。内部类其实也可以认为是外部类的一个成员变量，只要是成员变量，
各个对象都是不依赖的，静态属性的出现破坏了这一逻辑，所以java语言在语义层面不允许我们那么做，这其实不是技术问题，是一个语言的逻辑和语义问题。

> [参考博客: 关于Java内部类字段和方法不能使用static修饰的原因](https://my.oschina.net/u/1027043/blog/1823113)

**************************
## 类型强转
> 数学运算时,数据类型自动往大数据类型转: int float double

- Double -> int 直接(int)num;

- int/Integer -> Long 不能隐式转, 需要 Long.valueOf()

**********************

## 时间类型

1. 最早常用是 Date 然后 Calendar 然后Java8: Instant LocalDateTime ...

_获取指定时间_ [获取指定时间的时间戳](https://blog.csdn.net/jssongwei/article/details/71403354)

******************
# 类的结构
## 修饰符

### 权限修饰符
> [参考博客: java 权限修饰符](https://blog.csdn.net/yan8024/article/details/6426451)

| 权限修饰符 | 范围 | 注释 |
|:----|:----|:----|
| public | 任意范围 |  |
| protected | 子类/同包 | 子类是可以在任意包的 |
| default | 同包 | 同一个包下(也有说是:package private, 缺省) |
| private | 当前类 | 内部类从属于当前类 |

> 同包是指 `package XXX;` 是一致的, `package a;` 与 `package a.b;` 不是同包  

### 其他

## 成员属性
作为Java的bean, 或者大多数情况下, 属性都是私有的, 然后提供setter getter 方法,而且 一般来说, setter和getter方法是不能包含逻辑的, 也就是简单的赋值 取值
乍一看相比于C语言, 似乎这是多此一举, 但是注意面向对象思想, 一个对象对外提供的应该只是行为, 具有较强的语义性, 什么对象执行了什么方法, 而直接引用就可能将对象属性和静态属性混淆

## 方法
方法的签名: 
- [ ] 方法签名的详解

**************
# Object 

> [参考博客:  java的(PO,VO,TO,BO,DAO,POJO)解释](http://www.cnblogs.com/yxnchinahlj/archive/2012/02/24/2366110.html)
> | [VO DAO BO 等缩写的意义](https://zhuanlan.zhihu.com/p/35762537?group_id=969493512006373376)

## VO
> (value object) 值对象
1. 使用new关键字创建的, 由GC回收的, 
2. VO是值对象, 业务对象, 存活在业务层的, 是业务逻辑使用的
    - 它存在的目的就是为数据提供一个生存的地方
3. VO的属性是根据当前业务的不同而不同的
    - 也就是说，它的每一个属性都一一对应当前业务逻辑所需要的数据的名称。

## PO
> (persistant object) 持久对象
1. PO则是向数据库中添加新数据时创建，删除数据库中数据时削除的。
    - 并且它只能存活在一个数据库连接中，断开连接即被销毁。
2. PO是持久化对象, 是有状态的, 每个属性代表其当前状态, 他是物理数据的对象表示
    - 使用它能够让我们的程序与物理数据解耦，并且可以简化对象数据与物理数据之间的转换。
3. PO的属性是跟数据库表的字段一一对应的。
4. PO对象需要实现序列化接口

> 首先说PO和VO吧，它们的关系应该是相互独立的，一个VO可以只是PO的部分，也可以是多个PO构成，同样也可以等同于一个PO（当然我是指他们的属性）。
正因为这样，PO独立出来，数据持久层也就独立出来了，它不会受到任何业务的干涉。又正因为这样，业务逻辑层也独立开来，它不会受到数据持久层的影响，业务层关心的只是业务逻辑的处理，至于怎么存怎么读交给别人吧！
不过，另外一点，如果我们没有使用数据持久层，或者说没有使用hibernate，那么PO和VO也可以是同一个东西，虽然这并不好。

## TO
> (transfer Object) 数据传输对象
- 在应用程序不同tie(关系)之间传输的对象

## BO
> (business object) 业务对象
- 从业务模型的角度看,见UML元件领域模型中的领域对象。封装业务逻辑的java对象,通过调用DAO方法,结合PO,VO进行业务操作。
- 它装满了业务逻辑的处理，在业务逻辑复杂的应用中有用。

## POJO
> [Wikipedia: POJO](https://en.wikipedia.org/wiki/Plain_old_Java_object) `Plain Old Java Object`

> (plain ordinary java object) 简单无规则java对象
- 纯的传统意义的java对象。就是说在一些Object/Relation Mapping工具中，能够做到维护数据库表记录的persisent object完全是一个符合Java Bean规范的纯Java对象，没有增加别的属性和方法。我的理解就是最基本的Java Bean，只有属性字段及setter和getter方法！

## DAO
> (data access object) 数据访问对象
- 通常和PO结合使用，DAO中包含了各种数据库的操作方法

*************************
# 关键字
>  Java关键字和保留字

|||||||||
|:----|:----|:----|:----|:----|:----|:----|:----|
| abstract | class    | extends | implements | null      | strictfp     | true
| assert   | const    | false   | import     | package   | super        | try
| boolean  | continue | final   | instanceof | private   | switch       | void
| break    | default  | finally | int        | protected | synchronized | volatile
| byte     | do       | float   | interface  | public    | this         | while
| case     | double   | for     | long       | return    | throw
| catch    | else     | goto    | native     | short     | throws
| char     | enum     | if      | new        | static    | transient

- [ ]  transient 序列化时不进行序列化