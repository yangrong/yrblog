yrblog
======

##### 检测一个对象的类型

为了检测一个对象的类型，强烈推荐使用 Object.prototype.toString 方法； 因为这是唯一一个可依赖的方式。正如上面表格所示，typeof 的一些返回值在标准文档中并未定义， 因此不同的引擎实现可能不同。

除非为了检测一个变量是否已经定义，我们应尽量避免使用 typeof 操作符。

```js
onsole.log(Object.prototype.toString.call(123)) //[object Number]
console.log(Object.prototype.toString.call('123')) //[object String]
console.log(Object.prototype.toString.call(undefined)) //[object Undefined]
console.log(Object.prototype.toString.call(true)) //[object Boolean]
console.log(Object.prototype.toString.call({})) //[object Object]
console.log(Object.prototype.toString.call([])) //[object Array]
console.log(Object.prototype.toString.call(function(){})) //[object Function]
```

```js
Object.prototype.toString.call(function(){}) == '[object Function]'  //true

```


而instanceof 操作符用来比较两个操作数的构造函数。只有在比较自定义的对象时才有意义。 如果用来比较内置类型，将会和 typeof 操作符 一样用处不大。

```js
function Foo() {}
function Bar() {}
Bar.prototype = new Foo();

new Bar() instanceof Bar; // true
new Bar() instanceof Foo; // true

// 如果仅仅设置 Bar.prototype 为函数 Foo 本身，而不是 Foo 构造函数的一个实例
Bar.prototype = Foo;
new Bar() instanceof Foo; // false

```

```js
new String('foo') instanceof String; // true
new String('foo') instanceof Object; // true

'foo' instanceof String; // false
'foo' instanceof Object; // false

```


##### 数据类型转化

###### 转换为字符串
```js
'' + 10 === '10'; // true
```
将一个值加上空字符串可以轻松转换为字符串类型。

转换为数字
```js
+'10' === 10; // true
```
1. 当需要将数字转换成字符时，采用如下方式："" + 1。从性能上来看，将数字转换成字符时，有如下公式：("" +) > String() > .toString() > new String()。String()属于内部函数，所以速度很快。而.toString()要查询原型中的函数，所以速度逊色一些，new String()需要重新创建一个字符串对象，速度最慢。
2.  当需要将浮点数转换成整型时，应该使用Math.floor()或者Math.round()。而不是使用parseInt(),该方法用于将字符串转换成数字。而且Math是内部对象，所以Math.floor()其实并没有多少查询方法和调用时间，速度是最快的。

这里说到使用“+“运算符来转化变量类型，顺便mark一下一些关于运算符的小知识。<br>

使运算符时，尽量使用+＝，－＝、*＝、\=等运算符号，而不是直接进行赋值运算。

++ 运算
我们知道 ++运算就是让一个数字自身，+1。
```js
var num;
num++;
console.log(num);//NaN
```
其实这里是一个很低级错误，就是null初始化，没有声明是数字类型，呵呵。
初始化
```js
var num=0;
num++;
console.log(num);//1
```

###### 转换为布尔型

通过使用 否 操作符两次，可以把一个值转换为布尔型。
```js
!!'foo';   // true
!!'';      // false
!!'0';     // true
```

布尔类型，关键字：<br>
null <br>
"" <br>
undefined <br>
false <br>
0 <br>
 NaN <br>
除去以上六种情况，其他任何时候都是返回的是 true。


#### null和undefined的区别？

null是一个表示"无"的对象，转为数值时为0；undefined是一个表示"无"的原始值，转为数值时为NaN。

当声明的变量还未被初始化时，变量的默认值为undefined。
null用来表示尚未存在的对象，常用来表示函数企图返回一个不存在的对象。

undefined表示"缺少值"，就是此处应该有一个值，但是还没有定义。典型用法是：

（1）变量被声明了，但没有赋值时，就等于undefined。

（2) 调用函数时，应该提供的参数没有提供，该参数等于undefined。

（3）对象没有赋值的属性，该属性的值为undefined。

（4）函数没有返回值时，默认返回undefined。


null表示"没有对象"，即该处不应该有值。典型用法是：

（1） 作为函数的参数，表示该函数的参数不是对象。

（2） 作为对象原型链的终点。

