# Java 密封类

在 Java 中，**密封类（sealed）** 的核心作用是**限制子类的数量**，让父类能够明确声明“只有我指定的这几个类才能继承我”。结合 Java 17+ 的 **switch 模式匹配**，它能确保编译器帮我们检查是否覆盖了所有可能的子类，从而避免遗漏。

```java
// 1. 定义密封父类：只允许 Circle 和 Rectangle 继承它
sealed class Shape permits Circle, Rectangle {
}

// 2. 子类必须声明为 final（彻底封闭），防止被再次继承
final class Circle extends Shape {
    double radius;
    Circle(double radius) { 
        this.radius = radius; 
    }
}

final class Rectangle extends Shape {
    double width, height;
    Rectangle(double width, double height) { 
        this.width = width; 
        this.height = height; 
    }
}

// 3. 测试密封类的最大优势：编译器强制穷举
public class Main {
    public static void main(String[] args) {
        Shape s = new Circle(5.0);
        
        // 使用 switch 模式匹配（Java 21+）
        // 因为 Shape 只允许 Circle 和 Rectangle，
        // 编译器知道只有这两种可能，所以不需要写 default 分支！
        double area = switch (s) {
            case Circle c -> 3.14 * c.radius * c.radius;
            case Rectangle r -> r.width * r.height;
        };
        System.out.println("面积: " + area);
    }
}
```

### 关键点说明：

1. **sealed + permits**：父类 `Shape` 用 `permits` 圈定了“户口本”，只有 `Circle` 和 `Rectangle` 有资格继承。
2. **子类必须加修饰符**：子类必须是 `final`（不能再有孙子类）、`sealed`（继续限制孙子类）或 `non-sealed`（允许任意继承）。例子中用最稳妥的 `final`。
3. **最大的好处**：在 `switch` 中，**无需写 default 分支**。如果将来有人新增了一个 `Triangle` 子类但没在 `permits` 中声明，编译器会直接报错提醒你修改 `switch`，这极大地增强了代码的健壮性，避免了运行时忘记处理新类型的 bug。