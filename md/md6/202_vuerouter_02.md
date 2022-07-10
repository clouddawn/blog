# vue router 02

## router-link

* 使用 `router-link` 组件进行导航
* 通过 `to` 来指定链接
* `router-link` 将呈现一个带有正确 `href` 属性的 `<a>` 标签
* 使用 `router-link` 可以在不重新加载页面的情况下更改 URL，处理 URL 的生成以及编码。 

## router-view

* `router-view` 将显示与 url 对应的组件

## 安装和使用vue-router

### 安装

```
npm install vue-router --save
```

### 使用

* 在模块化工程中使用它（因为是一个插件, 所以可以通过Vue.use() 来安装路由功能）

  * 第一步：导入路由对象，并且调用 Vue.use(VueRouter)
  * 第二步：创建路由实例，并且传入路由映射配置
  * 第三步：在Vue实例中挂载创建的路由实例

  ```js
  import Vue from 'vue';
  import VueRouter from 'vue-router';
  
  Vue.use(VueRouter);
  ```

* 使用 vue-router 的步骤:

  * 第一步: 创建路由组件
  * 第二步: 配置路由映射: 组件和路径映射关系
  * 第三步: 使用路由: 通过`<router-link>`和`<router-view>`

```js
// router/index.js

import Vue from "vue";
import VueRouter from "vue-router";
// 注入插件
Vue.use(VueRouter);
// 定义路由
const routes = [
  {
    path: "/",
    redirect:'/about'
  },
  {
    path: "/hello",
    component: () => import("../components/HelloWorld.vue")
  },
  {
    path: "/about",
    component: () => import("../components/About.vue")
  }
];
// 创建 router 实例
const router = new VueRouter({
  routes,
});
// 到处 router 实例
export default router;
```

### 挂载到 Vue 实例中

```js
// main.js
import Vue from 'vue'
import App from './App'
import router from './router'

Vue.config.productionTip = false

new Vue({
  el: '#app',
  router,
  render: h => h(App)
})
```

### 使用路由

```vue
<template>
  <div id="app">
    <h1>我是网站的标题</h1>
    <router-link to="/about">about</router-link>
    <router-link to="/hello">hello</router-link>
    <router-view/>
    <p>我是网站的版权信息</p>
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>
```

* `router-link` 
  * 该标签是一个 `vue-router` 中已经内置的组件，它会被渲染成一个 `<a>` 标签。
* `router-view` 
  * 该标签会根据当前的路径，动态渲染出不同的组件
* 网页的其他内容，比如顶部的标题/导航，或者底部的一些版权信息等会和 `<router-view>` 处于同一个等级。
* 在路由切换时，切换的是 `<router-view>` 挂载的组件，其他内容不会发生改变。

### 路由的默认路径

* 默认情况下, 进入网站的首页, 我们希望 `<router-view>` 渲染首页的内容，需要多配置一个映射。

```js
const routes = [
    {
        path:"/",
        redirect:'/home'
    }
]
```

* path 配置的是根路径: /
* redirect 是重定向, 也就是我们将根路径重定向到 /home 的路径下。

### HTML5 的 History 模式

* 改变路径的方式有两种：
  * URL 的 hash
  * HTML5 的 history
  * 默认情况下，路径的改变使用的是 URL 的 hash

* 如果希望使用 HTML5 的 history 模式，进行如下配置即可：

```js
const router = new VueRouter({
    routes,
    mode:'history'
})
```

### router-link 补充

* `tag`
  * 指定 `<router-link>` 之后渲染成什么组件，比如下面的代码会被渲染成一个 `<li>` 元素，而不是 `<a>`
* `replace`
  * 不会留下 `history` 记录，所以指定 `replace` 的情况下，不能返回到上一个页面
* `active-class` 当 `<router-link>` 对应的路由匹配成功时，会自动给当前元素设置一个 `router-link-active` 的 `class`，设置 `active-class` 可以修改默认的名称
  * 在进行高亮显示的导航菜单或者底部 tabbar 时，会使用到该类
  * 但是通常不会修改类的属性，会直接使用默认的 router-link-active 

```vue
<template>
  <div id="app">
    <h1>我是网站的标题</h1>
    <router-link to="/about" tag="span" replace active-class="active">about</router-link>
    <router-link to="/hello" replace>hello</router-link>
    <router-view/>
    <p>我是网站的版权信息</p>
  </div>
</template>
```

* `router-link-active` 具体的名称也可以通过 `router` 实例的属性进行修改

```js
const router = new VueRouter({
  routes,
  mode:'history',
  linkActiveClass:'active'
});
```























