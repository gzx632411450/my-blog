---
{"banner":"zob_config/banners/013.jpg","create":"2023-05-30","update":"2023-05-30","status":["待完成"],"publish":false,"priority":1,"aliases":["Redis--索引笔记--Redis编码概览"],"tags":null,"banner_y":0.35,"参考网址":["http://mp.weixin.qq.com/s?__biz=MzI4NjExMDA4NQ==&mid=2648454563&idx=1&sn=d0d0f9a111784fe97b196d3f0160f6d5&chksm=f3c96d49c4bee45f6890a6a7d3d1ac8386e996dc5643aac5a19528a016ebd753b7fac8ad8d76&scene=21#wechat_redirect"],"dg-publish":true,"dg-note-icon":2,"dgPassFrontmatter":true,"noteIcon":2,"dg-path":"Redis/Redis--索引笔记--Redis编码概览. md","title":"📑 Redis--索引笔记--Redis 编码概览","permalink":"/Redis/Redis--索引笔记--Redis编码概览/"}
---

参考网址：
http://mp.weixin.qq.com/s?__biz=MzI4NjExMDA4NQ==&mid=2648454563&idx=1&sn=d0d0f9a111784fe97b196d3f0160f6d5&chksm=f3c96d49c4bee45f6890a6a7d3d1ac8386e996dc5643aac5a19528a016ebd753b7fac8ad8d76&scene=21#wechat_redirect



![zob_attach/RedisDB主体数据结构.png|1000](/img/user/zob_attach/RedisDB%E4%B8%BB%E4%BD%93%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84.png)

## [[2 知识库/1 数据库/Redis/永久笔记/📑 Redis--永久笔记--RedisObject\|📑 Redis--永久笔记--RedisObject]]
相当于所有元素的包装类型，ptr 指向目标元素，类似于 Java 中的对象布局的概念.
还有一个很神奇的地方是，对于一个类型可能有多个实现，但是我们只需要一种命令，这也被形象的称为**多态命令**
[[2 知识库/1 Java知识/JVM/永久笔记/📑 JVM--永久笔记--对象头和对象内存布局\|📑 JVM--永久笔记--对象头和对象内存布局]]
```c
    typedef struct redisObject {
        unsigned type:4;    // 类型信息
        unsigned encoding:4;   // 编码信息
        unsigned lru:LRU_BITS; /* lru time (relative to server.lruclock) */   // 这里是空转时长,如果内存不够了,会先淘汰这部的键
        int refcount;   // 引用计数法,当一个对象不再被引用的时候,就该删除了
        void *ptr;   // 指向数据地址
    } robj;
```

## 为什么 Redis 要采用那么多种不同的编码呢？
1. 举例，实现插入、删除、随机访问都是 O1 的"容器"，如何实现，是否需要多种"容器"；但是大部分都有一个动作的偏向，那个操作更多，就如分布式架构，读写分离，一写多读；所以说采用不同的编码，提升业务性能
2. 平时我们谈论的时间复杂度，有些时候确实会脱离现实；而对于 Redis，是真真切切的去从底层和实际考虑了，比如说用压缩列表和用链表，遍历都是 On，哪个快，我觉得可能是压缩列表快；压缩列表使用在小数量，小长度场景中
3. 去了解编码的好处就是，可以针对业务做一些提升，例如，我有时候就需要固定 65 个长度，这个时候可能就更换了一个编码，可能会造成数据的一个性能波动，可以检测波动，选择更好的编码，Trade-off

编码的关键原因是：我们不能完全依照时间复杂度来判断数量较小的情况。例如 O(9 n)和 o (n)都是 o (n+8)，具体则是需要判断一个长度范围来确定哪个更好。


