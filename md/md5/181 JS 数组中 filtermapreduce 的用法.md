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