#### JavaScript事件小结


###### 事件冒泡
###### 事件捕获
事件捕获的思想是不太具体的节点应该更早接收到事件，而最具体的节点最后接收到事件。

###### DOM0级事件处理程序
把一个函数赋值给一个事件，一个事件只能被一个函数赋值，后面定义的同名事件，会把前面的事件覆盖
```html
<input type="button" value="按钮2" id="btn2">
```
```js
document.getElementById('btn2').onclick = function() {
  alert('hello');
}
```
###### DOM2级事件处理程序
DOM2级事件定义了两个方法：用于处理指定和删除事件处理程序的操作：addEventListener()和removeEventListener()。它们都接收三个参数：要处理的事件名、作为事件处理程序的函数和一个布尔值。<br/>
IE事件处理程序:
attachEvent()添加事件
detachEvent()删除事件
这两个方法接收相同的两个参数：事件处理程序名称与事件处理函数
```html
<input type="button" value="按钮3" id="btn3">
```

```js
functionn sayHi(){
  alert('hello');
}
var eventUtil={
         	// 添加句柄
         	addHandler:function(element,type,handler){
               if(element.addEventListener){
                 element.addEventListener(type,handler,false);
               }else if(element.attachEvent){
                 element.attachEvent('on'+type,handler);
               }else{
                 element['on'+type]=handler;
               }
         	},
         	// 删除句柄
         	removeHandler:function(element,type,handler){
               if(element.removeEventListener){
                 element.removeEventListener(type,handler,false);
               }else if(element.detachEvent){
                 element.detachEvent('on'+type,handler);
               }else{
                 element['on'+type]=null;
               }
         	}
         	var btn_3 =document.getElementById('btn3');
         	
         	eventUtil.addHandler(btn_3,'click',sayHi);
```

三、事件对象
事件对象event
1、DOM中的事件对象
(1)、type:获取事件类型
(2)、target：事件目标
(3)、stopPropagation() 阻止事件冒泡
(4)、preventDefault() 阻止事件的默认行为
2、IE中的事件对象
(1)、type:获取事件类型
(2)、srcElement：事件目标
(3)、cancelBubble=true阻止事件冒泡
(4)、returnValue=false阻止事件的默认行为
