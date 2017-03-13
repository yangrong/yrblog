数组随机排序
-----------------

JavaScript 开发中有时会遇到要将一个数组随机排序（shuffle）的需求，一个常见的写法是这样：

```js
function shuffle(arr) {
   arr.sort(function () {
      return Math.random() - 0.5;
   });
}
```


这种写法是有问题的，它并不能真正地随机打乱数组。推荐下面的Fisher–Yates shuffle 算法，

一个实现如下（ES6）：
```js
function shuffle(arr) {
    let i = arr.length;
    while (i) {
        let j = Math.floor(Math.random() * i--);
        [arr[j], arr[i]] = [arr[i], arr[j]];
    }
}
```

一个实现如下（ES5）：
```js
function shuffle(arr) {
  var i = arr.length, t, j;
  while (i) {
    j = Math.floor(Math.random() * i--);
    t = arr[i];
    arr[i] = arr[j];
    arr[j] = t;
  }
}
```

本文参考 [关于 JavaScript 的数组随机排序]: http://web.jobbole.com/90696/
