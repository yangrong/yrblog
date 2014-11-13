#### ie6 hover 效果不显示的问题

#####  关于hover

在 CSS1 中此伪类仅可用于 a 对象。且对于无 href 属性（特性）的 a 对象，此伪类不发生作用。


在 CSS2 中此伪类可以应用于任何对象。但目前 IE5.5、IE6 仅支持 CSS1 中的 :hover，不过新出的 IE7 是支持 CSS2 中的 :hover。

```css
/*所以这段代码，在ie7 及以上的 浏览器都可以很好支持 但是在ie6就没有效果。*/
ul li:hover {
background: #eee;
}
```


那么为了兼容ie6 我们一般都会把 hover 效果写在a标签里面，然后给a便签 设置 display:block;
如下代码：

```html
	<a href="#"><span></span></a>
```


```css
	*{
    margin:0;
    padding:0;
}
a{
    border : 3px solid #999;
    display:block;
    height:200px;
    width:150px;
}

a span{
    display:none;
    height: 100px;
    width: 100px;
    background:#fa9db7
}


a:hover span{
    display:block;
  

}

```

上面这个代码在ie6 以上可以正常运行，但是ie6上不显示span元素，在ie6还有有bug。
这个时候

我们加一段css,就可以修复 ie6这个bug，在其他浏览器下也显示正常了。

```css
a:hover{
    background: none;
}
```
这个解决方案，有一个缺陷，就是a上不能设置背景，因为hover效果，背景会消失，这个时候只能在给a的外层加一个div 设置背景。
