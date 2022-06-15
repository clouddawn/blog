# webpack 03

## 什么是 loader？

* loader 是 webpack 中一个非常核心的概念。
* 用webpack来处理我们写的js代码，webpack会自动处理js之间相关的依赖。
* 但是，在开发中不仅仅有基本的js代码需要处理，也需要加载css、图片，还包括一些高级的将ES6转成ES5代码，将TypeScript转成ES5代码，将scss、less转成css，将.jsx、.vue文件转成js文件等等。
* webpack 本身对于这些转化是不支持的。
* 那怎么办呢？给webpack扩展对应的loader就可以啦。
* loader使用过程：
  步骤一：通过 npm 安装需要使用的 loader；
  步骤二：在 webpack.config.js 中的 module 关键字下进行配置。

## css 文件处理

```js
// webpack.config.js
const path = require("path");

module.exports = {
  entry: "./src/main.js",
  output: {
    path: path.resolve(__dirname,'./dist'), // __dirname 当前文件所在目录
    filename:'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [ 'style-loader', 'css-loader' ]
        // css-loader 只负责将 css 文件进行加载
        // style-loader 负责将样式添加到 DOM 中
        // 使用多个 loader 时，是从右向左
      }
    ]
  }
};
```

## less 文件处理

```js
// webpack.config.js
module.exports = {
    ...
    module: {
        rules: [{
            test: /\.less$/,
            use: [{
                loader: "style-loader" 
            }, {
                loader: "css-loader" 
            }, {
                loader: "less-loader" 
            }]
        }]
    }
};
```

## 图片文件处理

```js
const path = require("path");

module.exports = {
  entry: "./src/main.js",
  output: {
    path: path.resolve(__dirname,'./dist'), // __dirname 当前文件所在目录
    filename:'bundle.js',
    publicPath:'dist/'
  },
  module: {
    rules: [
      {
        test: /\.(png|jpg|gif)$/,
        use: [
          {
            loader: 'url-loader',
            options: {
              limit: 8192 // 小于8KB对图片进行base64编码
            }
          }
        ]
      }
    ]
  }
};
```

### 修改文件名称

```js
811d5b6450efd532dd415235501239ec.jpg
```

webpack 自动帮我们生成了一个非常长的名字，这是一个32位hash值，目的是防止名字重复。

但是，真实开发中，我们可能对打包的图片名字有一定的要求。

比如，将所有的图片放到一个文件夹中，跟上图片原来的名称，同时也要防止重复。

所以，我们可以在 options 中添加上如下选项：

* img ：文件要打包到的文件夹
* name：获取图片原来的名字，放在该位置
* hash:8 为了防止图片名称冲突，依然使用 hash ，但是只保留 8 位
* ext：使用图片原来的扩展名

```js
{
    test: /\.(png|jpg|gif)$/,
        use: [
            {
                loader: 'url-loader',
                options: {
                    limit: 8192,
                    name: 'img/[name].[hash:8].[ext]'
                }
            }
        ]
}
```

### ES6 语法处理

```
npm install --save-dev babel-loader@7.1.5 babel-core@6.26.3 babel-preset-es2015@6.24.1
```

-

```js
// webpack.config.js
{
    test: /\.js$/,
        exclude: /(node_modules|bower_components)/,
            use: {
                loader: 'babel-loader',
                    options: {
                        presets: ['es2015']
                    }
            }
}
```































