# Vue CLI

Vue CLI 是一个基于 Vue.js 进行快速开发的完整系统，提供：

* 通过 `@vue/cli` 实现的交互式的项目脚手架。
* 通过 `@vue/cli` + `@vue/cli-service-global` 实现的零配置原型开发。
* 一个运行时依赖（`@vue/cli-service`），该依赖：
  * 可升级；
  * 基于 webpack 构建，并带有合理的默认配置；
  * 可以通过项目内的配置文件进行配置；
  * 可以通过插件进行扩展。
* 一个丰富的官方插件集合，集成了前端生态中最好的工具。
* 一套完全图形化的创建和管理 Vue.js 项目的用户界面。

## 该系统的组件

### CLI

CLI (`@vue/cli`) 是一个全局安装的 npm 包，提供了终端里的 `vue` 命令。它可以通过 `vue create` 快速搭建一个新项目，或者直接通过 `vue serve` 构建新想法的原型。

### CLI 服务

CLI 服务 (`@vue/cli-service`) 是一个开发环境依赖。它是一个 npm 包，局部安装在每个 `@vue/cli` 创建的项目中。

CLI 服务是构建于 webpack 和 webpack-dev-server 之上的。它包含了：

- 加载其它 CLI 插件的核心服务；
- 一个针对绝大部分应用优化过的内部的 webpack 配置；
- 项目内部的 `vue-cli-service` 命令，提供 `serve`、`build` 和 `inspect` 命令。

### CLI 插件

CLI 插件是向你的 Vue 项目提供可选功能的 npm 包，例如 Babel/TypeScript 转译、ESLint 集成、单元测试和 end-to-end 测试等。Vue CLI 插件的名字以 `@vue/cli-plugin-` (内建插件) 或 `vue-cli-plugin-` (社区插件) 开头，非常容易使用。

当你在项目内部运行 `vue-cli-service` 命令时，它会自动解析并加载 `package.json` 中列出的所有 CLI 插件。

插件可以作为项目创建过程的一部分，或在后期加入到项目中。它们也可以被归成一组可复用的 preset。

## 插件

Vue CLI 使用了一套基于插件的架构。如果你查阅一个新创建项目的 `package.json` ，就会发现依赖都是以 `@vue/cli-plugin-` 开头的。插件可以修改 webpack 的内部配置，也可以向 `vue-cli-service` 注入命令。在项目创建的过程中，绝大部分列出的特性都是通过插件来实现的。基于插件的架构使得 Vue CLI 灵活且可扩展。

## Preset

一个 Vue CLI preset 是一个包含创建新项目所需预定义选项和插件的 JSON 对象，让用户无需在命令提示中选择它们。

在 `vue create` 过程中保存的 preset 会被放在你的 home 目录下的一个配置文件中（`~/.vuerc`）。你可以通过直接编辑这个文件来调整、添加、删除保存好的 preset。

## 缓存和并行处理

* `cache-loader` 会默认为 Vue/Babel/TypeScript 编译开启。文件会缓存在 `node_modules/.cache`中，如果你遇到了编译方面的问题，记得先删掉缓存目录之后再试试看。
* `thread-loader` 会在多核 CPU 的机器上为 Babel/TypeScript 转译开启。

## HTML 和静态资源

### Index 文件

`public/index.html` 文件是一个会被 html-webpack-plugin 处理的模板。在构建过程中，资源链接会被自动注入。另外，Vue CLI 也会自动注入 resource hint（`preload/prefetch`、manifest 和图标链接（当用到 PWA 插件时）以及构建过程中处理的 JavaScript 和 CSS 文件的资源链接。

### 插值

因为 index 文件被用作模板，所以你可以使用 lodash template 语法插入内容：

- `<%= VALUE %>` 用来做不转义插值；
- `<%- VALUE %>` 用来做 HTML 转义插值；
- `<% expression %>` 用来描述 JavaScript 流程控制。

除了被 `html-webpack-plugin` 暴露的默认值之外，所有客户端环境变量也可以直接使用。例如，`BASE_URL` 的用法：

```html
<link rel="icon" href="<%= BASE_URL %>favicon.ico">
```





























