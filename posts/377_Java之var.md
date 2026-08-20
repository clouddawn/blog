# Java var

`var` 是 Java 10 引入的一个特性，用于**局部变量类型推断**。它不是关键字，而是一个“保留类型名称”。

简单来说，使用 `var` 声明变量时，你不需要显式写出变量的类型，编译器会根据等号右边的初始化表达式自动推断出正确的类型。

### 使用场景

`var` 主要用于声明**带有初始化器的局部变量**。以下是一些典型的合法使用场景：

- **基本的局部变量声明**：

  ```java
  var message = "Hello, Java 10"; // 推断为 String 类型[reference:7]
  var number = 10;               // 推断为 int 类型[reference:8]
  var list = new ArrayList<String>(); // 推断为 ArrayList<String> 类型[reference:9][reference:10]
  ```

- **增强的 for-each 循环**：

  ```java
  List<String> names = Arrays.asList("Alice", "Bob");
  for (var name : names) { // 推断 name 为 String 类型[reference:11][reference:12]
      System.out.println(name);
  }
  ```

- **传统的 for 循环**：

  ```java
  for (var counter = 0; counter < 10; counter++) { // 推断 counter 为 int 类型[reference:13]
      // ...
  }
  ```

- **try-with-resources 语句**：

  ```java
  try (var input = new FileInputStream("file.txt")) { // 推断为 FileInputStream 类型[reference:14]
      // ...
  }
  ```

- **Lambda 表达式的参数**（自 Java 11 起）：

  ```java
  // 使用 var 声明 Lambda 参数，与不使用 var 效果相同[reference:15]
  var result = Stream.of("a", "b", "c")
                     .reduce((var x, var y) -> x + y); // 推断 x 和 y 为 String 类型[reference:16]
  ```

### ⛔ 使用限制

`var` 的使用有严格的限制，不能在以下场景中使用：

- **必须初始化**：声明时必须赋值，否则编译器无法推断类型。

  ```java
  var a; // 编译错误！
  ```

- **初始化值不能为 null**：`null` 没有类型信息，无法推断。

  ```java
  var emptyList = null; // 编译错误！
  ```

- **不能用于成员变量（字段）**：`var` 只能用于方法、构造器或代码块内部的局部变量。

  ```java
  class Example {
      private var field; // 编译错误！
  }
  ```

- **不能用于方法参数和返回值**：方法的参数和返回类型必须显式声明。

  ```java
  public void process(var param) { } // 编译错误！
  public var getResult() { }        // 编译错误！
  ```

- **不能用于 Lambda 表达式或数组初始化器**：这些场景需要明确的目标类型。

  ```java
  var p = (String s) -> s.length() > 10; // 编译错误！
  var arr = {1, 2, 3};                  // 编译错误！
  ```

### 最佳实践

使用 `var` 的核心原则是**提升而非损害代码的可读性**。

- **应该使用 var 的场景（信息显而易见时）**：
  - 右侧的初始化表达式已明确指明了类型，如 `var str = "Hello";`。
  - 用于简化冗长的泛型类型声明，如 `var map = new HashMap<String, List<Integer>>();`。
  - 在循环中，变量的类型从集合或循环变量中显而易见时。
- **谨慎或避免使用 var 的场景（类型不明显时）**：
  - 右侧是方法调用，且方法名不能清晰表达返回类型时，例如 `var result = obj.process();`。
  - 在较长的 Stream 流水线中，中间变量的类型可能不清晰。
  - 使用菱形操作符 `<>` 且未指定泛型类型时，可能被推断为 `Object` 类型。

### 总结

- **本质**：`var` 是一个语法糖，在编译时进行类型推断，**没有运行时开销**，Java 仍然是静态类型语言。
- **核心原则**：在保证代码可读性的前提下，合理使用 `var` 来减少样板代码。如果使用 `var` 会让代码变得模糊，就应该选择显式声明类型。





















