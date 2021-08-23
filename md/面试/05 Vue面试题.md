# Vue 

1. watch 和 computed 和 methods 区别是什么？

   watch 是监听数据，computed 是计算属性，methods 是方法。

   1. computed 和 methods 相比，最大区别是 computed 有缓存：如果 computed 属性依赖的属性没有变化，那么 computed 属性就不会重新计算。methods 则是看到一次计算一次。
   2. watch 和 computed 相比，computed 是计算出一个属性，而 watch 则可能是做别的事情，如上报数据。

2. 必考：Vue 有哪些生命周期钩子函数？分别有什么用？

   created  在创建组件之后做一些事情

   beforeCreate  在创建组件之前做一些事情

    mounted  在挂载组件之后做一些事情，可以进行数据请求

   beforeMount  在挂载组件之前做一些事情

   updated  在更新组件之后做一些事情

   beforeUpdate  在更新组件之前做一些事情

   destroyed    在组件毁灭之后做一些事情

   beforeDestory    在组件毁灭之前做一些事情

3. 必考：Vue 如何实现组件间通信？

   1. 父子组件：使用 v-on 通过事件通信
   2. 爷孙组件：使用两次 v-on 通过爷爷爸爸通信，爸爸儿子通信实现爷孙通信
   3. 任意组件：使用 eventBus = new Vue() 来通信，eventBus.$on 和 eventBus.$emit 是主要API
   4. 任意组件：使用 Vuex 通信

4. 必考：Vue 数据响应式怎么做到的？

   1. 答案在文档《[深入响应式原理](https://cn.vuejs.org/v2/guide/reactivity.html)》
   2. 要点
      1. 使用 Object.defineProperty 把这些属性全部转为 getter/setter
      2. Vue 不能检测到对象属性的添加或删除，解决方法是手动调用 Vue.set 或者 this.$set

5. 必考：Vue.set 是做什么用的？
   见上一题

6. Vuex 你怎么用的？

   1. 背下文档第一句：Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式
   2. 说出核心概念的名字和作用：State/Getter/Mutation/Action/Module

7. VueRouter 你怎么用的？

   1. 背下文档第一句：Vue Router 是 Vue.js 官方的路由管理器。

   2. 说出核心概念的名字和作用：History 模式/导航守卫/路由懒加载

   3. 说出常用 API：router-link/router-view/this.$router.push/this.$router.replace/this.$route.params

      ```js
       this.$router.push('/user-admin')
       this.$route.params
      ```

8. 路由守卫是什么？
   看官方文档的例子，背里面的关键的话



9. Vue 双向绑定 v-model





。。。28~