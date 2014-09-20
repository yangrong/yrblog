$.each 和$(selector).each()的区别
====================

本文转自别人的博客，在此基础上，添加了一些记录笔记。


$.each()

Posted on 2012 年 3 月 15 日 in jQuery, jQuery函数
|
by Jason
|
译自官方手册:jQuery.each()
对数组或对对象内容进行循环处理
jQuery.each( collection, callback(indexInArray, valueOfElement) )

collection   遍历的对象或数组

callback(indexInArray, valueOfElement) 在每一个对象上调用的函数

说明

一个通用的遍历函数 , 可以用来遍历对象和数组. 数组和含有一个length属性的伪数组对象 (伪数组对象如function的arguments对象)以数字索引进行遍历,从0到length-1, 其它的对象通过的属性进行遍历.

$.each()与$(selector).each()不同, 后者专用于jquery对象的遍历, 前者可用于遍历任何的集合(无论是数组或对象),如果是数组,回调函数每次传入数组的索引和对应的值(值亦可以通过this 关键字获取,但javascript总会包装this 值作为一个对象—尽管是一个字符串或是一个数字),方法会返回被遍历对象的第一参数
这里的值亦可以通过this，如果是数组的话，this，就是对应的each循环到的数组的值，如果是对象的话，就value的值。

```html 
//例子:———传入数组

<!DOCTYPE html>
<html>
<head>
<script src=”http://code.jquery.com/jquery-latest.js”></script>
</head>
<body>
<script>

$.each([52, 97], function(index, value) {
alert(index + ': ' + value);
});

</script>
</body>
</html>

//输出

0: 52
1: 97
```


```html 
//例子:———如果一个映射作为集合使用,回调函数每次传入一个键-值对

<!DOCTYPE html>
<html>
<head>
<script src=”http://code.jquery.com/jquery-latest.js”></script>
</head>
<body>
<script>

var map = {
'flammable': 'inflammable',
'duh’: 'no duh’
};
$.each(map, function(key, value) {
alert(key + ': ' + value);
});

</script>
</body>
</html>

//输出

flammable: inflammable
duh: no duh


```



```html 

//例子:———回调函数中 return false时可以退出$.each(), 如果返回一个非false 即会像在for循环中使用continue 一样, 会立即进入下一个遍历


<!DOCTYPE html>

<html>

<head>

  <style>

  div { color:blue; }

  div#five { color:red; }

  </style>

  <script src='http://code.jquery.com/jquery-latest.js'></script>

</head>

<body>

  <div id='one'></div>

  <div id='two'></div>

  <div id='three'></div>

  <div id='four'></div>

  <div id='five'></div>

<script>

    var arr = [ "one", "two", "three", "four", "five" ];//数组

    var obj = { one:1, two:2, three:3, four:4, five:5 }; // 对象

    jQuery.each(arr, function() {  // this 指定值

      $('#' + this).text('Mine is ' + this + '.');  // this指向为数组的值, 如one, two

       return (this != 'three'); 
      
       // 如果this = three 则退出遍历 因为第一次执行，第二次执行，都返回true 循环继续，第三次，返回false退出each操作。

   });

    jQuery.each(obj, function(i, val) {  // i 指向键, val指定值

      $('#' + i).append(document.createTextNode(” – ” + val));

    });

</script>

</body>

</html>

// 输出

Mine is one. – 1
Mine is two. – 2
Mine is three. – 3
- 4
- 5

```




```html 
//例子:———遍历数组的项, 传入index和value

<!DOCTYPE html>
<html>
<head>
<script src='http://code.jquery.com/jquery-latest.js'></script>
</head>
<body>
<script>
$.each( ['a','b','c'], function(i, l){
alert( 'Index #' + i + ': ' + l );
});

</script>
</body>
</html>

```





```html 


//例子:———遍历对象的属性,传入 key和value

<!DOCTYPE html>
<html>
<head>
<script src='http://code.jquery.com/jquery-latest.js'></script>
</head>
<body>
<script>

$.each( { name: “John”, lang: “JS” }, function(k, v){
alert( 'Key: ' + k + ' Value: ' + v );
});

</script>
</body>
</html>

```









1. 如果不想输出第一项 (使用retrun true)进入 下一遍历

```html 
<!DOCTYPE html>
<html>
<head>
<script src='http://code.jquery.com/jquery-latest.js'></script>
</head>
<body>
<script>

var myArray=["skipThis", "dothis", "andThis"];
$.each(myArray, function(index, value) {
if (index == 0) {
return true; // equivalent to ‘continue’ with a normal for loop
}
// else do stuff…
alert (index + ': '+ value);
});

</script>
</body>
</html>

```
