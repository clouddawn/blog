# Proxy-Reflect

## 监听对象的操作

* 需求：监听对象中属性被设置、获取的过程

  * 可以通过属性描述符中的存储属性描述符来做到；

  ```js
  const data = {
    title: "天幕红尘",
    author: "豆豆"
  };
  
  const render = {
    title() {
      document.querySelector("#one").innerHTML = `<h1>${data.title}</h1>`;
    },
    author() {
      document.querySelector("#two").innerHTML = `<h1>${data.author}</h1>`;
    }
  };
  
  Object.values(render).forEach(fun => fun());
  
  Object.keys(data).forEach(key => {
    let value = data[key];
    Object.defineProperty(data, key, {
      get() {
        return value;
      },
      set(newValue) {
        value = newValue;
        render[key]();
      }
    });
  });
  
  setTimeout(() => {
    data.title = "遥远的救世主";
    data.author = "还是豆豆";
    delete data.title;
  }, 3000);
  ```

* 但是这样做有什么缺点呢？

  * 首先，`Object.defineProperty` 设计的初衷，不是为了去监听一个对象中所有的属性的。
    * 我们在定义某些属性的时候，初衷其实是定义普通的属性，但是后面我们强行将它变成了数据属性描述符。
  * 其次，如果我们想监听更加丰富的操作，比如新增属性、删除属性，那么 `Object.defineProperty` 是无能为力的。

## Proxy 基本使用

* 在 ES6 中，新增了一个 Proxy 类，这个类从名字就可以看出来，是用于帮助我们创建一个代理的：

  * 也就是说，如果我们希望监听一个对象的相关操作，那么我们可以先创建一个代理对象（Proxy对象）；
  * 之后对该对象的所有操作，都通过代理对象来完成，代理对象可以监听我们想要对原对象进行哪些操作；

* 我们可以将上面的案例用 Proxy 来实现一次：

  * 首先，我们需要 new Proxy 对象，并且传入需要侦听的对象以及一个处理对象，可以称之为 handler；

  ```js
  const p = new Proxy(target, handler)
  ```

  * 其次，我们之后的操作都是直接对 Proxy 的操作，而不是原有的对象，因为我们需要在 handler 里面进行侦听；

## Proxy 的 set 和 get 捕获器

* 如果我们想要侦听某些具体的操作，那么就可以在 handler 中添加对应的捕捉器（Trap）：
* set 和 get 分别对应的是函数类型；
  * set 函数有四个参数：
    * target：目标对象（侦听的对象）；
    * property：将被设置的属性 key；
    * value：新属性值；
    * receiver：调用的代理对象；
  * get 函数有三个参数：
    * target：目标对象（侦听的对象）；
    * property：被获取的属性key；
    * receiver：调用的代理对象；

```js
const dataProxy = new Proxy(data, {
  get(target, key) {
    return target[key];
  },
  set(target, key, newValue) {
    target[key] = newValue;
    render[key]();
  },
  deleteProperty(target, propKey) {
    console.log(`data.${propKey}被刪了`);
  }
});
```

### has()

* `has()` 方法用来拦截 `HasProperty` 操作，即判断对象是否具有某个属性时，这个方法会生效。典型的操作就是in运算符。

* `has()` 方法可以接受两个参数，分别是目标对象、需查询的属性名。

```js
const p = {
  name: "孙悟空"
};

const pProxy = new Proxy(p, {
  has(target, proxyKey) {
    const result = proxyKey in target;
    if (result) {
      console.log("在呢，在呢");
    } else {
      console.log("没有，滚");
    }
    return result;
  }
});

console.log("name" in pProxy);
// 在呢，在呢
// true
console.log("age" in pProxy);
// 没有，滚
// false
```

### deleteProperty()

* `deleteProperty` 方法用于拦截 `delete` 操作。

```js
const p = {
  name: "孙悟空"
};

const pProxy = new Proxy(p, {
  deleteProperty(target, proxyKey) {
    delete target[proxyKey];
    console.log("删我干啥");
    return true;
  }
});

delete pProxy.name;
console.log(p.name);
// 删我干啥
// undefined
```

## Proxy 所有捕获器

* `handler.getPrototypeOf()`
  * `Object.getPrototypeOf ` 方法的捕捉器。
* `handler.setPrototypeOf()`
  * `Object.setPrototypeOf` 方法的捕捉器。
* `handler.isExtensible()`
  * `Object.isExtensible` 方法的捕捉器。
* `handler.preventExtensions()`
  * `Object.preventExtensions` 方法的捕捉器。
* `handler.getOwnPropertyDescriptor()`
  * `Object.getOwnPropertyDescriptor` 方法的捕捉器。
* `handler.defineProperty()`
  * `Object.defineProperty` 方法的捕捉器。
* `handler.ownKeys()`
  * `Object.getOwnPropertyNames` 方法和
    `Object.getOwnPropertySymbols` 方法的捕捉器。
* `handler.has()`
  * in 操作符的捕捉器。
* `handler.get()`
  * 属性读取操作的捕捉器。
* `handler.set()`
  * 属性设置操作的捕捉器。
* `handler.deleteProperty()`
  * delete 操作符的捕捉器。
* `handler.apply()`
  * 函数调用操作的捕捉器。
* `handler.construct()`
  * new 操作符的捕捉器。

