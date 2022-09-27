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
  * 绑定三：显示绑定； 
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
    
}
```

































