---
{"banner":"zob_config/banners/002.jpeg","create":"2023-05-30","update":"2023-05-30","status":["待完成"],"publish":false,"priority":1,"tags":[],"banner_x":0.5,"dg-publish":true,"dg-note-icon":2,"dgPassFrontmatter":true,"noteIcon":2,"dg-path":"Redis/Redis--子知识笔记--REDIS_STRING 类型.md","title":"📑 Redis--子知识笔记--REDIS_STRING 类型","permalink":"/Redis/Redis--子知识笔记--REDIS_STRING 类型/"}
---


前置：
>Redis 数据类型有不同的编码。
>String：数据结构


## 编码类型
REDIS_ENCODING_RAW ：RAW
REDIS_ENCODING_INT 
REDIS_ENCODING_EMBSTR : 短字符优化,缓存行 

## RAW 和 EMBSTR
长度 < 44 字节，使用 embstr。注意：使用的是utf-8，44 字节为 44 个英文字符， 14 个中文字符
这两类是由 SDS 来是实现的，其中尤其为 EMBSTR 最牛逼，对于 EMBST      R 来说，其长度较短，使用 ssdhdr 8 即可，在 Linux 下，缓存行通常为 64 字节，计算之后，理论上最优能够达到。

注：缓存行-24-3 是比较合适的，例如 64-27 = 37 字节长度。（实际效果需要测试）
```java
struct __attribute__ ((__packed__)) sdshdr8 {
    uint8_t len; /* used */
    uint8_t alloc; /* excluding the header and null terminator */ 
    unsigned char flags; /* 3 lsb of type, 5 unused bits */
    char buf[];  
};
```


## SDS/RAW
我们都知道 Redis 是用 C 语言写出来的, 那么自然字符串应该就是由 C 语言中的字符串数组构成的.
但是 C 语言的字符串数组如下
==C 语言使用 N+1 长度的 char 数组来表示 N 长度的字符串==, 
```C
char data[] = "aaa\0";
```
也就是说最后一个字符是\0, 也就是说 Redis 的字符串数组是以\0 来标识结尾的, 就存在一个问题, 假如我们要传的字符串, 里面就携带了\0, 那么就可能会出现字符串提早结束.
这类似于计算机网络中的透明传输的概念


为啥要 free 呢?
>这和字符串的扩容策略有关系, ==每次扩容, 扩容 ( len + addlen) * 2 比如说 === len = 6, add = 3, newLen = 18, 此时 free =6;
>这里就是时间换空间


封装成 SDS 的作用
1. Redis 采用了一个方法就是保存 len 的长度, 此时就解决了\0 能提前让结束的问题.
此外
2. ==常量级别复杂度获取长度 :== c 语言的 strlen 方法时间复杂度是 on, 但是包装成 SDS 之后, 计算长度只需要 O 1 的时间复杂度
3. ==不存在缓冲区溢出==: 对于 C 语言的话, 假如存在 s 1 和 s 2 两个字符, 两个字符内存连续, 然后我们拼接 s 1 字符, 此时可能会覆盖 s 2, 但是 SDS 不存在，因为修改的时候，会判断当前 free 是否满足扩容后的需求, ==否则就需要重新扩容==
4.  ==SDS 有空间预分配的功能==, 也就是说扩容之后, 会多分配一些内存, 然后 free 保存的就是多分配内存的大小. 这样做的好处是可以减少内存重分配的次数, 在源代码中体现就是减少 relalloc 函数
5. 二进制安全的数据结构

### SDS 源码
Free :   这里指的是当前容量下, 存储了多长的字符串
Len :    int len : 字符串的长度 `
Char buf[]; 内容，注意实际上会多存储一个\0

注意，这里想一想，Free 和 Len 都是什么类型的？
>其实是不固定，如果说长度很小，就一个字符，那么 Free 和 Len 都是 int 的话那么就太浪费了

所以，长度不同，Free 和 Len 占用位数也不同，所以说，Redis 扣内存是已经扣到极致了，所以说这样就早就了其快的特性
```java
/* Note: sdshdr5 is never used, we just access the flags byte directly.
 * However is here to document the layout of type 5 SDS strings. */
struct __attribute__ ((__packed__)) sdshdr5 {
    unsigned char flags; /* 3 lsb of type, and 5 msb of string length */
    char buf[];// buf[0]: z:  0101001
};
struct __attribute__ ((__packed__)) sdshdr8 {
    uint8_t len; /* used */
    uint8_t alloc; /* excluding the header and null terminator */
    unsigned char flags; /* 3 lsb of type, 5 unused bits */
    char buf[];
};
struct __attribute__ ((__packed__)) sdshdr16 {
    uint16_t len; /* used */
    uint16_t alloc; /* excluding the header and null terminator */
    unsigned char flags; /* 3 lsb of type, 5 unused bits */
    char buf[];
};
struct __attribute__ ((__packed__)) sdshdr32 {
    uint32_t len; /* used */
    uint32_t alloc; /* excluding the header and null terminator */
    unsigned char flags; /* 3 lsb of type, 5 unused bits */
    char buf[];
};
struct __attribute__ ((__packed__)) sdshdr64 {
    uint64_t len; /* used */
    uint64_t alloc; /* excluding the header and null terminator */
    unsigned char flags; /* 3 lsb of type, 5 unused bits */
    char buf[];
};
```

## INT
这里特别好玩!!!,明明是Long的长度，但是叫INT。（这句话面试的时候要说出来）
要注意的是，这里也是很简洁，直接存储在 RedisObject 中的 void * ptr 中，当存储一个值的时候，直接 ptr = (void * ) (Long（Value）)

注： 小知识，这里是 int_64,，所以实际上长度为 Long，这也是这里为什么使用 Long 强转的原因

作用： 减少一次引用

文件：object. c
```c
        if (value >= LONG_MIN && value <= LONG_MAX) {
            o = createObject(OBJ_STRING, NULL);
            o->encoding = OBJ_ENCODING_INT;
            o->ptr = (void*)((long)value);
        
        注：两段代码分别从两个方法中取出来
        
        else if (o->encoding == OBJ_ENCODING_INT) {
            value = (long)o->ptr;
```

### 哪些数字
| 值                   | 解释方式                   |     |
| -------------------- | -------------------------- | --- |
| 10086                |                            |     |
| +894                 |                            |     |
| -123                 |                            |     |
| 3.14                 | 浮点数，即字符串           |     |
| +2.56                | 浮点数，即字符串           |     |
| -5.12                | 浮点数，即字符串                           |     |
| 12345678901234567890 | 字符串                     |     |
| 3.14e6               | 字符串，无法表示科学计数法 |     |
| "one"                | 字符串                     |     |
| 123ad                | 字符串                     |     |

## 浮点数
这里要注意：
>浮点数在 Redis 中并没有小数位长度限制，但计算之后，只会处理 17 位