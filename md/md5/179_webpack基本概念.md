# webpack 的5个基本概念

本质上，webpack 是一个现代 JS 应用程序的静态模块打包器。当 webpack 处理应用程序时，它会递归地构建一个依赖关系图，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 bundle。

## 入口（entry）

入口起点（entry point）指示 webpack 应该使用哪个模块，来作为构建其内部依赖图的开始。进入入口起点后，webpack 会找出有哪些模块和库是入口起点（直接和间接）依赖的。

每个依赖项随即被处理，最后输出到称之为 bundles 的文件中。

可以通过配置 `entry` 属性，来指定一个入口起点（或多个入口起点）。默认值为 `./src`。

```js
// webpack.config.js
module.exports = {
    entry:'./path/to/my/entry/file.js'
}
```

## 出口（output）

output 属性告诉 webpack 在哪里输出它所创建的 bundles，以及如何命名这些文件，默认值为 `./dist`。基本上，整个应用程序结构，都会被编译到指定输出路径的文件夹中。你可以通过在配置中指定一个 `output` 字段，来配置这些处理过程：

```js
// webpack.config.js
const path = require('path'); // path 是一个 Node.js 核心模块，用于操作文件路径
moudule.exports = {
    entry: './path/to/my/entry/file.js',
    output:{
    	path: path.resolve(__dirname, 'dist'),
    	filename: 'my-first-webpack.bundle.js'
    }
}
```

## loader

loader 让 webpack 能够去处理那些非 JS 文件（webpack 自身只理解 JS）。loader 可以将所有类型的文件转换为 webpack 能够处理的有效模块，然后你就可以利用 webpack 的打包能力，对它们进行处理。

本质上，webpack loader 将所有类型的文件，转换为应用程序的依赖图（和最终的 bundle）可以直接引用的模块。

```js
// webpack.config.js
const path = require('path');
const config = {
  output: {
    filename: 'my-first-webpack.bundle.js'
  },
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
        // test 属性，用于标识出应该被对应的 loader 进行转换的某个或某些文件
        // use 属性，表示进行转换时，应该使用哪个 loader
    ]
  }
};

module.exports = config;
```

## 插件（plugins）

loader 被用于转换某些类型的模块，而插件则可以用于执行范围更广的任务，例如打包优化和压缩，以及重新定义环境中的变量。插件接口功能极其强大，可以用来处理各种各样的任务。

想要使用一个插件，你只需要 `require()` 它，然后把它添加到 `plugins` 数组中。多数插件可以通过选项（option）自定义。你也可以在一个配置文件中因为不同目的而多次使用同一个插件，这时就需要使用 `new` 操作符来创建它的一个实例。

```js
// webpack.config.js
const HtmlWebpackPlugin = require('html-webpack-plugin'); // 通过 npm 安装
const webpack = require('webpack'); // 用于访问内置插件

const config = {
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};

module.exports = config;
```

## 模式（mode）

通过选择 `development` 或 `production` 之中的一个，来设置 `mode` 参数，可以启用相应模式下的 webpack 内置的优化

```js
module.exports = {
    mode: `production`
}
```































