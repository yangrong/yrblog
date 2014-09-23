```html
<div class="logo">
	<div id="tree"></div>
	<div id="trunk">
		<div id="left-branch"></div>
		<div id="right-bottom-branch"></div>
		<div id="right-top-branch"></div>
	</div>
</div>
```


```css
.logo{
	height: 200px; width: 160px;
	margin: 150px auto;
	position: relative;
}

#tree {
	border-bottom: 200px solid #5b9a68;
	border-left: 80px solid transparent;
	border-right: 80px solid transparent;
	position: absolute; top: 0; left: 0;
	height: 0; width: 0;
}

#trunk{
	height: 85px; width: 16px;
	background: #3b543f;
	position: absolute; left: 72px; bottom: -20px;
}

#left-branch{
	background: #3b543f;
	height: 30px; width: 6px;
	position: absolute; left: -10px; top: 15px;
	
	transform: rotate(-50deg);
	-webkit-transform: rotate(-50deg);
	-moz-transform: rotate(-50deg);
	-ms-transform: rotate(-50deg);
	-o-transform: rotate(-50deg);
}

#right-bottom-branch{
	background: #3b543f;
	height: 50px; width: 6px;
	position: absolute; top: 15px; left: 23px;
	
	transform: rotate(50deg);
	-webkit-transform: rotate(50deg);
	-moz-transform: rotate(50deg);
	-ms-transform: rotate(50deg);
	-o-transform: rotate(50deg);
}
#right-top-branch{
	background: #3b543f;
	height: 27px; width: 6px;
	position: absolute; top: 2px; left: 20px;
	
	transform: rotate(50deg);
	-webkit-transform: rotate(50deg);
	-moz-transform: rotate(50deg);
	-ms-transform: rotate(50deg);
	-o-transform: rotate(50deg);
}
```

css写一个正三角形
```html
 <div id="boder_arrow"> </div>
```

```css
 #boder_arrow{border-width:20px;border-color:#ff6699 #ff3366 #cc0066 #990033;border-style:solid;width:0;height:0;line-height:0; }

/*只要一个正三角形，比如正下方的三角形*/

 #boder_arrow{border-width:20px;border-color:transparent transparent #cc0066 transparent;border-style:solid;width:0;height:0;line-height:0; }
```

css写一个正三角形,也可以用unicode几何图像

```html
<span class="form_hint">正确格式为：6~18个字符，可使用字母、数字、下划线，需以字母开头</span>
```
```css
.form_hint {
	display:block;
	background: #d45252;
	border-radius: 3px 3px 3px 3px;
	color: white;
	margin-left:8px;
	padding: 1px 6px;
	z-index: 999; 
	position: absolute; 

}
.form_hint::before {
	content: "\25C0";/*三角形图标*/
	color:#d45252;
	position: absolute;
	top:1px;
	left:-6px;
}
```
![替代文本](http://p1.qhimg.com/t01c1c4c54184411b64.png)
