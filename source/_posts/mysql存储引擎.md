---
title: mysql存储引擎
date: 2017-02-10 16:46:10
tags:
    - mysql
    - 存储引擎
categories: mysql
---
MySQL5.5以后默认使用InnoDB存储引擎，其中InnoDB和BDB提供事务安全表，其它存储引擎都是非事务安全表。
#InnoDB
InnoDB存储引擎提供了具有提交、回滚和崩溃恢复能力的事务安全。但是对比MyISAM的存储引擎，InnoDB写的处理效率差一些并且会占用更多的磁盘空间以保留数据和索引。
#MyISAM
它不支持事务，也不支持外键，尤其是访问速度快，对事务完整性没有要求或者以SELECT、INSERT为主的应用基本都可以使用这个引擎来创建表。

