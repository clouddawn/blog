# python中的class

Python 中的 `class` （类）是面向对象编程的核心。可以把类理解为生产对象的模具，而对象则是基于这个模具造出来的具体实物。

## 基本结构：`__init__` 与 `self`

* `__init__` 是构造方法，在创建对象时自动调用，用户初始化对象的属性。
* `self` 代表实例自身，在类内部定义方法时，第一个参数必须是 `self` （用于访问该实例的属性和方法）。

```python
class Dog:
    # 类属性（所有实例共享）
    species = "Canis familiaris"
    
    # 实例初始化
    def __init__(self, name, age):
        self.name = name # 实例属性
        self.age = age
        
    # 实例方法
    def bark(self):
        print(f"{self.name} 在汪汪叫！")
        
# 实例化（创建对象）
my_dog = Dog("旺财", 3)
print(my_dog.name) # 输出：旺财
my_dog.bark() # 输出：旺财 在汪汪叫！
```

