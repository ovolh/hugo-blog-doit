---
title: "redis 基础命令操作指南"
date: 2020-09-29 14:57:17
lastmod: 2022-06-07T10:16:26+08:00
draft: false
description: "redis 基础命令简单操作指南，方便以后查阅"
tags: [Redis]
featured_image: "redis.png"
categories: [Redis]
comment : true
disableToC: false
---

> 转载自：[finecho](https://learnku.com/blog/Lhao) 的 [Redis 基础学习](https://learnku.com/articles/24802)


# 启动 && 连接
启动：`service redis-server start`
连接：`redis-cli -h host -p port -a password`

# 数据类型
| 序号   | 数据类型                | 描述             |
| ----  | ---------              | ----             |
| 1     | string （字符串）       |            |
| 2     | hash （哈希）           |  key：value （键值对集合） 适合存储对象 |
| 3     | list （列表） | 简单的字符串列表，可以添加元素到列表的头部和尾部 |
| 4     | set （集合） | string 类型的无序集合，是通过哈希表实现的  |
| 5     | zset （有序集合） | zset 和 set 一样也是 string 类型元素的集合，且不允许重复的成员 <br> 不同的是每个元素都会关联一个 double 类型的分数。<br>redis 正是通过分数来为集合中的成员进行从小到大的排序 <br>zset 的成员是唯一的，但分数 (score) 却可以重复     |

# 操作指南
## key 操作
```redis
-- SET KEY_NAME VALUE（设置给定 key 的值。如果 key 已经存储其他值， SET 就覆写旧值，且无视类型）
> set name Lhao

-- GET KEY_NAME （获取指定 key 的值。如果 key 不存在，返回 nil 。如果key 储存的值不是字符串类型，返回一   个错误）
> get name // 输出：Lhao

-- DUMP KEY_NAME （序列化 name，输出序列化之后的值）
> dump name // 输出："\x00\x04Lhao\t\x00\xd3JL\xcf\xafsi\x8f"

-- EXISTS KEY_NAME （判断 key 是否存在）
> exists name // 输出：1

-- Expire KEY_NAME TIME_IN_SECONDS (设置有效时间，过期之后则删除，单位：s , 可对已存在的 key 进行操作)
> expire name 10 // 输出：1

-- Expireat KEY_NAME TIME_IN_UNIX_TIMESTAMP (指定过期时间戳)
> set name Lhao // 上面设置了过期时间，已经没了 ，哈哈
> expireat name 1551341040 // 输出：1

-- KEYS PATTERN (用于查找所有符合给定模式 pattern 的 key )
> set name Lhao
> keys * //（返回所有键名）输出：name
> set naes haha
> keys na* // 输出：name、naes

-- SELECT index (切换到指定的数据库，数据库索引号 index 用数字值指定，以 0 作为起始索引值)
> select 0 

-- MOVE KEY_NAME DESTINATION_DATABASE (将当前数据库的 key 移动到给定的数据库 db 当)
> move name 1 // (移动 name 到 1 数据库中)
> exists name // 输出：0
> select 1
> exists name // 输出：1

> expire name 10

-- TTL KEY_NAME (以秒为单位返回 key 的剩余过期时间)
> ttl name // 输出：8

-- PERSIST KEY_NAME (移除给定 key 的过期时间，使得 key 永不过期)
> persist name // 输出：1
> ttl name // 输出：-1 （表示不过期）

-- DEL KEY_NAME (删除已存在的键。不存在的 key 会被忽略)
> del name // 输出：1

> set name Lhao
> set age 24

-- RANDOMKEY (从当前数据库中随机返回一个 key)
> randomkey // 输出：age

-- FLUSHDB (清空当前数据库中的所有 key)
> flushdb

> set name Lhao

-- RENAME OLD_KEY_NAME NEW_KEY_NAME (修改 key 的名称)
> rename name newname
> get name // 输出：nli (不存在)
> set namecopy wjh
> rename newname namecopy
> get namecopy // 输出：Lhao

> set name Lhao

-- RENAMENX OLD_KEY_NAME NEW_KEY_NAME (用于在新的 key 不存在时修改 key 的名称)
> renamenx namecopy name // 输出：0 (此时修改 key 名不成功)

-- TYPE KEY_NAME (返回 key 所储存的值的类型)
> type name // 输出：string
```

## string 操作
```redis
> flushdb

> set title "my name is Lhao"
> get title // 输出：my name is Lhao

-- GETRANGE KEY_NAME start end （用于获取存储在指定 key 中字符串的子字符串。字符串的截取范围由 start 和 end 两个偏移量决定(包括 start 和 end 在内)）
> getrange title 0 4 // 输出：my na

-- GETSET KEY_NAME VALUE (用于设置指定 key 的值，并返回 key 的旧值)
> getset title "new title" // 输出：my name is Lhao
> get title // 输出：new title

-- MGET KEY1 KEY2 .. KEYN (返回所有(一个或多个)给定 key 的值。 如果给定的 key 里面，有某个 key 不存在，那么这个 key 返回特殊值 nil )
> mget title name 
// 输出：
 1) (nil)
 2) "new title"

-- SETEX KEY_NAME TIMEOUT VALUE (为指定的 key 设置值及其过期时间。如果 key 已经存在， SETEX 命令将会替换旧的值)
> setex name 60 liuhao

> del name

-- SETNX KEY_NAME VALUE（SET if Not eXists） 命令在指定的 key 不存在时，为 key 设置指定的值
> setnx name Lhao // 输出：1
> setnx title Lhao // 输出：0

-- SETRANGE KEY_NAME OFFSET VALUE （用指定的字符串覆盖给定 key 所储存的字符串值，覆盖的位置从偏移量 offset 开始）
> setrange name 3 Lhao // 输出：7
> get name // 输出：LhaLhao

-- STRLEN KEY_NAME (用于获取指定 key 所储存的字符串值的长度。当 key 储存的不是字符串值时，返回一个错误)
> strlen name // 输出：7

-- 用于同时设置一个或多个 key-value 对 (MSET key1 value1 key2 value2 .. keyN valueN )
> mset name Lhao age 24 // 输出：ok
> mget name age 
// 输出：
 1) "Lhao"
 2) "24"

-- MSETNX key1 value1 key2 value2 .. keyN valueN （用于所有给定 key 都不存在时，同时设置一个或多个 key-value 对）
> msetnx name Lhao age 24 // 输出：0
> msetnx name Lhao25 sex men //输出：0
> get sex // 输出：nli

-- INCR KEY_NAME 
// 将 key 中储存的数字值增一。
// 如果 key 不存在，那么 key 的值会先被初始化为 0 ，然后再执行 INCR 操作。
// 如果值包含错误的类型，或字符串类型的值不能表示为数字，那么返回一个错误。
// 本操作的值限制在 64 位(bit)有符号数字表示之内。
> incr name // 输出：(error) ERR value is not an integer or out of range
> incr money // 输出：1

-- DECRBY KEY_NAME DECREMENT_AMOUNT (将 key 中储存的数字加上指定的增量值)
> incrby money 80 // 输出：81

-- DECR KEY_NAME （将 key 中储存的数字值减一）
> decr money // 输出：80

-- DECRBY KEY_NAME DECREMENT_AMOUNT （将 key 所储存的值减去指定的减量值）
> decrby money 10 // 输出：70

-- APPEND KEY_NAME NEW_VALUE
// 为指定的 key 追加值。
// 如果 key 已经存在并且是一个字符串， APPEND 命令将 value 追加到 key 原来的值的末尾。
// 如果 key 不存在， APPEND 就简单地将给定 key 设为 value ，就像执行 SET key value 一样。
> append name " love" //  输出：8
> get name // 输出：Lhaolove
```

## hash 操作
```redis
> flushdb

-- HSET KEY_NAME FIELD VALUE (用于为哈希表中的字段赋值;如果哈希表不存在，一个新的哈希表被创建并进行 HSET 操作;如果字段已经存在于哈希表中，旧值将被覆盖)
> hset user name Lhao // 输出：1

-- HGET KEY_NAME FIELD_NAME (用于返回哈希表中指定字段的值)
> hget user name // 输出：Lhao

> hset user name wjh // 输出：0
> hget user name // 输出：wjh

-- HMSET KEY_NAME FIELD1 VALUE1 ...FIELDN VALUEN (用于同时将多个 field-value (字段-值)对设置到哈希表中)
> hmset user name Lhao age 24 // 输出：ok
> hmget user name age
// 输出：
 1) "Lhao"
 2) "24"

-- HDEL KEY_NAME FIELD1.. FIELDN（用于删除哈希表 key 中的一个或多个指定字段，不存在的字段将被忽略）
> hdel user name // 输出：1

-- HEXISTS KEY_NAME FIELD_NAME (用于查看哈希表的指定字段是否存在)
> hexists user name // 输出：0

-- HGETALL KEY_NAME (用于返回哈希表中，所有的字段和值;在返回值里，紧跟每个字段名(field name)之后是字段的值(value)，所以返回值的长度是哈希表大小的两倍)
> hgetall user
// 输出：
 1) "age"
 2) "24"

-- HINCRBY KEY_NAME FIELD_NAME INCR_BY_NUMBER（用于为哈希表中的字段值加上指定增量值）
> hincrby user age 1 // 输出：25

-- HKEYS key (用于获取哈希表中的所有域（field）)
> hkeys user
// 输出：
1) "age"

-- HLEN KEY_NAME （用于获取哈希表中字段的数量）
> hlen user //  输出：1

-- HSETNX KEY_NAME FIELD VALUE（用于为哈希表中不存在的的字段赋值）
> hsetnx user name hao // 输出：1
> hsetnx user age 24 // 输出：0

-- HVALS KEY_NAME FIELD VALUE（返回哈希表所有域(field)的值）
> hvals user 
// 输出：
1) "25"
2) "Lhao"
```

## list 操作
```redis
> flushdb

-- LPUSH KEY_NAME VALUE1.. VALUEN （将一个或多个值插入到列表头部。 如果 key 不存在，一个空列表会被创建并执行 LPUSH 操作。 当 key 存在但不是列表类型时，返回一个错误。）
> lpush users Lhao wjh // 输出：2

-- LRANGE KEY_NAME START END (返回列表中指定区间内的元素，区间以偏移量 START 和 END 指定。 其中 0 表示列表的第一个元素， 1 表示列表的第二个元素，以此类推。 你也可以使用负数下标，以 -1 表示列表的最后一个元素， -2 表示列表的倒数第二个元素，以此类推)
> lrange users 0 0 // 输出：wjh
> lrange users 0 -1 // 输出：wjh、Lhao 

-- BLPOP LIST1 LIST2 .. LISTN TIMEOUT （移出并获取列表的第一个元素， 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止）
> blpop users 10 
// 输出：
1) "users"
2) "wjh"
> lrange users 0 -1 // 输出：Lhao

-- BRPOPLPUSH LIST1 ANOTHER_LIST TIMEOUT （从列表中弹出第一个值，将弹出的元素插入到另外一个列表中并返回它； 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。）
> brpoplpush users users_two 10 // 输出：Lhao
> lrange users 0 -1 // 输出：(empty list or set)
> lrange users_two 0 -1 // 输出：Lhao

> lpush users wjh Lhao

-- LINDEX KEY_NAME INDEX_POSITION (用于通过索引获取列表中的元素。你也可以使用负数下标，以 -1 表示列表的最后一个元素， -2 表示列表的倒数第二个元素，以此类推。)
> lindex users 0 // 输出：lhao
> lindex users -1 // 输出：wjh

> del users

-- RPUSH KEY_NAME VALUE1..VALUEN (用于将一个或多个值插入到列表的尾部(最右边);如果列表不存在，一个空列表会被创建并执行 RPUSH 操作。 当列表存在但不是列表类型时，返回一个错误)
> rpush users Lhao wjh
> lrange 0 -1 // 输出：Lhao wjh

-- LINSERT key BEFORE|AFTER pivot value (用于在列表的元素前或者后插入元素。当指定元素不存在于列表中时，不执行任何操作;当列表不存在时，被视为空列表，不执行任何操作;如果 key 不是列表类型，返回一个错误)
> linsert users before wjh love // 输出：3
> lrange 0 -1 // 输出：Lhao love wjh

-- LLEN KEY_NAME (用于返回列表的长度。 如果列表 key 不存在，则 key 被解释为一个空列表，返回 0 。 如果 key 不是列表类型，返回一个错误)
> llen users // 输出：3

-- Lpop KEY_NAME (用于移除并返回列表的第一个元素)
> lpop users // 输出：Lhao
> lrange users 0 -1 // 输出：love wjh

-- LPUSHX KEY_NAME VALUE1.. VALUEN (将一个值插入到已存在的列表头部，列表不存在时操作无效)
> lpushx users Lhao // 输出：3
> lrange users 0 -1 // 输出：Lhao love wjh
> lpushx user you // 输出：0
> lpush users Lhao Lhao // 输出：5
> lrange users 0 -1 // 输出：Lhao Lhao Lhao love wjh

-- LREM KEY_NAME COUNT VALUE
// 根据参数 COUNT 的值，移除列表中与参数 VALUE 相等的元素
// count > 0 : 从表头开始向表尾搜索，移除与 VALUE 相等的元素，数量为 COUNT 。
// count < 0 : 从表尾开始向表头搜索，移除与 VALUE 相等的元素，数量为 COUNT 的绝对值。
// count = 0 : 移除表中所有与 VALUE 相等的值。

> lrem users 2 Lhao // 输出：2
> lrange users 0 -1 // 输出：Lhao love wjh 

-- LSET KEY_NAME INDEX VALUE (通过索引来设置元素的值;当索引参数超出范围，或对一个空列表进行 LSET 时，返回一个错误)
> lset users 0 liuhao // 输出：ok
> lrange users 0 -1 // 输出：liuhao love wjh

> lpush fruit apple cherry strawbrerry

-- LTRIM KEY_NAME START STOP (对一个列表进行修剪(trim)，就是说，让列表只保留指定 区间内的元素，不在指定区间之内的元素都将被删除;下标 0 表示列表的第一个元素，以 1 表示列表的第二个元素，以此类推。 你也可以使用负数下标，以 -1 表示列表的最后一个元素， -2 表示列表的倒数第二个元素，以此类推。)
> ltrim fruit 1 -1 // 输出：ok
> lrange fruit 0 -1 // 输出：cherry apple

-- RPOP KEY_NAME （用于移除列表的最后一个元素，返回值为移除的元素）
> rpop fruit // 输出：apple
> lrange fruit 0 -1 // 输出：cherry

> lpush fruit apple cherry // 输出：3

-- RPOPLPUSH SOURCE_KEY_NAME DESTINATION_KEY_NAME （用于移除列表的最后一个元素，并将该元素添加到另一个列表并返回）
> rpoplpush fruit users // 输出：cherry
> lrange users 0 -1 // 输出：cherry、apple
```

## set 操作
```redis
> flushdb

-- SADD KEY_NAME VALUE1..VALUEN（将一个或多个成员元素加入到集合中，已经存在于集合的成员元素将被忽略；假如集合 key 不存在，则创建一个只包含添加的元素作成员的集合；当集合 key 不是集合类型时，返回一个错误。）
> sadd users wjh Lhao // 输出：2
> sadd users wjh // 输出：0 

-- SMEMBERS key （返回集合中的所有的成员。 不存在的集合 key 被视为空集合）
> smembers users // 输出：wjh Lhao

-- SCARD KEY_NAME (返回集合中元素的数量)
> scard users // 输出：2 

> sadd usersTwo abing laoxia 
> smembers usersTwo // 输出：abing laoxia

-- SDIFF FIRST_KEY OTHER_KEY1..OTHER_KEYN (返回给定集合之间的差集。不存在的集合 key 将视为空集；差集的结果来自前面的 FIRST_KEY ,而不是后面的 OTHER_KEY1，也不是整个 FIRST_KEY OTHER_KEY1..OTHER_KEYN 的差集)
> sdiff users usersTwo // 输出：wjh Lhao
> sadd usersTwo Lhao
> sdiff users usersTwo // 输出：wjh

-- SDIFFSTORE DESTINATION_KEY KEY1..KEYN (将给定集合之间的差集存储在指定的集合中。如果指定的集合 key 已存在，则会被覆盖)
> sdiffstore usersThree users usersTwo // 输出：1
> smembers usersThree // 输出：wjh

> del users usersTwo usersThree

> sadd users wjh Lhao
> sadd usersTwo Lhao abing laoxia

-- SINTER KEY KEY1..KEYN (返回给定所有给定集合的交集。 不存在的集合 key 被视为空集。 当给定集合当中有一个空集时，结果也为空集(根据集合运算定律))
> sinter users usersTwo // 输出：Lhao

-- SINTERSTORE DESTINATION_KEY KEY KEY1..KEYN (将给定集合之间的交集存储在指定的集合中。如果指定的集合已经存在，则将其覆盖)
> sinterstore usersThree users usersTwo 
> smembers usersThree // 输出：Lhao

-- SISMEMBER KEY VALUE (判断成员元素是否是集合的成员)
> sismember users Lhao // 输出：1

> sadd fruits apple cherry
> sadd fruitsTwo strawbrerry

-- SMOVE SOURCE DESTINATION MEMBER
// 将指定成员 member 元素从 source 集合移动到 destination 集合。
// SMOVE 是原子性操作。
// 如果 source 集合不存在或不包含指定的 member 元素，则 SMOVE 命令不执行任何操作，仅返回 0 。否则， member 元素从 source 集合中被移除，并添加到 destination 集合中去。
// 当 destination 集合已经包含 member 元素时， SMOVE 命令只是简单地将 source 集合中的 member 元素删除。
// 当 source 或 destination 不是集合类型时，返回一个错误。
> smove fruitsTwo fruits strawbrerry  // 输出：1
> smembers fruits // 输出：cherry、apple、strawbrerry

-- SPOP key [count] (移除集合中的指定 key 的一个或多个随机元素，移除后会返回移除的元素)
> spop fruits // 输出：cherry
> smembers druits // 输出：strawbrerry、apple

-- SRANDMEMBER KEY [count] （返回集合中一个或多个随机数）
> srandmember fruit // 输出：apple 

-- SREM KEY MEMBER1..MEMBERN （移除集合中的一个或多个成员元素，不存在的成员元素会被忽略）
> srem fruits apple // 输出：1
> smembers fruits // 输出：strawbrerry

-- SUNION KEY KEY1..KEYN (返回给定集合的并集。不存在的集合 key 被视为空集)
> flushdb
> sadd fruits apple cherry 
> sadd fruitsTwo apple strawberry
> sunion fruits fruitsTwo // 输出：cherry、strawberry、apple

-- SUNIONSTORE DESTINATION KEY KEY1..KEYN （将给定集合的并集存储在指定的集合 destination 中。如果 destination 已经存在，则将其覆盖）
> sunionstore fruitsThree fruits fruitsTwo
> smembers fruitsThree // 输出：cherry、strawberry、apple

-- SSCAN key cursor [MATCH pattern] [COUNT count] （用于迭代集合中键的元素）
> sscan fruitsThree 0 match a* // (
输出：1) "0"
     2) 1) "apple"
)
```

## zset 操作
```redis
 > flushdb

 -- ZADD KEY_NAME SCORE1 VALUE1.. SCOREN VALUEN
    // 用于将一个或多个成员元素及其分数值加入到有序集当中。
    // 如果某个成员已经是有序集的成员，那么更新这个成员的分数值，并通过重新插入这个成员元素，来保证该成员在正确的位置上。
    // 分数值可以是整数值或双精度浮点数。
    // 如果有序集合 key 不存在，则创建一个空的有序集并执行 ZADD 操作。
    // 当 key 存在但不是有序集类型时，返回一个错误。
 > zadd myzset 1 "one" // 输出：1
 > zadd myzset 1 "uno"
 > zadd myzset 2 "two" 3 "three"

 -- ZRANGE key start stop [WITHSCORES]
    // 返回有序集中，指定区间内的成员。
    // 其中成员的位置按分数值递增(从小到大)来排序。
    // 具有相同分数值的成员按字典序(lexicographical order )来排列。
    // 如果你需要成员按值递减(从大到小)来排列，请使用 ZREVRANGE 命令。
    // 下标参数 start 和 stop 都以 0 为底，也就是说，以 0 表示有序集第一个成员，以 1 表示有序集第二个成员，以此类推。
    // 你也可以使用负数下标，以 -1 表示最后一个成员， -2 表示倒数第二个成员，以此类推
 > zrange myzset 0 -1 WITHSCORES
 // 输出：
     1) "one"
     2) "1"
     3) "uno"
     4) "1"
     5) "two"
     6) "2"
     7) "three"
     8) "3"

 -- ZCARD KEY_NAME （用于计算集合中元素的数量）
 > zcard myzset // 输出：4

 -- ZCOUNT key min max (用于计算有序集合中指定分数区间的成员数量)
 > zcount myzset 1 3 // 输出：4

 -- ZINCRBY key increment member (对有序集合中指定成员的分数加上增量 increment)
 > zincrby myzset 2 "one" // 输出：3
 > zrange myzset 0 -1 WITHSCORES
 // 输出：
     1) "uno"
     2) "1"
     3) "two"
     4) "2"
     5) "one"
     6) "3"
     7) "three"
     8) "3"

 > zadd mid_test 70 Lhao 70 wjh
 > zadd fin_test 80 Lhao 78 wjh

 -- ZINTERSTORE destination numkeys key [key ...] [WEIGHTS weight [weight ...]] [AGGREGATE SUM|MIN|MAX] （计算给定的一个或多个有序集的交集，其中给定 key 的数量必须以 numkeys 参数指定，并将该交集(结果集)储存到 destination 。）
 > zinterstore sum_point 2 mid_test fin_test
 > zrange sum_point 0 -1 WITHSCORES
 // 输出：
     1) "wjh"
     2) "148"
     3) "Lhao"
     4) "150"

 -- ZLEXCOUNT KEY MIN MAX （计算有序集合中指定字典区间内成员数量）
 > zadd newzset 0 a 0 b 0 c 0 d 0 e 0 f 0 g
 > zlexcount newzset - + // 输出：7
 > zlexcount newzset [b [f // 输出：5

 -- ZRANGEBYLEX key min max [LIMIT offset count] (通过字典区间返回有序集合的成员)
 > zrangebylex newzset - [c
 // 输出：
     1) "b"
     2) "a"
     3) "c"
 > zrangebylex newzset - (c
  // 输出：
     1) "b"
     2) "a"
 > zrangebylex newzset [aaa (g
  // 输出：
     1) "b"
     2) "a"
     3) "c"
     4) "d"
     5) "e"
     6) "f"

 > zadd salary 2500 jack 5000 tom 12000 peter

 -- ZRANGEBYSCORE key min max [WITHSCORES] [LIMIT offset count]
    // 返回有序集合中指定分数区间的成员列表。有序集成员按分数值递增(从小到大)次序排列。
    // 具有相同分数值的成员按字典序来排列(该属性是有序集提供的，不需要额外的计算)。
    // 默认情况下，区间的取值使用闭区间 (小于等于或大于等于)，你也可以通过给参数前增加 ( 符号来使用可选的开区间 (小于或大于)
 > zrangebyscore salary -inf +inf #显示整个有序集
 // 输出：
     1) "jack"
     2) "tom"
     3) "peter"
 > zrangebyscore salary -inf +inf WITHSCORES # 显示整个有序集及成员的 score 值
 // 输出：
     1) "jack"
     2) "2500"
     3) "tom"
     4) "5000"
     5) "peter"
     6) "12000"
 > zrangebyscore salary -inf 5000 WITHSCORES # 显示工资 <=5000 的所有成员
 // 输出：
     1) "jack"
     2) "2500"
     3) "tom"
     4) "5000"
 > zrangebyscore salary (5000 400000 # 显示工资大于 5000 小于等于 400000 的成员
 // 输出：
    1) "peter"

 -- ZRANK key member （返回有序集中指定成员的排名。其中有序集成员按分数值递增(从小到大)顺序排列）
 > zrank salary tom // 输出：1 （ # tom 的薪水排名，第二）

 -- ZREM key member [member ...] (用于移除有序集中的一个或多个成员，不存在的成员将被忽略;当 key 存在但不是有序集类型时，返回一个错误)
 > zrem salary tom // 输出：1
 > zrangebyscore salary -inf +inf WITHSCORES
 // 输出：
     1) "jack"
     2) "2500"
     3) "peter"
     4) "12000"

 > zadd myzset 0 aaaa 0 b 0 c 0 d 0 e 0 foo 0 zap 0 zip 0 ALPHA 0 alpha

 -- ZREMRANGEBYLEX key min max（用于移除有序集合中给定的字典区间的所有成员）
 > zremrangebylex myzset [alpha [omega // 输出：6
 > zrange myzset 0 -1
 // 输出：
     1) "ALPHA"
     2) "aaaa"
     3) "zap"
     4) "zip"

 > zadd salary 5000 tom

 -- ZREMRANGEBYRANK key start stop（用于移除有序集中，指定排名(rank)区间内的所有成员）
 > zremrangebyrank salary 0 1 // 输出：2
 > zrange salary 0 -1 WITHSCORES 
 // 输出：
     1) "peter"
     2) "12000"

 > zadd salary 2500 jack 5000 tom

 -- ZREMRANGEBYSCORE key min max (用于移除有序集中，指定分数（score）区间内的所有成员)
 > zremrangebyscore salary 1500 3500 // 输出：1
 > zrange salary 0 -1 WITHSCORES
 // 输出：
     1) "tom"
     2) "5000"
     3) "peter"
     4) "12000"

 > zadd salary 2500 jack

 -- ZREVRANGE key start stop [WITHSCORES]（返回有序集中，指定区间内的成员；其中成员的位置按分数值递减(从大到小)来排列。具有相同分数值的成员按字典序的逆序(reverse lexicographical order)排列；除了成员按分数值递减的次序排列这一点外， ZREVRANGE 命令的其他方面和 ZRANGE 命令一样）
 > zrevrange salary 0 -1 WITHSCORES
 // 输出：
     1) "peter"
     2) "12000"
     3) "tom"
     4) "5000"
     5) "jack"
     6) "2500"

 -- ZREVRANGEBYSCORE key max min [WITHSCORES] [LIMIT offset count]（返回有序集中指定分数区间内的所有的成员。有序集成员按分数值递减(从大到小)的次序排列）
 > zrevrangebyscore salary +inf -inf # 逆序排列所有成员
 //输出：
     1) "peter"
     2) "tom"
     3) "jack"
 > zrevrangebyscore salary 10000 200 # 逆序排列薪水介于 10000 和 2000 之间的成员
 // 输出：
     1) "tom"
     2) "jack"

 -- ZREVRANK key member（返回有序集中成员的排名。其中有序集成员按分数值递减(从大到小)排序；排名以 0 为底，也就是说， 分数值最大的成员排名为 0 ；使用 ZRANK 命令可以获得成员按分数值递增(从小到大)排列的排名）
 > zrevrank salary peter // 输出：0
 > zrevrank salary tom // 输出：1

 -- ZSCORE key member (返回有序集中，成员的分数值。 如果成员元素不是有序集 key 的成员，或 key 不存在，返回 nil )
 > zscore salary peter // 输出：12000

 > zadd programmer 2000 peter 3500 jack 5000 tom
 > zadd manager 2000 herry 3500 mary 4000 bob

 -- ZUNIONSTORE destination numkeys key [key ...] [WEIGHTS weight [weight ...]] [AGGREGATE SUM|MIN|MAX]（计算给定的一个或多个有序集的并集，其中给定 key 的数量必须以 numkeys 参数指定，并将该并集(结果集)储存到 destination；默认情况下，结果集中某个成员的分数值是所有给定集下该成员分数值之和）

 > zunionstore salary 2 programmer manager WEIGHTS 1 3 # # 公司决定加薪。。。除了程序员。。。
 > zrange salary 0 -1 WITHSCORES
 // 输出：
      1) "peter"
      2) "2000"
      3) "jack"
      4) "3500"
      5) "tom"
      6) "5000"
      7) "herry"
      8) "6000"
      9) "mary"
     10) "10500"
     11) "bob"
     12) "12000"
```