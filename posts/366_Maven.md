# Maven

作为一个前端开发，可以把 **Maven** 理解为后端世界的 **npm + 构建工具（如Webpack/Vite）**，只不过它管理的是 Java 代码，而不是 JavaScript。

### 1. 依赖管理（相当于 `package.json` + `node_modules`）

前端用 `npm install` 下载 `node_modules`，后端用 Maven 下载 `.jar` 包（存放在本地仓库 `.m2/repository`）。

- `pom.xml`（相当于后端的 `package.json`）。
- **你项目里的情况**：项目引用了 `Jeecg-Boot 3.0` 和公司自研框架 `twqcframework.boot`。Maven 会自动把这些框架依赖的百万级底层 Jar 包（如 Spring、MyBatis）全部拉取下来，你无需手动去找。

### 2. 多模块管理（相当于 Monorepo / Workspaces）

你们项目描述是 **“多模块”**，这意味着 Maven 把项目拆成了好几个子工程（类似于前端 `pnpm-workspace` 里的多个子包）。

- 通常会有个**父级 pom.xml**（相当于 root 配置），统一规定所有子模块用的 Java 版本（8）、编码格式、公共依赖版本。
- 子模块（比如 `-api`、`-service`、`-system`）各自有自己的 `pom.xml`。Maven 保证它们之间可以互相引用（比如 `system` 模块引用 `api` 模块），就像前端 monorepo 里 `packages/A` 引用 `packages/B`。

### 3. 构建生命周期（相当于 `npm run build`）

前端构建（`npm run build`）产出 `dist` 文件夹，Maven 构建（`mvn clean package`）则产出可运行的 `.jar` 文件（Java 的部署包）。

Maven 有一套标准的“生命周期”命令，我把它翻译给你：

| Maven 命令      | 前端类比                     | 实际效果                                                     |
| :-------------- | :--------------------------- | :----------------------------------------------------------- |
| `mvn clean`     | `rm -rf node_modules/.cache` | 删除上次编译的临时文件（`target` 目录）。                    |
| `mvn compile`   | `tsc`（只编译）              | 只把 Java 代码编译成 `.class` 字节码。                       |
| `mvn test`      | `npm run test`               | 运行单元测试（检查代码逻辑是否正确）。                       |
| **mvn package** | **npm run build**            | **最常用**。编译 + 测试，最后把整个后端项目打包成一个可执行的 `.jar` 包（放在 `target/` 目录下）。 |
| `mvn install`   | `npm link`                   | 把打包好的 `.jar` 安装到本地 Maven 仓库，供本机其他项目引用。 |

### 4. 针对你项目的特殊关注点（给前端提个醒）

- **端口 7017 是怎么来的？**：Maven 本身不带端口，端口是在 `application.yml`（相当于后端的 `.env`）里配置的。但 Maven 可以通过 **Profile（环境配置）** 来切换不同的配置文件（如 `dev`、`test`、`prod`），类似于前端 `.env.development` 和 `.env.production`。
- **为什么代码规模这么大（731个Java文件）？**：因为 Maven 强制要求按 **Controller（接口层）**、**Service（业务层）**、**Mapper（数据库层）** 分层存放。这么多文件如果没有 Maven 的结构化管理，依赖早就乱成一锅粥了。
- **联调时必用命令**：如果后端改了 Java 代码，你需要重启服务。在 IDE 里点击启动本质上也是在运行 `mvn spring-boot:run`（这是专门为 SpringBoot 提供的快捷启动命令，相当于 `npm run dev`）。

**总结给你的核心印象**：你可以把 `pom.xml` 当作 `package.json`，把 Maven 的执行过程理解为 **“先彻底清理缓存，再下载所有依赖，最后把所有零散的 Java 文件编译打包成一个完整的压缩包”** 的过程。

