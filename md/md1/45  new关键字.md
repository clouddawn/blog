# new 关键字执行过程

```javascript
function Person(name, age, gender) {
  this.name = name;
  this.age = age;
  this.sex = gender;
  this.eat = function (food) {
    console.log(food);
  };
}
var mcs = new Person("梅长苏", 31, "男");
console.log(mcs);
```

(1) new 构造函数可以在内存中创建一个空的对象  
(2) this 就会指向刚才创建的空对象  
(3) 执行构造函数里面的代码，给这个空对象添加属性和方法  
(4) 返回这个对象（所以构造函数里面不需要 return）

![image](../images/45/n3.png)
