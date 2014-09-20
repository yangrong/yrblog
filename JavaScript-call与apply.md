yrblog
======


###### call与apply————将函数作为对象的方法来调用

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
