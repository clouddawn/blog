# v-for

我们可以用`v-for`指令基于一个数组来渲染一个列表。`v-for`指令需要使用`item in items`形式的特殊语法，其中`items`是源数据数组，而`item`则是被迭代的数组元素的别名。

```html
    <ul id="example-1">
      <li v-for="item in items":key="item.name">{{ item.name}}</li>
    </ul>

    <script>
      var example1 = new Vue({
        el: "#example-1",
        data: {
          items: [{ message: "Foo" }, { message: "Bar" },{
              name:"姜大牙"
          },{name:"陈墨涵"}],
        },
      });
    </script>
```

## key

* 预期：`number | string | boolean | symbol`

* `key`的特殊`attribute`主要用在 Vue 的虚拟 DOM 算法，在新旧 nodes 对比时辨识 VNodes。
* 如果不使用 `key`，Vue 会使用一种最大限度减少动态元素并且尽可能的尝试就地修改/复用相同类型元素的算法。
* 而使用`key`时，它会基于`key`的变化重新排列元素顺序，并且会移除`key`不存在的元素。
* 有相同父元素的子元素必须有独特的`key`，重复的`key`会造成渲染错误。

```html
<ul>
  <li v-for="item in items" :key="item.id">...</li>
</ul>
```

* 它也可以用于强制替换元素/组件而不是重复使用它，当遇到如下场景是它可能会很有用：
  * 完整地触发组件的生命周期钩子
  * 触发过渡

```html
<transition>
  <span :key="text">{{ text }}</span>
</transition>
```

* 当`text`发生改变时，`<span>`总是会被替换而不是被修改，因此会触发过渡。



https://codesandbox.io/s/competent-https-i33hk?file=/src/main.js































