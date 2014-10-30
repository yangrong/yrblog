单行文字垂直居中:

```html
<p>单行文字</p>
```

```css
p{

line-height:30px;
border: 1px dashed #cccccc;

}
```

多行文字垂直居中：


```html
<p class="mulit_line mt10">
  <span style="font-size:12px;">这里是高度为150像素的标签内的多行文字，文字大小为12像素。<br>这里是第二行，用来测试多行的显示效果。</span>
</p>
```

```css
.mulit_line {
line-height: 150px;//设置p元素的行高
border: 1px dashed #cccccc;
}

.mulit_line span {
display: inline-block;
line-height: 1.4em;//重新设置行高
vertical-align: middle;
}
```

