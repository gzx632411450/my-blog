---
{"banner":"zob_config/banners/014.jpeg","create":"2023-06-29","update":"2023-06-29","status":["待完成"],"publish":false,"priority":1,"aliases":["Redis--永久笔记--String字符串"],"tags":[],"dg-publish":true,"dg-note-icon":2,"dgPassFrontmatter":true,"noteIcon":2,"dg-path":"Redis/Redis--永久笔记--String 字符串","title":"📑 Redis--永久笔记--String 字符串","permalink":"/Redis/Redis--永久笔记--String 字符串/"}
---



## 编码实现
[Redis--永久笔记--REDIS_STRING类型](📑%20Redis--子知识笔记--REDIS_STRING类型.md)

## 应用场景
验证码、计数器、订单重复提交、⽤户登录信息、商品详情

![](/img/user/zob_attach/Pasted image 20230705112419.png)


>注：APPEND 可以用于存储日志

| 命令             | 作用               | 备注                                                              | 时间复杂度 |
| ---------------- | ------------------ | ----------------------------------------------------------------- | ---------- |
| SET KEY VALUE    | 给 key 设置值      | 没有就创建, 有则更新                                              | o1         |
| get KEY          | 根据 key 获取      | 没有返回 nil, 注意处理                                            | o1         |
| getSET KEYS...   | 获取旧值&设置新值  |                                                                   | o1         |
| MSET/NX KEYS...  | 为多个 Key 设值    | 节省资源、时间, 避免多次 SET                                      | oN         |
| MGET/NX KEYS...  | 获取多个 Key 的值  |                                                                   | oN         |
| STRLEN KEY       |                    |                                                                   | o1         |
| GETRANGE         | 返回字符串范围内值 | 0 开始正数索引；-1 开始倒数索引。注：若索引超过字符串长度, 填充 0 | on         |
| SETRANGE         | 设置字符串范围内值 |                                                                   |            |
| APPEND KEY VALUE | 追加内容           | 若 Key 不存在, 则新建再追加                                       | ON         |
| INCRBY KEY VALUE | 加 n               | 若类型不对，返回错误；不存在则新建                                |            |
| DECRBY KEY VALUE | 减 n               | 若类型不对，返回错误                                              |            |
| INCRBYFLOAT      | 浮点数操作         | 目标/增量可为浮点数、整型；使用该命令结保留 17 位小鼠             | o1           |
|                  |                    |                                                                   |            |
