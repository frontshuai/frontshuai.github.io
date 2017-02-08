---
title: {{ title }}
date: {{ date }}
tags: [nginx,location]
---
|模式     |含义|
|:---------:|:----:|
|location = /uri| = 表示精确匹配只有完全相等才会匹配成功|
|location ^~ /uri| ^~ 表示对路由进行前缀匹配|
|location ~ /uri| ~ 表示对路由进行正则匹配|
|location ~* /uri| ~* 表示对路由进行不区分大小写的正则匹配|
|location /uri| 不带任何修饰符也表示前缀匹配|
|location /| 默认匹配，任何没有匹配到的uri