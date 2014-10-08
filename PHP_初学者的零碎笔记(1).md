#### PHP_初学者的零碎笔记

##### 变量

###### global 关键词
关键词用于访问函数内的全局变量，可被函数外部访问 <br/>
要做到这一点，请在（函数内部）变量前面使用 global 关键词，声明在函数外部会报错。

一般普通的变量，函数内部不能访问函数外部的变如下

```php
$x=5; // 全局作用域

function myTest() {

  echo "变量 x 是：$x";

}


 myTest();
 
```

函数报错，显示x没有定义。

如果函数内部要访问函数外的变量，使用如下方法：
PHP 在名为 $GLOBALS[index] 的数组中存储了所有全局变量。变量的名字就是数组的键。
```php
$x=5;
$y=10;

function myTest() {
  $GLOBALS['y']=$GLOBALS['x']+$GLOBALS['y'];
} 

myTest();
echo $y; // 输出 15
```

###### static 关键词

通常，当函数完成/执行后，会删除所有变量。不过，有时我需要不删除某个局部变量。实现这一点需要更进一步的工作。
要完成这一点，请在您首次声明变量时使用 static 关键词.

这里比较像，是js的全局变量，我们在函数中，变量前没有定义var 表示是全局变量，当函数运行的时候，改变的变量的值会影响全局。
```php
function myTest() {
  static $x=0;
  echo $x;
  $x++;
}

myTest();//0
myTest();//1
myTest();//2

```

###### strlen() 函数返回字符串的长度，以字符计。
```php
echo strlen("Hello world!");//12
```


###### count() 函数返回数组的长度
```php
$cars=array("Volvo","BMW","SAAB");
$arrlength=count($cars);//3
```


###### PHP strpos() 函数 (类似indexof的方法)
```php
echo strpos("Hello world!","world");//6
```


##### PHP 常量

定义常量的实例：
```php
define("GREETING", "Welcome to W3School.com.cn!", true);//f对大小写不敏感
echo GREETING;// Welcome to W3School.com.cn!
echo "<br>";
echo greeting;// Welcome to W3School.com.cn!


// 定义对大小写敏感的常量
define("GREETING_1", "Welcome to W3School.com.cn!");
echo GREETING_1;// Welcome to W3School.com.cn!
echo "<br>";
// 不会输出常量的值
echo greeting_1;
```

##### PHP 字符串运算符
```php
$a = "Hello";
$b = $a . " world!";
echo $b; // 输出 Hello world!

$x="Hello";
$x .= " world!";
echo $x; // 输出 Hello world!
```

##### PHP 逻辑运算符

xor	 异或	$x xor $y	如果 $x 和 $y 有且仅有一个为 true，则返回 true。


##### PHP 数组运算符(PHP 数组运算符用于比较数组)



如下：
```php
$x = array("a" => "red", "b" => "green"); 
$y = array("c" => "blue", "d" => "yellow"); 
$z = $x + $y; // $x 与 $y 的联合
var_dump($z);//array(4) { ["a"]=> string(3) "red" ["b"]=> string(5) "green" ["c"]=> string(4) "blue" ["d"]=> string(6) "yellow" }
var_dump($x == $y);//bool(false)
var_dump($x === $y);//bool(false)
var_dump($x != $y);//bool(true)
var_dump($x <> $y);//bool(true)
var_dump($x !== $y);//bool(true)
```

##### PHP 默认参数值
```php
function setHeight($minheight=50) {
  echo "The height is : $minheight <br>";
}

setHeight(350);
setHeight(); // 将使用默认值 50
setHeight(135);
setHeight(80);
```

##### PHP 关联数组（相当于是js的对象）
```php
$age=array("Peter"=>"35","Ben"=>"37","Joe"=>"43");
```

