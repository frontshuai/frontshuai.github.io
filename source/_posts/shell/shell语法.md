---
title: shell语法
date: 2017-06-01 15:09:20
tags:
    - shell
categories: shell
---

# shell基础语法
```
#!/bin/bash        // 表明解析器
echo "Hello World !"
your_name="xiaoming"  # 声明变量
echo "I am $your_name" #变量使用
echo "I am ${your_name}" #大括号可省略
echo 'I am $your_name'   #单引号，变量不解析
echo ${#your_name}       #输出字符串长度
echo ${your_name:0:4}    #截取字符串

readonly your_name      #声明只读变量

test="test property"
echo $test
unset test
echo $test

a=2
b=4;
echo $b
echo `expr $a + $b`   #相加运算符号
printf "%-2s加上%-2s等于%-10s\n" $a $b `expr $a + $b`   # printf的使用

sum()
{
  return `expr $a + $b`
}

sum $a $b

echo "${a}加${b}等于$?"
files=`ls ./`         #执行命令
for file in ${files[*]}
do
  echo $file
done
books=("book1" "book2" "book3")
echo ${books[0]}   #访问单个数组元素
echo ${#books[*]}  #获得数组长度
for book in ${books[@]} #循环遍历数组
do
  echo $book
done

echo "test info" > /tmp/test #输出结果到文件/tmp/test
echo "test info 2" >> /tmp/test #输出结果追加到/tmp/test
echo "test info 3" >> /tmp/test 2>&1 #将输出和错误输入合并后追加输出到/tmp/test

echo `wc < /tmp/test`     #把／tmp/test文件作为输入
command > file 2>&1
#包含外部文件
#. filename
#source filename

```