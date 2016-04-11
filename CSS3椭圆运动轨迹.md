```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>椭圆的运动轨迹</title>
</head>
<style type="text/css">
	html{-ms-text-size-adjust:100%;-webkit-text-size-adjust:100%;}
ul,li,div,p,body{margin:0;padding:0;text-align:left;}
body, html {background:#001424;text-align: left;height: 100%;width: 100%;font-family: "Microsoft YaHei","Helvetica Neue",Arial, HelveticaNeue, "Helvetica-Neue", Helvetica, "BBAlpha Sans", sans-serif;font-size:62.5%;font-weight: normal;}
@-webkit-keyframes star_ani_00{
    0%{
        opacity: 0;
    }
    100%{
        opacity: 1;
    }   
}
@keyframes star_ani_00{
    0%{
        opacity: 0;
    }
    100%{
        opacity: 1;
    }   
}
@-webkit-keyframes star_ani_01{
    0%,100%{
        -webkit-transform: translateY(0rem);
    }
    50%{
        -webkit-transform: translateY(-35rem);
    }
}
@keyframes star_ani_01{
    0%,100%{
        transform: translateY(0rem);
    }
    50%{
       transform: translateY(-35rem);
    }
}
@-webkit-keyframes star_ani_02{
    0%,100%{
        -webkit-transform: translateX(0rem) scale(0.8);
    }    
    50%{
        -webkit-transform: translateX(10rem) scale(1);
    }
}
@keyframes star_ani_02{
    0%,100%{
        transform: translateX(0rem) scale(0.8);
    }    
    50%{
        transform: translateX(10rem) scale(1);
    }
}
@-webkit-keyframes star_ani_03{
    0%,100%{
        -webkit-transform: translateX(0rem);
    }
    50%{
        -webkit-transform: translateX(-36rem);
    }
}
@keyframes star_ani_03{
    0%,100%{
        transform: translateX(0rem);
    }
    50%{
        transform: translateX(-36rem);
    }
}

@-webkit-keyframes star_ani_04{
    0%,100%{
        -webkit-transform: translateY(0rem) scale(0.8);
    }    
    50%{
        -webkit-transform: translateY(10.5rem) scale(1);
    }
}
@keyframes star_ani_04{
    0%,100%{
        transform: translateY(0rem) scale(0.8);
    }    
    50%{
        transform: translateY(10.5rem) scale(1);
    }
}

@-webkit-keyframes star_ani_05{
    0%,100%{
        -webkit-transform: translateX(0rem);
    }
    50%{
        -webkit-transform: translateX(-26.5rem);
    }
}
@keyframes star_ani_05{
    0%,100%{
        transform: translateX(0rem);
    }
    50%{
        transform: translateX(-26.5rem);
    }
}

@-webkit-keyframes star_ani_06{
    0%,100%{
        -webkit-transform: translateY(0rem) scale(0.8);
    }    
    50%{
        -webkit-transform: translateY(8rem) scale(1);
    }
}
@keyframes star_ani_06{
    0%,100%{
        transform: translateY(0rem) scale(0.8);
    }    
    50%{
        transform: translateY(8rem) scale(1);
    }
}
.main{
    position: relative;
    height:100%;
}
.wrap-icon{
    position:absolute;
    background-size: 100%;
    background-repeat: no-repeat;
    left:50%;
    top: 12%;
    z-index: 2;
    opacity: 0;
}

.wrap-icon1{
    width: 2.7rem;
    height: 2.7rem;
    margin-left:-5.5rem;
    margin-top: 28rem;
    /*默认页面是调用cpu 进行渲染,当写了3d 或者 opacity 就可以开启gpu渲染*/
   -webkit-animation:star_ani_00 0.5s 4s linear forwards;
    animation:star_ani_00 0.5s 4s linear forwards;
}
.wrap-icon1 span{
    width:2.7rem;
    height:2.7rem;
    display: block;
    -webkit-animation:star_ani_02 16s 4s ease-in-out infinite;
    animation:star_ani_02 16s 4s ease-in-out infinite;
}
.wrap-icon1 i{
    width:1.5rem;
    height:1.5rem;
    border-radius:1.5rem;
    display: block;
    background:#f60;
    background-size: 100% 100%;
    -webkit-animation:star_ani_01 16s 0s ease-in-out infinite;
    animation:star_ani_01 16s 0s ease-in-out infinite;
}

.wrap-icon2{
    width: 2.7rem;
    height: 2.7rem;
    margin-left: 17.8rem;
    margin-top: 8rem;
    -webkit-animation:star_ani_00 0.5s 5s linear forwards;
    animation:star_ani_00 0.5s 5s linear forwards;
}
.wrap-icon2 span{
    width:2.7rem;
    height:2.7rem;
    display: block;
    -webkit-animation:star_ani_03 20s 0s ease-in-out infinite;
    animation:star_ani_03 20s 0s ease-in-out infinite;
}
.wrap-icon2 i{
    width:1.5rem;
    height:1.5rem;
    border-radius:1.5rem;
    display: block;
    background:#f60;
    background-size: 100% 100%;
    -webkit-animation:star_ani_04 20s 5s ease-in-out infinite;
    animation:star_ani_04 20s 5s ease-in-out infinite;
}


.wrap-icon3{
    width: 2.7rem;
    height: 2.7rem;
    margin-left: 12.4rem;
    margin-top: 9rem;
    -webkit-animation:star_ani_00 0.5s 2.5s linear forwards;
    animation:star_ani_00 0.5s 2.5s linear forwards;
}
.wrap-icon3 span{
    width:2.7rem;
    height:2.7rem;
    display: block;
    -webkit-animation:star_ani_05 10s 0s ease-in-out infinite;
    animation:star_ani_05 10s 0s ease-in-out infinite;
}
.wrap-icon3 i{
    width:2rem;
    height:2rem;
    border-radius:1rem;
    display: block;
    background:#f60;
    background-size: 100% 100%;
    -webkit-animation:star_ani_06 10s 2.5s ease-in-out infinite;
    animation:star_ani_06 10s 2.5s ease-in-out infinite;
}
.wrap-bg{
    width:28rem;
    height:28rem;
    position: absolute;
    top:12%;
    left:50%;
    margin-left:-14rem;
    border:0.1rem solid #aaa;
    border-radius:28rem;
    -webkit-transform:scale3d(1,0.3,1);
    transform:scale3d(1,0.3,1);
}
.wrap-bg2{
    width:36rem;
    height:36rem;
    position: absolute;
    top:12%;
    left:50%;
    margin-left:-18rem;
    margin-top:-4rem;
    border:0.1rem solid #aaa;
    border-radius:28rem;
    -webkit-transform:scale3d(1,0.3,1);
    transform:scale3d(1,0.3,1);
}
.wrap-bg3{
    width:32rem;
    height:32rem;
    position: absolute;
    top:12%;
    left:50%;
    margin-left:-16rem;
    margin-top:-3rem;
    -webkit-transform:rotate(4deg);
    transform:rotate(4deg);
}
.wrap-bg3 span{
    display: block;
    width:100%;
    height:100%;
    border:0.1rem solid #aaa;
    border-radius:28rem;
    -webkit-transform:scale3d(0.32,1,1);
    transform:scale3d(0.32,1,1);
}
.wrap-sun{
    position: absolute;
    width:5.3rem;
    height:5.3rem;
    top:12%;
    left:50%;
    margin-left:-2.6rem;
    margin-top:11rem;
    background:url(images/sun.png) no-repeat;
    background-size: 100%;
}
    
</style>
<body>
	<div class="box">

<div class="wrap-bg"></div>
<div class="wrap-bg2"></div>
<div class="wrap-bg3"><span></span></div>

<div class="wrap-icon wrap-icon1">
    <span><i></i></span>
</div>

<div class="wrap-icon wrap-icon2">
    <span><i></i></span>
</div>

<div class="wrap-icon wrap-icon3">
    <span><i></i></span>
</div>

<div class="wrap-sun"></div>

</div>
</body>
</html>
```
