##### display:none和visibility:hidden的区别？

display:none  隐藏对应的元素，在文档布局中不再给它分配空间，它各边的元素会合拢，
就当他从来不存在。

visibility:hidden  隐藏对应的元素，但是在文档布局中仍保留原来的空间。

```html
<div class='fir'></div>
<div class='sed'></div>
```


```css
div{
    height:100px;
    width:100px;
}

.fir{
    background:red;
   visibility:hidden
   //仍然会占据原来的 height:100px; width:100px;位置，只是那区域变成空白
}
.sed{
    background:green;
}
```
