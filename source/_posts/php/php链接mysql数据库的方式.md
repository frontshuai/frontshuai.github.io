---
title: php链接mysql数据库的方式
date: 2017-02-09 16:27:36
tags:
    - php
categories: php
---
# mysql连接数据库共三种方式
## 1.mysql扩展
>**Warning**
本扩展自 PHP 5.5.0 起已废弃，并在将来会被移除。应使用 MySQLi 或 PDO_MySQL 扩展来替换之。参见 MySQL：选择 API 指南以及相关 FAQ 以获取更多信息。用以替代本函数的有：
mysqli_connect()
PDO::__construct()

在新写的代码中不建议使用该方式连接数据库。
详细介绍：http://php.net/manual/zh/book.mysql.php


## 2.mysqli扩展(有时候称mysql增强扩展)
可以连接mysql4.1及以上版本，mysqli在php5及以上版本中支持。
相对于mysql扩展，mysqli增加了
* 面向对象接口
* prepared语句支持（译注：关于prepare请参阅mysql相关文档）
* 多语句执行支持
* 事务支持
* 增强的调试能力
* 嵌入式服务支

详细介绍：http://php.net/manual/zh/book.mysqli.php

## PDO
PHP数据对象，是PHP应用中的一个数据库抽象层规范。PDO提供了一个统一的API接口可以使得你的PHP应用不去关心具体要 连接的数据库服务器系统类型。也就是说，如果你使用PDO的API，可以在任何需要的时候无缝切换数据库服务器，比如从Firebird 到MySQL，仅仅需要修改很少的PHP代码。
详细介绍：http://php.net/manual/zh/book.pdo.php