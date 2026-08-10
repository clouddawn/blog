# Spring Boot

**Spring Boot的本质，就是后端的“Vite + React脚手架”**——它把Java后端开发中繁琐的配置和依赖全给你包好了，让你能直接写业务逻辑。

### 1. 它到底是什么？（前端类比）

- **Spring（老祖宗）**：相当于 **原生 JavaScript** + **Node.js** 核心库。功能极其强大，但配置复杂得吓人（到处都是`xml`配置文件），就像用原生JS手动搭建项目。
- **Spring Boot（你用的）**：相当于 **Vite/Create-React-App**。它提出了“**约定大于配置**”。你说你想写React，Vite一键给你配好Webpack/Babel；你说你想写Java Web，Spring Boot一键给你配好**内嵌的Tomcat（相当于后端的Webpack Dev Server）**，你写一个`@RestController`，它就自动帮你把路由挂好了。

### 2. 它到底解决了什么痛点？

作为前端，你最烦启动项目时要手动配`webpack.config.js`。后端以前比这还烦：

- **痛点A（依赖打架）**：前端有`package.json`，但版本不对会报错。后端有`pom.xml`（Maven）或`build.gradle`（Gradle）。Spring Boot给你一个**“BOM（物料清单）”**，你只要引入`spring-boot-starter-web`，它就把所有版本匹配的包（JSON解析、Web服务器等）像“套餐”一样全给你端上来，**绝对不会版本冲突**。
- **痛点B（重启太慢）**：前端改代码热更新很快。Spring Boot集成了**Spring DevTools**，你改完Java代码，它自动重启应用（比传统部署快很多），虽然比不上前端的HMR，但已经是后端的“热部署”了。

### 3. 你的前端代码怎么和它说话？（核心工作流）

全栈开发中，Spring Boot几乎只干一件事：**暴露API接口（Controller）**。

你看看这个“翻译”：

- **前端的 app.get('/user', (req, res) => { ... })**
- **等于 Spring Boot 的：**

```java
@RestController // 告诉Spring：这是个API控制器
@RequestMapping("/user") // 告诉Spring：基础路径是 /user
public class UserController {

    @GetMapping // 告诉Spring：这是个 GET 请求
    public String getUser() {
        return "{\"name\":\"张三\"}"; 
        // 实际上你会返回一个 User对象，Spring Boot会自动帮你转成 JSON（内置了Jackson，相当于前端的JSON.stringify）
    }
}
```

你看，连路由写法都和Express/NestJS极其相似。

### 4. “依赖注入”（IoC）—— 它的“Hooks”

前端用`useState`、`useEffect`管理状态；后端用**“依赖注入”**管理对象。
你不用手动 `new` 一个数据库操作类，只要在类上写 `@Autowired`，Spring Boot 就会像 React 的 Context 一样，自动把现成的实例**注入**到你的类里。

```java
@Autowired 
private UserService userService; // 不需要 new！Spring自动帮你挂载好
```

### 5. 最重要的“躺平”技巧（必看）

作为转全栈的前端，**你刚开始根本不需要深究Spring Boot的底层原理**。你只需要掌握这三板斧就够了：

1. **Controller（控制器）**：写 `@GetMapping` / `@PostMapping`，处理前端来的请求。
2. **Service（服务层）**：写具体的业务逻辑（比如算价格、调数据库）。
3. **Repository（数据层）**：用 Spring Data JPA 或 MyBatis 操作数据库（相当于前端的`axios`去调第三方接口，只不过这里是调MySQL）。

**给前端的特别提醒（跨域 CORS）**：你前端跑在 `localhost:3000`，后端跑在 `localhost:8080`，必报跨域错误。别慌！在你的Controller上直接加一行 `@CrossOrigin`，瞬间解决，就像在`vite.config.ts`里配代理一样简单。

