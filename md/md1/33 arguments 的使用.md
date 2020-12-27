# arguments 的使用

当我们不确定有多少个参数传递的时候，可以用 arguments 来获取。在 JavaScript 中，arguments 实际上它是当前函数的一个**内置对象**。所有函数都内置了一个 arguments 对象，arguments 对象中**存储了传递的所有实参**。

只有函数才有 arguments 对象，而且是每个函数都内置好了这个 arguments 。

**arguments 展示形式是一个伪数组**。  
伪数组并不是真正意义上的数组，具有以下特点：

- 可以进行遍历
- 具有 length 属性
- 按索引方式存储数据
- 不具有数据的 push, pop 等方法

```javascript
function fun() {
  console.log(arguments);
  console.log(arguments.length);
  console.log(arguments[0]);
}
fun(2, 4, 6, 5, 9);
```

![image](../images/33/1.png)(1)

```javascript
function fun() {
  console.log(arguments);
  for (var i = 0; i < arguments.length; i++) {
    console.log(arguments[i]);
  }
}
fun(2, 4, 6, 5, 9);
```

![image](../images/33/2.png)(2)

## 示例一

- 利用函数求任意个数的最大值

```javascript
function getMax() {
  var max = arguments[0];
  for (var i = 1; i < arguments.length; i++) {
    if (max < arguments[i]) {
      max = arguments[i];
    }
  }
  console.log(max);
}
getMax(2, 4, 6, 5, 9);
getMax(43, 98, 8, 23, 98, 43);
getMax(1, 89, 342, 9887);
```

![image](../images/33/3.png)(3)
