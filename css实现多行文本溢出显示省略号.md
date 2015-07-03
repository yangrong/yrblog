

##  css实现多行文本溢出显示省略号


### 单行溢出省略号


```html
<p>时光未央,岁月静好。</p>
```


```css
p{
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    width:150px;
}
```

但是这个属性并不支持多行文本溢出显示省略号，这里根据应用场景介绍几个方法来实现这样的效果。

WebKit浏览器或移动端的页面
在WebKit浏览器或移动端（绝大部分是WebKit内核的浏览器）的页面实现比较简单，可以直接使用WebKit的CSS扩展属性(WebKit是私有属性)-webkit-line-clamp ；注意：这是一个 不规范的属性（unsupported WebKit property），它没有出现在 CSS 规范草案中。
-webkit-line-clamp用来限制在一个块元素显示的文本的行数。 为了实现该效果，它需要组合其他的WebKit属性。


常见结合属性：

```css
display: -webkit-box; 必须结合的属性 ，将对象作为弹性伸缩盒子模型显示 。
-webkit-box-orient 必须结合的属性 ，设置或检索伸缩盒对象的子元素的排列方式 。
text-overflow: ellipsis;，可以用来多行文本的情况下，用省略号“…”隐藏超出范围的文本 。
overflow : hidden;
text-overflow: ellipsis;
display: -webkit-box;
-webkit-line-clamp: 2;
-webkit-box-orient: vertical;
```


这个属性比较合适WebKit浏览器或移动端（绝大部分是WebKit内核的）浏览器。


```html
<p>时光未央,岁月静好。时光未央,岁月静好。时光未央,岁月静好。时光未央,岁月静好。时光未央,岁月静好。</p>
```


```css
p{
width:220px;
position: relative;
line-height:18px;
height: 54px;
overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box;
-webkit-line-clamp: 3;
/*盒模型为三行，超过三行第三行尾部显示省略号*/
-webkit-box-orient: vertical;
}
```

