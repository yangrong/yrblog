appendChild&innerHTML
-----------------

appendChild和innerHTML是两个常用的给节点添加内容的方法。

###### appendChild
appendChild() 方法在指定元素节点的最后一个子节点之后添加节点。

##### innerHTML
innerHTML 属性设置或返回表格行的开始和结束标签之间的 HTML内容
dom.innerHTML  -> 这个获取html内容（获取的是一个字符串）
dom.innerHTML = '<a>链接</a>' -> 这样是给dom上面的添加html内容，以字符串的方式。

appendChild区别于innerHTML在于前者要求插入的元素应该是dom元素，且只是将插入的元素，放在父节点的最后一个节点上
而后者是字符串，字符串将覆父层元素已有的所有内容。

如果我们要把一个字符串，比如
```js
var link ='<a herf='#'>a link</a>'
```
通过appendChild方法放入父层的最后一个节上。
我们可以用如下方法（jquery环境下）
```js
var link ='<a herf='#'>a link</a>'
/*父层节点的位置*/
var father=$('#father');
father[0].appendChild($(link)[0]);
```
JQuery 提供的一个函数
append(content)方法的功能是向指定的元素中追加内容，被追加的content参数，可以是字符、HTML元素标记，还可以是一个返回字符串内容的函数。
