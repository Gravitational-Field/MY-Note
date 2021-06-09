### Java中的引用类型（强、软、弱、虚）
[ Java的四种引用方式\_林老师带你学编程-CSDN博客\_java 引用](https://blog.csdn.net/linzhiqiang0316/article/details/88591907)

> Java 对象有 4 种引用方式，分别是强引用，软引用，弱引用，虚引用，这四种引用强度依次减弱。
- 强引用
强引用是最常见的，一个变量用等号赋值，就是把这个变量指向强引用。只要有强引用，GC 永远不会回收掉该对象。
- 软引用
软引用引用的对象，虽然是存活的，但当GC回收时，会考虑当前内存是否足够，内存紧缺不足则会强制回收，内存足够则不回收。
软应用的创建需要借助SoftReference 类来实现。如下：
```java
SoftReference<String>sr = new SoftReference<String\>(new String("hello"));
System.out.println(sr.get());
```

- 弱引用
软引用的对象，虽然是存活的，但当GC回收时，只要扫描到，就会被回收，而不考虑JCM内存空间是否足够。
弱引用的需要 WeakReference 类来实现。
```java
WeakReference<String>sr = new WeakReference<String\>(new String("hello"));
System.out.println(sr.get());
System.gc(); //通知JVM的gc进行垃圾回收
System.out.println(sr.get());  //null
```
第二个输出结果是 null，这说明只要 JVM 进行垃圾回收，被弱引用关联的对象必定会被回收掉。

- 虚引用
虚引用并不会印象对象的生命周期，对象跟虚引用有关联，跟跟没有引用与它关联一样，在任何时候都可能被垃圾回收器回收。
另外，虚引用必须和引用队列关联使用，当GC进行回收一个对象时，如果发现它有虚引用，会把虚引用加入到与之关联的引用队列中。程序通过判断引用队列中是否已经加入虚引用，来了解被引用的对象是否要被垃圾回收，如果程序发现虚引用已经被加入到了引用队列，那么就可以在所引用的对象的内存被回收之前采取必要的行动。
Java中使用PhantomReference来实现


![[Pasted image 20210512224334.png]]