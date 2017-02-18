---
title: mysql学习笔记（一）
date: 2017-02-10 23:48:45
tags:
    - mysql
    - 存储引擎
categories: mysql
---
# mysql逻辑架构
![mysql逻辑架构图](http://ol3m0nyfn.bkt.clouddn.com/2012031510324452.png)
mysql逻辑架构图一共分为三层
1. 连接处理，授权认证，安全等
2. 包括查询解析、分析、优化、缓存以及其他内置函数。所有跨存储引擎的功能都在这一层实现：存储过程、触发器、视图等
3. 包括存储引擎。存储引擎负责MySQL中数据的存储和提取

# 并发控制
当有大量的查询需要同时修改数据时，都会产生并发控制的问题。

锁的类型分为读锁和写锁

锁的粒度分为表锁和行级锁

锁会带来的问题：在进行标的修改时，例如使用alter table修改大表的时候会导致长时间锁表

# 事务
事务就是一组原子性的查询，或则说是一个独立的工作单元。
事务ACID特性

1. 原子性（atomicity）- 事务被视为最小的不可分割的工作单元。
2. 一致性（consistency）- 数据库总是重一个状态变到另一个状态，就事务内的所有语句要不全执行，要不都不执行。
3. 隔离性（isolation) - 事务在执行完毕之前，对其他事务是不可见的。
4. 持久性（durability）- 一旦事务提交，则其修改就会永久保存到数据库。

# 隔离级别
1. READ UNCOMMITED(未提交读) - 该级别中的事务修改，即使没有提交，对其他事务也是可见的。事务可以读取为提交的数据也叫脏读。
会导致很多问题，从性能上说不会比其他级别好很多，但却缺其他级别的很多好处。很少使用。
2. READ COMMIT(提交读) - 大部分数据库系统都是该级别。该级别下，一个事务在完全执行完之前，对其他事务是不可见的。
3. REPEATABLE READ(可重复读) - 该级别保证同一个事务多次读取同样记录的结果是一样的。在两次读的中间会有其他事务对数据进行修改导致不一致。
InnoDB和XtraDB存储引擎通过多版本并发控制解决该问题（幻读）。该级别为数据库默认级别。
4. SERIALIZABLE(可串行化) 最高级别隔离，强制事务串行执行，避免可重复读中会产生的幻读问题。实际上就是该级别下都强制加锁，但是会导致大量的超时和锁争用的问题。

# MySQL中事务
mysql提供了两种事务型存储引擎：InnoDB和NDBCluster。
MySQL默认采用自动提交的模式。如果不是显示地开始一个事务，则每个查询都别当作一个事务执行提交操作。在当前连接中，可以通过
设置AUTOCOMMIT变量来启用或禁用自动提交模式。

```
mysql> show variables like 'autocommit';
```
|Variable_name|Value|
|:-|-|
|autocommit|on|

关闭自动提交
```
mysql>set autommit=0;
```
> commit的巧用：如上所说mysql都是默认事务并是自动提交的。所以在进行大数据插入时可设置autocommit=0,在插入完
所有数据后再设置autommit=1。这样做能提升插入速度。

# mysql设置隔离级别
设置mysql整体级别
```
mysql> set transaction isolation level read committed;
```
设置mysql当前隔离级别
```
myslq> set session transaction isolation level read committed;
```
# MySQL的存储引擎
存储引擎是针对表级别的，同一个库里可以有不同的引擎表。
mysql5.1之后的引擎默认是InnoDB。
例如查看user表是什么引擎：
第一种
```
mysql> show table status like 'user';
```
第二种
```
mysql>show create table user;
```
## InnoDB
InnoDB表是基于聚簇索引建立的。聚簇索引对主键查询性能很高，但是二级索引会包含主键列，所以如果主键列如果很大，其他所有
索引都会很大。InnoDB表采用MVCC来支持高并发，并且实现了四个标准的隔离级别。其默认级别是REPEATABLE READ。
## MyISAM
MySQL5.1之前的默认存储引擎。MyISAM提供大量的特性，包括全文索引、压缩、空间函数。但是MyISAM不支持事务和行级锁。
## Archive
只支持insert和select。select需要全表扫描（适合日志和数据采集类应用）。或则在需要快速insert的场景下需要
## Blackhole
该引擎没有实现任何的存储机制，他会丢弃所有的插入数据。只是做日志记录，可以用于复制数据到备份。

## CSV
## Federated
# Merge
Merge引擎是MyISAM的一个变种。
# Memory
数据不会被修改，重启以后丢失也没用，可以使用Memory表。