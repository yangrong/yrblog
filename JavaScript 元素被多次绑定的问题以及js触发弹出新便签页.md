最近一个业务场景，点击按钮，然后通过按钮上的特定的参数请求一个url并返回数据，通过不同的情况，处理不同的事件，其中一种情况是js触发打开新标签页，如下代码？
```html
  <a href="#" class="pay-monthly"  data-id='1001' data-type='1'>立即购买</a>
  <a  target="_blank"  href="#" class="open-blank"></a>

```

```js
/*这个js是基于wrap框架写的*/
W('.pay-monthly').on('click', function(e) {
	e.preventDefault();
	var _this = W(this),
		packageId = _this.getAttr('data-packageid'),
		type = _this.getAttr('data-type'),
		payUrl = '/packag/scribe?packageid=' + packageId + '&type=' + type,
		requestUrl = '/packag/bpackage?packageid=' + packageId + '&type=' + type;
		
//每次点击做一次请求
	QW.Ajax.get(requestUrl, function(responseText) {
		var state = responseText.evalExp().errno;
		if (state == 1001) {
             
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
应该是把监听事件，移到请求的外面，避免多次绑定。
解决了，多次绑定时间的问题，上面的程序，还是不能在屏蔽了弹出窗口的浏览器上执行，因为a标签的属性是 target="_blank" ，点击a标签，浏览器会认为程序恶意打开弹窗，给屏蔽了。
这里有一个方法，可以骗过浏览器，如下代码里：


```js
W('.pay-monthly').on('click', function(e) {
  e.preventDefault();
	  /*点击事件触发时候，用 window.open()就马上打开新窗口,这个是不会被屏蔽掉的。（任何浏览器下）*/
	  var newWindow  = window.open('about:blank');
	  var _this = W(this),
	    packageId = _this.getAttr('data-packageid'),
	    type = _this.getAttr('data-type'),
	    payUrl = '/packag/scribe?packageid=' + packageId + '&type=' + type,
	    requestUrl = '/packag/bpackage?packageid=' + packageId + '&type=' + type;
   
  QW.Ajax.get(requestUrl, function(responseText) {

    var state = responseText.evalExp().errno;
    if (state == 1001) {      
      W('#tophead .btn-login-pop').click();
      //不需要打开窗口的情况下，把浏览器关了就是，就当什么事情没有发生过。
	  newWindow.close();

    }
    if (state == 1002) {
			newWindow.close();
     
    }
    if (state == 1000) {
     //给打开的新标签页赋值。让页面可以正常打开。不被任何浏览器屏蔽哦。
		newWindow.location.href = payUrl;
       
    }
  });

});
```
不过不幸的是，这个程序通过测试发现，只能勉强骗过chrome而已的。ie下 还有一些浏览器比如360浏览器的7.2版本是不给支持的。
还是用如下解决方案。

```js
W('.pay-monthly').on('click', function(e) {
  e.preventDefault();
  /*
  点击之后立即触发的window.open打开的新标签不会被任何浏览器屏蔽，包括ie6
  */
  var newWindow  = window.open('about:blank');

  var _this = W(this),
    packageId = _this.getAttr('data-packageid'),
    type = _this.getAttr('data-type'),
    payUrl = '/packag/scribe?packageid=' + packageId + '&type=' + type,
    requestUrl = '/packag/bpackage?packageid=' + packageId + '&type=' + type;

  QW.Ajax.get(requestUrl, function(responseText) {
    var state = responseText.evalExp().errno;
    if (state == 1001) {

    //不需要的情况下关闭窗口就是，就好像什么都没有发生过一样。

	  newWindow.close();
      W('#tophead .btn-login-pop').click();
    }

    if (state == 1002) {
       
       newWindow.close();
    }
    if (state == 1000) {
    //给打开的窗口赋值url
       newWindow.location.href = payUrl;
    }
  });

});
```
