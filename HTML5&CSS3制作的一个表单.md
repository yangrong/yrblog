### HTML5&CSS3制作的一个表单

本文只是为了mark一些新鲜的css3，html5的属性，都可以用于移动端。

```html
<div class="contact">
<form class="contact_form" action="#" method="post" name="contact_form">
    <ul>
        <li>
             <h2>联系我们</h2>
             <span class="required_notification">* 表示必填项</span>
        </li>
        <li>
            <label for="name">姓名:</label>
            <input type="text"  placeholder="Sunbest" required />
            <span class="form_hint">正确格式为：6~18个字符，可使用字母、数字、下划线，需以字母开头</span>
        </li>
        <li>
            <label for="email">电子邮件:</label>
            <input type="email" name="email" placeholder="sayingforever@163.com" required />
            <span class="form_hint">正确格式为：sayingforever@163.com</span>
        </li>
        <li>
            <label for="website">网站:</label>
            <input type="url" name="website" placeholder="http://www.amonyous.com" required pattern="(http|https)://.+"/>
            <span class="form_hint">正确格式为：http://www.amonyous.com</span>
        </li>
        <li>
            <label for="message">留言:</label>
            <textarea name="message" cols="40" rows="6" placeholder="" required ></textarea>
        </li>
        <li>
        	<button class="submit" type="submit">提交</button>
        </li>
    </ul>
</form>
</div>
```

placeholder属性：
placeholder 属性提供可描述输入字段预期值的提示信息（hint）。
该提示会在输入字段为空时显示，并会在字段获得焦点时消失。

required属性 ： required 属性规定必需在提交之前填写输入字段
过去验证表单会通过js和正则去判断填写的内容是否正确，如email的验证。 

HTML5的出现为我们提供一些属性，不用编写js和正则即可解决这个检验表单内容。 

:required 

必须，那input不能为空的意思。 

:valid 

有效，即当填写的内容符合要求的时候触发。 

:invalid 

无效，即当填写的内容不符合要求的时候触发。

如下面css实例
```css
/*input:required，表示所有带required属性的input*/
.contact_form input:required, .contact_form textarea:required {background: #fff url(images/red_asterisk.png) no-repeat 98% center;}
/*contact_form input:required:valid，表示所有带required属性的input输入内容，
 *合法，这里的是否合法，
 *会根据input的type属性，比如type="email"，那这里输入的内容应该是符合email格式的才会执行这个css 语句*/
.contact_form input:required:valid, .contact_form textarea:required:valid {background: #fff url(images/valid.png) no-repeat 98% center;box-shadow: 0 0 5px #5cd053;border-color: #28921f;}
/*contact_form input:required:invalid，表示所有带required属性的input输入内容，不合法，执行这个css */
.contact_form input:focus:invalid, .contact_form textarea:focus:invalid {background: #fff url(images/invalid.png) no-repeat 98% center;box-shadow: 0 0 5px #d45252;border-color: #b03535;}
```


