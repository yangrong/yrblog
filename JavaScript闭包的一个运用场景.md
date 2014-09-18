JavaScript闭包的一个运用场景
=================


最近在练习原生的js，下面代码的所有的li都绑定同一个事件
```html
	<div id='menu'>
		<ul>
			<li>first</li>
			<li>second</li>
			<li>third</li>
		</ul>
	</div>
```
如jquery框架，我们回直接用
```js
  $('#menu li').click(function(){
         console.log('do  something');
  })
```

但是用原生的js
我们就会只能用for语句，一个一个li元素绑定了 
如下 ：
```js
	var menuLi = document.getElementById('menu').getElementsByTagName('li');
	var menuContent = document.getElementById('content').getElementsByTagName('li');

	function siblings(elem) {
		var a = [];
		var b = elem.parentNode.children;
		for (var i = 0; i < b.length; i++) {
			if (b[i] !== elem) a.push(b[i]);
		}
		return a;
	}

 for (var i = 0; i < menuLi.length; i++) {
		
	menuLi[i].onclick = (function(i) {
		console.log(menuContent[i]);
		console.log(menuContent[i].className);

 	})(i)
}
```
我们这里看到的运行结果是每一次我们log出来的，都是i=2的时候的情况，这个是为什么呢？
因为这个函数是在点击（onclick）事件的时候触发的，for语句已经在最开始浏览加载js文件的执行了一遍了，所以执行完一遍，i已经是最后2了。

那我们就用js中的闭包来解决这个问题
```js
	for (var i = 0; i < menuLi.length; i++) {
		var num = i;
		menuLi[i].onclick = (function(num) {
			console.log(menuContent[num]);
			console.log(menuContent[num].className);
		})(num);
	}
```
这里我们用闭包把函数封装起来，然后调用参数会因为函数的参数，如果是个变量的话，相当于在内存从新开辟个地址，来存函数参数，这样大家就都不重复了。
我们执行这段代码的时候，会发现，这个页面加载完之后，所以的结果，都会log出来，点击事件触发的时候，没有执行，这个是因为，
```
(function(e){
/*函数处理逻辑*/
})(e)
```
这样函数就在for语句执行的时候一起执行了，没有等点击事件触发的时候再执行。

我们要这样写就ok了
```js
	for (var i = 0; i < menuLi.length; i++) {
	var num = i;
	menuLi[i].onclick = (function(_num) {
		return function(){
			console.log(menuContent[_num]);
			console.log(menuContent[_num].className);
		}

	})(num)
}
```

这个函数执行，只是return一个函数是吧，return的函数体，会在onclick时间的时候触发。
