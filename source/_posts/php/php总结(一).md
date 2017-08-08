---
title: php总结(一)
date: 2017-05-17 15:09:00
tags:
	- php
---

# shell
1. php执行shell
```
exec('whoami', $res, $status)
foreach($res as $item) {
	echo $item;  // $res保存的是一个数组，没一行为数组中一个元素
}
echo $status; // 保存外部命令返回的状态吗
```

```
echo shell_exec('whoami'); // 执行外部命令并返回数组结果
```

```
 system('whoami');  //执行外部命令，并输出执行结果
```
# 系统变量
1. 获得系统变量
```
phpinfo(); //输出系统变量和php配置等
```

```
echo $_ENV('USER'); // 获得执行命令用户名
```

```
echo getenv('USER'); // 获得执行命令用户名
```

```
putenv('USER=test'); // 只在当前请求中生效
echo getenv('USER'); //输出test，
```
$_ENV,putenv互相不影响

# 一个全能的类

```
namespace App\Test2\;
trait Test2A {
    function getReturnType() { /*1*/ }
    function getReturnDescription() { /*2*/ }
}
```
```
namespace App\Test;  // 域名空间
use App\Test2\Test2A; // 引用类
public class test {    // 类申明
	const constStatic = 'const static'; // 类常量，声明不能带$符号
	public $var1;
	public $var2 = 'var2 value';
	protected $var3 = 'protected';
	private $var4 = '$var4 value';
	public static $staticVar = 'static val';
	
	
	use Test2A;   // 复用trait
	
	
	public function __construct() {
		echo 'create new class';  // 当new创建类的时候会被调用
	}
	
	public function __destruct() {
		echo 'destruct class'; // 析构函数即使在使用 exit() 终止脚本运行时也会被调用
	}
	
	
	
	public function func1() {。  // 被定义为公有的类成员可以在任何地方被访问
		echo $this->$var2;
	}
	
	protected function func1() {   // 被定义为受保护的类成员则可以被其自身以及其子类和父类访问
		echo $this->$var2;
	}
	
	private function func1() {     // 被定义为私有的类成员则只能被其定义所在的类访问
		echo static::$staticVar;   // 优先输出子类的属性
		static::staticFun2()       //
		echo self::$staticVar;     // 输出改语句在的类的属性，如果没有改属性会抛错
	}
	
	public static function staticFun2()
	{
		echo 'static function';
		// $this->func1();        // 静态方法无法调用非静态方法
	}
	
	public function __call($name, $arguments)  // 当调用不可达方法时会调用改方法
	{
		echo "call function " . $name . " with arguments " . implode(',', $arguments);
	}
	
	
	public function __callStatic($name, $arguments) // 当调用不存在的static function时，该方法被调用
	{
		echo "call static function " . $name . " with arguments " . implode(',', $arguments);
	}
	
	
	public function __set()    // 当设置不存在的属性的时候调用
	{
		echo "set a null property";
	}
	
	
	public function __get()   // 当取不存在的属性是被调用
	{
		echo "get a null property";
	}
	
	public function __isset()   // 当用isset() 或 empty() 判断不可达的属性的时候会被调用
	{
		echo "call isset at inaccessible properties";
	}
	
	public function __unset()    // 当在不可达的属性在调用unset的时候会被调用
	{
		echo "call when unset used on inaccessible properties";
	}
	
	
	public function __sleep() // 当对象被serialize()时，该函数被调用
	{
		return array('var1');
	}
	
	public function __wakeup() // 当unserialize() one function时，该函数会被调用
	{
		echo "this function will be call when unserialize() this function";
	}
	
	
	public function __toString()  // 当对象被当作字符串使用时，值是该函数返回的值
	{
		return "I am a string";
	}
	
	
	public function __invoke()
	{
		return 'I am a class";
	}
	
	public funtion __debuginfo()  // 当使用var_dump时，会使用该函数的返回内容
	{
		return 'This method is called by var_dump() when dumping an object to get the properties that should be shown';
	}
	
	public function __clone() // 当对象复制完成后会调用该函数
	{
		echo "asdfadf";
	}
	
	public static function __set_state($an_array) // 当使用var_export的时候，该函数被调用
    {
        $obj = new A;
        $obj->var1 = $an_array['var1'];
        $obj->var2 = $an_array['var2'];
        return $obj;
    }
	
}

```

