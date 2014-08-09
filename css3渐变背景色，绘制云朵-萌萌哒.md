```html
<div id = "cloud"><span class='shadow'></span></div>

```

```css
body {
	background: #ccc;
}
#cloud {
	width: 350px; height: 120px;
	
	background: #f2f9fe;
	/*这里的5%是指渐变从5%开始做 #f2f9fe到#d6f0fd的渐变 */
	background: -webkit-linear-gradient(top, #f2f9fe 5%, #d6f0fd 100%);

	
	border-radius: 100px;
	-webkit-border-radius: 100px;
	-moz-border-radius: 100px;
	
	position: relative;
	margin: 120px auto 20px;
}

#cloud:after, #cloud:before {
	content: '';
	position: absolute;
	background: #f2f9fe;
	z-index: -1
}

#cloud:after {
	width: 100px; height: 100px;
	top: -50px; left: 50px;
	
	border-radius: 100px;
	-webkit-border-radius: 100px;
	-moz-border-radius: 100px;
}

#cloud:before {
	width: 180px; height: 180px;
	top: -90px; right: 50px;
	
	border-radius: 200px;
	-webkit-border-radius: 200px;
	-moz-border-radius: 200px;
}

.shadow {
	width: 350px;
   
	position: absolute; bottom: -10px; 
	background: #000;
	z-index: -1;
	

	-moz-box-shadow: 0 0 25px 8px rgba(0, 0, 0, 0.4);
	-webkit-box-shadow: 0 0 5px 8px rgba(0, 0, 0, 0.4);
	
	border-radius: 50%;
	-moz-border-radius: 50%;
	-webkit-border-radius: 50%;
}

```


css3阴影：
E {box-shadow:inset x-offset y-offset blur-radius spread-radius color}
换句说：
对象选择器 {text-shadow:投影方式 X轴偏移量 Y轴偏移量 阴影模糊半径 阴影扩展半径 阴影颜色}
x-offset y-offset 设置为0的时候，阴影围绕物象形成。
阴影模糊半径：阴影的虚化程度，值越大，越模糊。如果设置为0，则会产生实体，没有羽化效果的边缘效果。
阴影扩展半径：阴影产生的范围，值越大，阴影范围越大。
