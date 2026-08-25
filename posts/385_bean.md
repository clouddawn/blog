# Bean

在 Spring 的世界里，**Bean** 是最核心、出现频率最高的概念。你可以把它理解为 **“由 Spring 容器（IoC 容器）管理的 Java 对象”**。

------

### Bean 到底是什么？

- **普通对象**：你 `new StreamingChatModel()` 出来的实例，用完即丢，JVM 垃圾回收了就没了，Spring 对它毫不知情。
- **Bean**：你把对象交给 Spring 容器（一个大工厂）托管。Spring 负责创建它、给它喂依赖（注入）、管理它的存活时间，当你需要时，直接从容器里取出来用。

**打个比方**：

- 普通对象 = 你自己去菜市场买菜、洗菜、切菜、炒菜。
- Bean = 你点外卖，把需求告诉平台（Spring 容器），平台做好后送到你手上，你只管吃。

------

### 为什么不用 `new`，非要搞个 Bean 的概念？

如果用 `new` 创建对象，代码会硬编码耦合。比如你的 `ChatAssistant` 依赖 `StreamingChatModel`，如果你在代码里写 `new OpenAiStreamingChatModel(...)`，以后想换成阿里云的通义千问，就得去改所有 `new` 的地方。

而定义为 **Bean** 后，由 Spring 容器统一管理依赖关系。你在业务代码里只需要声明“我需要一个 `StreamingChatModel`”，Spring 自动把正确的实例注入进来，替换实现时只需要改一个 `@Bean` 方法，其他代码**零修改**。这就是 **控制反转（IoC）** 的精髓。

------

### 如何定义一个 Bean？

#### 1. 注解标记类（`@Component` 及其衍生注解）

在类上直接加 `@Component`、`@Service`、`@Repository`、`@Controller`。Spring 启动时扫描这些注解，自动把该类实例化为 Bean。

```java
@Service
public class UserService { // 这个类本身就是一个 Bean
    // ...
}
```

#### 2. 配置类中的 `@Bean` 方法

**适用于第三方库**（比如你无法修改 `OpenAiStreamingChatModel` 的源码，没法给它加 `@Component`）。在你的 `LangChain4jConfig` 中，下面的方法返回值就是一个 Bean：

```java
@Bean  // 这个方法的返回值（StreamingChatModel 对象）会被 Spring 容器管理
StreamingChatModel streamingChatModel() {
    return OpenAiStreamingChatModel.builder()
            .baseUrl("https://api.deepseek.com")
            .apiKey(apiKey)
            .build();
}
```

> **关键点**：方法名 `streamingChatModel` 默认就是 Bean 的 ID（名称），返回的对象就是 Bean 实例。

------

### Bean 的三大核心属性

#### 1. Bean 的名称（ID）

每个 Bean 在容器中都有唯一的名字。你可以通过 `@Bean("customName")` 或 `@Component("customName")` 自定义，不指定则默认用方法名或类名首字母小写。

#### 2. Bean 的作用域（Scope）—— 极其重要

决定 Bean 被创建几次：

- **@Scope("singleton")（默认）**：**单例**。容器启动时创建一次，整个应用生命周期内共用这一个实例。你的 `StreamingChatModel` 和 `ChatAssistant` 都是单例，所以整个系统只维护一个 DeepSeek 连接，极其高效。
- **@Scope("prototype")**：**原型**。每次获取（或注入）时都创建一个全新的实例。适合有状态的对象（比如非线程安全的临时计算器）。

#### 3. Bean 的延迟加载（Lazy）

默认单例 Bean 在项目启动时就创建。如果你想让 Bean 在第一次被使用时才创建，加 `@Lazy` 注解，可以加快项目启动速度。

------

### Bean 的完整生命周期

Spring 容器管理 Bean 的整个过程如下（你在 `@Configuration` 中看不到这些细节，但它们是底层骨架）：

1. **实例化**：调用构造方法（或工厂方法）创建对象。（你的 `streamingChatModel()` 方法执行了 `build()`）
2. **属性注入**：Spring 把依赖的其他 Bean 赋值进来。（`chatAssistant` 方法中的两个参数就是在这里被注入的）
3. **Aware 接口回调**（了解即可）：如果 Bean 实现了 `BeanNameAware` 等接口，Spring 会传递容器信息。
4. **初始化前置处理**：执行 `@PostConstruct` 或 `afterPropertiesSet()` 方法。
5. **初始化完成**：Bean 正式可用，等待被业务代码调用。
6. **销毁**：容器关闭时，执行 `@PreDestroy` 或 `destroy()` 方法释放资源（如关闭数据库连接池）。

------

### 如何获取并使用 Bean？

- **方式一：依赖注入（推荐）**。在任意 Spring 管理的组件中，用 `@Autowired` 或构造器注入。

  ```javascript
@RestController
  public class ChatController {
      private final ChatAssistant chatAssistant; // Spring 自动把 Bean 注入进来
      public ChatController(ChatAssistant chatAssistant) {
          this.chatAssistant = chatAssistant;
      }
  }
  ```
  
- **方式二：手动从容器取**。通过 `ApplicationContext.getBean(Class)` 获取（不常用，除非特殊场景）。

------

### 总结：Bean 的本质就这一句话

> **Bean 就是把对象的“创建工作”从你的业务代码中剥离，交给 Spring 容器托管。从此你只负责“用”，不负责“造”。**
