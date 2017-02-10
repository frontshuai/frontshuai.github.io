---
title: nginx日志分割
tags:
    - nginx
date: 2017-02-09 16:10:13
categories: nginx
---
配置日志循环，而不需使用logrotate或配置cron任务。需要使用到$time_iso8601 内嵌变量来获取时间。$time_iso8601格式如下：2015-08-07T18:12:02+02:00。然后使用正则表达式来获取所需时间的数据。
按天分割日志
$time_iso8601格式如下：2015-08-07T18:12:02+02:00
按天分割：
```
if ($time_iso8601 ~ "^(\d{4})-(\d{2})-(\d{2})") {
    set $year $1;
    set $month $2;
    set $day $3;
}
access_log /data/logs/nginx/test.com-$year-$month-$day-access.log;
```

也可以使用Perl语法来捕获，如下：


```
if ($time_iso8601 ~ "^(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})") {}
access_log /data/logs/nginx/www.ttlsa.com-$year-$month-$day-access.log;
```

按小时分割：

```
if ($time_iso8601 ~ "^(\d{4})-(\d{2})-(\d{2})T(\d{2})")
{
    set $year $1;
    set $month $2;
    set $day $3;
    set $hour $4;
}
access_log /data/logs/nginx/test.com-$year-$month-$day-$hour-access.log;
```
