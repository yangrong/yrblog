#### font-family & src
```css
@font-face {
/*这里声明字体类型*/
font-family: 'MyFontFamily';
/*local是指本地有，就在用本地这个字体文件*/
/*eot,ttf,woff等不同格式声明，是由于不同浏览器对不同字体格式的声明写的*/
src: local(MyFontFamily),
url('font.eot?#iefix') format('embedded-opentype'),
/*IE6+*/
url('font.woff') format('woff'), 
url('font.ttf') format('truetype'),
url('font.svg#svgFontName') format(‘svg');
}

```


#### unicode-range属性
unicode 的区间（字体库里面的区间）

```css
/*这个css表示运用的MyFontFamily这个字体库的两个区间分别是U+2E80-FFFF, U+00-0F和U+00F-FFF,运用一个字体库的两个区间*/
@font-face {
font-family: 'MyFontFamily';
src: url('font1.ttf') format(‘truetype');
unicode-range: U+2E80-FFFF, U+00-0F;
}
@font-face {
font-family: 'MyFontFamily';
src: url('font2.ttf') format(‘truetype');
unicode-range: U+00F-FFF;
}
```

1) 以下unicode范围指定的大写字母,小写字母、符号和标点符号:

unicode-range: U+0021-U+007B;


2) 以下unicode范围指定所有大写字母,小写字母和数字:


unicode-range:
    U+0030-U+0039, /* 0-9 */
    U+0041-U+005A, /* Uppercase A-Z */
    U+0061-U+007A; /* Lowercase a-z */

3) 以下unicode范围指定仅显示字母字符串中使用:

unicode-range:
    U+0054-U+0054, /* T */
    U+0061-U+007A, /* a-z */
    U+002E-U+002E; /* . (period) */


#### 浏览器兼容性
支持的浏览如下

##### 手机浏览器
iOS Safari
• Android Browser 2.1+
• Opera Mobile
• Chrome for Android
• Firefox for Android
• IE Mobile
• UC

##### pc浏览器

• IE5.5~IE8，IE9+
• Firefox 3.5+
• Chrome，Safari，Opera

IE5.5~IE8属于不标准的支持(部分支持)，部分支持在IE9指只支持文本结束字体。Safari iOS 4.1及以下只支持SVG的字体。

如图
![](http://p8.qhimg.com/t0137f1a984fb14c371.png "可选的title")


#### Web Fonts 包括的几种字体

TrueType(.ttf), OpenType(.ttf, .otf)<br>
Embedded OpenType(.eot)<br>
SVG Font(.svg, .svgz)<br>
Web Open Font Format(.woff, .woff2)<br>

TrueType,OpenType(在网页中只两种格式没有区别)： <br>
windows mac系统是默认支持的<br>
Embedded OpenType： <br>
IE5.5~IE8只支持 Embedded OpenType(.eot)这种格式 <br>
SVG Font(.svg, .svgz)：<br>
svg自己的一套使用svg来描述字体的格式

Web Open Font Format(.woff, .woff2)：<br>
w3c提出的一种字体格式，woff2相对woff体积小，但是浏览器支持情况没有woff好

![](http://p5.qhimg.com/t01faeab7f8ead32e87.png "可选的title")


#### Web Fonts 的两方面的运用

##### 作为字体使用的优点


• 页面美观、⾃动适配⾼清屏（使用户看到的效果和设计
一致，更趋向于设计图的效果）
• 显示生僻字
• ⽀持选中、复制、查找、修改⽅便
• 对搜索引擎、翻译工具、缩放、⽆障碍设备原生支持；


#### 使用Web Fonts
##### 本地使用<br/>
将拿到的字体转换成兼容浏览器的多个版本<br/>
通过CSS 定义@font-face 引⽤对应的字体<br/>
在线字体服务<br/>
[Google Fonts ](https://www.google.com/fonts "可选的title")
[Just Font](http://cn.justfont.com/ "可选的title")
[有字库](http://www.youziku.com/ "可选的title")
 

```css
<link href='http://fonts.googleapis.com/css?family=Open+Sans' rel='stylesheet'>
```


Google Fonts 的国内代理服务
[360 网站卫士(不支持SSL)](http://libs.useso.com/ "可选的title")
[LUG@USTC](https://lug.ustc.edu.cn/ "可选的title")



#### 引用Web Fonts
```css
.title {
font-family: ‘myFontFamily’;
}
```

作为字体使用的一些问题
• 版权问题
• 盗版
• 授权费
• 授权范围
• 中文字体问题（授权费高，字体文件体积大）
• 文件庞大（好几MB）
• 字体转换（中文字体文件，都要自己转化。有些由于文件过大，没有直接转化。中文字体文件都要压缩要转化。压缩，就是将没有用到的字剔除，剩下的字体文件，只包含我们需要的文字，及字体子集）


#### 字体压缩转换工具
字体子集(embedded subset) 

[字蛛](http://font-spider.org/ "")

通过分析html，css 中的文件的字体，定义的字体，筛选出来，对字体文件进行压缩，把没有出现的字，从字体文件中剔除。


[方正字库的所有字体](http://font.qiwoo.org/ "")

字蛛依赖的网上工具
Fontforge<br/>
ttf2eot<br/>
sfnt2woff<br/>
woff2_compress<br/>


#### 作为Icon 使用
优点：矢量性（放大不失真），颜色可以在css定义

#### Icon Fonts 在线库

https://icomoon.io/app/ 

http://fortawesome.github.io/Font-Awesome/icons/

http://iconfont.cn/

http://fontello.com/


Icon Fonts 使用
```html
<h2><span class=“icon icon-name”></span>IconFonts</h2>
```

```css
.icon {
font-family: 'fonticon';
speak: none;
user-select: none;
}
.icon-name:before {
content: "\e900";
}
```

制作Icon
设计师提供矢量图- SVG 格式
对齐到像素
曲线闭合
色彩填充
在线导入，制作
Icomoon
iconfont*
foontello
