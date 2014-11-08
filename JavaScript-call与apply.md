yrblog
======


###### call与apply————将函数作为对象的方法来调用（改变this，也就是上下文环境的函数方法）

一般情况下，我们声明一个函数
```js
var yr='yangrong'
function getY(){
var yr='haha';
console.log(this.yr)
}

getY();//yangrong
```
这里的this是指向window的，因为getY这个函数是在window声明的.

下面这个方法是在aObj对象下声明的，所以他的this就会指向在aObj，而不是指向的是window

```js
var aObj={yr:'yangrong be happy'}
aObj.getName=function(){console.log(this.yr)}
function (){console.log(this.yr)}
var yr='someTime low'
aObj.getName() //yangrong be happy 
```

所以我们要让在window下声明的函数，this指针指向特定的对象，方法如下：
```js

function getStuate(){console.log(this.staute)}
var staute = 'unhappy'
getStuate();//unhappy 
var changeStu = {staute:'happy'}
getStuate.call(changeStu)  //happy 
```


今天碰到一个问题，以为也是用函数上下文来解释他取值问题，结果出错了，下面我场景重现一下。
```js
var name ='Tom';
var objA = {
  name:'John',
  way:function(){
  console.log(name);//Tom
  }
}
objA.way();
```
我以为，是因为name没有指定this，所以会指向window下面的name，其实是错的，这个真正的原因是，这里的name是一个变量，而不是属性，objA木有变量啦，objA里面的name 是objA的一个属性。所以变量name，只能在window下面去找，然后返回Tom。


```js
var name ='Tom';
var objA = {
  name:'John',
  way:function(){
  console.log(this.name);//John
  }
}
objA.way();
```

