JavaScript阻止事件冒泡和浏览器的默认行为.md
==============

在使用javascript编程时会遇到一个问题,就是当你给html添加事件时,由于浏览器默认的为冒泡型事件触发机制,所以会触发你不想触发的事件.那么通过如下的函数可以解决这个问题.[兼容IE和FF]


1.阻止事件冒泡,使成为捕获型事件触发机制.

```js
function stopBubble(e) { 
//如果提供了事件对象，则这是一个非IE浏览器 
if ( e && e.stopPropagation ) 
    //因此它支持W3C的stopPropagation()方法 
    e.stopPropagation(); 
else
    //否则，我们需要使用IE的方式来取消事件冒泡 
    window.event.cancelBubble = true; 
}
```

2.当按键后,不希望按键继续传递给如HTML文本框对象时,可以取消返回值.即停止默认事件默认行为.

```js
function stopDefault( e ) { 
    //阻止默认浏览器动作(W3C) 
    if ( e && e.preventDefault ) 
        e.preventDefault(); 
    //IE中阻止函数器默认动作的方式 
    else
        window.event.returnValue = false; 
    return false; 
}
```
