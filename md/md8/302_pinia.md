# Pinia VS Vuex

Vuex 是 Vue2 时代的官方状态管理方案，而在 Vue3 之后，Vue 官方推荐使用 Pinia 作为新一代状态管理库。

* **API 更简洁：**Pinia 不再强制区分 mutations 和 actions ，代码量更少，上手简单。
* **Pinia 对 TypeScript 支持度更高。**
* **模块化更自然：** 每个 store 独立定义，直接引入即可，不需要复杂的命名空间。

* **调试体验更好：**Pinia 集成 Vue Devtools，支持时间旅行、action 调试、热更新。

所以在新项目中，会优先选择 Pinia，它更轻量、开发体验更好，特别适合 Vue3 + TS 的现代前端项目。