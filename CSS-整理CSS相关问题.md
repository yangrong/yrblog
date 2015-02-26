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
   /*仍然会占据原来的 height:100px; width:100px;位置，只是那区域变成空白*/
}
.sed{
    background:green;
}
```


##### CSS中 link 和@import 的区别是？

(1) link属于HTML标签，而@import是CSS提供的;<br/>
(2) 页面被加载的时，link会同时被加载，而@import引用的CSS会等到页面被加载完再加载,所以@import引用会慢一点<br/>
(3) import只在IE5以上才能识别，而link是HTML标签，无兼容问题;<br/>
(4) link方式的样式的权重 高于@import的权重;<br/>
