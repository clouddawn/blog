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

## 原型

在 JavaScript 中，**原型（Prototype）** 是对象之间共享属性和方法的**核心继承机制**。你可以把它理解为**“对象蓝本的链接”**。

为了让你彻底搞懂，我把原型拆解为三个层次，并结合你刚才封装的 `forEach` 来解释：

### 1. 核心概念：`prototype`（函数特有的）

**只有函数（包括构造函数和普通函数）才拥有 prototype 属性。**
这个属性的值是一个普通对象，它的作用就是：**当该函数作为构造函数（配合 new）使用时，生成的所有实例对象都会自动继承这个 prototype 上的属性和方法。**

> **结合你的代码**：`Array` 是一个内置构造函数，`Array.prototype` 就是所有数组实例（如 `[1,2,3]`）的“公共祖先”。你把 `forEach2` 挂载到 `Array.prototype` 上，所以每一个数组都能通过原型链找到并调用它。

------

### 2. 实例链接：`__proto__`（对象特有的）

**每个对象（除了 null）都有一个内部属性 [[Prototype]]（在浏览器中通常表现为 __proto__），它指向创建该对象的构造函数的 prototype。**

> **例子验证**：
>
> ```javascript
> const myArray = [1, 2, 3];
> // 实例的 __proto__ 指向构造函数的 prototype
> console.log(myArray.__proto__ === Array.prototype); // true
> 
> // 因为你在 Array.prototype 上加了 forEach2
> console.log(myArray.forEach2); // 能取到 function，这就是原型链在起作用
> ```

------

### 3. 原型链（查找机制）

当你试图访问一个对象的属性或方法时，JS 引擎会这样执行：

1. 先查对象自身有没有（比如 `myArray` 自身的 `length` 属性）；
2. 如果没有，就顺着 `__proto__` 往上找，去找 `Array.prototype`；
3. 如果还没有，就继续往上找 `Array.prototype.__proto__`（即 `Object.prototype`）；
4. 直到找到 `null` 为止，如果还没找到就返回 `undefined`。

这就是你封装的 `forEach2` 能被 `myArray.forEach2(...)` 调用的底层原理——**方法本身并不在数组实例上，而在它们的公共原型上**。

------

### 4. 一个直观的自定义类比

为了帮你深刻记忆，看下面这个手动模拟：

```javascript
// 1. 定义一个“人”的构造函数
function Person(name) {
  this.name = name;
}

// 2. 在 Person.prototype 上挂载公共方法（相当于你的 Array.prototype.forEach2）
Person.prototype.sayHello = function() {
  console.log('Hello, ' + this.name);
};

// 3. 创建实例
const p1 = new Person('Tom');
const p2 = new Person('Jerry');

// 4. 调用
p1.sayHello(); // Hello, Tom （p1 自身没有 sayHello，是通过原型链找到的）
console.log(p1.sayHello === p2.sayHello); // true（内存中只存了一份，节省内存）
```

------

### 5. 特别提醒（你之前的代码中涉及的重要细节）

- **原型是可以修改的**：你向 `Array.prototype` 添加方法，所有数组立即生效（包括已经创建好的数组），非常灵活。
- **缺点**：如果所有开发者都随意改原型，容易造成“命名冲突”和代码混乱，所以通常建议用 `Object.defineProperty` 设为不可枚举，或使用独立函数代替。

------

### 一句话总结

> **原型就是 JS 用来实现“继承”的共享机制**：构造函数提供 `prototype` 作为“模具”，实例通过 `__proto__` 连接这个模具，从而共享上面的所有功能。你封装的 `forEach2`，正是利用了“模具”的共享特性，让所有数组都有了遍历能力。



## class 与 原型

**class 是“语法糖”，它的底层完全基于“原型”**。两者是“设计图纸”与“施工规范”的关系，本质上是同一套机制。

为了让你看得通透，我分三个维度来拆解：

### 1. 本质映射（核心对照表）

当你写一个 `class` 时，JavaScript 引擎在底层会把它翻译成构造函数 + 原型操作：

| `class` 语法（表层）         | 原型/构造函数（底层）                    | 说明                                   |
| :--------------------------- | :--------------------------------------- | :------------------------------------- |
| `class Person {}`            | `function Person() {}`                   | `class` 其实就是创建了一个**构造函数** |
| `constructor()` 里面的逻辑   | 函数体内部的代码                         | 初始化实例属性                         |
| `sayHi() {}`（类内部的方法） | `Person.prototype.sayHi = function() {}` | **所有实例共享**该方法，挂在原型上     |
| `static eat()`（静态方法）   | `Person.eat = function() {}`             | 直接挂在类（构造函数）上，实例拿不到   |

**验证代码：**

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
  sayHi() {
    console.log('Hi ' + this.name);
  }
}

// 等价于以前的原型写法：
function Person(name) {
  this.name = name;
}
Person.prototype.sayHi = function() {
  console.log('Hi ' + this.name);
};

// 验证底层原理：
console.log(typeof Person); // "function"（class 本质就是函数）
const p = new Person('Tom');
console.log(p.__proto__ === Person.prototype); // true（实例仍然通过原型链链接）
```

------

### 2. 继承的关联（`extends` 就是在连原型链）

当你使用 `class Child extends Parent` 时，它底层做的事情，就是你之前理解的原型链的“串联”：

- `Child.prototype.__proto__ === Parent.prototype`（让子类的原型，继承父类的原型）
- `Child.__proto__ === Parent`（让子类的构造函数，继承父类的构造函数，用于静态方法继承）

**用原型手工模拟继承：**

```javascript
// class 写法
class Animal { move() {} }
class Dog extends Animal { bark() {} }

// 底层原型等价于：
Object.setPrototypeOf(Dog.prototype, Animal.prototype); // 实例方法继承
Object.setPrototypeOf(Dog, Animal); // 静态方法继承
```

------

### 3. 与你的 `forEach2` 封装有什么直接关系？

你之前写的：

```javascript
Array.prototype.forEach2 = function(callback) { ... }
```

如果现代 JS 允许用 `class` 重新定义数组，它本质上会写成：

```javascript
class Array {
  constructor() { ... }
  forEach2(callback) { ... } // 等同于 Array.prototype.forEach2
}
```

**得出结论**：你之前在原型上添加 `forEach2`，其实就是手动给 `Array` 这个“类”添加了一个实例方法。`class` 语法帮你自动把方法挂到 `prototype` 上，并让它**默认不可枚举**（而直接用 `Array.prototype.forEach2 =` 默认是可枚举的，这也是为什么官方推荐用 `Object.defineProperty` 来修饰）。

------

### 4. 两者共存的“核心差异”（避坑指南）

虽然 `class` 底层是原型，但它们有细微差别，你需要知道：

- **提升（Hoisting）**：`function` 声明会提升，但 `class` 声明**不会**（必须先定义后使用）。
- **严格模式**：`class` 内部代码自动处于 `"use strict"` 下。
- **原型方法的枚举性**：`class` 里定义的方法不可枚举（`enumerable: false`），这刚好避免了用 `for...in` 遍历对象时跑出奇怪的方法（这一点比你手动挂载 `forEach2` 更安全）。

------

### 一句话灵魂总结

> **class 是原型机制的“高级封装”**。你以前写 `构造函数.prototype.xxx = ...` 是“手动挡”，现在写 `class { xxx() {} }` 是“自动挡”，但底层的引擎盖下，转动的依然是 **原型链** 这根链条。









