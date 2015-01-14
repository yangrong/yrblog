###  由于作用域问题，不能清除定时器

运用场景：循环一个对象，执行对应的定时器操作，然后估计对象里面的属性的值的不同情况，停止定时器

```js

 function run(data) {
 //len 取的外部变量 
 		var timer = null;
		for (var i = 0; i < len; i++) {
			if (!!data[i].src) {
			//这里运用的闭包，如果不封装起来，执行的for结束之后，setInterval才执行，那么i就永远是 len 
				(function(item, index, self) {
						timer = setInterval(function() {
						if (item.curNum < self.maxNum) {
							updateSrc(index);
							item.curNum++;
						}else{
						//这里预期是满足的条件的是，清除timer这个定时器。
						// 但是实际效果 会看到定时器，不断执行clearInterval(timer);(预期的定时器没有被清除)
							clearInterval(timer);
						}
					}, self.t)
				})(data[i], i);
			}
		}
	}
```
这里出现这个定时器清除不了，是因为var timer = null; 是for循环的外声明的.执行for循环的时候，会建立len (外部变量传进来的数组的长度)个 setInterval,不断赋值给for循环外的timer变量，所以满足条件的时候，clearInterval(timer)清除的其实是，最后一个setInterval赋值给了timer的这个定时器，还有其他的定时器还在执行。解决方案，只需要把定时器，放在for循环里面就好了。


