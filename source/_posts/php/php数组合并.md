---
title: php数组合并
date: 2017-02-10 14:51:31
categories: php
tags:
    - php
---

# php数组合并
1. 数组运算符操作：+
>
The + operator returns the right-hand array appended to the left-hand array; for keys that exist in both arrays, the elements from the left-hand array will be used, and the matching elements from the right-hand array will be ignored.
两个数组相加结果为把第二个数组链接在第一个数组之后，如果两个数组有key重复的就取第一个数组，抛弃第二个数组

2. 数组函数：array_merge
>
If the input arrays have the same string keys, then the later value for that key will overwrite the previous one. If, however, the arrays contain numeric keys, the later value will not overwrite the original value, but will be appended.
如果输入的数组中有相同的字符串键名，则该键名后面的值将覆盖前一个值。然而，如果数组包含数字键名，后面的值将不会覆盖原来的值，而是附加到后面。


## 例子

```
$a = array(
    0 => 1,
    1 => 2
);
$b = array(
    0 => 3
    2 => 4
);

$c1 = $a + $b; // $c结果为  array(0 => 1, 1 => 2, 2=> 2)
$c2 = array_merge($a, $b) // 结果是 array(0 => 1, 1 => 2, 2=> 3, 3 => 4)
$d = array(f
    'a' => 111,
    'b' => 222,
);

$e = array(
    'a' => 333,
    'c' => 444
);
$f1 = $a + $b; // 结果是 array('a' => 111, 'b' => 222, 'c' => 444)

$f2 = array_merge($a, $b) // 结果是 array('a' => 333, 'b' => 222, 'c' => 444)

```