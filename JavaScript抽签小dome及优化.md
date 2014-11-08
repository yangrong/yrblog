#### JavaScript抽签小dome及优化

今天做了一个用js实现的，在一个数组里面随机抽取三个数。
```js
 function produceNum (arr,num) {
 	var numArr=[];
 	while(numArr.length<num){
 	 //根据数组的长度，生成指定的索引值，这里是生成的 0—9的任意数字（数组长度为10）
 		var newNum =Math.floor(Math.random()*arr.length);
 		//判断不重复
 		if(numArr.indexOf(newNum)==-1){
 			numArr.push(arr[newNum])
 		}
 	}
 	return numArr;
 	}
 
```

这个方法起来有一个问题，就是，当我们的去的抽签的数字足够大，比如在一个数组1000的数字里面去100个，那取到重复索引值的可能性，就大大提高了这样增加if语句的判断次数。优化方案如下：

```js
 function produceNum (arr,num) {
 	var numArr=[];
 	for(var i=0;i<num;i++){
 		var newNum =Math.floor(Math.random()*(arr.length));
   //取到一个值，然后这个值从数组里删除掉，不用判断重复
 		numArr.push(arr[newNum]);
 		arr.splice(newNum,1);
 		console.log(arr);
 	}
 	return numArr;
 	}
 
```

但是这个方法中使用的 splice()方法，将指定的数组删除，其实性能只是比前面那个方法好一些而已，因我们再用splice()的时候，比如一个长度100的数组，我们删除了第55个元素，那么剩下的45个元素，会一个一个向前进，那么这样，我们会经过45次运算，也是不太可取了。所以下面的方法，我们直接将最后一个元素补到前面的被删除的元素的位置，就可以了。

```js
 function produceNum (arr,num) {
 	var numArr=[];
 	for(var i=0;i<num;i++){
 		var newNum =Math.floor(Math.random()*(arr.length-i));
 		numArr.push(arr[newNum]);
 		//将最后的值赋值给对应要删除的位置（替换）
 		arr[newNum] = arr[arr.length-1];
 		//删除数组最后一个元素。
 		arr.length =arr.length -1;
 		console.log(arr);
 	}
 	return numArr;
 	}
``` 
