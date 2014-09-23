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
/*contact_form input:required:valid，表示所有带required属性的input输入内容，合法，这里的是否合法，会根据input的type属性，比如type="email"，那这里输入的内容应该是符合email格式的才会执行这个css 语句*/
.contact_form input:required:valid, .contact_form textarea:required:valid {background: #fff url(images/valid.png) no-repeat 98% center;box-shadow: 0 0 5px #5cd053;border-color: #28921f;}
/*contact_form input:required:invalid，表示所有带required属性的input输入内容，不合法，执行这个css */
.contact_form input:focus:invalid, .contact_form textarea:focus:invalid {background: #fff url(images/invalid.png) no-repeat 98% center;box-shadow: 0 0 5px #d45252;border-color: #b03535;}
```