以下是表单对应的全部css代码
```css
body{font:13px/26px "微软雅黑";}
/*注意这里的outline: none;是为了清除chrome浏览器自带的输入框focus时候的边框颜色，对页面样式的整体风格的影响*/
*:focus {outline: none;}
.contact{width:720px;background:#F1F1F1;margin:20px auto;padding:10px;}

/* === Form Typography === */
.contact_form h2{font-size:18px;font-weight:bold;}
.contact_form label{font-size:14px;}
.form_hint, .required_notification{font-size: 12px;}

/* === List Styles === */
.contact_form ul {width:720px;list-style-type:none;padding:0px;}
.contact_form li{padding:12px; border-bottom:1px solid #DFDFDF;position:relative;} 
.contact_form li:first-child, .contact_form li:last-child {border-bottom:1px solid #777;}

/* === Form Header === */
.contact_form h2 {margin:0;display: inline;}
.required_notification {color:#d45252; margin:5px 0 0 0; display:inline;float:right;}

/* === Form Elements === */
.contact_form label {width:150px;margin-top: 3px;display:inline-block;float:left;padding:3px;}
.contact_form input {height:20px; width:220px; padding:5px 8px;}
.contact_form textarea {padding:8px; width:300px;}
.contact_form button {margin-left:156px;}

	/* form element visual styles */
.contact_form input, .contact_form textarea { 
	border:1px solid #aaa;
	box-shadow: 0px 0px 3px #ccc, 0 10px 15px #eee inset;
	border-radius:2px;
	padding-right:30px;
	/*transition动画属性，这个在博客的其他文章（CSS3 transition过渡动画.md）有提起过，这里不做详细说明 */
	-moz-transition: padding .25s; 
	-webkit-transition: padding .25s; 
	-o-transition: padding .25s;
	transition: padding .25s;
}
/*:focus 选择器，css3的新属性，之前我们只能js来控制blur focus表单的获取焦点和失去焦点，现在css即可实现。*/

.contact_form input:focus, .contact_form textarea:focus {
	background: #fff url(images/red_asterisk.png) no-repeat; 
	border:1px solid #555; 
	box-shadow: 0 0 3px #aaa; 
	padding-right:70px;
}

/* === HTML5 validation styles === */	
.contact_form input:required, .contact_form textarea:required {background: #fff url(images/red_asterisk.png) no-repeat 98% center;}
.contact_form input:required:valid, .contact_form textarea:required:valid {background: #fff url(images/valid.png) no-repeat 98% center;box-shadow: 0 0 5px #5cd053;border-color: #28921f;}
.contact_form input:focus:invalid, .contact_form textarea:focus:invalid {background: #fff url(images/invalid.png) no-repeat 98% center;box-shadow: 0 0 5px #d45252;border-color: #b03535;}


/* === Form hints === */
.form_hint {
	background: #d45252;
	border-radius: 3px 3px 3px 3px;
	color: white;
	margin-left:8px;
	padding: 1px 6px;
	z-index: 999; 
	position: absolute; 
	display: none;
}
.form_hint::before {
/*\25C0 : unicode几何图像 ,这个在CSS小圣诞树—css实现的三角形的博客里面提起过， */
	content: "\25C0";
	color:#d45252;
	position: absolute;
	top:1px;
	left:-6px;
}

/* + : 相邻兄弟选择器（Adjacent sibling selector）可选择紧接在另一元素后的元素，且二者有相同父元素。*/
.contact_form input:focus + .form_hint {display: inline;}
.contact_form input:required:valid + .form_hint {background: #28921f;}
.contact_form input:required:valid + .form_hint::before {color:#28921f;}
	
/* === Button Style === */
button.submit {
	background-color: #68b12f;
	background: -webkit-gradient(linear, left top, left bottom, from(#68b12f), to(#50911e));
	background: -webkit-linear-gradient(top, #68b12f, #50911e);
	background: -moz-linear-gradient(top, #68b12f, #50911e);
	background: -ms-linear-gradient(top, #68b12f, #50911e);
	background: -o-linear-gradient(top, #68b12f, #50911e);
	background: linear-gradient(top, #68b12f, #50911e);
	border: 1px solid #509111;
	border-bottom: 1px solid #5b992b;
	border-radius: 3px;
	-webkit-border-radius: 3px;
	-moz-border-radius: 3px;
	-ms-border-radius: 3px;
	-o-border-radius: 3px;
	box-shadow: inset 0 1px 0 0 #9fd574;
	-webkit-box-shadow: 0 1px 0 0 #9fd574 inset ;
	-moz-box-shadow: 0 1px 0 0 #9fd574 inset;
	-ms-box-shadow: 0 1px 0 0 #9fd574 inset;
	-o-box-shadow: 0 1px 0 0 #9fd574 inset;
	color: white;
	font-weight: bold;
	padding: 6px 20px;
	text-align: center;
	text-shadow: 0 -1px 0 #396715;
}
button.submit:hover {
	opacity:.85;
	cursor: pointer; 
}
button.submit:active {
	border: 1px solid #20911e;
	box-shadow: 0 0 10px 5px #356b0b inset; 
	-webkit-box-shadow:0 0 10px 5px #356b0b inset ;

	-moz-box-shadow: 0 0 10px 5px #356b0b inset;
	-ms-box-shadow: 0 0 10px 5px #356b0b inset;
	-o-box-shadow: 0 0 10px 5px #356b0b inset;
	
}
```
