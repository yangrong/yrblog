```js


/*
 * CookieStorage.js
 * 本类实现像localStorage和sessionStorage一样的存储API，不同的是，它是基于HTTP Cookies实现的.
 */
function CookieStorage(maxage, path) {  // 两个参数分别代表储存有效期和作用域
  // 获取一个储存全部cookies的对象
  var cookies = (function() { // 类型之前介绍的getCookies函数
    var cookies = {};           // 该对象最终会返回
    var all = document.cookie;  // 以大字符串的形式获取所有cookies的信息
    if (all === "")             // 如果该属性为空白符
      return cookies;         // 返回一个空对象
    var list = all.split("; "); // 分离出名/值对
    for(var i = 0; i < list.length; i++) {  // 遍历每个cookie
      var cookie = list[i];
      var p = cookie.indexOf("=");        // 找到第一个“=”符号
      var name = cookie.substring(0,p);   // 获取cookie的名字
      var value = cookie.substring(p+1);  // 获取cookie对应的值
      value = decodeURIComponent(value);  // 对其值进行解码
      cookies[name] = value;              // 将名值对存储到对象中
    }
    return cookies;
  }());
  // 将所有cookie的名字存储到一个数组中
  var keys = [];
  for(var key in cookies) keys.push(key);
  // 现在定义储存API公共的属性和方法
  // 储存的cookies的个数
  this.length = keys.length;
  // 返回第n个cookie的名字，如果n越界则返回null
  this.key = function(n) {
    if (n < 0 || n >= keys.length) return null;
    return keys[n];
  };
  // 返回指定名字的cookie值，如果不存在则返回null
  this.getItem = function(name) { return cookies[name] || null; };
  // 储存cookie值
  this.setItem = function(key, value) {
    if (!(key in cookies)) { // 如果要促成的cookie还不存在
      keys.push(key);      // 将指定的名字加入到储存所有cookie名的数组中
      this.length++;       // cookies个数加一
    }
    // 将该名/值对数据存储到cookie对象中.
    cookies[key] = value;
    // 开始正式设置cookie.
    // 首先将要储存的cookie的值进行编码，同时创建一个“名称=编码后的值”形式的字符串
    var cookie = key + "=" + encodeURIComponent(value);
    // 将cookie的属性也加入到该字符串中
    if (maxage) cookie += "; max-age=" + maxage;
    if (path) cookie += "; path=" + path;
    // 通过document.cookie属性来设置cookie
    document.cookie = cookie;
  };
  // 删除指定的cookie
  this.removeItem = function(key) {
    if (!(key in cookies)) return;  // 如果cookie不存在，则什么也不做
    // 从内部维护的cookies组删除指定的cookie
    delete cookies[key];
    // 同时将cookie中的名字也在内部的数组中删除.
    // 如果使用ES5定义的数组indexOf()方法会更加简单.
    for(var i = 0; i < keys.length; i++) {  // 遍历所有的名字
      if (keys[i] === key) {              // 当我们找到了要找的那个
        keys.splice(i,1);               // 将它从数组中删除.
        break;
      }
    }
    this.length--;                          // cookies个数减一
    // 最终通过将该cookie的值设置为空字符串以及将有效期设置为0来删除指定的cookie.
    document.cookie = key + "=; max-age=0";
  };
  // 删除所有的cookies
  this.clear = function() {
    // 循环所有的cookies的名字，并将cookies删除
    for(var i = 0; i < keys.length; i++)
      document.cookie = keys[i] + "=; max-age=0";
    // 重置所有的内部状态
    cookies = {};
    keys = [];
    this.length = 0;
  };
}




```
