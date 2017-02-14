---
title: mysql转换表的引擎
date: 2017-02-11 02:04:45
tags:
    - mysql
categories: mysql
---
三种方式
1. alter table
> 该方式需要执行很长时间
```
mysql> alter table mytable engine=InnoDB;
```
2. 导入导出
使用mysqldump导出表，修改导出文件里的create table后面表的名称。
创建新的表。
> mysqldump导出的表里会包含drop table，所以要注意！删除该句。防止数据丢失

3. 创建和查询

```
mysql> create table new_table_name like table_name;
mysql> alter table new_table_name engine=InnoDB;
mysql> insert into new_table_name select * from table_name;
```
