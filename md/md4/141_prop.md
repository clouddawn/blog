# Prop

## Prop 的大小写

* HTML 中的 attribute 名是大小写不敏感的，所以浏览器会把所有大写字符解释为小写字符。
* 这意味着当你使用 DOM 中的模板时，camelCase（驼峰命名法）的 prop 名需要使用其等价的 kebab-case（短横线分隔命名）命名：

```js
Vue.component('blog-post', {
  // 在 JavaScript 中是 camelCase 的
  props: ['postTitle'],
  template: '<h3>{{ postTitle }}</h3>'
})
```

```html
<!-- 在 HTML 中是 kebab-case 的 -->
<blog-post post-title="hello!"></blog-post>
```

* 注意，如果你使用字符串模板，那这个限制就不存在了

## Prop 类型

* 到这里，我们只看到了以字符串数组形式列出的 prop:

```js
props: ['title', 'likes', 'isPublished', 'commentIds', 'author']
```

* 但是，通常你希望每个 prop 都有指定的值类型。
* 这时，你可以对形象形式列出 prop，这些 property 的名称和值分别是 prop 各自的名称和类型:

```js
props: {
  title: String,
  likes: Number,
  isPublished: Boolean,
  commentIds: Array,
  author: Object,
  callback: Function,
  contactsPromise: Promise // or any other constructor
}
```

* 这不仅为你的组件提供了文档，还会在它们遇到错误的类型时从浏览器的 JavaScript 控制台提示用户。

## 传递静态或动态 Prop

* 你已经知道了可以像这样给 prop 传入一个静态的值：

```html
<blog-post title="My journey with Vue"></blog-post>
```

* 你也知道 prop 可以通过 `v-bind`动态赋值，例如：

```html
<!-- 动态赋予一个变量的值 -->
<blog-post v-bind:title="post.title"></blog-post>

<!-- 动态赋予一个复杂表达式的值 -->
<blog-post
  v-bind:title="post.title + ' by ' + post.author.name"
></blog-post>
```

* 在上述两个示例中，我们传入的值都是字符串类型的，但实际上任何类型的值都可以传给一个 prop。

#### 传入一个数字

```html
<!-- 即便 `42` 是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
<!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
<blog-post v-bind:likes="42"></blog-post>

<!-- 用一个变量进行动态赋值。-->
<blog-post v-bind:likes="post.likes"></blog-post>
```

#### 传入一个布尔值

```html
<!-- 包含该 prop 没有值的情况在内，都意味着 `true`。-->
<blog-post is-published></blog-post>

<!-- 即便 `false` 是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
<!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
<blog-post v-bind:is-published="false"></blog-post>

<!-- 用一个变量进行动态赋值。-->
<blog-post v-bind:is-published="post.isPublished"></blog-post>
```

#### 传入一个数组

```html
<!-- 即便数组是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
<!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
<blog-post v-bind:comment-ids="[234, 266, 273]"></blog-post>

<!-- 用一个变量进行动态赋值。-->
<blog-post v-bind:comment-ids="post.commentIds"></blog-post>
```

#### 传入一个对象

```html
<!-- 即便对象是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
<!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
<blog-post
  v-bind:author="{
    name: 'Veronica',
    company: 'Veridian Dynamics'
  }"
></blog-post>

<!-- 用一个变量进行动态赋值。-->
<blog-post v-bind:author="post.author"></blog-post>
```

#### 传入一个对象的所有 property

* 如果你想要将一个对象的所有 property 都作为 prop 传入，你可以使用不带参数的 `b-bind`（取代`v-bind:prop-name`）。
* 例如对于一个给定的对象`post`:

```js
post: {
  id: 1,
  title: 'My Journey with Vue'
}
```

* 下面的模板：

```html
<blog-post v-bind="post"></blog-post>
```

* 等价于：

```html
<blog-post
  v-bind:id="post.id"
  v-bind:title="post.title"
></blog-post>
```

## 单向数据流

* 所有的 prop 都使得其父子 prop 之间形成了一个**单向下行绑定**：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。

* 这样会防止子组件意外变更父级组件的状态，从而导致你的应用的数据流向难以理解。

* 额外的，每次父级组件发生变更时，子组件中所有的 prop 都将会刷新为最新的值。

* 这意味着你不应该在一个子组件内部改变 prop。

* 如果你这样做了，Vue 会在浏览器的控制台中发出警告。

* 这里有两种常见的试图变更一个 prop 的情形：

  * 一、这个 prop 用来传递一个初始值：这个子组件接下来希望将其作为一个本地的 prop 数据来使用。
  * 在这种情况下，最好定义一个本地的 data property 并将这个 prop 用作其初始值。

  ```js
  props: ['initialCounter'],
  data: function () {
    return {
      counter: this.initialCounter
    }
  }
  ```

  * 二、这个 prop 以一种原始的值传入且需要进行转换。在这种情况下，最好使用这个 prop 的值来定义一个计算属性：

  ```js
  props: ['size'],
  computed: {
    normalizedSize: function () {
      return this.size.trim().toLowerCase()
    }
  }
  ```

  * 注意在 JavaScript 中对象和数组是通过引用传入的，所以对于一个数组或对象类型的 prop 来说，在子组件中改变变更这个对象或数组本身将会影响到父组件的状态。































