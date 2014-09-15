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
