# 泛型

Java泛型（Generics）是JDK 5引入的核心特性，本质是**参数化类型**，即把类型作为参数传递。它的主要价值在于**编译时类型安全检查**和**消除强制类型转换**。

### 1. 泛型类与接口（定义型别）

在类名或接口名后加 `<T>`，T 代表类型占位符（常用 `T`-Type, `E`-Element, `K,V`-Key/Value）。

```java
// 定义一个泛型类
public class Box<T> {
    private T content;

    public void set(T content) { this.content = content; }
    public T get() { return content; }
}

// 使用（Java 7之后右侧钻石语法 <> 可省略类型）
Box<String> stringBox = new Box<>(); 
stringBox.set("Hello");
String str = stringBox.get(); // 无需强制转型
```

### 2. 泛型方法（区别于泛型类）

**关键规则**：方法返回值前的 `<T>` 必须声明，这表示该方法独立拥有泛型能力，即使所在类不是泛型类。

```java
public class Util {
    // 泛型方法：交换数组中的两个元素
    public static <T> void swap(T[] array, int i, int j) {
        T temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }
}
// 调用时编译器会自动类型推断
Util.swap(new String[]{"A", "B"}, 0, 1);
```

------

### 3. 通配符（Wildcard）—— `?`

当你不关心具体类型，或想限制类型范围时，使用通配符。这是泛型中最容易混淆的部分。

- **无界通配符 ?**：表示未知类型，用于只读操作（因为不知道类型，不能 `add` 元素，除了 `null`）。

  ```java
  public void printList(List<?> list) { // 可以接收 List<String> 或 List<Integer>
      for (Object o : list) System.out.println(o);
  }
  ```

- **上界通配符 <? extends T>**：限定类型为 **T 或 T 的子类**（上限）。**频繁读取**时使用。

  ```java
  public double sum(List<? extends Number> list) { // 接收 List<Integer>, List<Double>
      return list.stream().mapToDouble(Number::doubleValue).sum();
  }
  // 注意：只能读，不能写入（除了 null），因为你不知道具体是 Integer 还是 Double
  ```

- **下界通配符 <? super T>**：限定类型为 **T 或 T 的父类**（下限）。**频繁插入**时使用。

  ```java
  public void addNumbers(List<? super Integer> list) { // 接收 List<Integer> 或 List<Number>
      list.add(1);   // 可以安全放入 Integer
      list.add(2);
      // 注意：读取时只能拿到 Object 类型
  }
  ```

------

### 4. 核心原则：PECS（Producer-Extends, Consumer-Super）

这是牢记通配符用法的口诀：

- **Producer (生产者)**：如果你要从集合中 **读取** 数据，用 `extends`（上界）。
- **Consumer (消费者)**：如果你要向集合中 **写入** 数据，用 `super`（下界）。
- 既是生产又是消费，则不用通配符。

------

### 5. 类型擦除（Type Erasure）—— 必须理解的底层机制

Java 的泛型是**编译时**特性。编译后，泛型信息会被擦除，替换为原始类型（Raw Type）。

- `List<String>` 和 `List<Integer>` 在**运行时**字节码是同一个 `List` 类。
- **影响**：无法在运行时通过反射获取泛型实际参数（除非通过子类继承保留），无法 `new T()`，无法 `new T[]`，无法在静态上下文中使用泛型参数。

------

### 6. 泛型与继承

**List<String> 并不是 List<Object> 的子类！** 即使 String 是 Object 的子类，这两个泛型类型之间也没有父子关系。

```java
// 错误！编译不通过
List<Object> objList = new ArrayList<String>(); 

// 正确：利用通配符表示范围
List<? extends Object> wildcardList = new ArrayList<String>(); 
```


