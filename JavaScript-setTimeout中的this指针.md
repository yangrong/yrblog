yrblog
======

web development

作为第一个参数的函数将会在全局作用域中执行，因此函数内的 this 将会指向这个全局对象。

```js
function Foo() {
    this.value = 42;
    this.method = function() {
        // this 指向全局对象
        console.log(this.value); // 输出：undefined
    };
    setTimeout(this.method, 500);
}
new Foo();
```

这里输出 undefined,是因为this.method执行函数里面的this,指向的不是Foo的实例对象，而是windows对象，所以这里的this.value,是undedined；


在写组件的时候，遇到两次关于setTimeout的坑

