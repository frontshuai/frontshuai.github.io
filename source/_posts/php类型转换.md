---
title: php类型转换
date: 2017-02-10 14:51:31
tags:
    - php
---
php类型转换一共三种方式
## 在变量前加圆括号，括号内为目标类型
```
<?php
$a = (int)'11';  // 把'11'转化为int型
$b = (float)'11'; // 把'11'转化为float型
```

## 使用intval,floatval,strval函数转换

```
<?php
$a = intval('11'); // 把'11'转化为int型
$b = floatval('11'); // 把'11'转化为float型
```

## 使用settype函数
```
<?php
$a = '11';
settype($a, 'int'); // 把'11'转化为int型
settype($a, 'float'); // 把'11'转化为float型
```