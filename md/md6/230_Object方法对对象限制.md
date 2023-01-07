# Object 方法对对象限制

## Object.preventExtensions()

* 让一个对象变的不可扩展，也就是永远不能再添加新的属性。

```js
const obj = {
  name: "王冰冰",
  age: 18,
};
Object.preventExtensions(obj);
obj.address = "吉林";
console.log(obj); // {name: '王冰冰', age: 18}
```

## Object.seal()

* 封闭一个对象，阻止添加新属性并将现有属性标记为不可配置，当前属性的值只要是可写的就可以改变。

```js
const obj = {
  name: "王冰冰",
  age: 18,
};

Object.defineProperty(obj, "address", {
  enumerable: true,
  configurable: true,
  writable: true,
  value: "吉林"
});

Object.seal(obj);

delete obj.age;
obj.slogan = "永远十八岁";
console.log(obj); // {name: '王冰冰', age: 18, address: '吉林'}
```

## Object.freeze()

* **Object.freeze()** 方法可以**冻结**一个对象。
* 一个被冻结的对象再也不能被修改；
* 冻结了一个对象则不能向这个对象添加新的属性，不能删除已有属性，不能修改该对象已有属性的可枚举性、可配置性、可写性，以及不能修改已有属性的值。
* 此外，冻结一个对象后该对象的原型也不能被修改。
* `freeze()` 返回和传入的参数相同的对象。

```js
const obj = {
  name: "王冰冰",
  age: 18,
};
Object.defineProperty(obj, "address", {
  enumerable: true,
  configurable: true,
  writable: true,
  value: "吉林"
});
Object.freeze(obj);

delete obj.age;
obj.slogan = "永远十八岁";
console.log(obj); // {name: '王冰冰', age: 18, address: '吉林'}
```

## 小结

* 禁止对象扩展新属性：`preventExtensions `
  * 给一个对象添加新的属性会失败（在严格模式下会报错）； 

* 密封对象，不允许配置和删除属性：*seal* 
  * 实际是调用*preventExtensions* 
  * 并且将现有属性的*configurable:false* 

* 冻结对象，不允许修改现有属性： *freeze* 
  * 实际上是调用*seal* 
  * 并且将现有属性的 *writable: false*





































