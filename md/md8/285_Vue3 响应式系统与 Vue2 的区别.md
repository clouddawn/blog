# Vue3 响应式系统与 Vue2 的区别？

Vue3响应式系统使用 Proxy 代替 Vue2 的 `Object.defineProperty`，能监听对象新增和删除属性，数组变化也能自动追踪，性能更好，初始化和更新更快。



## 1. 响应实现方式

* Vue2 使用 `Object.defineProperty` ，需要递归为每个属性定义 `getter/setter` ，无法监听新增或删除属性。
* Vue3 使用 Proxy 拦截对象操作（`get`、`set`、`deleteProperty` 等），可监听新增/删除属性，依赖追踪更精准。

## 2. 性能差异

* Vue3 Proxy 更轻量，初始化和更新性能比 Vue2 高。
* Vue2 对数组方法进行了单独拦截， Vue3 可以直接监听索引和长度变化。

## 3. 数组和对象处理

* Vue2 数组变化只能通过方法拦截（push、pop、splice），新增对象属性需要 `Vue.set`。
* Vue3 可以直接修改对象或数组，视图会自动更新。

