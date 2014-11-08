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

###### 转换为布尔型

通过使用 否 操作符两次，可以把一个值转换为布尔型。
```js
!!'foo';   // true
!!'';      // false
!!'0';     // true
```

