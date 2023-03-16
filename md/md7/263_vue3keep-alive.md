# keep-alive

* 默认情况下，在切换组件后，原组件会被销毁掉，再次回来时会重新创建组件；
* 但是，某些情况希望继续保持组件的状态，而不是销毁，这个时候就可以使用一个内置组件：keep-alive。

```html
<keep-alive include="MeiChangSu,MengZhi">
    <component :is="currentTab" :name="names[currentTab]"></component>
</keep-alive>
```

## 属性

* `include - string | RegExp | Array`。只有名称匹配的组件会被缓存；
* `exclude - string | RegExp | Array`。任何名称匹配的组件都不会被缓存；
* `max - number | string`。最多可以缓存多少组件实例，一旦达到这个数字，那么缓存组件中最近没有被访问的实例会被销毁；
* `include` 和 `exclude` 允许组件有条件地缓存：
  * 二者都可以用逗号分隔字符串、正则表达式或一个数组来表示；
  * 匹配首先检查组件自身的 name 选项；

```html
<keep-alive include="a,b">
  <component :is="view" />
</keep-alive>

<keep-alive :include="/a|b/">
  <component :is="view" />
</keep-alive>

<keep-alive :include="['a', 'b']">
  <component :is="view" />
</keep-alive>
```

## 缓存组件的生命周期

* 对于缓存的组件来说，再次进入时，是**不会执行 created 或者 mounted 等生命周期函数**的： 
  * 但是有时候确实需要监听到何时重新进入到了组件，何时离开了组件； 
  * 这个时候我们可以使用 `activated` 和 `deactivated` 这两个生命周期钩子函数来监听；

```js
activated() {
  console.log('悄悄地，我来了');
},
deactivated() {
  console.log('悄悄地，我走了');
}
```

## Webpack的代码分包

* 默认的打包过程：
  * 默认情况下，在构建整个组件树的过程中，因为组件和组件之间是通过模块化直接依赖的，那么 webpack 在打包时就会将组
    件模块打包到一起（比如一个 app.js 文件中）；
  * 这个时候随着项目的不断庞大，app.js 文件的内容过大，会造成首屏的渲染速度变慢；
* 打包时，代码的分包：
  * 所以，对于一些不需要立即使用的组件，我们可以单独对它们进行拆分，拆分成一些小的代码块 chunk.js；
  * 这些 chunk.js 会在需要时从服务器加载下来，并且运行代码，显示对应的内容；

```js
import("./utils/math.js").then(({sum}) => {
  console.log(sum(9, 9));
});
```

## Vue中实现异步组件

* 如果我们的项目过大了，对于某些组件我们希望通过异步的方式来进行加载（目的是可以对其进行分包处理），那么 Vue 中给我们提供了一个函数：`defineAsyncComponent`。
* `defineAsyncComponent` 接受两种类型的参数：
  * 类型一：工厂函数，该工厂函数需要返回一个 Promise 对象；
  * 类型二：接受一个对象类型，对异步函数进行配置；

* 类型一的写法

  ```js
  import {defineAsyncComponent} from "vue";
  const MengZhi = defineAsyncComponent(() => import("./components/MengZhi.vue"))
  ```

* 类型二的写法

  ```js
  import {defineAsyncComponent} from "vue";
  
  const MengZhi = defineAsyncComponent({
    // 工厂函数
    loader: () => import("./components/MengZhi.vue"),
    // 加载过程中显示的组件
    loadingComponent: Loading,
    // 加载失败时显示的组件
    errorComponent: Error,
    // 在显示 loadingComponent 之前的延迟 | 默认值：200（单位：ms）
    delay: 1000
  });
  ```

## 异步组件和Suspense

* **Suspense是一个内置的全局组件，该组件有两个插槽：** 
  * `default`：如果 `default` 可以显示，那么显示 `default` 的内容； 
  * `fallback`：如果 `default` 无法显示，那么会显示 `fallback` 插槽的内容；

```html
<Suspense>
    <template #default>
        <AsyncHome />
    </template>
    <template #fallback>
        <Loading />
    </template>
</Suspense>
```

## $refs 的使用

* 某些情况下，我们在组件中想要直接获取到元素对象或者子组件实例：
  * 在 Vue 开发中我们是不推荐进行 DOM 操作的；
  * 这个时候，我们可以给元素或者组件绑定一个 ref 的 attribute 属性；
* 组件实例有一个$refs属性：
  * 它一个对象Object，持有注册过 ref attribute 的所有 DOM 元素和组件实例。























