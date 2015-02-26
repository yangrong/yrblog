localStorage是浏览器用于存储本地数据的一个对象.浏览器支持还是不错的,至少ie8系已经开始支持.其他现代浏览器的支持更不在话下
```js
//这里的就是一段简单的localStorage的实现方式，每次刷新页面，显示的数字都会在原来的基础上+1
var storage = window.localStorage;
if (!storage.getItem("pageLoadCount")) storage.setItem("pageLoadCount",0);
storage.pageLoadCount = parseInt(storage.getItem("pageLoadCount")) + 1;//必须格式转换
document.getElementById("count").innerHTML = storage.pageLoadCount;
```
```js
//清除所有的localStorage
localStorage.clear()
```

```js
//遍历localStorage存储的key
var storage = window.localStorage;
function showStorage(){
 //循环显示localStorage里的键值对
 for(var i=0;i<storage.length;i++){
  //key(i)获得相应的键，再用getItem()方法获得对应的值
  document.write(storage.key(i)+ " : " + storage.getItem(storage.key(i)) + "<br>");
 }
}
```
###### localStorage获取到的变量的格式
```js
storage.setItem("pageLoadCount",0);
//无论是cookie还是 localStorage获取的值都是string类型，所以取到值，我们一般要走数据转换
(storage.getItem("pageLoadCount")) + 1；


localStorage.lasttime = new Date().toUTCString();
//解码日期
var lasttime = new Date(Date.parse(localStorage.lasttime));

localStorage.data = JSON.stringigy(data);
//解码Json格式
var data = JSON.parse(localStorage.data);

//cookie的编码，解码用的是
//编码
encodeURIComponent(new Date());
//解码
decodeURIComponent(encodeURIComponent(new Date())
```

###### localStorage的兼容
```js
//记录数据
var arrDisplay = [0, 1, 1, 1];

//存储，IE6~7 cookie 其他浏览器HTML5本地存储
if (window.localStorage) {
    localStorage.setItem("menuTitle", arrDisplay);	
} else {
    Cookie.write("menuTitle", arrDisplay);	
}

//读取数据
var strStoreDate = window.localStorage? localStorage.getItem("menuTitle"): Cookie.read("menuTitle");	

```

###### 其他本地存储的tip:
1. sessionStorage是一个跟浏览器生命周期相同的本地存储,在页面刷新后保持之前输入的数据的场景下特别有效.
sessionStorage用于本地存储一个会话（session）中的数据，这些数据只有在同一个会话中的页面才能访问并且当会话结束后数据也随之销毁。因此sessionStorage不是一种持久化的本地存储，仅仅是会话级别的存储。
而localStorage用于持久化的本地存储，除非主动删除数据，否则数据是永远不会过期的。
2. 可以用localStorage.clear()方法彻底清除localStorage.
3. localStorage对于每个域都有5兆的存储空间,而且对于存储数据条数也有不同的限制.
4. localStorage只能存储文本数据.如果你想存储图像,那也不是不可能的,可以用canvas将图片转换成dataurl的形式,然后存储起来.
5. 请关注localStorage的存储性能,在某些浏览器中存取数据非常慢,例如opera中.
6. Web Storage的概念和cookie相似，区别是它是为了更大容量存储设计的。Cookie的大小是受限的，并且每次你请求一个新的页面的时候Cookie都会被发送过去，这样无形中浪费了带宽，另外cookie还需要指定作用域，不可以跨域调用。
