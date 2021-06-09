 ## 一、数据类型

### 基本类型

- byte/8
- char/16
- short/16
- int/32
- float/32
- long/64
- double/64
- boolean/~

**补充一个表，字节数、数据范围、缓冲池范围**
![[Pasted image 20210531104802.png]]
boolean 只有两个值：true、false，可以使用 1 bit 来存储，但是具体大小没有明确规定。JVM 会在编译时期将 boolean 类型的数据转换为 int，使用 1 来表示 true，0 表示 false。JVM 支持 boolean 数组，但是是通过读写 byte 数组来实现的

`Byte`,`Short`,`Integer`,`Long` 这 4 种包装类默认创建了数值 **\[-128，127\]** 的相应类型的缓存数据，`Character` 创建了数值在\[0,127\]范围的缓存数据，`Boolean` 直接返回 `True` Or `False`。两种浮点数类型的包装类 `Float`,`Double` 并没有实现常量池技术。缓存的范围区间的大小只是在性能和资源之间的权衡。


### 包装类型

基本类型都有对应的包装类型，基本类型与其对应的包装类型之间的赋值使用自动装箱与拆箱完成。



### 向上转型和向下转型





数组本身是一个引用数据类型



## 二、Object类

### 概览

Object类是所有类的父类，所有Java对象可调用Object类的方法，

| 方法                   | 说明                                                         |
| :--------------------- | :----------------------------------------------------------- |
| Object clone()         | 创建与该对象的类相同的新对象                                 |
| boolean equals(Object) | 比较两对象是否相等                                           |
| int hashCode()         | 返回该对象的散列码值                                         |
| String toString()      | 返回该对象的字符串表示                                       |
| Class getClass()       | 返回一个对象运行时的实例类                                   |
| void finalize()        | 当垃圾回收器确定不存在对该对象的更多引用时，对象垃圾回收器调用该方法 |
| void notify()          | 激活等待在该对象的监视器上的一个线程                         |
| void notifyAll()       | 激活等待在该对象的监视器上的全部线程                         |
| void wait()            | 在其他线程调用此对象的 notify() 方法或 notifyAll() 方法前，导致当前线程等待 |

### getClass() 方法

getClass() 方法返回对象所属的类，是一个 Class 对象。通过 Class 对象可以获取该类的各种信息，包括类名、父类以及它所实现接口的名字等。



hashcode如何计算？

hashCode是为了产生一段数值，使两个内容相等的对象，hashcode值相同。如果不重写hashcode方法，会调用Object的hashCode方法，导致两个对象永远不会相同。

equals方法和 == 的区别



equals为true 和 hashcode码的关系



hash值如何计算？

### Object类和泛型














## 三、 Class类





## 四、String类

String为什么是线程安全的？

​		String具有不变性，也就是说一经创建，不可改变。存储在String pool中，



> 什么是线程安全?
>
> ​		当多个线程访问某一个类（对象或方法）时，对象对应的公共数据区始终都能表现正确，那么这个类（对象或方法）就是线程安全的。
>
> https://www.cnblogs.com/mostknow/p/10083584.html

String不可变性的好处：

- 可以缓存hash值
- String Pool的需要
- 安全性（保证传输参数不可变）
- 线程安全



### String, StringBuffer and StringBuilder区别

**1. 可变性**

- String 不可变
- StringBuffer 和 StringBuilder 可变

**2. 线程安全**

- String 不可变，因此是线程安全的
- StringBuilder 不是线程安全的
- StringBuffer 是线程安全的，内部使用 synchronized 进行同步

[StackOverflow : String, StringBuffer, and StringBuilder](https://stackoverflow.com/questions/2971315/string-stringbuffer-and-stringbuilder)

### String Pool

​		字符串常量池（String Pool）保存着所有字符串字面量（literal strings），这些字面量在编译时期就确定。还可以使用 String 的 intern() 方法在运行过程将字符串添加到 String Pool 中。

​		当一个字符串调用 intern() 方法时，如果 String Pool 中已经存在一个字符串和该字符串值相等，那么就会返回 String Pool 中字符串的引用；否则，就会在 String Pool 中添加一个新的字符串，并返回这个新字符串的引用。**(有则获得，没有则添加后再获得)**

字面量："aaa" 会自动放入字符串常量池

​		在 Java 7 之前，String Pool 被放在运行时常量池中，它属于永久代。而在 Java 7，String Pool 被移到堆中。这是因为永久代的空间有限，在大量使用字符串的场景下会导致 OutOfMemoryError 错误。



### new String("abc")

​		在字符串常量池中没有"abc"该字符串字面量时，new String("abc") 会创建两个对象，一个是在堆中，一个是在堆的字符串常量池中，其中堆中的values引用指向字符串常量池中的字面量。



## 三、运算

### 参数传递










### Comparator与Comparable的区别
[Java中Comparable和Comparator区别小结 - 温布利往事 - 博客园 (cnblogs.com)](https://www.cnblogs.com/xujian2014/p/5215082.html)
**Comparable：**
- Comparable是一个排序接口。当一个类实现了该接口，即表示该类支持排序。排序规则按照实现的方法compareTo来确定， 比如说实现了Comparable接口的类的对象的列表或数组可以通过Collections.sort或Arrays.sort进行自动排序。实现此接口的对象可以用作有序映射中的键或有序集合中的集合，无需指定比较器。

**Comparator：**、
- Comparator是比较接口，我们如果需要控制某个类的次序，而该类本身不支持排序(即没有实现Comparable接口)，那么我们就可以建立一个“该类的比较器”来进行排序，这个“比较器”只需要实现Comparator接口，并实现compare(T o1, T o2) 函数。也就是说，我们可以通过实现Comparator来新建一个比较器，然后通过这个比较器对类进行排序。   
**使用：**
```java
Arrays.sort(people,new PersonCompartor());
```
**Comparable和Comparator区别比较：**
- Comparable是排序接口，若一个类实现了Comparable接口，就意味着“该类支持排序”。而Comparator是比较器，我们若需要控制某个类的次序，可以建立一个“该类的比较器”来进行排序。
- Comparable相当于“内部比较器”，而Comparator相当于“外部比较器”。
- 两种方法各有优劣， 用Comparable 简单， 只要实现Comparable 接口的对象直接就成为一个可以比较的对象，但是需要修改源代码。 用Comparator 的好处是不需要修改源代码， 而是另外实现一个比较器， 当某个自定义的对象需要作比较的时候，把比较器和对象一起传递过去就可以比大小了， 并且在Comparator 里面用户可以自己实现复杂的可以通用的逻辑，使其可以匹配一些比较简单的对象，那样就可以节省很多重复劳动了。




















# 参考文献



【1】[C语言编程网](http://c.biancheng.net/java/)

