---
title: nginx location路由匹配规则
date: 2017-02-08 18:59:48
tags:
  - nginx
  - location
categories: nginx
---
| 模式     | 含义 |
| :---------: | :----: |
| location = /uri | = 表示精确匹配只有完全相等才会匹配成功 |
| location ^~ /uri | ^~ 表示对路由进行前缀匹配 |
| location ~ /uri | ~ 表示对路由进行正则匹配 |
| location ~* /uri | ~* 表示对路由进行不区分大小写的正则匹配 |
| location /uri | 不带任何修饰符也表示前缀匹配 |
| location /| 默认匹配，任何没有匹配到的uri |

多个 location 配置的情况下匹配顺序为(匹配到某一等级就结束，同一规则时匹配长度长的优先):

1. 首先精确匹配 =
2. 其次前缀匹配 ^~
3. 其次是按文件中顺序的正则匹配
4. 然后匹配不带任何修饰的前缀匹配。
5. 最后是交给 / 通用匹配
6. 当有匹配成功时候，停止匹配，按当前匹配规则处理请求

例子：
```
location = / {
   echo "规则A";
}
location = /login {
   echo "规则B";
}
location ^~ /static/ {
   echo "规则C";
}
location ^~ /static/files {
    echo "规则X";
}
location ~ \.(gif|jpg|png|js|css)$ {
   echo "规则D";
}
location ~* \.png$ {
   echo "规则E";
}
location /img {
    echo "规则Y";
}
location / {
   echo "规则F";
}
```
测试uri及nginx结果:

1. 访问根目录 /，比如 http://localhost/ 将匹配 规则A
2. 访问 http://localhost/login 将匹配 规则B，http://localhost/register 则匹配 规则F
3. 访问 http://localhost/static/a.html 将匹配 规则C
4. 访问 http://localhost/static/files/a.exe 将匹配 规则X，虽然 规则C 也能匹配到，但因为最大匹配原则，最中选中了 规则X。你可以测试下，去掉规则 X ，则当前 URL 会匹配上 规则C。
5. 访问 http://localhost/a.gif, http://localhost/b.jpg 将匹配 规则D 和 规则 E ，但是 规则 D 顺序优先，规则 E 不起作用，而 http://localhost/static/c.png 则优先匹配到 规则 C
6. 访问 http://localhost/a.PNG 则匹配 规则 E ，而不会匹配 规则 D ，因为 规则 E 不区分大小写。
7. 访问 http://localhost/img/a.gif 会匹配上 规则D,虽然 规则Y 也可以匹配上，但是因为正则匹配优先，而忽略了 规则Y。
8. 访问 http://localhost/img/a.tiff 会匹配上 规则Y。
