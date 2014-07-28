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
1.sessionStorage是一个跟浏览器生命周期相同的本地存储,在页面刷新后保持之前输入的数据的场景下特别有效.
2.可以用localStorage.clear()方法彻底清除localStorage.
3.localStorage对于每个域都有5兆的存储空间,而且对于存储数据条数也有不同的限制.
4.localStorage只能存储文本数据.如果你想存储图像,那也不是不可能的,可以用canvas将图片转换成dataurl的形式,然后存储起来.
5.请关注localStorage的存储性能,在某些浏览器中存取数据非常慢,例如opera中.
