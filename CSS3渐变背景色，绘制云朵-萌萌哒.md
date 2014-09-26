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
换句说：<br/>
对象选择器 {text-shadow:投影方式 X轴偏移量 Y轴偏移量 阴影模糊半径 阴影扩展半径 阴影颜色}<br/>
x-offset y-offset 设置为0的时候，阴影围绕物象形成。<br/>
阴影模糊半径：阴影的虚化程度，值越大，越模糊。如果设置为0，则会产生实体，没有羽化效果的边缘效果。<br/>
阴影扩展半径：阴影产生的范围，值越大，阴影范围越大。<br/>

还可以支持绘制多个阴影（虽然这示例略搓）：

```html
<div class="boxshadow">
</div>
```

```css
.boxshadow{
    width:100px;
    height:100px;
    box-shadow:4px 2px 6px #f00, /*第一个阴影*/
    -4px -2px 6px #000, /*第二个阴影*/
    0px 0px 12px 5px #33CC00 inset/*第三个阴影*/
   }
```

当然css3也支持文字阴影，如下演示
```html
<div class="demo">IMOOC</div>
```

```css
.demo {
    width: 340px;
    padding: 30px;
    font: bold 55px/100% "微软雅黑";
    color: #566F89;
    background: #000;
    }
```

径向渐变：
```css
.radial{
    display:block; 
    width:150px; 
    height:150px; 
    border:1px solid blue; }
.radial{

    background-image:-webkit-gradient(radial, 45 45, 10, 52 50, 30, from(#A7D30C), to(rgba(1,159,98,0)), color-stop(90%, #019F62));
}
```
-webkit-gradient(radial, inner_center, inner_radius, outer_center, outer_radius, / stop...)
对应的值：<br/>
inner_center	内部中心点，径向渐变起始圆环<br/>
inner_radius	内部半径，径向渐变起始圆<br/>
outer_center	外部渐变结束圆的中心点<br/>
outer_radius	外部渐变结束圆的半径<br/>



