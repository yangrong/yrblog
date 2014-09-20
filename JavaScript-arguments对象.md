yrblog
======

##### arguments 对象

JavaScript 中每个函数内都能访问一个特别变量 arguments。这个变量维护着所有传递到这个函数中的参数列表。

注意: 由于 arguments 已经被定义为函数内的一个变量。 因此通过 var 关键字定义 arguments 或者将 arguments 声明为一个形式参数， 都将导致原生的 arguments 不会被创建。
arguments 变量不是一个数组（Array）。 尽管在语法上它有数组相关的属性 length，但它不从 Array.prototype 继承，实际上它是一个对象（Object）。

因此，无法对 arguments 变量使用标准的数组方法，比如 push, pop 或者 slice。 虽然使用 for 循环遍历也是可以的，但是为了更好的使用数组方法，最好把它转化为一个真正的数组。


传递参数

下面将参数从一个函数传递到另一个函数，是推荐的做法。
```js
function foo() {
    bar.apply(null, arguments);
}
function bar(a, b, c) {
    // do stuff here
}
```

虽然arguments对象不是一个真正的javascript数组，但是我们还是可以轻易的把它转换成标准的数据 ，然后进行数组操作。
```js
var args = Array.prototype.slice.call(arguments);
```
