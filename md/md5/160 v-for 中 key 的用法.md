# v-for 中 key 的用法

我们可以用 `v-for` 指令基于一个数组来渲染一个列表。`v-for` 指令需要使用 `item in items` 形式的特殊语法，其中 `items` 是源数据数组，而 `item` 则是被迭代的数组元素的别名。

为了给 Vue 一个提示，以便它能追踪每个节点的身份，从而重用和重新排序现有元素，需要为每项提供一个唯一 `key` attribute :

```html
<div v-for="item in items" v-bind:key="item.id">
  <!-- 内容 -->
</div>
```

---

```html
<ul id="example-1">
  <li v-for="item in items" :key="item.message">
    {{ item.message }}
  </li>
</ul>
```

-

```js
var example1 = new Vue({
  el: '#example-1',
  data: {
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
```

![image](../images5/162/01.PNG)





















