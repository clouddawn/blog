# class 详解

## 认识 class 定义类

* 按照构造函数形式创建类，不仅仅和编写普通的函数过于相似，而且代码并不容易理解。
  * 在 ES6（ECMAScript2015）新的标准中使用了 class 关键字来直接定义类；
  * 但是类本质上依然是前面所讲的构造函数、原型链的语法糖而已；
* 那么，如何使用 class 来定义一个类呢？
  * 可以使用两种方式来声明类：类声明和类表达式；

```js
class Person {
    
}

const Student = class {
    
}
```

## 类和构造函数的异同

* 类的特性： 
  * 它和构造函数的特性其实是一致的；

```js
class Person {};

const p = new Person();

console.log(Person.prototype.constructor === Person); // true

console.log(p.__proto__ === Person.prototype); // true

console.log(typeof Person); // function
```

## 类的构造函数

* 如果我们希望在创建对象的时候给类传递一些参数，这个时候应该如何做呢？ 
  * 每个类都可以有一个自己的构造函数（方法），这个方法的名称是固定的`constructor`； 
  * 当我们通过 `new` 操作符，操作一个类的时候会调用这个类的构造函数`constructor`； 
  * 每个类只能有一个构造函数，如果包含多个构造函数，那么会抛出异常； 

* 当我们通过 `new` 关键字操作类的时候，会调用这个 `constructor` 函数，并且执行如下操作： 
  * 在内存中创建一个新的对象（空对象）； 
  * 这个对象内部的 `[[prototype]]` 属性会被赋值为该类的 `prototype` 属性； 
  * 构造函数内部的 `this`，会指向创建出来的新对象； 
  * 执行构造函数的内部代码（函数体代码）； 
  * 如果构造函数没有返回非空对象，则返回创建出来的新对象；

## 类的实例方法

* 在构造函数中我们定义的属性都是直接放到了this上，也就意味着它是放到了创建出来的新对象中：
  * 对于实例的方法，我们是希望放到原型上的，这样可以被多个实例来共享；
  * 这个时候我们可以直接在类中定义；

```js
class Person {
    constructor(name,age,height){
        this.name = name;
        this.age = age;
        this.height = height;
    }
    running(){
        console.log(this.name + '在跑步~');
    }
    eating(){
        console.log(this.name + ' 在吃饭~');
    }
}
```

## 类的访问器方法

```js
class Person {
    constructor(name){
        this._name = name;
    }
    set name(newName){
        console.log("调用了 name 的 setter 方法");
        this._name = newName;
    }
    get name(){
        console.log("调用了 name 的 getter 方法");
        return this._name;
    }
}
```

## 类的静态方法

* 静态方法通常用于定义直接使用类来执行的方法，不需要有类的实例，使用 static 关键字来定义：

```js
class Person {
    constructor(age){
        this.age = age;
    }
    static create(){
        return new Person(Math.floor(Math.random() * 100));
    }
}
```

## ES6 类的继承 - extends

```js
class Person {
    
}

class Student extends Person {
    
}
```

## super 关键字

* 上面的代码中使用了一个 super 关键字，这个 super 关键字有不同的使用方式： 
  * 注意：在子（派生）类的构造函数中使用 this 或者返回默认对象之前，必须先通过 super 调用父类的构造函数！ 
  * super 的使用位置有三个：子类的构造函数、实例方法、静态方法；

```js
// 调用 父对象/父类 的构造函数
super([arguments]);

// 调用 父对象/父类 上的方法
super.functionOnParent([arguments]);
```

## 继承内置类

* 我们也可以让我们的类继承自内置类，比如Array：

```js
class NewArray extends Array {
    lastItem(){
        return this[this.length - 1];
    }
}
const array = new NewArray(10,20,30);
console.log(array.lastItem());
```

## 类的混入 mixin

* JavaScript 的类只支持单继承：也就是只能有一个父类
  * 那么在开发中我们我们需要在一个类中添加更多相似的功能时，应该如何来做呢？ 
  * 这个时候我们可以使用混入（mixin）；

```js
function mixinRunner(BaseClass){
    return class extends BaseClass {
        running(){
            console.log("running~");
        }
    }
}

function mixinEater(BaseClass){
    return class extends BaseClass {
        eating(){
            console.log("eating~");
        }
    }
}

class Person {
    
}

class NewPerson extends mixinEater(mixinRunner(Person)){
    
}

const np = new NewPerson();
np.eating();
np.running();
```

## JavaScript 中的多态

* 面向对象的三大特性：封装、继承、多态。
  * 前面两个我们都已经详细解析过了，接下来我们讨论一下JavaScript的多态。
* JavaScript有多态吗？
  * 维基百科对多态的定义：多态（英语：polymorphism）指为不同数据类型的实体提供统一的接口，或使用一个单一的符号来表示多个不同的类型。
  * 非常的抽象，个人的总结：不同的数据类型进行同一个操作，表现出不同的行为，就是多态的体现。
* 那么从上面的定义来看，JavaScript 是一定存在多态的。

```js
function sum(a,b){
    console.log(a + b);
}

sum(10, 20);
sum("abc", "cba");
```





































