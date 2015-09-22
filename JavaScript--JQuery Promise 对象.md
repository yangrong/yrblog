## JQuery Promise 对象



延迟对象，在jQuery的1.5引入，是通过调用jQuery.Deferred()方法创建一个可链式调用的工具对象。 它可以注册多个回调到回调队列， 调用回调队列，准备代替任何同步或异步函数的成功或失败状态。

延迟对象是可链式调用的，类似于jQuery对象是可链接的方式，  但它有其自己的方法。 创建一个Deferred（延迟）对象后，你可以通过使用下面任何方法 直接从对象创建或者链式调用 或 保存对象的一个变量，调用该变量的一个或多个方法。

Promises是jQuery.Deferred()的一个方法－－返回一个 Promise 对象用来观察当某种类型的所有行动绑定到集合，排队与否还是已经完成。


接下来 看下面两个实例：

```html

<!DOCTYPE html>
<html>
<head>
  <style>
div {
  height: 50px; width: 50px;
  float: left; margin-right: 10px;
  display: none; background-color: #090;
}
</style>
  <script src="http://code.jquery.com/jquery-latest.js"></script>
</head>
<body>
 
<button>Go</button>
<p>Ready...</p>
<div></div>
<div></div>
<div></div>
<div></div>
 
 
<script>
$("button").bind( "click", function() {
  $("p").append( "Started...");
 
  $("div").each(function( i ) {
    $( this ).fadeIn().fadeOut( 1000 * (i+1) );
  });
 
 
 /*** 这里会监测 div元素的动画 是否执行 执行结束之后， 执行done() 里面对应 方法***/
  $( "div" ).promise().done(function() {
    $( "p" ).append( " Finished! " );
  });
});
</script>
 
</body>
</html>


```




```html

<!DOCTYPE html>
<html>
<head>
  <style>
div {
  height: 50px; width: 50px;
  float: left; margin-right: 10px;
  display: none; background-color: #090;
}
</style>
  <script src="http://code.jquery.com/jquery-latest.js"></script>
</head>
<body>
 
<button>Go</button>
<p>Ready...</p>
<div></div>
<div></div>
<div></div>
<div></div>
 
 
<script>
var effect = function() {
  return $("div").fadeIn(800).delay(1200).fadeOut();
};
 
$("button").bind( "click", function() {
  $("p").append( " Started... ");


/* 这里的when方法 当 effect函数执行结束之后 会执行done里面的内容 */ 
  $.when( effect() ).done(function() {
    $("p").append(" Finished! ");
  });
});
 
</script>
 
</body>
</html>

```

