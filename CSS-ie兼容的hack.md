#### ie兼容的hack

1）IE6      ：  _classname<br>

2）IE6/IE7：  *classname<br>

3）IE7      ：  +classname    OR    *+classname<br>

4）IE8/IE9：  classname\0<br>

5）IE9       ：  classname\9\0<br>

6）only IE ：  classname\9<br>

7）建议不要使用 !important，这个是优先级最高的hack，高于内联CSS，除IE6外都支持。<br>
这个优先级别，手机端的曾经在夜间模式里面用过简直是秒杀所有。

建议使用优雅降级：<br>

比如：在HTML页面中加入如下代码<br>
```html
<!--ie7一下-->
<!--[if lt IE 7 ]><html class="ie6"><![endif]-->
```

```html
<!--[if IE 7 ]><html class="ie7"><![endif]-->
```

```html
<!--ie8-->
<!--[if IE 8 ]><html class="ie8"><![endif]-->
```
```html
<!--ie9-->
<!--[if IE 9 ]><html class="ie9"><![endif]-->
```
在CSS页面中，对使用hack的CSS用.ie6/7/8/9来分别限制展示效果。


还有一个常见的写法

```css
*html{
/*只有ie6识别*/
}

*+html{
/*只有ie7识别*/
}

```



