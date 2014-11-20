#### 兼容ie6、7的inline-block

如下代码做一个页数导航

```html
<ul>
		<li><a href="#">1</a></li>
		<li><a href="#">2</a></li>
		<li><a href="#">3</a></li>
		<li><a href="#">4</a></li>
	</ul>
```


css代码片段：


```css
*{
	padding:0;
	margin: 0;
}

ul {
	width: 1000px;
	margin: 0 auto;
	text-align: center;

}
ul li{
	display: inline-block;
	margin-right: 6px;
	padding-right: 6px;
}
ul li a
{
font-size: 1em;
margin: 0 .2em;
display: inline-block;
letter-spacing: 0;
vertical-align: middle;
background: #4a576c;
border: 1px solid #4a576c;
color: #fff;
width: 35px;
height: 30px;
line-height: 30px;
padding:0;
text-align: center;
text-decoration: none;
}
```

其实我们以为应该是这样的：
![](http://p0.qhimg.com/t01639209961b6efa86.png)

但是ie6，ie7是这样显示的：
![](http://p2.qhimg.com/t019b0d04dbacb63ecd.png)



IE6/IE7下对display:inline-block的支持性不好。<br>
1、inline元素的display属性设置为inline-block时，所有的浏览器都支持;<br>
2、block元素的display属性设置为inline-block时，IE6/IE7浏览器是不支持的；<br>

所以这里我的li元素  还是占满整行显示。

解决方案：

直接让块元素设置为内联对象呈递（设置属性display:inline），然后触发块元素的layout（如：zoom:1 或float属性等）。代码如下：

我们直接在li的css定义里面补充,如下属性，就可以正常显示了 
```html
ul li{ _zoom:1;*display:inline;}
```