## Proxy 的 construct 和 apply

* 它们是应用于函数对象的

```js
function getName(name1, name2) {
  console.log(this);
  console.log(name1, name2);
}

const getNameProxy = new Proxy(getName, {
  apply(target, thisArg, argArray) {
    return target.apply(thisArg, argArray);
  }
});
getNameProxy.apply("崔永元", ["刘德华", "梁朝伟"]);


class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

const PersonProxy = new Proxy(Person, {
  construct(target, argArray, newTarget) {
    console.log("new new new");
    return new target(...argArray);
  }
});

console.log(new PersonProxy("飞飞", "88"));
```

## Reflect 的作用

* Reflect 也是 ES6 新增的一个 API ，它是一个对象，字面的意思是反射。
* 那么这个 Reflect 有什么用呢？
  * 它主要提供了很多操作 JavaScript 对象的方法，有点像 Object 中操作对象的方法；
  * 比如 `Reflect.getPrototypeOf(target)` 类似于 ` Object.getPrototypeOf()`；
  * 比如 `Reflect.defineProperty(target, propertyKey, attributes)` 类似于 `Object.defineProperty()` ；
* 既然有 Object 可以做这些操作，为什么还需要有 Reflect 这样的新增对象呢？
  * 因为在早期的 ECMA 规范中没有考虑到这种对**对象本身**的操作如何设计会更加规范，所以将这些 API 放到了 Object 上面；
  * 但是 Object 作为一个构造函数，这些操作实际上放到它身上并不合适；
  * 所以在 ES6 中新增了 Reflect，让这些操作都集中到了 Reflect 对象上；

## Reflect 的常见方法

* 它和 Proxy 是一一对应的，也是13个：
* `Reflect.getPrototypeOf(target)`
  * 类似于 `Object.getPrototypeOf()`。
* `Reflect.setPrototypeOf(target, prototype)`
* 设置对象原型的函数. 返回一个 `Boolean`， 如果更新成功，则返回 `true`。
* `Reflect.isExtensible(target)`
  * 类似于 `Object.isExtensible()`
* `Reflect.preventExtensions(target)`
  * 类似于 `Object.preventExtensions()`。返回一个`Boolean`。
* `Reflect.getOwnPropertyDescriptor(target, propertyKey)`
  * 类似于 `Object.getOwnPropertyDescriptor()`。如果对象中存在该属性，则返回对应的属性描述符, 否则返回 undefined.
* `Reflect.defineProperty(target, propertyKey, attributes)`
  * 和 `Object.defineProperty()` 类似。如果设置成功就会返回 `true`。
* `Reflect.ownKeys(target)`
  * 返回一个包含所有自身属性（不包含继承属性）的数组。(类似于 `Object.keys()`, 但不会受 enumerable 影响).
* `Reflect.has(target, propertyKey)`
  * 判断一个对象是否存在某个属性，和 **in 运算符** 的功能完全相同。
* `Reflect.get(target, propertyKey[, receiver])`
  * 获取对象身上某个属性的值，类似于 `target[name]`。
* `Reflect.set(target, propertyKey, value[, receiver])`
  * 将值分配给属性的函数。返回一个 Boolean，如果更新成功，则返回 true。
* `Reflect.deleteProperty(target, propertyKey)`
  * 作为函数的 delete 操作符，相当于执行 `delete target[name]`。
* `Reflect.apply(target, thisArgument, argumentsList)`
  * 对一个函数进行调用操作，同时可以传入一个数组作为调用参数。和 `Function.prototype.apply()` 功能类似。
* `Reflect.construct(target, argumentsList[, newTarget])`
  * 对构造函数进行 new 操作，相当于执行` new target(...args)`。

## Reflect的使用

* 将之前 Proxy 案例中对原对象的操作，都修改为 Reflect 来操作：

```js
function getName(name1, name2) {
  console.log(this);
  console.log(name1, name2);
}

const getNameProxy = new Proxy(getName, {
  apply(target, thisArg, argArray) {
    return Reflect.apply(target, thisArg, argArray);
  }
});
getNameProxy.apply("崔永元", ["刘德华", "梁朝伟"]);


class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

const PersonProxy = new Proxy(Person, {
  construct(target, argArray, newTarget) {
    console.log("new new new");
    return Reflect.construct(target, argArray);
  }
});

console.log(new PersonProxy("飞飞", "88"));
```

## Receiver 的作用

* 如果源对象（obj）有 setter、getter 的访问器属性，那么可以通过 receiver 来改变里面的 this；

```js
const obj = {
  _name: "安欣",
  get name() {
    return this._name;
  },
  set name(newValue) {
    this._name = newValue;
  }
};

const objProxy = new Proxy(obj, {
  get(target, p, receiver) {
    console.log("get-----------------");
    return Reflect.get(target, p, receiver);
  },
  set(target, p, value, receiver) {
    console.log("set----------------");
    Reflect.set(target, p, value, receiver);
  }
});

objProxy.name = "高启强";
console.log(objProxy.name);
```

## Reflect 的 construct

```js
function Student(name, age) {
  this.name = name;
  this.age = age;
}

function Teacher() {

}

const stu = Reflect.construct(Student, ["why", 18], Teacher);
console.log(stu.__proto__ === Teacher.prototype);
```

























