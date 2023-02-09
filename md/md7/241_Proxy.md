# Proxy

## 概述

Proxy 用于修改某些操作的默认行为，等同于在语言层面做出修改，所以属于一种“元编程”（meta programming），即对编程语言进行编程。

Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。Proxy 这个词的原意是代理，用在这里表示由它来“代理”某些操作，可以译为“代理器”。

```js
const obj = new Proxy({}, {
  get(target, propKey, receiver) {
    console.log(`getting ${propKey}!`);
    return Reflect.get(target, propKey, receiver);
  },
  set(target, propKey, value, receiver) {
    console.log(`setting ${propKey}!`);
    return Reflect.set(target, propKey, value, receiver);
  }
});
```

上面代码对一个空对象架设了一层拦截，重定义了属性的读取（`get`）和设置（`set`）行为。对设置了拦截行为的对象`obj`，去读写它的属性，就会得到下面的结果。

```js
obj.count = 1;
// setting count!

++obj.count
// getting count!
// setting count!
```

上面代码说明，Proxy 实际上重载（overload）了点运算符，即用自己的定义覆盖了语言的原始定义。

ES6 原生提供 Proxy 构造函数，用来生成 Proxy 实例。

```js
const proxy = new Proxy(target, handler);
```

Proxy 对象的所有用法，都是上面这种形式，不同的只是 handler 参数的写法。其中，`new Proxy()` 表示生成一个 Proxy 实例，target 参数表示所要拦截的目标对象，handler 参数也是一个对象，用来定制拦截行为。

下面是另一个拦截读取属性行为的例子。

```js
const proxy = new Proxy({},{
    get(target, propKey){
        return 35;
    }
});
console.log(proxy.time); // 35
console.log(proxy.name); // 35
console.log(proxy.title); // 35
```

上面代码中，作为构造函数，Proxy 接受两个参数。

* 第一个参数是所要代理的目标对象（上例是一个空对象），即如果没有 Proxy 的介入，操作原来要访问的就是这个对象；
* 第二个参数是一个配置对象，对于每一个被代理的操作，需要提供一个对应的处理函数，该函数将拦截对应的操作。
  * 比如，上面代码中，配置对象有一个 get 方法，用来拦截对目标对象属性的访问请求。
  * get 方法的两个参数分别是目标对象和所要访问的属性。可以看到，由于拦截函数总是返回 35，所以访问任何属性都得到 35。

注意，要使得 Proxy 起作用，必须针对 Proxy 实例（上例是 proxy 对象）进行操作，而不是针对目标对象（上例是空对象）进行操作。

如果 handler 没有设置任何拦截，那就等同于直接通向原对象

```js
const target = {};
const handler = {};
const proxy = new Proxy(target, handler);
proxy.a = "b";
console.log(target.a); // b
```

上面代码中，`handler`是一个空对象，没有任何拦截效果，访问`proxy`就等同于访问`target`。

一个技巧是将 Proxy 对象，设置到`object.proxy`属性，从而可以在`object`对象上调用。

```js
const object = {
    proxy: new Proxy(target, handler);
}
```

Proxy 实例也可以作为其他对象的原型对象。

```js
const proxy = new Proxy({},{
    get(target, propKey){
        return 35;
    }
})

let obj = Object.create(proxy);
console.log(obj.time); // 35
```

上面代码中，`proxy`对象是`obj`对象的原型，`obj`对象本身并没有`time`属性，所以根据原型链，会在`proxy`对象上读取该属性，导致被拦截。

同一个拦截器函数，可以设置拦截多个操作。

```js
const handler = {
    get(target, name){
        if(name === 'prototype'){
            return Object.prototype;
        }
        return `Hello ${name}`;
    },
    apply(target, thisBinding, args){
        return args[0];
    },
    construct(target, args){
        return {value: args[1]};
    }
}

const fproxy = new Proxy(function(x,y){
    return x + y;
}, handler);

fproxy(1,2); 
```





























