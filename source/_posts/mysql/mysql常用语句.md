---
title: mysql常用语句
date: 2017-02-11 02:16:39
tags:
    - mysql
categories: mysql
---
## 基础操作
1. 登陆mysql
```
root> mysql -u username -p
```
回撤之后输入密码
2. 修改用户密码
```
mysql> update user set password=password("newPassword") where user="root";
```
3. 添加新用户
 + 新用户test可以在任何机器上登陆，对所有库和表并有增删改查的权限
```
mysql> grant select,delete,update,create,drop on *.* to test@"%" identified by "1234"
```
 + test，对db1下所有表有权限，只能通过特定ip机器登陆
 ```
 mysql> grant select,delete,update,create,drop on db1.* to test@"10.127.10.20" identified by "1234"
 ```
4. 对库的操作
 + 创建库
 ```
 mysql> create database db2;
 ```
 + 显示所有数据库
 ```
 mysql> show databases;
 ```
 + 选中数据库
 ```
 mysql> use db2;
 ```
 + 删除数据库
 ```
 mysql> drop database db2;
 ```
5. 对表的基本操作
 + 创建表
 ```
 mysql> create table tableName(<字段名1> <类型1> [,..<字段名n> <类型n>]);
 ```
 + 删除表
 ```
 mysql> drop table tableName;
 ```
 + 插入数据
 ```
 mysql> insert into <表名> [( <字段名1>[,..<字段名n > ])] values ( 值1 )[, ( 值n )];
 ```
 + 选择数据
 ```
 mysql> select <字段1，字段2，...> from < 表名 > where < 表达式 >;
 ```
 + 删除数据
 delete from 表名 where 表达式
 + 修改数据
 update MyClass set name='Mary' where id=1;
 + 添加字段
 alter table 表名 add字段 类型 其他;
 + 添加索引
 alter table 表名 add index 索引名 (字段名1[，字段名2 …]);
 + 删除索引
 alter table 表名 drop index 索引名;
 + 添加字段
 ALTER TABLE table_name ADD field_name field_type;
 + 修改原字段
 ALTER TABLE table_name CHANGE old_field_name new_field_name field_type;
 + 删除字段
 ALTER TABLE table_name DROP field_name;
 + 修改表名
 rename table 原表名 to 新表名;
5. 导出数据
 + 导出库数据
 mysqldump -u 用户名 -p 数据库名 > 导出的文件名
 + 导出表数据
 mysqldump -u 用户名 -p 数据库名 表名> 导出的文件名