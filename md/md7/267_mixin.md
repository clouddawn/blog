# mixin

* 使用组件化的方式开发Vue应用程序，组件和组件之间有时候会存在相同的代码逻辑，如何实现对相同的代码逻辑进行抽取呢？
* 在Vue2和Vue3中都支持的一种方式就是使用Mixin来完成：
  * Mixin提供了一种非常灵活的方式，来分发Vue组件中的可复用功能；
  * 一个Mixin对象可以包含任何组件选项；
  * 当组件使用Mixin对象时，所有Mixin对象的选项将被「混合」进入该组件本身的选项中；

* About.vue

```html
<template>
  <div>
    <h2>About</h2>
    <ul>
      <li v-for="item in names">{{ item }}</li>
    </ul>
  </div>
</template>

<script>
import namesMixin from "../mixins/names-mixin.js";

export default {
  mixins: [namesMixin],
  data() {
    return {
      names: ["王传君", "王鸥", "王千源"]
    };
  },
  mounted() {
    this.sayHello();
  },
  methods: {
    sayHello() {
      console.log("我是about-say-hello");
    }
  }
};
</script>
```

* names-mixin.js

```js
export default {
  data() {
    return {
      names: ["刘谦", "刘涛", "刘诗诗", "刘德华", "刘烨"]
    };
  },
  mounted() {
    console.log("names-mixin");
  },
  methods: {
    sayHello() {
      console.log("我是names-mixin");
    }
  }
};
```

## mixin 的合并规则

* 如果Mixin对象中的选项和组件对象中的选项发生了冲突，那么Vue会如何操作呢？
  * 这里分成不同的情况来进行处理；
* 情况一：如果是data函数的返回值对象
  * 返回值对象默认情况下会进行合并；
  * 如果data返回值对象的属性发生了冲突，那么会保留组件自身的数据；
* 情况二：如果是生命周期钩子函数
  * 生命周期的钩子函数会被合并到数组中，都会被调用；
* 情况三：值为对象的选项，例如 methods、components 和 directives，将被合并为同一个对象。
  * 比如都有methods选项，并且都定义了方法，那么它们都会生效；
  * 但是如果对象的key相同，那么会取组件对象的键值对；

## 全局混入mixin

* 如果组件中的某些选项，是所有的组件都需要拥有的，那么这个时候我们可以使用全局的mixin：
  * 全局的Mixin可以使用 应用app的方法 mixin 来完成注册；
  * 一旦注册，那么全局混入的选项将会影响每一个组件；

```js
import {createApp} from "vue";
import App from "./App.vue";

const app = createApp(App)

app.mixin({
  created() {
    console.log("global mixin created");
  }
});

app.mount("#app");
```























