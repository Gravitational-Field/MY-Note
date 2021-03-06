

#### Q1. Redis与MySQL双写一致性如何保证？
[美团二面：Redis与MySQL双写一致性如何保证？ (juejin.cn)](https://juejin.cn/post/6964531365643550751)

##### 1、数据的一致性分类
数据的一致性即为数据保持一致，在分布式系统中可以理解为多个节点中数据的值是一致的。
- 强一致性
最符合用户直觉，写入是什么，读取出来就是什么，但实现起来对系统性能会有很大影响。

- 弱一致性
在数据写入成功后，不保证立即能读到写入的值，也不保证多久后数据能够达到一致，只是尽力保证到某个时间级别后，数据能够达到一致状态。

- 最终一致性
是弱一致性的一个特例，系统会保证在一定时间内能够达到一个数据一致的状态。这种方式是业界大型分布式系统的数据一致性上比较推崇的模型。


##### 2、缓存模式
-   Cache-Aside Pattern
-   Read-Through/Write through
-   Write behind

1、Cache-Aside Pattern 旁路缓存模式
读：先读缓存，缓存命中即返回；缓存未命中，从数据库中读，并放到缓存中，再返回数据。
写：~~先删缓存，再写到数据库中~~ 先更新数据库，再**删除**缓存  （可能会产生脏读问题）

2、Read-Through/Write through  读写穿透模式
本质是将**缓存作为主要数据存储位置**，同步更新缓存和数据；并且增加了一层**抽象的缓存层Cache Provider**来处理应用程序和数据库缓存进行交互。
读穿透：从缓存中读，读到直接返回；若缓存未命中，从数据库中加载到缓存，再返回去。
写穿透：由缓存抽象层完成数据库和缓存数据的**更新**。

3、Write behind  异步缓存写入模式
也是由**抽象的缓存层Cache Provider**负责数据库与缓存的读写。
**Read/Write Through**是同步更新缓存和数据的；Write behind则只更新缓存，不直接更新数据库，通过批量异步的方式来更新数据库。
缓存和数据库的一致性不强，适合频繁写入的场景，Mysql的InnoDB Buffer Pool机制使用这种模式。

##### 3、操作缓存时，到底是删除缓存还是更新缓存？
各有各的优势，删除缓存能够避免脏读。更新缓存能够提高效率。

##### 4、双写的情况下，先操作数据库还是先操作缓存？
先操作数据库，再更新缓存。
##### 5、三种方案保证数据库与缓存的最终一致性？
一定要确保在操作数据库后，更新了缓存。
缓存延时双删策略：
删除缓存重试机制：
读取biglog异步删除缓存：









