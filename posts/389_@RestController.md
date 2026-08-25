# @RestController

`@RestController` 是 Spring 框架中用于**构建 RESTful Web 服务**的核心注解。它专门用在**控制器（Controller）类**上，用来处理 HTTP 请求并直接返回数据（如 JSON/XML），而不是返回视图页面（如 JSP）。

可以把它理解为一个“**加强版**”的 `@Controller`，专门为前后端分离的 API 开发而生。

------

### 它到底是什么？

`@RestController` 其实是一个**组合注解**，它等价于：

```java
@Controller
@ResponseBody
```

这意味着：

- **@Controller**：将类标记为 Spring MVC 的控制器，能处理 Web 请求。
- **@ResponseBody**：告诉 Spring，**控制器中所有方法的返回值**应该直接写入 HTTP 响应体（Response Body）中，而不是解析为视图名称进行跳转。

所以，当一个类被标记为 `@RestController` 后，它的所有方法都会**默认**把返回的对象自动序列化为 **JSON**（或其他格式）返回给客户端。

------

### 基本用法示例

假设我们要开发一个用户管理的 REST API，代码会是这样：

```java
import org.springframework.web.bind.annotation.*;

import java.util.ArrayList;
import java.util.List;

@RestController // 1. 标记为REST控制器
@RequestMapping("/api/users") // 2. 定义基础URL路径
public class UserController {

    // 模拟数据，实际项目中会注入 UserService
    private final List<String> users = new ArrayList<>();

    // 3. 处理 GET 请求：获取所有用户
    @GetMapping
    public List<String> getUsers() {
        // 返回值 List<String> 自动转为 JSON 数组返回
        return users;
    }

    // 4. 处理 GET 请求：根据ID获取单个用户
    @GetMapping("/{id}")
    public String getUserById(@PathVariable int id) {
        // 返回值 String 直接作为纯文本/JSON字符串返回
        return "User " + id;
    }

    // 5. 处理 POST 请求：新增用户
    @PostMapping
    public String addUser(@RequestBody String user) {
        users.add(user);
        // 返回一个字符串，表示操作成功
        return "User added: " + user;
    }
}
```

**请求与响应示例：**

- `GET /api/users` → 返回 `["Alice", "Bob"]` (JSON数组)
- `GET /api/users/1` → 返回 `"User 1"` (纯文本)
- `POST /api/users` (Body: `"Charlie"`) → 返回 `"User added: Charlie"`

------

### 与 `@Controller` 的核心区别

这是开发者最容易混淆的地方，下面是核心对比：

| 特性                       | **@RestController**                          | **@Controller**                                        |
| :------------------------- | :------------------------------------------- | :----------------------------------------------------- |
| **主要用途**               | 构建 **RESTful API**，返回数据（JSON/XML）   | 构建传统 Web 应用，返回视图页面（JSP/Thymeleaf）       |
| **默认行为**               | 方法返回值**直接写入** HTTP 响应体           | 方法返回值通常表示**视图名称**，由视图解析器渲染       |
| **是否需要 @ResponseBody** | **不需要**，默认所有方法都带 `@ResponseBody` | **需要**，每个要返回数据的方法都必须加 `@ResponseBody` |
| **典型返回类型**           | 对象、集合、`ResponseEntity<T>`              | `ModelAndView`、`String`（视图名）                     |
| **前后端分离**             | ✅ **天然适合**，直接返回 JSON 给前端         | ❌ 不适合，主要用于服务端渲染                           |

------

### 进阶用法和最佳实践

#### 1. **配合 @RequestMapping / @GetMapping 等映射注解**

`@RestController` 本身不处理 URL 映射，需要结合 `@RequestMapping` 或其快捷注解（`@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`）来定义路由。

#### 2. **返回复杂对象（自动转JSON）**

Spring Boot 默认使用 Jackson 库，它会自动将 Java 对象序列化为 JSON：

```java
@GetMapping("/{id}")
public User getUser(@PathVariable Long id) {
    // 假设从数据库查到了 User 对象
    User user = new User(id, "Alice", "alice@example.com");
    return user; // 自动转换为 {"id":1,"username":"Alice","email":"alice@example.com"}
}
```

#### 3. **灵活控制响应状态码和头信息**

如果需要对响应进行更精细的控制（如设置状态码、响应头），可以使用 `ResponseEntity`：

```java
@PostMapping
public ResponseEntity<User> createUser(@RequestBody User user) {
    // 假设保存成功，返回201 Created状态，并在响应体中包含新用户信息
    User savedUser = userService.save(user);
    return ResponseEntity.status(HttpStatus.CREATED).body(savedUser);
}
```

#### 4. **异常处理**

REST API 开发中，通常使用 `@RestControllerAdvice` 配合 `@ExceptionHandler` 进行全局异常处理，统一返回规范的错误 JSON 结构。

#### 5. **注入 Service 层**

通过**构造器注入**（最推荐的方式）使用 `UserService`：

```java
@RestController
@RequestMapping("/api/users")
public class UserController {
    
    private final UserService userService;

    // 构造器注入，Spring 4.3+ 可省略 @Autowired
    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping
    public List<User> getUsers() {
        return userService.findAll();
    }
}
```

------

### 注意事项

- **不要返回视图名**：如果你在 `@RestController` 的方法里返回 `"login"`，客户端收到的不是跳转到 `login.html`，而是**字符串 "login" 本身**。
- **处理静态资源**：`@RestController` 不负责处理静态资源（如图片、CSS、JS），这部分应由 Spring MVC 的静态资源映射处理。
- **可以混用**：在同一个项目中，可以同时存在 `@RestController`（处理 API）和 `@Controller`（处理页面请求），它们互不干扰。

------

### 一句话总结

**@RestController = @Controller + @ResponseBody，专门用来创建“只返回数据、不返回页面”的 RESTful 接口，是 Spring Boot 开发前后端分离应用的标准做法。**