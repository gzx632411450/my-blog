---
{"banner":"zob_config/banners/014.png","create":"2023-05-31","update":"2023-05-31","status":["待完成"],"publish":false,"priority":1,"aliases":["未命名"],"tags":null,"dg-publish":true,"dg-note-icon":2,"dgPassFrontmatter":true,"noteIcon":2,"dg-path":"Redis/Redis--索引笔记--Redis总览","title":"📑 Redis--索引笔记--Redis总览","permalink":"/Redis/Redis--索引笔记--Redis总览/"}
---


## Redis 设计思想
单线程，无事务，较难保证（Redis）强一致性、快
>最好的解决办法就是不去解决。当然这是有先决条件的，这个事情是否是必要的。拿生物演化来说，多少一年的演化，实际上也没有那种适应能力强，跑得快，功能能力强，防御也高的动物，为什么呢，这类生物的并不是不适合生存，而是没有必要，当你跑得快之后，基本上很难被攻击到，而防御力高肯定或多或少会牺牲一些优势，相反防御力高，就不一定你需要很快的速度，因为大部分动物都很难解决掉你，你就没有跑得快的需求了。
>而 Redis 就是这种，虽然使用 Redis 往往可能会需要我们解决更多的问题，但是对他来说，跑得快就够了，这些问题留给其他人解决吧。


## 基础部分
[[Redis--永久笔记--Redis适用场景\|Redis--永久笔记--Redis适用场景]]
[📑 Redis--永久笔记--Redis为什么那么快](📑%20Redis--永久笔记--Redis为什么那么快.md)
[📑 Redis--索引笔记--Redis编码概览](📑%20Redis--索引笔记--Redis编码概览.md)
[分布式锁](📑%20Redis--永久笔记--分布式锁.md)
[Redis--永久笔记--AOF](📑%20Redis--永久笔记--AOF.md)
[📑 Redis--永久笔记--RDB](📑%20Redis--永久笔记--RDB.md)
[📑 Redis--永久笔记--缓存雪崩和缓存穿透和缓存击穿](📑%20Redis--永久笔记--缓存雪崩和缓存穿透和缓存击穿.md)
[📑 Redis--永久笔记--Redis缓存相关核心问题](📑%20Redis--永久笔记--Redis缓存相关核心问题.md)

## 优化部分
[[2 知识库/1 数据库/Redis/索引笔记/📑 Redis--索引笔记--缓存、优化、问题解决等\|📑 Redis--索引笔记--缓存、优化、问题解决等]]
[[2 知识库/1 数据库/Redis/永久笔记/📑 Redis--永久笔记--6.0中如何实现IO的多线程\|📑 Redis--永久笔记--6.0中如何实现IO的多线程]]