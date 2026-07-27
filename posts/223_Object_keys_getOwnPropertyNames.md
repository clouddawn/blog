# Object.keys 和 Object.getOwnPropertyNames 的区别

## Object.keys

* `Object.keys()` 方法会返回一个由给定对象的自身**可枚举属性**组成的数组，数组中属性名的排列顺序和正常循环遍历该对象时返回的顺序一致。

## Object.getOwnPropertyNames

* `Object.getOwnPropertyNames()` 方法返回一个由指定对象的所有自身属性的属性名（**包括不可枚举属性**）组成的数组。

```js
const obj = {
  name: "孙悟空"
};

Object.defineProperties(obj, {
  age: {
    value: 500,
    enumerable: false,
  },
  height: {
    enumerable: true,
    get() {
      return "俺老孙想多高就多高";
    }
  }
});
console.log(Object.keys(obj)); // ['name', 'height']
console.log(Object.getOwnPropertyNames(obj)); // ['name', 'age', 'height']
```