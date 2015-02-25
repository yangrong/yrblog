### JavaScript经典实例收集整理

#### 跨浏览器事件

##### 跨浏览器添加事件
```js
//跨浏览器添加事件
    function addEvent(obj,type,fn){
        if(obj.addEventListener){
            obj.addEventListener(type,fn,false);
        }else if(obj.attachEvent){//IE
            obj.attchEvent('on'+type,fn);
        }

    }

```
#####  跨浏览器移除事件
```js
//跨浏览器移除事件
function removeEvent(obj,type,fn){
    if(obj.removeEventListener){
        obj.removeEventListener(type,fn,false);
    }else if(obj.detachEvent){//兼容IE
        obj.detachEvent('on'+type,fn);
    }

}

```
##### 跨浏览器阻止默认行为
```js
 //跨浏览器阻止默认行为
    function preDef(ev){
        var e = ev || window.event;
        if(e.preventDefault){
            e.preventDefault();
        }else{
            e.returnValue =false;
        }

    }
```

##### 跨浏览器获取目标对象

```js
//跨浏览器获取目标对象
function getTarget(ev){
    if(ev.target){//w3c
        return ev.target;
    }else if(window.event.srcElement){//IE
        return window.event.srcElement;
    }
}  

```
##### 跨浏览器获取滚动条位置
```js
//跨浏览器获取滚动条位置，sp == scroll position
    function getSP(){
        return{
            top: document.documentElement.scrollTop || document.body.scrollTop,
            left : document.documentElement.scrollLeft || document.body.scrollLeft;
        }
    }

```
##### 跨浏览器获取可视窗口大小
```js
 //跨浏览器获取可视窗口大小
          function  getWindow () {
            if(typeof window.innerWidth !='undefined') {
                return{
                    width : window.innerWidth,
                    height : window.innerHeight
                }

            } else{
                return {
                    width : document.documentElement.clientWidth,
                    height : document.documentElement.clientHeight
                }
            }
        }

```
#### js 对象冒充

```js

    function Person(name , age){
        this.name = name ;
        this.age = age ;
        this.say = function (){
            return "name : "+ this.name + " age: "+this.age ;
        } ;
    }

    var o = new Object() ;//可以简化为Object()
    Person.call(o , "zhangsan" , 20) ;
    console.log(o.say() );//name : zhangsan age: 20 

```

#### js 异步加载和同步加载

异步加载也叫非阻塞模式加载，浏览器在下载js的同时，同时还会执行后续的页面处理。
在script标签内，用js创建一个script元素并插入到document中，这种就是异步加载js文件了：

```js

(function() {     
    var s = document.createElement('script');    
    s.type = 'text/javascript';     
    s.async = true;    
    s.src = 'http://yourdomain.com/script.js';    
    var x = document.getElementsByTagName('script')[0];    
     x.parentNode.insertBefore(s, x); 
})();
```


#### 同步加载

　　平常默认用的都是同步加载。如：
```html
<script src="http://yourdomain.com/script.js"></script>
```
　　同步模式又称阻塞模式，会阻止流览器的后续处理。停止了后续的文件的解析，执行，如图像的渲染。浏览器之所以会采用同步模式，是因为加载的js文件中有对dom的操作，重定向，输出document等默认行为，所以同步才是最安全的。
　　通常会把要加载的js放到body结束标签之前，使得js可在页面最后加载，尽量减少阻塞页面的渲染。这样可以先让页面显示出来。

　　同步加载流程是瀑布模型，异步加载流程是并发模型。

#### js获取屏幕坐标
```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=gb2312" />
    <meta http-equiv="X-UA-Compatible" content="IE=EmulateIE7"/>
    <meta name="auther" content="fq" />
    <title>获取鼠标坐标</title>
</head>
<body>
<script type="text/javascript">
    function mousePosition(ev){
        if(ev.pageX || ev.pageY){
            return {x:ev.pageX, y:ev.pageY};
        }
        return {
            x:ev.clientX + document.body.scrollLeft - document.body.clientLeft,
            y:ev.clientY + document.body.scrollTop - document.body.clientTop
        };
    }
    function mouseMove(ev){
        ev = ev || window.event;
        var mousePos = mousePosition(ev);
        document.getElementById('xxx').value = mousePos.x;
        document.getElementById('yyy').value = mousePos.y;
    }
    document.onmousemove = mouseMove;
</script>
X:<input id="xxx" type="text" /> Y:<input id="yyy" type="text" />
</body>
</html>  
```
注释：
1.documentElement 属性可返回文档的根节点。<br/>
2.scrollTop() 为滚动条向下移动的距离<br/>
3.document.documentElement.scrollTop 指的是滚动条的垂直坐标<br/>
4.document.documentElement.clientHeight 指的是浏览器可见区域高度<br/>

