# Pinia

* Pinia（发音为/piːnjʌ/，如英语中的“peenya”）是最接近piña（西班牙语中的菠萝）的词；
  * Pinia 开始于大概 2019 年，最初是作为一个实验为 Vue 重新设计状态管理，让它用起来像组合式 API（Composition API）。
  * 从那时到现在，最初的设计原则依然是相同的，并且目前同时兼容Vue2、Vu e3，也并不要求你使用 Composition API；
  * Pinia 本质上依然是一个状态管理的库，用于跨组件、页面进行状态共享（这点和 Vuex 一样）；

## Pinia 和 Vuex 的区别

* 那么我们不是已经有 Vuex 了吗？为什么还要用 Pinia 呢？
  * Pinia 最初是为了探索 Vuex 的下一次迭代会是什么样子，结合了 Vuex 5 核心团队讨论中的许多想法；
  * 最终，团队意识到 Pinia 已经实现了 Vuex5 中大部分内容，所以最终决定用 Pinia 来替代 Vuex；
  * 与 Vuex 相比，Pinia 提供了一个更简单的 API，具有更少的仪式，提供了 Composition-API 风格的 API；
  * 最重要的是，在与 TypeScript 一起使用时具有可靠的类型推断支持；

* 和 Vuex 相比，Pinia 有很多的优势：
  * 比如 mutations 不再存在：
    * 它们经常被认为**非常冗长**；
    * 他们最初带来了 devtools 集成，但这不再是问题；
  * 更友好的 TypeScript 支持，Vuex 之前对 TS 的支持很不友好；
  * 不再有 modules 的嵌套结构：
    * 可以灵活使用每一个 store，它们是通过扁平化的方式来相互使用的；
  * 也不再有命名空间的概念，不需要记住它们的复杂关系；

## 如何使用 Pinia ？

* 安装

  ```ts
  yarn add pinia
  ```

* 创建一个 pinia 并且将其传递给应用程序：

  ```ts
  // stores/index.ts
  
  import {createPinia} from "pinia";
  
  const pinia = createPinia();
  
  export default pinia;
  ```

  -

  ```ts
  // main.ts
  
  import {createApp} from "vue";
  import App from "./App.vue";
  
  import pinia from "./stores";
  
  createApp(App)
      .use(pinia)
      .mount("#app");
  ```

## 认识 Store

* 什么是 Store？
  * 一个 Store （如 Pinia）是一个实体，它会持有为绑定到你组件树的状态和业务逻辑，也就是保存了全局的状态；
  * 它有点像始终存在，并且每个人都可以读取和写入的组件；
  * 你可以在你的应用程序中定义任意数量的 Store 来管理你的状态；
* Store有三个核心概念：
  * state、getters、actions；
  * 等同于组件的data、computed、methods；
  * 一旦 store 被实例化，你就可以直接在 store 上访问 state、getters 和 actions 中定义的任何属性；

## 定义一个 Store

* Store 是使用 `defineStore()` 定义的， 
  * 并且它需要一个唯一名称，作为第一个参数传递； 

```ts
// stores/counter.ts

import {defineStore} from "pinia";

export const useCounter = defineStore("counter",{
  state(){
    return {
      counter: 10
    }
  }
})
```

* 这个 name，也称为 id，是必要的，Pinia 使用它来将 store 连接到 devtools。
* 返回的函数统一使用 useX 作为命名方案，这是约定的规范；

## 使用定义的 Store

* Store 在它被使用之前是不会创建的，可以通过调用 use 函数来使用Store：

```html
<script setup lang="ts">
import {useCounter} from "../stores/counter";

const counterStore = useCounter();
</script>

<template>
  <h1>{{ counterStore.counter }}</h1>
</template>
```

* 注意 Store 获取到后不能被解构，否则会失去响应式：
  * 为了从 Store 中提取属性同时保持其响应式，您需要使用`storeToRefs()`。

```ts
const {counter} = counterStore; // 不是响应式的
const {counter: counter2} = toRefs(counterStore); // 是响应式的
const {counter: counter3} = storeToRefs(counterStore); // 是响应式的
```

## 认识和定义 State

* state 是 store 的核心部分，因为 store 就是用来管理状态的。
  * 在 Pinia 中，状态被定义为返回初始状态的函数；

```ts
export const useCounter = defineStore("counter",{
  state(){
    return {
      counter: 10,
      name: "王冰冰",
      age: 33
    }
  }
})
```

## 操作 State

* 读取和写入 state：

  * 默认情况下，您可以通过 store 实例访问状态来直接读取和写入状态；

  ```ts
  import {useCounter} from "../stores/counter";
  
  const counterStore = useCounter();
  
  
  function incrementCount() {
    counterStore.counter++;
  }
  
  function changeName() {
    counterStore.name = "谭松韵";
  }
  ```

* 重置 state
  * 可以通过调用 store 上的 `$reset()` 方法将状态重置到其初始值;

  ```ts
  counterStore.$reset()
  ```

* 改变 State：

  * 除了直接用 `store.counter++` 修改 `store`，你还可以调用 `$patch` 方法；
  * 它允许您使用部分“`state`”对象同时应用多个更改；

  ```ts
    counterStore.$patch({
      counter: 100,
      name: "谭松韵"
    });
  ```

* 替换 state
  * 不能完全替换掉 store 的 state，因为那样会破坏其响应性。

  ```ts
  // 这实际上并没有替换`$state`
  store.$state = { count: 24 }
  // 在它内部调用 `$patch()`：
  store.$patch({ count: 24 })
  ```

## 认识和定义 Getters

* Getters 相当于 Store 的计算属性：
  * 它们可以用 `defineStore()` 中的 `getters` 属性定义；
  * `getters` 中可以定义接受一个 `state` 作为参数的函数；

```ts
import {defineStore} from "pinia";

export const useCounter = defineStore("counter",{
  state(){
    return {
      counter: 10,
      name: "王冰冰",
      age: 33
    }
  },
  getters: {
    doubleCounter(){
      return this.counter * 2;
    },
    info(state){
      return `我叫${state.name}，今年${state.age}岁。`
    }
  }
})
```

## 访问 getters

* 访问当前 store 的 getters

  ```ts
  const counterStore = useCounter();
  console.log(counterStore.doubleCounter);
  console.log(counterStore.info);
  ```

* getters 也可以返回一个函数，这样就可以接受参数

```ts
import {defineStore} from "pinia";

export const useCounter = defineStore("counter", {
  state() {
    return {
      users: [
        {
          id: 100, name: "王冰冰", age: 33
        },
        {
          id: 101, name: "撒贝宁", age: 47
        },
        {
          id: 102, name: "尼格买提", age: 40
        }
      ]
    };
  },
  getters: {
    getUserById() {
      return (id: number) => {
        return this.users.find(item => item.id === id);
      };
    }
  }
});
```

-

```html
<template>
  <h1>{{ counterStore.getUserById(101) }}</h1>
</template>
```













































