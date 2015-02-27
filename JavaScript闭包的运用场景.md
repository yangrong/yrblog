## 详解js闭包&JavaScript闭包的一个运用场景

#### 闭包有三个特性：

1. 函数嵌套函数
2. 函数内部可以引用外部的参数和变量
3. 参数和变量不会被垃圾回收机制回收

#### 闭包的定义及其优缺点

闭包 是指有权访问另一个函数作用域中的变量的函数，创建闭包的最常见的方式就是在一个函数内创建另一个函数，通过另一个函数访问这个函数的局部变量


使用闭包有一个优点，也是它的缺点，就是可以把局部变量驻留在内存中，可以避免使用全局变量。全局变量在每个模块都可调用，这势必将是灾难性的。（所以推荐使用私有的，封装的局部变量。）


一般函数执行完毕后，局部活动对象就被销毁，内存中仅仅保存全局作用域。但闭包的情况不同！

### 嵌套函数的闭包

```js
   function aaa() {  
          var a = 1;  
          return function(){
           alert(a++)
          };  
        }         
        var fun = aaa();  
        fun();// 1 执行后 a++，，然后a还在~  
        fun();// 2   
        fun = null;//a被回收！！ 
```

闭包会使变量始终保存在内存中，如果不当使用会增大内存消耗。




### javascript的垃圾回收原理

（1） 在javascript中，如果一个对象不再被引用，那么这个对象就会被GC回收；
（2） 如果两个对象互相引用，而不再被第3者所引用，那么这两个互相引用的对象也会被回收。

### 使用闭包的好处

那么使用闭包有什么好处呢？使用闭包的好处是：

1. 希望一个变量长期驻扎在内存中
2. 避免全局变量的污染
3. 私有成员的存在


#### 全局变量的累加

```js
var a = 1;
function abc(){
        a++;
        alert(a);
}
abc();              //2
abc();            //3
```

#### 局部变量

```js

function abc(){
        var a = 1;
        a++;
        alert(a);
}
abc();                       //2
abc();                    //2
```


那么怎么才能做到变量a既是局部变量又可以累加呢？

#### 局部变量的累加

```js
function outer(){
        var x=10;
        return function(){             //函数嵌套函数
                x++;
                alert(x);
        }
}
var y = outer();      //外部函数赋给变量y;
y();                 //y函数调用一次，结果为11，相当于outer()()；
y();                //y函数调用第二次，结果为12，实现了累加
```


函数声明与函数表达式

在js中我们可以通过关键字function来声明一个函数：

```js
function abc(){
        alert(123);
}
abc();
```
我们也可以通过一个"()"来将这个声明变成一个表达式：

```js
(function (){
        alert(123);
})();                   //然后通过()直接调用前面的表达式即可，因此函数可以不必写名字；
```

#### 模块化代码，减少全局变量的污染

```js
var abc = (function(){      //abc为外部匿名函数的返回值
        var a = 1;
        return function(){
                a++;
                alert(a);
        }
})();
abc();    //2 ；调用一次abc函数，其实是调用里面内部函数的返回值    
abc();    //3
```


#### 私有成员的存在

```js
var aaa = (function(){
        var a = 1;
        function bbb(){
                a++;
                alert(a);
        }
        function ccc(){
                a++;
                alert(a);
        }
        return {
                b:bbb,             //json结构
                c:ccc
        }
})();
aaa.b();     //2
aaa.c()      //3
```


#### 使用匿名函数实现累加

//使用匿名函数实现局部变量驻留内存中，从而实现累加

```js

 function box(){
     var age = 100;
     return function(){          //匿名函数
          age++;
          return age;
     };

 } 
var b = box();
alert(b());
alert(b());    //即alert(box()())；
alert(b());
alert(b);            //     function () {
                        //   age++;
                       // return age;
                      //       }

b = null；  //解除引用，等待垃圾回收
```



过度使用闭包会导致性能的下降。函数里放匿名函数，则产生了闭包


#### 内存泄露问题

由于IE的js对象和DOM对象使用不同的垃圾收集方法，因此闭包在IE中会导致内存泄露问题，也就是无法销毁驻留在内存中的元素
```js
function closure(){
    var oDiv = document.getElementById('oDiv');//oDiv用完之后一直驻留在内存中
    oDiv.onclick = function () {
        alert('oDiv.innerHTML');//这里用oDiv导致内存泄露
    };
}
closure();
//最后应将oDiv解除引用来避免内存泄露
function closure(){
    var oDiv = document.getElementById('oDiv');
    var test = oDiv.innerHTML;
    oDiv.onclick = function () {
        alert(test);
    };
    oDiv = null;
}

```
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

 for (var i = 0; i < menuLi.length; i++) {
		
	menuLi[i].onclick = (function(i) {
		//第一次点击的时候，for循环已经执行到最后一步了。
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
这里我们用闭包把函数封装起来，因为函数的参数是以值得方式传递的（对象传递的是内存中引用，也是一个值），所以增加一个自动执行函数，把参数 i 传进去（因为是以值传递）所以也就是把每次循环的 i 都复制了一次（内存中开辟了新地址），这样每个循环体都有一个独立的 i ，所以对自执行函数（闭包）里面的 i 的引用都是独立的。
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

这个函数执行，只是return一个函数，return的函数体，会在onclick时间的时候触发。

下面我们来看一下，一个最常见的闭包的运用场景
```js

var testbibao = '闭包可以访问外面的变量，函数';
(function() {
	var name = '我在闭包里面，闭包外面的函数没有办法取到我的值';
	var age = '34';
	var status = 'single';

	function createMember() {
		console.log('闭包')
	}

	function getMemberDetails() {
		// [...]
		console.log(testbibao);
	}
	createMember();
	getMemberDetails(); //输出：闭包可以访问外面的变量，函数
})();

	/*函数内部的局部变量函数外部不能访问*/
function test() {
		console.log(name);//输出空白
	}

function getMemberDetails() {
	console.log('闭包里面有一个同名函数，但是互相不影响的，素不素啊！')
}

test(); //这里输出空值，因为闭包里面的变量外面访问不到
getMemberDetails();

```