#### DTD已声明的情况下：
```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```
如果在页面中添加这行标记的话

##### IE

document.body.clientWidth ==> BODY对象宽度<br/>
document.body.clientHeight ==> BODY对象高度<br/>
document.documentElement.clientWidth ==> 可见区域宽度<br/>
document.documentElement.clientHeight ==> 可见区域高度
##### Firefox
<br/>
document.documentElement.scrollHeight ==> 浏览器所有内容高度<br/>
document.body.scrollHeight ==> 浏览器所有内容高度<br/>
document.documentElement.scrollTop ==> 浏览器滚动部分高度<br/>
document.body.scrollTop ==>始终为0<br/>
document.documentElement.clientHeight ==>浏览器可视部分高度<br/>
document.body.clientHeight ==> 浏览器所有内容高度

##### Chrome
<br/>
document.documentElement.scrollHeight ==> 浏览器所有内容高度<br/>
document.body.scrollHeight ==> 浏览器所有内容高度<br/>
document.documentElement.scrollTop==> 始终为0<br/>
document.body.scrollTop==>浏览器滚动部分高度<br/>
document.documentElement.clientHeight ==> 浏览器可视部分高度<br/>
document.body.clientHeight ==> 浏览器所有内容高度<br/>
浏览器所有内容高度即浏览器整个框架的高度，包括滚动条卷去部分+可视部分+底部隐藏部分的高度总和<br/>
浏览器滚动部分高度即滚动条卷去部分高度即可视顶端距离整个对象顶端的高度。

综上

1、document.documentElement.scrollTop和document.body.scrollTop始终有一个为0，所以可以用这两个的和来求scrollTop


2、scrollHeight、clientHeight 在DTD已声明的情况下用documentElement，未声明的情况下用body

###### clientHeight

 在IE和FF下，该属性没什么差别，都是指浏览器的可视区域，即除去浏览器的那些工具栏状态栏剩下的页面展示空间的高度。


###### PageX和clientX

PageX:鼠标在页面上的位置,从页面左上角开始,即是以页面为参考点,不随滑动条移动而变化


clientX:鼠标在页面上可视区域的位置,从浏览器可视区域左上角开始,
即是以浏览器滑动条此刻的滑动到的位置为参考点,随滑动条移动 而变化.

可是悲剧的是,PageX只有FF特有,IE则没有这个，所以在IE下使用这个：


PageY=clientY+scrollTop-clientTop;(只讨论Y轴,X轴同理,下同)


scrollTop代表的是被浏览器滑动条滚过的长度


offsetX:IE特有,鼠标相比较于触发事件的元素的位置,以元素盒子模型的内容区域的左上角为参考点,如果有boder`,可能出现负值


只有clientX和screenX 皆大欢喜是W3C标准.其他的,都纠结了.
最给力的是，chrome和safari一条龙通杀!完全支持所有属性

图片描述

#### js拖拽效果

```html
<!doctype html>
<html lang="zn-CN">
<head>
    <meta http-equiv="Content-Type" content="text/html;charset=UTF-8" />
    <title></title>
    <style type="text/css">
        #login{
            height: 100px;
            width: 100px;
            border: 1px solid black;
            position: relative;
            top:200px;
            left: 200px;
            background: red;
        }
    </style>
</head>
<body>
<div id="login"></div>
<script type="text/javascript">
    var oDiv = document.getElementById("login");
    oDiv.onmousedown = function(e){
        var e = e || window.event;//window.event兼容IE,当事件发生时有效

        var diffX = e.clientX - oDiv.offsetLeft;//获取鼠标点击的位置到所选对象的边框的水平距离
        var diffY = e.clientY - oDiv.offsetTop;

        document.onmousemove = function(e){ //需设为document对象才能作用于整个文档
            var e = e||window.event;
            oDiv.style.left = e.clientX - diffX + 'px';//style.left表示所选对象的边框到浏览器左侧距离
            oDiv.style.top = e.clientY -diffY + 'px';
        };
        document.onmouseup = function(){
            document.onmousemove = null;//清除鼠标释放时的对象移动方法
            document.onmouseup = null;
        }
    }
