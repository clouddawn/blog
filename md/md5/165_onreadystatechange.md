## XMLHttpRequest.onreadystatechange

#### 语法

```js
XMLHttpRequest.onreadystatechange = callback;
```

* 当 `readyState` 的值改变的时候，`callback` 函数会被调用



## XMLHttpRequest.readyState

* `XMLHttpRequest.readyState` 属性返回一个 XMLHttpRequest 代理当前所处的状态。
* 一个 XHR 代理总是处于下列状态中的一个：

| 值   | 状态             | 描述                                      |
| ---- | ---------------- | ----------------------------------------- |
| 0    | UNSENT           | XHR 代理已被创建，但尚未调用 open() 方法  |
| 1    | OPENED           | open() 方法已被调用                       |
| 2    | HEADERS_RECEIVED | send() 方法已被调用，响应头也已经被接受   |
| 3    | LOADING          | 下载中；responseText 属性已经包含部分数据 |
| 4    | DONE             | 下载完成；数据传输已经彻底完成或失败      |



## XMLHttpRequest.responseXML

* XMLHttpRequest.responseXML 属性时一个只读值，它返回一个包含请求检索的 HTML 或 XML 的 Document ，如果请求未成功，尚未发送，或者检索的数据无法正确解析为 XML 或 HTML，则为 null 。



## element.getElementsByTagName

* `Element.getElementsByTagName()` 方法返回一个动态的包含所有指定标签名的元素的 HTML 集合
* 返回的列表是动态的，这意味着它会随着 DOM 树的变化自动更新自身

#### 语法

```js
elements = element.getElementsByTagName(tagName);
```

* `elements` 搜索到的元素的动态 HTML 集合，它们的顺序是在子树中出现的顺序；如果没有搜索到元素则这个集合为空。
* `element` 搜索从 `element` 开始；请注意，只有 `element` 的后代元素会被搜索，不包括 `element` 元素自己。
* `tagName` 要查找的限定名，字符 `"*"` 代表所有元素。



## String.prototype.trim()

* `trim()` 方法返回一个从两头去掉空白字符的字符串，并不影响原字符串本身。



## JSON.parse()

* `JSON.parse()` 方法用来解析 JSON 字符串，构造由字符串描述的 JavaScript 值或对象。



## JSON.stringify()

* `JSON.parse()` 的逆运算



## Array.prototype.map()

* `map()` 方法创建一个新数组，其结果是该数组中的每个元素调用一次提供的函数后的返回值。

```js
const array1 = [1, 4, 9, 16];
const map1 = array1.map(x => x * 2);
console.log(map1);
```



## Array.prototype.join()

* `join()` 方法将一个数组的所有元素连接成一个字符串并返回这个字符串。
* 如果数组只有一个项目，那么将返回该项目而不使用分隔符。

```js
const elements = [1, 2, 3];
console.log(elements.join('-'));
```



























