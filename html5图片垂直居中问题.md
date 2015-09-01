

## html5图片垂直居中问题


很久写过一篇css文字垂直居中。今天主要讨论一下移动端，图片垂直居中，适应场景 比如说，图片轮播图（整屏显示的时候）。

```html

<div class="img_bg">
  <div class="pic-box">
    <img src="http://xqproduct.xiangqu.com/FuWqf3VvGKNcz4KqNmv5u6A2RgOs?imageView2/2/w/200/q/95/format/jpg/@w/$w$@/@h/$h$@/501x501/" alt=""/>
    <p>文字描述</p>
  </div>
</div>


```


#### fle布局
```css

    html,body{
      height: 100%;
    }

    .img_bg{
    
    /*设置高度，flex盒子的居中才会生效的*/
        height: 100%;
        display: flex;
         justify-content: center;
         align-items: center;
         background: black;
    }

    .pic-box{
        color:#fff;
        text-align: center;
    }
   
      li img{
          max-width: 100%;
          max-height: 100%;
      }

```

#### transform,无需要父层元素设置高度
```css


    .img_bg{
        height: 100%;
         background: black;
    }

    .pic-box{
        color:#fff;
        text-align: center;
        position: absolute;
          top: 50%;
          left: 50%;
          transform: translate3d(-50%,-50%,0);
          -ms-transform: translate3d(-50%,-50%,0);
          -moz-transform: translate3d(-50%,-50%,0);
          -webkit-transform: translate3d(-50%,-50%,0);
          -o-transform: translate3d(-50%,-50%,0);
    }
   


 img{
  max-width: 100%;
  max-height: 100%;
  
}



```
