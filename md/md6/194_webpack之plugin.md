# webpack 之 plugin

## 认识 plugin

* **plugin 是什么？**
  * plugin 是插件的意思，通常是用于对某个现有的架构进行扩展。
  * webpack 中的插件，就是对 webpack 现有功能的各种扩展，比如打包优化，文件压缩等等。

* **loader 和 plugin 区别**
  * loader 主要用于转化某些类型的模块，它是一个转换器。
  * plugin 是插件，它是对 webpack 本身的扩展，是一个扩展器。
* **plugin 的使用过程**
  * 通过 npm 安装需要使用的 plugins （某些 webpack 已经内置的插件不需要安装）
  * 在 webpack.config.js 中的 plugins 中配置插件。

## 添加版权的 plugin

* 该插件名字叫 BannerPlugin，属于 webpack 自带的插件

```js
const path = require("path");
const webpack = require("webpack");

module.exports = {
  ...,
  module: {
  ...,
  plugins: [
    new webpack.BannerPlugin('最终版权归rebot所有')
  ]
};
```

## 打包 html 的 plugin

* 目前，我们的index.html文件是存放在项目的根目录下的。
  * 真实发布项目时，发布的是dist文件夹中的内容，但是dist文件夹中如果没有index.html文件，那么打包的js等文件也就没有意义了。
  * 所以，我们需要将index.html文件打包到dist文件夹中，这个时候就可以使用HtmlWebpackPlugin插件
* HtmlWebpackPlugin 插件可以为我们做这些事情：
  * 自动生成一个 index.html 文件(可以指定模板来生成)
  * 将打包的 js 文件，自动通过 script 标签插入到 body 中

* 安装HtmlWebpackPlugin插件

  ```
  npm install html-webpack-plugin@3.2.0 --save-dev
  ```

  -

```js
const path = require("path");
const webpack = require("webpack");
const htmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  ...,
  module: {
  ...,
  plugins: [
    new webpack.BannerPlugin('最终版权归rebot所有'),
    new htmlWebpackPlugin({
      template:'index.html'
    })
  ]
};
```

## js 压缩的 plugin

* 在项目发布之前，我们需要对 js 等文件进行压缩处理

  ```
  npm install uglifyjs-webpack-plugin@1.1.1 --save-dev
  ```

-

```js
const path = require("path");
const webpack = require("webpack");
const htmlWebpackPlugin = require("html-webpack-plugin");
const uglifyWebpackPlugin = require("uglifyjs-webpack-plugin");

module.exports = {
  ...,
  module: {
  ...,
  plugins: [
    new webpack.BannerPlugin('最终版权归rebot所有'),
    new htmlWebpackPlugin({
      template:'index.html'
    }),
    new uglifyWebpackPlugin()
  ]
};
```

## 搭建本地服务器

* webpack提供了一个可选的本地开发服务器，这个本地服务器基于node.js搭建，内部使用express框架，可以实现我们想要的让浏览器自动刷新显示我们修改后的结果。

* 不过它是一个单独的模块，在webpack中使用之前需要先安装它

  ```
  npm install --save-dev webpack-dev-server@2.9.1
  ```

* **devserver** 也是作为 webpack 中的一个选项，选项本身可以设置如下属性：

  * **contentBase**：为哪一个文件夹提供本地服务，默认是根文件夹
  * **port**：端口号
  * **inline**：页面实时刷新
  * **historyApiFallback**：在SPA页面中，依赖HTML5的history模式
  * webpack.config.js 文件配置修改如下：

  ```js
    devServer: {
      contentBase:'./dist',
      inline: true,
      port: 9999,
    }
  ```

  * 我们可以再配置另外一个scripts（在 package.json 文件中）：
    * `--open` 参数表示直接打开浏览器

  ```json
  "scripts": {
      "dev": "webpack-dev-server --open"
  },
  ```

  



















