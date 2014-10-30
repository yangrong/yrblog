#### line-block的居中定位问题

项目里遇到将一个元素设置inline-block，为了设置padding值,这样影响到了同级元素的垂直居中设置。

```html
<div>
    <span class='first'>first</span>
    <span class='second'>second</span>
</div>
```

```css
div{
    height:40px;
    line-height:40px;
    border:1px solid #336699;
}

.first{
    position:relative;
    left:4px;
    top:2px;
    display:inline-block;
    padding:4px;
    
}

```

我们看到 我们在父层设置了 height:40px; line-height:40px;为了子层的行内元素居中。<br>
但是这里的 <span class='second'>second</span>并没有居中。<br>
这里是因为 <span class='first'>first</span>元素的设置的上边距把父层元素的垂直对齐方式（默认为 baseline：基线对齐；）这条基线给拉低了，所以其他同级行内元素，也是根据这条基线来对齐。<br>
这里注意，只有设置padding-top会引起，其他的padding的方向不会影响到基线的位置。