</script>
</body> 
</html>
```
offsetTop 返回的是数字，而 style.top 返回的是字符串，除了数字外还带有单位：px。

#### js获取图片原始大小尺寸
```js
var img = $("#img_id"); // Get my img elem
var pic_real_width, pic_real_height;
$("&lt;img/&gt;") // Make in memory copy of image to avoid css issues
    .attr("src", $(img).attr("src"))
    .load(function() {
        pic_real_width = this.width;   // Note: $(this).width() will not
        pic_real_height = this.height; // work for in memory images.
    });
```

#### js循环遍历数组

```js
       //循环遍历数组  
       var animals = ["cat",'dog','human','whale','seal'];  
       var animalString = "";  
       for(var i = 0;i<animals.length;i++){  
           animalString += animals[i] + " ";  
       }  
       alert(animalString);  //输出数组里的每个项
```

#### 遍历二维数组

```js

        var arr=[[0,0,0,0,0,0],[0,0,1,0,0,0],[0,2,0,3,0,0],[0,0,0,0,0,0]]; 
        for(var i=0;i<arr.length;i++){ 
         //遍历每一个具体的值 
         for(var j=0;j<arr[i].length;j++){ 
                    document.writeln(arr[i][j]+" "); 
              } 
            document.writeln("<br/>"); 
         } 
```


#### 阻止表单重复提交

有两种方法可以解决：一是提交之后，立刻禁用点击按钮；第二种就是提交之后取消后续的表单提交操作。
```js

document.getElementById("btn").disabled = true;//第一次提交后，将按钮禁用
```

这种方式只能用于通过提交按钮防止重复提交，还可以使用如下方式：
```js

var flag = false;//设置一个监听变量
if(flag ==true)return;//退出事件
flag = true;//表示提交过一次了
```


#### 字符串部分

##### 在字符串中查找子字符串

```js

    var test = 'Welcome to my blog!';
    var value = 'blog';
    var subValue = test.indexOf(value);
    console.log(subValue);//14,子字符串的索引
```

##### Number和Math部分

数字可以是一个直接量，也可以是一个对象，但是Math对象不同，他没有构造函数，并且其所有的属性和方法都是直接通过这个对象来访问的

把十进制转化为一个十六进制值
```js

var num = 255;
console.log(num.toString(16));//ff
//js中，十进制数字以0x开头，八进制数字总是以0开头

```
##### 随进产生颜色

```js

    function randomVal(val){
        return Math.floor(Math.random()*(val + 1));
    }

    function randomColor(){
        return 'rgb(' + randomVal(255) + ',' + randomVal(255) + ',' + randomVal(255) + ')';
    }
```

目前，所有浏览器都支持RGB表示法和十六进制表示法，除了IE7，它只支持十六进制表示法

在角度和弧度之间转换
```js

var rad = degrees*(Math.PI/180);

var degrees = rad*(180/Math.PI);

```


#### 数组部分

##### 创建多维数组

```js
    var arrayLength = 3;//设置数组长度

    //创建数组
    var multiArray = new Array(arrayLength);
    for(var i =0;i<multiArray.length;i++){
        multiArray[i] = new Array(arrayLength);
    }

    //给第一个数组索引添加项
    multiArray[0][0] = 'phone';
    multiArray[0][1] = 'book';
    multiArray[0][2] = 'TV';

    //第二个
    multiArray[1][0] = 2;
    multiArray[1][1] = 1;
    multiArray[1][2] = 98;

    //第三个
    multiArray[2][0] = ['java','python'];
    multiArray[2][1] = ['js','C++'];
    multiArray[2][2] = ['Haskell','php'];
```

##### 排序数组

```js
     var fruits = ['banana','apple','orange','strawberry'];
    console.log(fruits.sort());//Array [ "apple", "banana", "orange", "strawberry" ]

    var num = [32,43,2,5,-23,0,4];
    console.log(num.sort());//Array [ -23, 0, 2, 32, 4, 43, 5 ]
```

Array对象的sort方法会按照字母顺序来排序数组元素。对于数字，是按照字符编码的顺序进行排序


```js
function compare(a,b){
    return a-b;
}
var num = [32,43,2,5,-23,0,4];
console.log(num.sort(compare));//Array [ -23, 0, 2, 4, 5, 32, 43 ] 
```
