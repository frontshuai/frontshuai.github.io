---
title: php调试常用方式
date: 2017-03-24 17:01:10
categories: php
tags:
    - php
    - 调试
---

##php错误退出时，打印错误日志

```
function shutdown_function()
{
    $e = error_get_last();
    print_r($e);
}
register_shutdown_function('shutdown_function');
```

##代码直接退出返回json数据结构，调试数据
```
header('Content-Type: application/json');
echo json_encode(array('test' => 'testInfo'));exit;
```