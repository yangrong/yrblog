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


##### CSS 选择符有哪些？哪些属性可以继承？优先级算法如何计算？ CSS3新增伪类有那些？

   *   1.id选择器（ # myid）<br/>
        2.类选择器（.myclassname）<br/>
        3.标签选择器（div, h1, p）<br/>
        4.相邻选择器（h1 + p）<br/>
        5.子选择器（ul < li）<br/>
        6.后代选择器（li a）<br/>
        7.通配符选择器（ * ）<br/>
        8.属性选择器（a[rel = "external"]）<br/>
        9.伪类选择器（a: hover, li: nth - child）<br/>

    *   可继承的样式： font-size font-family color, UL LI DL DD DT;<br/>

    *   不可继承的样式：border padding margin width height ;<br/>

    *   优先级就近原则，同权重情况下样式定义最近者为准;<br/>

    *   载入样式以最后载入的定位为准;<br/>

优先级为:


   !important >  id > class > tag  <br/>

   important 比 内联优先级高 <br/>

CSS3新增伪类举例：

##### CSS 选择符有哪些？哪些属性可以继承？优先级算法如何计算？ CSS3新增伪类有那些？

   *   1.id选择器（ # myid）<br/>
        2.类选择器（.myclassname）<br/>
        3.标签选择器（div, h1, p）<br/>
        4.相邻选择器（h1 + p）<br/>
        5.子选择器（ul < li）<br/>
        6.后代选择器（li a）<br/>
        7.通配符选择器（ * ）<br/>
        8.属性选择器（a[rel = "external"]）<br/>
        9.伪类选择器（a: hover, li: nth - child）<br/>

    *   可继承的样式： font-size font-family color, UL LI DL DD DT;<br/>

    *   不可继承的样式：border padding margin width height ;<br/>

    *   优先级就近原则，同权重情况下样式定义最近者为准;<br/>

    *   载入样式以最后载入的定位为准;<br/>

优先级为:


   !important >  id > class > tag  <br/>

   important 比 内联优先级高 <br/>

CSS3新增伪类举例：


p:first-of-type 选择属于其父元素的首个 p 元素的每个 p 元素。<br/>
p:last-of-type  选择属于其父元素的最后 p 元素的每个 p 元素。<br/>
p:only-of-type  选择属于其父元素唯一的 p 元素的每个 p 元素。<br/>
p:only-child    选择属于其父元素的唯一子元素的每个 p 元素。<br/>
p:nth-child(2)  选择属于其父元素的第二个子元素的每个 p 元素。<br/>
:enabled  :disabled 控制表单控件的禁用状态。<br/>
:checked        单选框或复选框被选中。<br/>

E:nth-child(n)
匹配所有在其父元素中排第n个的E元素。n可以是数字/关键字/公式，例如：
```css
tr:nth-child(3) { …… }     /* 匹配所有表格里面排第3的行<tr> */
tr:nth-child(2n+1) { …… }  /* 2n+1，公式，匹配所有奇数行 */
tr:nth-child(odd) { …… }   /* odd：关键字，匹配所有奇数行 */
tr:nth-child(2n) { …… }    /* 2n：匹配所有偶数行*/
tr:nth-child(even) { …… }  /* even：关键字，匹配所有偶数行li */
```


兼容ie6的清楚浮动
```css
.clearfix:after{content: ".";display: block;height: 0;clear: both;visibility: hidden;}
.clearfix{display: inline-block;} /* for IE/Mac */
```
