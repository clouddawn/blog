# 自己封装一个forEach方法

可以通过向 `Array` 原型添加一个新的方法来重新封装类似于 `forEach` 的功能。

下面是一个简单的实现示例：

```js
// 定义 forEach2 方法 
Array.prototype.forEach2 = function(callback) {    
  for (var i = 0; i < this.length; i++) {        	
    callback(this[i], i, this);    
 }
}; 

// 使用 forEach2 方法 
const myArray = [1, 2, 3, 4, 5]; 

myArray.forEach2(function(element, index) {    
   console.log("Element:", element);    
   console.log("Index:", index);
});
```

在这个示例中，我们通过向 `Array.prototype` 添加一个名为 `forEach2` 的新方法，这个方法接受一个回调函数作为参数，然后在数组的每个元素上调用该回调函数，传递当前元素、索引和数组本身作为参数。

**注意:** 修改原型是一种常见的扩展 JavaScript 内置对象的方法，但也需要谨慎使用，因为它可能会影响到整个代码库。确保在适当的情况下使用，并清楚了解潜在的影响。













