最近一个业务场景，如下代码？
```html
  <a href="#" class="pay-monthly"  data-packageid='1001' data-type='1'>立即购买</a>
  <a  target="_blank"  href="#" class="open-blank"></a>

```

```js
/*这个js是基于wrap框架写的*/
W('.pay-monthly').on('click', function(e) {
	e.preventDefault();
	var _this = W(this),
		packageId = _this.getAttr('data-packageid'),
		type = _this.getAttr('data-type'),
		payUrl = '/package/subscribe?packageid=' + packageId + '&type=' + type,
		requestUrl = '/package/buypackage?packageid=' + packageId + '&type=' + type;
		
//每次点击做一次请求
	QW.Ajax.get(requestUrl, function(responseText) {
		var state = responseText.evalExp().errno;
		if (state == 1001) {
            runFlag = 1;
			W('#tophead .btn-login-pop').click();
		}
		if (state == 1002) {
		//每次请求，绑定监听点击事件
    W('#popnotice-wrap .continue').on('click', function(e) {
    //程序触发点击a标签，触发页面打开新标签
           W('.open-blank').click();
    });
		}
		if (state == 1000) {
		//do sth
		}
	});

});

```

这程序，我们在一般的浏览器（无拦截js弹出窗口）上运行的时候，会发现一次运行，是预期的效果，就是打开一个新的标签，但是第二次点击的时，会打开两个标签，第三次，打开三个便签，以此类推，这里就是 每请求一次，满足条件的情况下，给这个元素W('#popnotice-wrap .continue')绑定一个click事件，当click事件被触发的时候，所有绑定的事件就会依次触发<br>
应该是吧监听事件，移到请求的外面，避免多次绑定。
解决了，多次绑定时间的问题，上面的程序，还是不能在屏蔽了弹出窗口的浏览器上执行，因为a标签的属性是 target="_blank" ，点击a标签，浏览器会认为程序恶意打开弹窗，给屏蔽了。
这里有一个方法，可以骗过浏览器，如下代码里：


```js
W('.pay-monthly').on('click', function(e) {
  e.preventDefault();
  var _this = W(this),
    packageId = _this.getAttr('data-packageid'),
    type = _this.getAttr('data-type'),
    payUrl = '/package/subscribe?packageid=' + packageId + '&type=' + type,
    requestUrl = '/package/buypackage?packageid=' + packageId + '&type=' + type;
  var elLink = W('.open-blank'),
        runFlag = '';
  //这里用  在手动点击W('.pay-monthly')元素，执行setInterval，setInterval执行的点击事件，浏览器，就不会屏蔽掉了。
  var runInterval = setInterval(function(){
            if(runFlag){
                if(2==runFlag){
                    elLink.attr('href', payUrl).click();
                }
                clearInterval(runInterval);
            }
        },300);
  QW.Ajax.get(requestUrl, function(responseText) {
    var state = responseText.evalExp().errno;
    if (state == 1001) {
    //返回值，清空定时器。
            runFlag = 1;
      W('#tophead .btn-login-pop').click();
    }
    if (state == 1002) {
      runFlag = 1;
      W('#popnotice-wrap .continue').attr('href', payUrl);
    }
    if (state == 1000) {
    //传值给定时器，定时器获取信息，触发click事件
      runFlag = 2;
    }
  });

});
```
