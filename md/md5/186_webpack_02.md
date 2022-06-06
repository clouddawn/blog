# webpack 02

## webpack 安装

* 安装 webpack 首先需要安装 node.js，node.js 自带了软件包管理工具 npm

* 全局安装 webpack（3.6.0）

  ```
  npm install webpack@3.6.0 -g
  ```

* 局部安装 webpack

  ```
  cd 对应目录
  npm install webpack@3.6.0 --save-dev
  ```

  * `--save-dev` 是开发时依赖，项目打包后不需要继续使用的。

* 为什么全局安装后，还需要局部安装呢？
  * 在终端直接执行 webpack 命令，使用的全局安装的 webpack
  * 当在 package.json 中定义了 scripts 时，其中包含了 webpack 命令，那么使用的是局部 webpack

## 文件和文件夹解析

* **dist文件夹**：用于存放之后打包的文件
* **src文件夹**：用于存放我们写的源文件
  * main.js：项目的入口文件。
  * mathUtils.js：定义了一些数学工具函数，可以在其他地方引用，并且使用。
* index.html：浏览器打开展示的首页html
* package.json：通过npm init生成的，npm包管理的文件

[点击查看源码](https://github.com/clouddawn/webpack_-/tree/main/01_wepack%E8%B5%B7%E6%AD%A5)

## JS 文件的打包

* 现在的 JS 文件中使用了模块化的方式进行开发，他们可以直接使用吗？不可以。

  * 如果直接在 index.html 引入这两个 JS 文件，浏览器并不能识别其中的模块化代码。
  * 另外，当项目中有许多这样的 JS 文件时,一个个引用非常麻烦，并且后期非常不方便对它们进行管理。

* 我们应该怎么做呢？使用 webpack 工具，对多个 js 文件进行打包。

  * webpack就是一个模块化的打包工具，可以对模块化的代码进行处理。
  * 另外，如果在处理完所有模块之间的关系后，将多个js打包到一个js文件中，引入时就变得非常方便了。

* OK，如何打包呢？使用webpack的指令即可

  ```
  webpack src/main.js dist/bundle.js
  ```

* 打包后会在dist文件下，生成一个bundle.js文件
  * bundle.js文件，是webpack处理了项目直接文件依赖后生成的一个js文件，我们只需要将这个js文件在index.html中引入即可

## 入口和出口

如果每次使用 webpack 的命令都需要写上入口和出口作为参数，非常麻烦，可以创建一个 webpack.config.js 文件，将这两个参数写到配置中，在运行时，直接读取。

```js
const path = require("path");

module.exports = {
  // 入口：可以是字符串/数组/对象
  entry: "./src/main.js",
  // 出口：通常是一个对象，里面至少包含两个重要属性，path 和 filename
  output: {
    path: path.resolve(__dirname,'./dist'), 
    // 注意：paht 通常是一个绝对路径
    // __dirname 当前文件所在目录
    filename:'bundle.js'
  }
};
```

## 局部安装 webpack

* 目前，我们使用的webpack是全局的webpack，如果我们想使用局部来打包呢？

  * 因为一个项目往往依赖特定的webpack版本，全局的版本可能很这个项目的webpack版本不一致，导出打包出现问题。
  * 所以通常一个项目，都有自己局部的webpack。

* 第一步，项目中需要安装自己局部的webpack

  ```
  npm install webpack@3.6.0 --save-dev
  ```

* 第二步，通过 node_modules/.bin/webpack 启动 webpack 打包

  ```
  node_modules/.bin/webpack
  ```

## package.json 中定义启动

* 但是，每次执行都敲这么一长串太不方便了，我们可以在package.json 的 scripts 中定义自己的执行脚本。

* package.json 中的 scripts 的脚本在执行时，会按照一定的顺序寻找命令对应的位置。

  * 首先，会寻找本地的 node_modules/.bin 路径中对应的命令。

  * 如果没有找到，会去全局的环境变量中寻找。

  * 那如何执行 build 指令呢？

    ```
    npm run build
    ```

    























