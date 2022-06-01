# class

class 声明创建一个基于原型继承的具有给定名称的新类。

## 示例

### 声明一个类

在下面的例子中，我们首先定义一个名为 Polygon 的类，然后继承它来创建一个名为 Square 的类。注意，构造函数中使用的 super() 只能在构造函数中使用，并且必须在使用 this 关键字前调用。

```js
class Polygon {
    constructor(height,width){
        this.name = 'Polygon';
        this.height = height;
        this.width = width;
    }
}
class Square extends Polygon {
    constructor(length){
        super(length,length);
        this.name = 'Square';
    }
}
console.log(new Square(9).height); // 9
console.log(new Square(9).name); // Square
```

