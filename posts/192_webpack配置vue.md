# webpack 配置 vue

## 引入 vue.js

* 我们希望在项目中使用 vue.js，那么必然需要对其有依赖，所以需要先进行安装

  * 因为我们后续是在实际项目中也会使用 vue 的，所以并不是开发时依赖

  ```js
  npm install vue@2.5.21 --save
  ```

* 修改 webpack 的配置，指定版本

  * 默认为 runtime-only ，代码中不可以有任何的 template
  * 需要指定为 runtime-compiler ，代码中可以有 template，有compiler 可以用于编译 template

  ```js
  resolve: {
      alias: {
          'vue$':'vue/dist/vue.esm.js'
      }
  }
  ```

* 安装 vue-loader 和 vue-template-compiler

  ```js
  npm install vue-loader@13.0.0 vue-template-compiler@2.5.21 --save-dev
  ```

  

