# webpack 01

## 什么是 webpack ？

从本质上来说，webpack 是一个现代的 JavaScript 应用的静态**模块打包**工具。

### 前端模块化

目前前端模块化使用的一些方案：AMD、CMD、CommonJS、ES6。

在 ES6 之前，要想进行模块化开发，就必须借助于其他的工具。并且在通过模块化开发完成了项目后，还需要处理模块间的各种依赖，并且将其进行整合打包。

而 webpack 其中一个核心就是让我们可能进行模块化开发，并且会帮助我们处理模块间的依赖关系。

而且不仅仅是 JS 文件，CSS、图片、json文件等等在 webpack 中都可以被当做模块来使用。

### 打包

webpack 中的各种资源模块进行打包合并成一个或多个包（Bundle）。并且在打包的过程中，还可以对资源进行处理，比如压缩图片，将 scss 转成 css，将 ES6 语法转成 ES5 语法，将 TypeScript 转成 JS 等等操作。

## 和 grunt/gulp 的对比

**grunt/gulp 的核心是 Task**，我们可以配置一系列的 task，并且定义 task 要处理的事物（例如 ES6、ts 转化、图片压缩、scss 转成 css），之后让 grunt/gulp 来依次执行这些 task，而且让整个流程自动化。所以 grunt/gulp 也被称为前端自动化任务管理工具。

**什么时候用 grunt/gulp呢？**

如果你的工程模块化依赖非常简单，甚至是没有用到模块化的概念。只需要进行简单的合并、压缩，就使用 grunt/gulp 即可。但是如果整个项目使用了模块化管理，而且相互依赖非常强，我们就可以使用更加强大的 webpack 了。

**所以，grunt/gulp 和 webpack 有什么不同呢？**

* grunt/gulp 更加强调的是前端流程的自动化，模块化不是它的核心。
* webpack 更加强调模块化开发管理，而文件压缩合并、预处理等功能，是它的附带功能。

## webpack 和 node 和 npm 的关系

* webpack 为了可以正常运行，必须依赖 node 环境
* node 环境为了可以正常的执行很多代码，其中必须包含各种依赖的包
* npm（node packges manager）是包管理工具





















































