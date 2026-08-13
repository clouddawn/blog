# class

在Java中，提到“class的用法”通常需要区分两个层面：**语法关键字（class）**和**元数据类（java.lang.Class）**。前者是定义蓝图，后者是获取蓝图信息的“镜子”（反射核心）。

### 1. 基础用法：定义类（关键字 `class`）

这是最直观的用法，用于定义属性、方法和构造器。这里有一个关键细节：**内部类**和**匿名类**在实际开发中高频使用。

```java
// 1. 普通外部类
public class User {
    private String name;
    public User(String name) { this.name = name; }
}

// 2. 静态内部类（无需依赖外部类实例，常用作Builder）
public class Result {
    private int code;
    private Result(Builder b) { this.code = b.code; }
    public static class Builder {
        private int code;
        public Builder code(int code) { this.code = code; return this; }
        public Result build() { return new Result(this); }
    }
}

// 3. 匿名类（常用于一次性接口实现，如事件监听）
Runnable task = new Runnable() {
    @Override
    public void run() {
        System.out.println("匿名类执行");
    }
};
```

------

### 2. 核心进阶：反射（`java.lang.Class`）

这是Java动态特性的基石。获取 `Class` 对象有**三种方式**，适用不同场景：

| 获取方式            | 代码示例                                           | 适用场景                               |
| :------------------ | :------------------------------------------------- | :------------------------------------- |
| **类名.class**      | `Class<User> clazz = User.class;`                  | 编译时已知类型（最安全、高效）         |
| **实例.getClass()** | `Class<?> clazz = user.getClass();`                | 运行时已有对象实例                     |
| **Class.forName()** | `Class<?> clazz = Class.forName("com.demo.User");` | **动态加载**（配置驱动、JDBC驱动加载） |

拿到 `Class` 对象后，最常用的**反射操作**如下（注意：**高版本JDK（9+）** 对私有API访问有模块化限制，需添加 `--add-opens` 参数）：

```java
// 假设有类：public class Person { private String name; public void say() {} }

// 1. 创建实例（替代 new）
Class<?> clazz = Person.class;
// 注意：newInstance() 已弃用，推荐使用构造器
Constructor<?> constructor = clazz.getDeclaredConstructor();
constructor.setAccessible(true); // 无视私有构造器
Person p = (Person) constructor.newInstance();

// 2. 调用私有方法
Method method = clazz.getDeclaredMethod("say");
method.setAccessible(true); // 突破 private 限制
method.invoke(p);

// 3. 修改私有字段
Field field = clazz.getDeclaredField("name");
field.setAccessible(true);
field.set(p, "新名字");
```

------

### 3. 高级用法：类型令牌（`Class<T>` 泛型）

在Spring、Fastjson等框架中，经常看到方法参数携带 `Class<T>`。这是为了**在运行时保留泛型类型信息**，解决Java泛型擦除问题。

```java
// 泛型工具类示例：利用 Class<T> 确保类型安全
public class BeanUtils {
    // T 由调用时传入的 clazz 动态决定
    public static <T> T createInstance(Class<T> clazz) throws Exception {
        return clazz.getDeclaredConstructor().newInstance();
    }
}

// 调用：返回的就是 User 类型，无需强转
User user = BeanUtils.createInstance(User.class);
```

------

### 4. 必备注意事项（避坑指南）

- **性能开销**：反射比直接调用慢（约几倍至几十倍）。**不要**在循环体或高频调用的热路径中使用纯反射，建议配合缓存（如将 `Method` 缓存为静态常量）。
- **破坏封装性**：`setAccessible(true)` 会打破 `private` 保护，在安全敏感场景（如金融计算）需慎用。
- **JDK 9+ 模块化**：若操作 `java.base` 等系统模块内的私有API，需在JVM启动参数中添加 `--add-opens java.base/java.lang=ALL-UNNAMED`，否则会抛出 `InaccessibleObjectException`。

### 总结选择建议

- **写业务代码**：只用 `new` 关键字定义类，**尽量不使用反射**，保持代码清晰可维护。
- **写框架/工具**：必用 `Class.forName()` + 反射，配合泛型 `Class<T>` 增强扩展性。
- **获取类型**：优先用 `类名.class`（编译期检查），其次 `对象.getClass()`，最后才用 `Class.forName()`（需处理 `ClassNotFoundException`）。