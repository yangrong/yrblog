下面总结几个，最近在移动端开发的时候，开始尝试用的几个css3属性

##### 1. box-sizing
这个属性有两个值：
第一个值：content-box（css2规范里的标准，就是设置一个元素的width只会包括content部分，不包括padding，border两个属性所以我们一般在css2中，设置了一个圆度的对固定width（或者是height），一般就不会设置padding，第一个是计算麻烦，第二是在ie6下有兼容性的问题）
第二个值：border-box（css3规范里的标准，元素盒子的内容会包括内容区域+padding+border）

```html
<div class="container">
<div class="box">这个 div 占据左半部分。</div>
<div class="box">这个 div 占据右半部分。</div>
</div>
```
```css
.container
{
width:30em;
border:1px solid;
}
.box
{
box-sizing:border-box;
-moz-box-sizing:border-box; /* Firefox 一般我们现在在移动端不用再考虑了*/
-webkit-box-sizing:border-box; /* Safari */
width:50%;
border:1em solid red;
padding:10px;
float:left;
}
```
这样设置的好处，第一直观上，比较好理解，方便计算，第二，在给元素设置百分比的width的时候，可以把border和padding一起算到百分比里一起做计算。
过去，我们要一个子元素，相对父层元素设置width：100%;使得子元素（这个子元素要求绝对定位），相对父层，完成展开，但是，如果要设置border，和padding
元素的时候，就会超出父层的宽度。没有达到理想的width：100%的效果，如果非要这样实现，就必须如下实现
```html
<div class='father'>
  <div class="border"><!--这一个层负责设置width100%-->
    <div class="child"><!--这一个层负责设置pading,border-->
      这个层负责设置padding，border
    </div>
  </div>
</div>
```

##### 1.flex
弹性布局
```html
 <div class="header">
	 <div class="logo">logo部分，宽高固定</div>
	 <div class="nav">nav部分，高度固定，宽度自适应</div>
 </div>
 <div class="content">
	 <div class="con1">固定宽度</div>
	 <div class="con2">内容初始化第2模块</div>
	 <div class="con3">固定宽度</div>
 </div>
 <div class="footer">底部，宽度不定，高度固定</div>
```

```css
html,body{height:100%;margin:0;}/*需要添加高度控制，否则无法撑满整个屏幕*/
body{display:-webkit-box;
-webkit-box-orient:vertical;/*按照垂直方向上进行自适应处理*/
}
 .content,.header{display:-webkit-box;/*为content,header部分也添加box的展示模式，子元素会float，left,所以不要再给子元素设置float：left了这样会使元素显示不了*/}
 .header{height:50px;min-width:500px;}/*顶部模块高度定死*/
 .logo{width:100px;height:50px;background:#99f;}/*为区分模块，设置了背景色 logo部分固定宽高*/
 .nav{height:50px;background:#ccc;}/*nav模块不固定宽度*/
.nav{-webkit-box-flex:1;}
 .content{min-height:100px;-webkit-box-flex:1;/*分配剩余的所有空间*/}/*为防止之后的调整窗口大小是出现影响视觉效果的问题，特设置最小高度*/
 .con1{width:200px;background:#f99;}/*固定宽度，高度不定*/
 .con2{min-width:200px;background:#999;}/*同上的min-height*/
 .con3{width:100px;background:#9f9;}/*固定宽度，高度不定*/

 .footer{height:50px;min-width:500px;background:#ccc;}/*固定高度*/
.con2{-webkit-box-flex:1;}/*中间第二个元素自适应*/
```


我们将上面的css代码改成：
```css
html,body{height:100%;margin:0;}/*需要添加高度控制，否则无法撑满整个屏幕*/
body{display:-webkit-box;
-webkit-box-orient:vertical;/*按照垂直方向上进行自适应处理*/
}
 .content,.header{display:-webkit-box;/*为content,header部分也添加box的展示模式，子元素会float，left,所以不要再给子元素设置float：left了这样会使元素显示不了*/}
 .header{height:50px;min-width:500px;}/*顶部模块高度定死*/
 .logo{width:100px;height:50px;background:#99f;}/*为区分模块，设置了背景色 logo部分固定宽高*/
 .nav{height:50px;background:#ccc;}/*nav模块不固定宽度*/
 .nav{-webkit-box-flex:1;}
 .content{min-height:100px;-webkit-box-flex:1;/*分配剩余的所有空间*/}/*为防止之后的调整窗口大小是出现影响视觉效果的问题，特设置最小高度*/
 .con1{min-width:200px;background:#f99;}/*固定宽度，高度不定*/
 .con2{min-width:200px;background:#999;}/*同上的min-height*/
 .con3{min-width:100px;background:#9f9;}/*固定宽度，高度不定*/

 .footer{height:50px;min-width:500px;background:#ccc;}/*固定高度*/
  .con1{-webkit-box-flex:1;}/*中间第一个元素自适应*/
   .con2{-webkit-box-flex:1;}/*中间第二个元素自适应*/
 .con3{-webkit-box-flex:1;}/*中间第三个元素自适应*/
```
这样可以看到内容区域的是三个元素的都自适应了

我们再把代码做一个小调整
```css
  .con1{-webkit-box-flex:1;}/*中间第一个元素自适应*/
  .con2{-webkit-box-flex:2;}/*中间第二个元素自适应*/
 .con3{-webkit-box-flex:3;}/*中间第三个元素自适应*/
```
这里在chrome 33版本上，没有达到我们理想的效果，没有办法等分 ，之后，再按比列分给各个元素。
在chrome 36+表现良好。
