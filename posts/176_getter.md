# getter

**get**语法将对象属性绑定到查询该属性时将被调用的函数。

## 语法

```js
{get prop() { ... } }

{get [expression]() { ... } }
```

### 参数

- `prop`

  要绑定到给定函数的属性名。

- `expression`

  从 ECMAScript 2015 开始，还可以使用一个计算属性名的表达式绑定到给定的函数。

## 描述

有时需要允许访问返回动态计算值的属性，或者你可能需要反映内部变量的状态，而不需要使用显式方法调用。在 JavaScript 中，可以使用 *getter* 来实现。

尽管可以结合使用 getter 和 setter 来创建一个伪属性，但是不可能同时将一个 getter 绑定到一个属性并且该属性实际上具有一个值。

使用`get`语法时应注意以下问题：

- 可以使用数值或字符串作为标识；
- 必须不带参数
- 它不能与另一个 `get `或具有相同属性的数据条目同时出现在一个对象字面量中（不允许使用 `{ get x() { }, get x() { } }` 和 `{ x: ..., get x() { } }`）。

## 实例一

```js
const obj = {
  log: ['a', 'b', 'c'],
  get latest() {
    if (this.log.length === 0) {
      return undefined;
    }
    return this.log[this.log.length - 1];
  }
};

console.log(obj.latest);
// expected output: "c"
```

### 使用`delete`操作符删除 getter

```js
delete obj.latest;
```

-

```js
const obj = {
    log: ['a', 'b', 'c'],
    get latest() {
      if (this.log.length === 0) {
        return undefined;
      }
      return this.log[this.log.length - 1];
    }
  };

console.log(obj.latest) // 'c'

delete obj.latest;

console.log(obj.latest) // undefined
```

### 使用`defineProperty`在现有对象上定义 getter

- 要随时将 getter 添加到现有对象，使用 [`Object.defineProperty()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty).

```js
var o = { a:0 }

Object.defineProperty(o, "b", { get: function () { return this.a + 1; } });

console.log(o.b) // 1

Object.defineProperty(o,'c',{
    get(){
        return 'c3'
    }
})

console.log(o.c) //'c3'
```

### 使用计算出的属性名

```js
var expr = 'foo';

var obj = {
  get [expr]() { return 'bar'; }
};

console.log(obj.foo); // "bar"
```





