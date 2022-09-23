# 数组中的 find / findIndex 方法

## Array.prototype.find()

* `find()` 方法返回数组中满足提供的测试函数的第一个元素的值，否则返回 `undefined`

```js
const nums = [10,5,11,100,55];
const found = nums.find((item)=>{
  return item > 99
})
console.log(found);
```

## Array.prototype.findIndex()

* `findIndex()` 方法返回数组中满足提供的测试函数的第一个元素的索引。若没有找到对应元素则返回-1。

```js
const nums = [10,5,11,100,55];
const found = nums.findIndex((item)=>{
  return item > 99
})
console.log(found);
```

