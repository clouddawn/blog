# loader和plugin的区别

* loader是加载器，plugin是插件。
* 加载器就是用来加载文件的，比如 js loader 是用来加载 js 的，把高级的 js 转译成低版本的 js，css loader 是用来加载 css 的。
* 插件是用来加强 webpack 功能的，比如 HtmlWebpackPlugin 是用来加载 Html 的，MiniCssExtractPlugin 可以把多个 CSS 文件合并成一个 CSS 文件。
* 总的来说，加载器主要用来加载文件，而插件的功能更加丰富。