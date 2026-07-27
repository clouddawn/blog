# JS 函数的 this 指向

## 为什么需要 this ？

* 在常见的编程语言中，几乎都有 this 这个关键字（Objective-C 中使用的是 self），但是 JavaScript 中的 this 和常见的面向对象语言中的this不太一样： 

  * 常见面向对象的编程语言中，比如 Java、C++、Swift、Dart 等等一系列语言中，this 通常只会出现在类的方法中。 

  * 也就是你需要有一个类，类中的方法（特别是实例方法）中，this 代表的是当前调用对象。 

  * 但是 JavaScript 中的 this 更加灵活，无论是它出现的位置还是它代表的含义。 

* 我们来看一下编写一个 obj 的对象，有 this 和没有 this 的区别

```js
// 有this
var obj = {
    name:'孙悟空',
    running:function(){
        console.log(obj.name + " running");
    },
    eating:function(){
        console.log(obj.name + " eating");
    },
    studying:function(){
        console.log(obj.name + " studying");
    }
}
// 无this
var obj = {
    name:'孙悟空',
    running:function(){
        console.log(this.name + " running");
    },
    eating:function(){
        console.log(this.name + " eating");
    },
    studying:function(){
        console.log(this.name + " studying");
    }
}
```

## this 指向什么呢？

* 我们先说一个最简单的，this 在全局作用于下指向什么？ 
  * 这个问题非常容易回答，在浏览器中测试就是指向 window 

* 但是，开发中很少直接在全局作用域下去使用 this，通常都是在**函数中使用**。 
  * 所有的函数在被调用时，都会创建一个执行上下文： 
  * 这个上下文中记录着函数的调用栈、AO 对象等； 
  * this也是其中的一条记录；



## this 到底指向什么呢？

* 我们先来看一个让人困惑的问题： 
  * 定义一个函数，我们采用三种不同的方式对它进行调用，它产生了三种不同的结果

```js
function foo(){
    console.log(this);
}
// 直接调用
foo(); // window
// 将 foo 放到一个对象中，再调用
var obj = {
    name:"孙悟空",
    foo:foo
}
obj.foo() // obj 对象
// 通过 call/apply 调用
foo.call("abc"); // String {'abc'}
```

* 这个的案例可以给我们什么样的启示呢？ 
  * 1.函数在调用时，JavaScript 会默认给 this 绑定一个值； 
  * 2.this 的绑定和定义的位置（编写的位置）没有关系； 
  * 3.this 的绑定和调用方式以及调用的位置有关系； 
  * 4.this 是在运行时被绑定的； 

* 那么 this 到底是怎么样的绑定规则呢？
  * 绑定一：默认绑定； 
  * 绑定二：隐式绑定； 
  * 绑定三：显式绑定； 
  * 绑定四：new绑定；

## 规则一：默认绑定

* 什么情况下使用默认绑定呢？独立函数调用。 
  * 独立的函数调用我们可以理解成函数没有被绑定到某个对象上进行调用；

```js
function foo(func){
    func();
}
var obj = {
    name:"孙悟空",
    bar(){
        console.log(this);
    }
}
foo(obj.bar);
```

## 规则二：隐式绑定

* 另外一种比较常见的调用方式是通过某个对象进行调用的：
  * 也就是它的调用位置中，是通过某个对象发起的函数调用。

```js
function foo(){
    console.log(this);
}

var obj1 = {
    name:"obj1",
    foo:foo
}

var obj2 = {
    name:"obj2",
    obj1:obj1
}

obj2.obj1.foo();
```

### 规则三：显式绑定

* 隐式绑定有一个前提条件： 
  * 必须在调用的对象内部有一个对函数的引用（比如一个属性）； 
  * 如果没有这样的引用，在进行调用时，会报找不到该函数的错误； 
  * 正是通过这个引用，间接的将 this 绑定到了这个对象上； 

* 如果我们不希望在 **对象内部** 包含这个函数的引用，同时又希望在这个对象上进行强制调用，该怎么做呢？ 
  * JavaScript 所有的函数都可以使用 call 和 apply 方法（这个和 Prototype 有关）。 
    * 它们两个第一个参数是相同的，后面的参数，apply 为数组，call 为参数列表； 
  * 这两个函数的第一个参数都要求是一个对象，这个对象的作用是什么呢？就是给this准备的。 
  * 在调用这个函数时，会将 this 绑定到这个传入的对象上。 

* 因为上面的过程，我们明确的绑定了 this 指向的对象，所以称之为 **显式绑定**。

## call、apply、bind

* 通过 call 或者 apply 绑定 this 对象

  * 显式绑定后，this 就会明确的指向绑定的对象

  ```js
  function foo(){
      console.log(this);
  }
  foo.call(window); // window
  foo.call({name:"孙悟空"}) 
  foo.call(123)
  ```

* 如果我们希望一个函数总是显式的绑定到一个对象上，可以怎么做呢？

  ```js
  function foo(){
      console.log(this);
  }
  var obj = {
      name:"孙悟空"
  }
  var bar = foo.bind(obj);
  bar(); // obj对象
  ```

## 内置函数的绑定思考

* 有些时候，我们会调用一些 JavaScript 的内置函数，或者一些第三方库中的内置函数。
  * 这些内置函数会要求我们传入另外一个函数；
  * 我们自己并不会显式的调用这些函数，JavaScript 内部或者第三方库内部会帮助我们执行；
  * 这些函数中的 this 又是如何绑定的呢？

