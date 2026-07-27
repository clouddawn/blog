# vue cli

* CLI 是 Command-Line Interface, 翻译为命令行界面；
* 我们可以通过 CLI 选择项目的配置，创建出项目；
* Vue CLI 已经内置了 webpack 相关的配置，不需要从零来配置；

## vue cli 安装和使用

* 全局安装，这样在任何时候都可以通过 vue 的命令来创建项目；

  ```js
  npm install @vue/cli -g
  ```

* 升级 Vue CLI：

  * 如果是比较旧的版本，可以通过下面的命令来升级

    ```js
    npm update @vue/cli -g
    ```

* 通过 Vue 的命令来创建项目

  ```js
  vue create 项目的名称
  ```

## vue create 项目的过程

```js
? Please pick a preset: (Use arrow keys)
> Default ([Vue 3] babel, eslint) // 选择vue3版本，并且默认选择babel、eslint
  Default ([Vue 2] babel, eslint) // 选择vue2版本，并且默认选择babel、eslint
  Manually select features // 手动选择希望获取到的特性
```

.

```js
// 选择需要的特性
? Check the features needed for your project: 
>(*) Babel  // 是否选择babel                               
 ( ) TypeScript // 是否使用 typescript
 ( ) Progressive Web App (PWA) Support // 项目是否支持PWA
 ( ) Router  // 是否默认添加Router路由
 ( ) Vuex // 是否默认添加Vuex状态管理
 ( ) CSS Pre-processors // 是否选择CSS预处理器
 (*) Linter / Formatter // 是否选择ESLint对代码进行格式化限制
 ( ) Unit Testing // 是否添加单元测试
 ( ) E2E Testing // 是否添加E2E测试
```

.

```js
// 是否将配置信息放到独立的文件中
? Where do you prefer placing config for Babel, ESLint, etc.? (Use arrow keys)                         
> In dedicated config files
  In package.json  
```





































