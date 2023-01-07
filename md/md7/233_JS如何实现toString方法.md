# JS 如何实现 Number.prototype.toString 方法？

## 预期效果

```js
const num1 = 123;
console.log(num1,typeof num1); // 123 'number'
const str_num1 = num1.toString();
console.log(str_num1,typeof str_num1); // 123 string
```

## 实现方式

```js
Number.prototype._ToString = function(){
    return this + "";
};
const num1 = 123;
console.log(num1,typeof num1); // 123 'number'
const str_num1 = num1._ToString();
console.log(str_num1,typeof str_num1); // 123 string
```

