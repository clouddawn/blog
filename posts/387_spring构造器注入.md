# Spring 构造器注入

在 Spring 框架中，**构造器注入（Constructor-based Dependency Injection）** 是指：**容器在创建 Bean 实例时，通过调用带有参数的构造方法，将依赖的对象作为参数传递进去**。

它是 Spring 官方**最推荐**的依赖注入方式。

------

### 核心机制：Spring 是如何做的？

当 Spring 扫描到 `@Service` 等注解并准备创建 `UserService` 时，流程如下：

1. **查找构造方法**：Spring 查看该类的所有构造方法。
2. **参数匹配**：根据构造方法的参数类型（如 `UserRepository`），在 Spring 容器中查找对应的 Bean。
3. **实例化并注入**：通过反射调用该构造方法，将找到的 Bean 作为实参传入，创建出完整的对象。

> **关键点（Spring 4.3+ 特性）**：如果目标类**只有一个**构造方法，那么**可以省略 @Autowired 注解**，Spring 会自动使用该构造器进行注入。如果有多个构造方法，则必须用 `@Autowired` 明确告诉 Spring 用哪一个。

------

### 为什么官方“强推”构造器注入？

| 优势                      | 详细说明                                                     |
| :------------------------ | :----------------------------------------------------------- |
| **不可变性（Immutable）** | 依赖字段可以被声明为 `private final`，对象创建后依赖永不改变，线程安全，且符合函数式编程思想。 |
| **杜绝 NPE（空指针）**    | 构造器强制调用者必须传入依赖，否则对象根本无法创建。这保证了你调用 `userService` 的任何方法时，`userRepository` 一定不为 null。 |
| **单元测试极简**          | 测试时无需启动 Spring 容器，直接 `new UserService(mockRepository)` 就能注入 Mock 对象，测试飞起。 |
| **规避循环依赖的隐患**    | Spring 虽然能解决 Setter/字段注入的循环依赖，但构造器注入如果出现循环依赖（A 构造需要 B，B 构造需要 A），Spring 在**启动时就会直接报错**，迫使你第一时间重构设计，而不是带着隐患上线。 |

------

### 推荐的最佳实践写法（配合 Lombok）

日常开发中，配合 Lombok 可以完美解决代码冗余问题：

**传统写法：**

```java
@Service
public class UserService {
    private final UserRepository userRepository;
    private final EmailService emailService;

    // 单个构造方法，@Autowired 可省略
    public UserService(UserRepository userRepository, EmailService emailService) {
        this.userRepository = userRepository;
        this.emailService = emailService;
    }
}
```

**Lombok 极简写法：**
使用 `@RequiredArgsConstructor` 会自动生成包含所有 `final` 字段的构造器，效果完全一样：

```java
@Service
@RequiredArgsConstructor  // 自动生成构造器
public class UserService {
    private final UserRepository userRepository;
    private final EmailService emailService;
    // 无需显式写构造方法，Spring 同样会自动注入
}
```

------

### 进阶细节：如果只有一个实现类，如何精确匹配？

构造器注入默认按**类型（Type）**匹配。如果有多个同类型 Bean（比如 `UserRepository` 有两个实现类 `MysqlRepo` 和 `RedisRepo`），就需要结合 `@Qualifier` 使用。

写法是在**构造方法的参数**前加注解：

```java
public UserService(
    @Qualifier("mysqlRepo") UserRepository userRepository) {
    this.userRepository = userRepository;
}
```

------

### 特殊场景：如果我有多个构造方法怎么办？

假设你为了兼容老代码，写了多个构造器：

```java
@Service
public class UserService {
    private final UserRepository userRepository;

    // 必须指定这个为注入构造器
    @Autowired
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    // 无参构造（仅供特殊工具使用）
    public UserService() {
        this.userRepository = null;
    }
}
```

此时，`@Autowired` 必须加在你想让 Spring 调用的那个构造器上，否则 Spring 会因无法确定选哪个而报错。