* **setTimeout、数组的 forEach、div 的点击**

  ```js
  setTimeout(function(){
      console.log(this) // window
  },1000)
  ```

  .

  ```js
  var names = ["大张伟","李诞","谢楠","陈鲁豫"];
  var obj = {
      name:"孟川"
  }
  names.forEach(function(item){
      console.log(this) // obj
  },obj); 
  ```

  .

  ```js
  var box = document.querySelector(".box");
  box.onclick = function(){
      console.log(this === box); // true
  }
  ```

## new 绑定

* JavaScript 中的函数可以当做一个类的构造函数来使用，也就是使用 new 关键字。
* 使用 new 关键字来调用函数，会执行如下的操作：
  * 创建一个全新的对象；
  * 这个新对象会被执行 prototype 连接；
  * 这个新对象会绑定到函数调用的 this 上；
  * 如果函数没有返回其他对象，表达式会返回这个新对象；

```js
// 我们通过一个 new 关键字调用一个函数时（构造器），这个时候 this 是在调用这个构造器时创建出来的对象
// this = 创建出来的对象
// 这个绑定过程就是 new 绑定

function Person(name,age){
    this.name = name;
    this.age = age;
}

var p1 = new Person("王冰冰",33);
console.log(p1.name, p1.age);

var p2 = new Person("刘亦菲",36);
console.log(p2.name, p2.age);
```

## 规则优先级

#### 1. 默认规则的优先级最低

#### 2. 显式绑定优先级高于隐式绑定

```js
var person = {
  name:"孟川",
  win:function(){
    console.log('我晋级了',this)
  }
};
person.win.call('call');
person.win.apply('apply');
var newPerson = person.win.bind('bind');
newPerson();
```

#### 3. new 绑定优先级高于隐式绑定

```js
var person = {
  name:"孟川",
  win:function(){
    console.log('我晋级了',this)
  }
};
new person.win()
```

#### 4. new 绑定优先级高于 bind

* new 绑定和 call、apply 是不允许同时使用的，所以不存在谁的优先级更高
* new 绑定可以和 bind 一起使用，new 绑定优先级更高

```js
function win(){
  console.log('孟川晋级了',this);
};
var newWin = win.bind('bind');
new newWin();
```

## this 规则之外 - 忽略显式绑定

* 如果在显式绑定中，我们传入一个 null 或者 nudefined，那么这个显式绑定会被忽略，使用默认规则：

  ```js
  function win(){
    console.log('孟川晋级了',this);
  };
  var newWin = win.bind(null);
  newWin();
  win.call(undefined);
  win.apply(null);
  ```

## this 规则之外 - 间接函数引用

* 另外一种情况，创建一个函数的**间接引用**，这种情况使用默认绑定规则。

  * 赋值（obj2.foo = obj2.foo）的结果是 foo 函数；
  * foo 函数被直接调用，那么是默认绑定；

  ```js
  function foo(){
      console.log(this);
  }
  var obj1 = {
      name:"obj1",
      foo:foo
  }
  var obj2 = {
      name:"obj2"
  }
  obj1.foo(); // obj1
  (obj2.foo = obj1.foo)(); // window
  ```

## 面试题

```js
var name = "window";
var person = {
  name:"person",
  sayName:function(){
    console.log(this.name);
  }
}
function sayName(){
  var sss = person.sayName;
  sss();
  person.sayName();
  (person.sayName)(); 
  (b = person.sayName)(); 
}
sayName();
```

.

```js
var name = 'window';

var person1 = {
  name:"person1",
  foo1(){
    console.log(this.name);
  },
  foo2:()=> console.log(this.name),
  foo3(){
    return function(){
  console.log(this.name)
    }
  },
  foo4(){
    return ()=>{
      console.log(this.name);
    }
  }
}

var person2 = {
  name:"person2"
}

person1.foo1(); 

 person1.foo1.call(person2); 

person1.foo2(); 
person1.foo2.call(person2); 

person1.foo3()();
person1.foo3.call(person2)(); 
person1.foo3().call(person2); 

person1.foo4()(); 
person1.foo4.call(person2)(); 
person1.foo4().call(person2); 
```

.

```js
var name = 'window';

function Person(name){
  this.name = name;
  this.foo1 = function(){
    console.log(this.name);
  },
  this.foo2 = () => console.log(this.name),
  this.foo3 = function(){
    return function(){
      console.log(this.name);
    }
  },
  this.foo4 = function(){
    return ()=>{
      console.log(this.name);
    }
  }
}

var person1 = new Person('person1');
var person2 = new Person('person2');

person1.foo1();
person1.foo1.call(person2);

person1.foo2();
person1.foo2.call(person2);

person1.foo3()(); 
person1.foo3.call(person2)(); 
person1.foo3().call(person2); 

person1.foo4()(); 
person1.foo4.call(person2)(); 
person1.foo4().call(person2); 
```

.

```js
var name = 'window';

function Person(name){
  this.name = name;
  this.obj = {
    name:"obj",
    foo1: function(){
      return function(){
        console.log(this.name);
      }
    },
    foo2:function(){
      return () => {
        console.log(this.name);
      }
    }
  }
}  

var person1 = new Person('person1');
var person2 = new Person('person2');

person1.obj.foo1()(); 
person1.obj.foo1.call(person2)(); 
person1.obj.foo1().call(person2);  

person1.obj.foo2()(); 
person1.obj.foo2.call(person2)();
person1.obj.foo2().call(person2); 
```

































