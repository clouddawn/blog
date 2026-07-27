# typescript 装饰器的用法

* 装饰器是一种特殊类型的声明，它能够被附加到类声明，方法，访问符，属性和参数上。
* 装饰器使用 @expression 这种形式， expression 求值后必须为一个函数，它会在运行时被调用，被装饰的声明信息作为参数传入。
* 例如，有一个 @sealed 装饰器，我们会这样定义 sealed 函数

```ts
function sealed(target) {
    // do something with "target" ...
}
```

## 装饰器工厂

* 如果我们要定制一个修饰器如何应用到一个声明上，我们得写一个装饰器工厂函数。装饰器工厂就是一个简单的函数，它返回一个表达式，以供修饰器在运行时调用。
* 我们可以通过下面的方式来写一个修饰器工厂函数：

```ts
function color(value:string){ // 这是一个装饰器工厂
  return function (target){ //  这是装饰器
    // do something with "target" and "value"...
  }
}
```

## 装饰器组合

* 多个装饰器可以同时应用到一个声明上，就像下面的实例：

  * 书写在同一行上：

  ```ts
  @f @g x
  ```

  * 书写在多行上：

  ```ts
  @f
  @g
  x
  ```

* 当多个装饰器应用于一个声明上，他们的求值方式与复合函数相似。
* 在这个模型下，当复合 f 和 g 时，复合的结果等同于 f(g(x)) 。

* 同样的，在 TypeScript 里，当多个装饰器应用在一个声明上时会进行如下步骤的操作：
  * 由上至下依次对装饰器表达式求值。
  * 求值的结果会被当做函数，由下至上依次调用。

* 如果我么使用装饰器工厂的话，可以通过下面的例子来观察它们求值的顺序：

```ts
function f() {
    console.log("f(): evaluated");
    return function (target, propertyKey: string, descriptor: PropertyDescriptor) {
        console.log("f(): called");
    }
}

function g() {
    console.log("g(): evaluated");
    return function (target, propertyKey: string, descriptor: PropertyDescriptor) {
        console.log("g(): called");
    }
}

class C {
    @f()
    @g()
    method() {}
}
```

* 在控制台里会打印出如下结果：

```ts
f(): evaluated
g(): evaluated
g(): called
f(): called
```

## 装饰器求值

* 类中不同声明上的装饰器将按以下规定的顺序应用：
  * 参数装饰器，然后依次是方法装饰器，访问符装饰器，或属性装饰器应用到每个实例成员。
  * 参数装饰器，然后依次是方法装饰器，访问符装饰器，或属性装饰器应用到每个静态成员。
  * 参数装饰器应用到构造函数。
  * 类装饰器应用到类。

## 类装饰器

* 类装饰器在类声明之前被声明（紧靠着类声明）。
* 类装饰器应用于类构造函数，可以用来监视，修改或替换类定义。
* 类装饰器不能用在声明文件中（.d.ts），也不能用在任何外部上下文中（比如 declare 的类）。
* 类装饰器表达式会在运行时当做函数被调用，类的构造函数作为其唯一的参数。
* 如果类装饰器返回一个值，它会使用提供的构造函数来替换类的声明。

* **注意**，如果你要返回一个新的构造函数，你必须注意处理好原来的原型链。在运行时的装饰器调用逻辑中，不会为你做这些。
* 下面是使用类装饰器（@sealed）的例子，应用在 Greeter 类：

```ts
@sealed
class Greeter {
    greeting: string;
    constructor(message: string) {
        this.greeting = message;
    }
    greet() {
        return "Hello, " + this.greeting;
    }
}
```

* 我们可以这样定义 @sealed 装饰器

```ts
function sealed(constructor: Function) {
    Object.seal(constructor);
    Object.seal(constructor.prototype);
}
```

* 当 @sealed 被执行的时候，它将密封此类的构造函数和原型。



注释：

[1] https://www.tslang.cn/docs/handbook/decorators.html







































