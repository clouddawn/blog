# Spring MVC

**Spring Boot 是“自动配置引擎”（基建狂魔），而 Spring MVC 是“代码组织架构”（施工图纸）。**

你用了Spring Boot，**默认就在用Spring MVC**，只是你没感知到它。下面我用纯前端视角，帮你彻底吃透Spring MVC：

### 1. 它到底是什么？（前端终极类比）

Spring MVC 的核心本质就是一个**“后端路由分发器 + 中间件拦截器”**。

- **前端对标**：它就像 **Express.js 的 app.use() 和 app.get() 体系** + **React Router 的路由匹配机制**。
- **核心职责**：浏览器发来一个请求（如 `GET /user`），Spring MVC 负责把这个请求**精准地传送到你写的某个 Java 方法上**，然后把方法返回的结果（JSON）**再传送回前端**。

### 2. 一次请求在 Spring MVC 里的“快递之旅”（必看！）

为了让你像看前端生命周期一样看懂它，我把它的核心组件翻译成前端术语：

| Spring MVC 组件                     | 前端对标                                               | 它的实际工作                                                 |
| :---------------------------------- | :----------------------------------------------------- | :----------------------------------------------------------- |
| **DispatcherServlet**（前端控制器） | **Vue/React Router 的总路由入口**                      | 所有请求进来的“大门”，它负责接单（接收所有HTTP请求）。       |
| **HandlerMapping**（处理器映射器）  | **路由配置文件（routes.js）**                          | 它查一下“`GET /user`”应该交给哪个类处理？相当于路由匹配。    |
| **Controller**（控制器）            | **Next.js 的 page/api 文件** 或 **Express 的路由回调** | 就是你的 `@GetMapping` 所在的类，专门写业务接收参数的地方。  |
| **ModelAndView**（模型和视图）      | **（旧时代）JSP / EJS 模板引擎**                       | **请注意！** 这是老古董。现在前后端分离，**这里的“View”不再是页面，而是直接变成 @ResponseBody 返回的 JSON 数据**。 |
| **ViewResolver**（视图解析器）      | **（已废弃）**                                         | 现在你基本用不到，因为你不返回 `xxx.jsp` 页面，而是直接返回 JSON。 |

------

### 3. 你现在写的代码，到底哪部分是 Spring MVC？

你打开你的 `UserController.java`，这个文件里的每一个注解，都是 Spring MVC 在干活：

```java
@RestController  // 【核心】这是Spring MVC提供的！告诉系统：这里面的返回值全部自动转成JSON
@RequestMapping("/api/v1") // 【核心】这就是路由前缀，相当于前端 router 的 base path
public class UserController {

    @GetMapping("/user/{id}") // 【核心】精确匹配 GET 请求，相当于 app.get('/user/:id')
    public User getUser(@PathVariable Long id) { // @PathVariable 就是解构出路由参数
        return new User(id, "前端大神");
        // Spring MVC 自动把 User对象 转成 {"id":1,"name":"前端大神"} 返回
    }
}
```

你看，**你根本不需要关心请求是怎么被解析的，Spring MVC 在背后全帮你做了**。

------

### 4. 前端最关心的“中间件”（拦截器）在哪？

既然对标 Express 的中间件，那登录校验（JWT Token）怎么拦截？

- 在 Spring MVC 中，它不叫 `app.use()`，叫做 **Interceptor（拦截器）** 或 **Filter（过滤器）**。
- 你可以写一个类实现 `HandlerInterceptor`，在里面验证 Token。如果验证失败，就直接拦截掉，**请求根本到不了上面的 getUser 方法**。这和你用 Axios 拦截器 或 Express 中间件做鉴权是完全一样的逻辑。

------

### 5. 终极结论：Boot 和 MVC 到底什么关系？

- **Spring MVC** 定义了“请求->方法->返回”的**代码编写规范**（也就是你天天写的 `@GetMapping`）。
- **Spring Boot** 只是觉得“配置 MVC 太烦了”（以前配 MVC 要手动配 XML，就像手动配 Webpack），于是 **Spring Boot 自动把 Spring MVC 的配置全给你设定好了**，你直接写 `@RestController` 就能用。

**给你的建议：**
你现在是前端转全栈，**完全不需要去翻 Spring MVC 那本厚厚的官方文档**。你只需要知道两件事：

1. **返回 JSON 用 @RestController**（这是 MVC 给你的）。
2. **接收前端传来的 JSON 用 @RequestBody**（比如 `public void add(@RequestBody User user)`，这和前端 `req.body` 一模一样）。

