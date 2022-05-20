# JS 数组中 filter/map/reduce 的用法?

```js
let arr = [1,9,2,8,3,7,4,6,5];
```

要求：删选出数组中小于5的所有元素，然后乘以2，再求和

for 循环写法

```js
let arr = [1,9,2,8,3,7,4,6,5];
let total = 0;
for(let i=0; i<arr.length; i++){
    if(arr[i]<5){
        total += arr[i]*2;
    }
}
console.log(total); // 20
```

filter/map/reduce

```js
let arr = [1,9,2,8,3,7,4,6,5];
let total = arr.filter(value => value < 5).map(value => value*2).reduce((prev,curv) => prev + curv,0)
console.log(total); // 20
```

## Array.prototype.reduce()

`reduce()` 方法对数组中的每个元素按序执行一个由您提供的 reducer 函数，每一次运行 reducer 会将先前元素的计算结果作为参数传入，最后将其结果汇总为单个返回值。

第一次执行回调函数时，不存在“上一次的计算结果”。如果需要回调函数从数组索引为0的元素开始执行，则需要传递初始值。否则，数组为0的元素将被作为初始值，迭代器将从第二个元素开始执行（索引为1而不是0）。

```js
const array1 = [2,4,6,8];
// 无初始值
const sum = array1.reduce((prev,curv)=>prev+curv);
console.log(sum);
// 有初始值
const sum2 = array1.reduce((prev,curv)=> {
    return prev+curv
},0)
```







参考：

1. [Array.prototype.reduce()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)