## 常用编码和类型
[[2 知识库/1 数据库/Redis/永久笔记/📑 Redis--永久笔记--String字符串\|📑 Redis--永久笔记--String字符串]]
[[2 知识库/1 数据库/Redis/永久笔记/📑 Redis--永久笔记--Set集合\|📑 Redis--永久笔记--Set集合]]
[[2 知识库/1 数据库/Redis/永久笔记/📑 Redis--永久笔记--List列表\|📑 Redis--永久笔记--List列表]]
[[2 知识库/1 数据库/Redis/永久笔记/📺 Redis--永久笔记--Hash类型\|📺 Redis--永久笔记--Hash类型]]
[[2 知识库/1 数据库/Redis/永久笔记/📑 Redis--永久笔记--Sorted Set类型\|📑 Redis--永久笔记--Sorted Set类型]]
[[2 知识库/1 数据库/Redis/永久笔记/📑 Redis--永久笔记--HyperLogLogs\|📑 Redis--永久笔记--HyperLogLogs]]
[[2 知识库/1 数据库/Redis/永久笔记/📑 Redis--永久笔记--GEO\|📑 Redis--永久笔记--GEO]]



Redis支持多种数据类型，每种类型都有不同的type和encoding。
![Pasted image 20230629082946.png](/img/user/zob_attach/Pasted%20image%2020230629082946.png)
以下是Redis支持的数据类型及其可能的type和encoding值：

字符串类型（string）：
    type: [[📑 📑 Redis--永久笔记--REDIS_STRING类型\|REDIS_STRING]] （可点击）
    encoding：
        REDIS_ENCODING_RAW 
        REDIS_ENCODING_INT 
        REDIS_ENCODING_EMBSTR : 短字符优化,缓存行 

列表类型（list）：
type: REDIS_LIST    
encoding：
    [[REDIS_ENCODING_ZIPLIST\|REDIS_ENCODING_ZIPLIST]]:  内存紧凑连续存储,长度 < 64,个数 < 512个 ,紧凑,不适合很多个元素存储
    [[2 知识库/1 数据库/Redis/子知识笔记/📑 Redis--子知识笔记--REDIS_ENCODING_LINKEDLIST\|📑 Redis--子知识笔记--REDIS_ENCODING_LINKEDLIST]] : 内存不紧凑非连续存储,任意个数,插入方便

集合类型（set）：****
type: REDIS_SET     
encoding：
    [[2 知识库/1 数据库/Redis/子知识笔记/📑 Redis--子知识笔记--REDIS_ENCODING_INTSET\|REDIS_ENCODING_INTSET]] : 内存较为紧凑整数集合,较小无需集合
    REDIS_ENCODING_HT(哈希表) : 较大的无需集合

有序集合类型（sorted set）：
type: [[2 知识库/1 数据库/Redis/索引笔记/📑 Redis--子知识笔记--REDIS_ZSET\|📑 Redis--子知识笔记--REDIS_ZSET]]     
encoding：
    [[2 知识库/1 数据库/Redis/子知识笔记/📑 Redis--子知识笔记--REDIS_ENCODING_ZIPLIST\|📑 Redis--子知识笔记--REDIS_ENCODING_ZIPLIST]]: 元素较少的
    [[2 知识库/1 数据库/Redis/子知识笔记/📑 Redis--子知识笔记--REDIS_ENCODING_SKIPLIST\|REDIS_ENCODING_SKIPLIST]]: 元素较多的  

哈希类型（hash）：
type: [[2 知识库/1 数据库/Redis/永久笔记/📑 Redis--永久笔记--REDIS_HASH\|📑 Redis--永久笔记--REDIS_HASH]]:     （可点击）
encoding： 
    REDIS_ENCODING_ZIPLIST: 较小的哈希表
    REDIS_ENCODING_HT : 适用于元素较多的哈希表

>大多编码类型的分类都分为元素较多，元素较少时候，这也是为了能够尽最大程度利用好内存

## [[📑 Redis--永久笔记--REDIS_ENCODING_HT\|📑 Redis--永久笔记--REDIS_ENCODING_HT]]