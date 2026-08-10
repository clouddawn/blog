# record

 Java `record` 是在 **Java 14** 中预览、**Java 16** 正式发布的一种**轻量级类**，专门用来承载不可变的数据。

它诞生的核心目的是：**用极简的语法，替代传统 Java 类中那些冗长、重复、无聊的样板代码（getter、setter、构造器、equals、hashCode、toString）。**

------

### 1. 基础语法与“编译器的魔法”

当你写下这一行代码时：

```java
public record ApiResponse<T>(int code, String message, T data) {}
```

**编译器在背后自动为你生成了以下全部内容：**

1. **私有 final 字段**：`private final int code;`、`private final String message;`、`private final T data;`（注意，字段是私有的，且不可变）。
2. **全参构造器**：`public ApiResponse(int code, String message, T data)`。
3. **访问器方法**：**注意，不叫 getCode()，而是直接叫 code()**。即 `int code()`、`String message()`、`T data()`。
4. **equals(Object o) 方法**：比较两个 record 对象时，比较的是**所有字段的值**是否相等。
5. **hashCode() 方法**：根据所有字段计算哈希值。
6. **toString() 方法**：打印格式为 `ApiResponse[code=0, message=success, data=User]`。

------

### 2. 如何自定义 Record（扩展功能）

虽然 `record` 是数据载体，但它也允许你添加自定义逻辑，你之前代码中的静态工厂方法 `ok()` 和 `error()` 就是最好的例子。

**① 添加实例方法和静态方法**

```java
public record User(String name, int age) {
    // 实例方法：基于数据计算新值
    public String greeting() {
        return "Hello, " + name;
    }

    // 静态工厂方法（就像你的 ok/error）
    public static User of(String name) {
        return new User(name, 18);
    }
}
```

**② 紧凑构造器（Compact Constructor）—— 用于数据校验和规范化**
这是 `record` 独有的特性。当你想在对象创建时校验参数，但又不想写完整的构造器代码时，可以使用“紧凑构造器”，它甚至不需要写参数列表：

```java
public record ApiResponse<T>(int code, String message, T data) {
    // 紧凑构造器：会在标准构造器之前执行
    public ApiResponse {
        // 校验：如果 code 小于 0，抛异常
        if (code < 0) {
            throw new IllegalArgumentException("Code must be non-negative");
        }
        // 规范化：如果 message 为 null，赋默认值
        if (message == null) {
            message = "No message";
        }
        // 注意：这里不需要写 this.code = code; 编译器会自动赋值
    }
}
```

**③ 自定义全参构造器（极少使用）**
如果你想完全自己控制构造逻辑，也可以显式写出全参构造器，但需给所有字段赋值：

```java
public record Point(int x, int y) {
    public Point(int x, int y) {
        if (x < 0 || y < 0) throw new IllegalArgumentException();
        this.x = x; // 必须显式赋值
        this.y = y;
    }
}
```

------

### 3. Record 的“死穴”（核心限制）

使用 `record` 前，必须理解它的设计边界：

| 限制项             | 说明                                                         |
| :----------------- | :----------------------------------------------------------- |
| **隐式 final**     | `record` 不能被继承（不能 `extends` 其他类，但它可以实现 `interface`）。 |
| **不可变（浅层）** | 所有组件字段都是 `final` 的，一旦创建就不能修改（没有 setter）。 |
| **必须全参构造**   | 没有无参构造器。如果你需要无参构造，说明它不该用 `record`（应改用 `class`）。 |
| **不能有实例字段** | 你只能在头部定义组件，不能在类体内定义额外的非静态字段。但可以定义静态字段。 |
| **不能是抽象类**   | 因为它是最终不可变的数据快照。                               |

------

### 4. 什么时候该用 Record？（最佳实践）

- **✅ 强烈推荐使用场景**：
  - **DTO（数据传输对象）**：如 API 请求/响应体、微服务间的消息体。
  - **VO（值对象）**：如坐标 `Point(x,y)`、货币 `Money(amount, currency)`。
  - **多值返回**：代替 `Map` 或 `Object[]`，让返回值有明确的字段名。
  - **数据中间层**：如 JPA 的投影（Projection）结果。
- **❌ 绝对不要用的场景**：
  - 需要频繁修改字段值（如 Hibernate/JPA 的实体 `@Entity`，因为需要代理和脏检查）。
  - 需要继承其他父类（如 Spring 的 `BaseEntity`）。
  - 需要复杂的生命周期或业务行为（如状态机）。

------

### 5. 对比 Lombok 的 `@Data`

你一定听说过 `@Data`，它们很像，但有本质区别：

| 对比点         | `record`（原生）     | `@Data`（Lombok）                  |
| :------------- | :------------------- | :--------------------------------- |
| **可变性**     | 不可变（无 setter）  | 可变（有 setter）                  |
| **继承**       | 不能继承             | 可以继承（普通类）                 |
| **依赖**       | 无需额外依赖（原生） | 需要引入 Lombok 插件               |
| **延迟初始化** | 不支持               | 支持（如 `@Data` 配合 `@Builder`） |

**结论**：如果数据创建后不会变，优先用 `record`；如果需要增删改查（如数据库实体），用普通 `class` 或 Lombok。

------

### 6. 回到你的 `ApiResponse` 代码

结合你的例子，使用 `record` 的收益非常明显：

```java
// 调用你的方法
ApiResponse<User> resp = ApiResponse.ok(new User("张三"));

// 获取数据时，用的是访问器，而不是 getter
int statusCode = resp.code();      // 不是 resp.getCode()
String msg = resp.message();       // 不是 resp.getMessage()
User user = resp.data();           // 不是 resp.getData()

// 打印时自带漂亮格式
System.out.println(resp); 
// 输出：ApiResponse[code=0, message=success, data=User[name=张三]]
```

这种写法让代码极其简洁，且因为不可变，在并发环境下天然线程安全，非常适合作为统一响应体在 Controller 中返回。