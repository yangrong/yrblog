// @description 准备为图片预加载使用的插件
// 使用的图片容器css类名为lazy-load-wrap
// 图片真实地址为data-lazy-src
// 当lazy-load-wrap容器进入视口，则开始替换容器内所有需要延迟加载的图片路径，并更改容器的加载状态
//第一种方法
$.fn.compassLazyLoad=function(){
    var _HEIGHT=window.innerHeight,
    _lazyLoadWrap=$('.lazy-load-wrap');

    var methods={
        setOffsetTop:function(){
            $.each(_lazyLoadWrap,function(i,n){
                $(n).attr({
                    'top':n.offsetTop-_HEIGHT,
                    'status':'wait'
                });
            })
        },
        isShow:function(){
            var _scrollTop=$(window).scrollTop;
            //利用image容器判断是否进入视口，而非image本身
            $.each(_lazyLoadWrap,function(){
                var _that=$(this);
                if (_that.attr('status')==='done') {
                    return;
                };
                if (_that.attr('top')<=_scrollTop) {
                    _that.find('img[data-lazy-src]').each(function(i,n){
                        n.src=$(n).data('lazy-src');
                    });
                    _that.attr('status','done');
                };
            })
        },
        scroll:function(){
            $(window).on('scroll',function(){
                methods.isShow();
            });
        },
        init:function(){
            methods.setOffsetTop();
            methods.isShow();
            methods.scroll();
        }
    };
    methods.init();

}


//第二种方法

var exist=(function($){
    var timer=null,
    temp=[].slice.call($('.container'));
    ret={};

    for(var i=0,len=temp.length-1;i<=len;i++){
        ret[i]=temp[i];
    }
    var isExist=function(winTop,winEnd){
        for(var i in ret){
            console.log(ret);
            var item=ret[i],
            eleTop=item.offsetTop,
            eleEnd=eleTop+item.offsetHeight;

            if((eleTop>winTop&&eleTop<=winEnd)||(eleEnd>winTop&&eleEnd<=winEnd)){
                $(item).css('background','none');
                new Tab($(item).attr('id'),data).init;
                delete ret[i];
            }
        }
    }
    return {
        timer:timer;
        isExist:isExist;
    };
})($);



//第三种方法
Zepto(function ($) {
    var swiper = new Swiper('.swiper-container', {
        pagination: '.swiper-pagination',
        paginationClickable: true,
        autoplay: 3000,
        loop: true,
        autoplayDisableOnInteraction: false
    });
    (function lazyLoad() {
        var imgs = $(".lazyLoad");
        var src = '';
        $.each(imgs, function (index, item) {
            src = $(item).attr('data-src');
            $(item).attr('src', src);
        });
    })();
});
$(function () {
    var lazyLoadTimerId = null;
    /// 智能加载事件
    $(window).bind("scroll", function () {
        clearTimeout(lazyLoadTimerId);
        lazyLoadTimerId = setTimeout(function () {
            // 延迟加载所有图片
            var isHttp = (location.protocol === "http:");
            $("#ym_images img").each(function () {
                var self = $(this);
                if (self.filter(":above-the-fold").length > 0) {
                    var originUrl = self.attr("data-original");
                    self.attr("src", originUrl);
                }
            });
        }, 500);
    });
});
