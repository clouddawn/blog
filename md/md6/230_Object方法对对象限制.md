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

