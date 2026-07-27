# window

* 浏览器提供了全局对象 window
* window 里面有 console、document、Object、Array、Function
* 数组和函数是特殊的对象

```js
var person = {} 等价于 var person = new Object()

var a = [1,2,3] 等价于 var a = new Array(1,2,3)

function f(){} 等价于 var f = new Function()
```

* 挂在 window 上的东西可以在任何地方**直接**用



![image](../images2/65/n1.PNG)

![image](../images2/65/n2.PNG)

## 关于 window

- window 变量和 window 对象是两个东西。
- window 变量是一个容器，存放 window 对象的地址。
- window 对象是 Heap 里的一坨数据。
- 不信的话，可以让 var x = window, 那么这个 x 就指向了 window 对象， window 变量就可以去死了。

## 同理

- console 和 console 对象不是同一个东西。
- Object 和 Object 函数对象不是同一个东西。
- 前者是内存地址，后者是一坨内存。













