# babel

## babel 是什么？

* Babel 是一个工具链，主要用于旧浏览器或者环境中将 ECMAScript 2015+ 代码转换为向后兼容版本的
   JavaScript；
* 包括：语法转换、源代码转换等；

## babel 的底层原理

* babel 是如何做到将我们的一段代码（ES6、TypeScript、React）转成另外一段代码（ES5）的呢？
  * 从一种源代码（原生语言）转换成另一种源代码（目标语言），这是编译器的工作，事实上我们可以将 babel 看成是一个编译器。
  * Babel 编译器的作用就是将我们的源代码，转换成浏览器可以直接识别的另外一段源代码；
* Babel 也拥有编译器的工作流程：
  * 解析阶段（Parsing）
  * 转换阶段（Transformation）
  * 生成阶段（Code Generation）

## babel 编译器执行原理

* babel 的执行阶段

![image](../images7/248/01.png)

* 当然，这只是一个简化版的编译器工具流程，在每个阶段又会有自己具体的工作：

![image](../images7/248/02.png)



## babel-loader

* 在实际开发中，我们通常会在构建工具中通过配置 babel 来对其进行使用的，比如在 webpack 中。
* 安装相关依赖：

```js
npm install babel-loader @babel/core
```

* 我们可以设置一个规则，在加载 js 文件时，使用我们的 babel：

```js
module: {
    rules: [
        {
            test: /\.m?js$/,
            use: {
                loader: "babel-loader"
            }
        }
    ]
}
```

## 指定使用的插件

* 必须指定使用的插件才会生效

```js
{
    test: /\.m?js$/,
    use: {
        loader: "babel-loader",
        options: {
            plugins: [
                "@babel/plugin-transform-block-scoping",
                "@babel/plugin-transform-arrow-functions"
            ]
        }
    }
}
```

## babel-preset

* 如果我们一个个去安装使用插件，那么需要手动来管理大量的 babel 插件，我们可以直接给 webpack 提供一个  preset，webpack 会根据我们的预设来加载对应的插件列表，并且将其传递给 babel。 

* 比如常见的预设有三个： 
  * env 
  * react 
  * TypeScript 

* 安装 preset-env：

  ```js
  npm install @babel/preset-env
  ```

.

```js
{
    test: /\.m?js$/,
    use: {
        loader: "babel-loader",
        options: {
            presets: [
                ["@babel/preset-env"]
            ]
        }
    }
}
```

## babel 的配置文件

* 像之前一样，我们可以将 babel 的配置信息放到一个独立的文件中，babel 给我们提供了两种配置文件的编写：
  * babel.config.json（或者.js，.cjs，.mjs）文件；
  * babelrc.json（或者.babelrc，.js，.cjs，.mjs）文件；
* 它们两个有什么区别呢？目前很多的项目都采用了多包管理的方式（babel本身、element-plus、umi等）；
  * .babelrc.json：早期使用较多的配置方式，但是对于配置 Monorepos 项目是比较麻烦的；
  * babel.config.json（babel7）：可以直接作用于 Monorepos 项目的子包，更加推荐；

```js
module.exports = {
    presets: [
        ["@babel/preset-env"]
    ]
}
```





























