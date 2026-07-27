# $emit

## `vm.$emit(eventName,[...args])`

### 参数

* `{string} eventName`
* `[...args]`

触发当前实例上的事件，附加参数都会传给监视器回调。

### 示例

* 只配合一个事件使用`$emit`:

```js
Vue.component('welcome-button', {
  template: `
    <button @click="$emit('welcome')">
      Click me to be welcomed
    </button>
  `
})
```

```html
<div id="emit-example-simple">
  <welcome-button @welcome="sayHi"></welcome-button>
</div>
```

```js
new Vue({
  el: '#emit-example-simple',
  methods: {
    sayHi: function () {
      alert('Hi!')
    }
  }
})
```

* 配合额外的参数使用`$emit`:

```js
Vue.component('magic-eight-ball', {
  data: function () {
    return {
      possibleAdvice: ['Yes', 'No', 'Maybe']
    }
  },
  methods: {
    giveAdvice: function () {
      var randomAdviceIndex = Math.floor(Math.random() * this.possibleAdvice.length)
      this.$emit('give-advice', this.possibleAdvice[randomAdviceIndex])
    }
  },
  template: `
    <button v-on:click="giveAdvice">
      Click me for advice
    </button>
  `
})
```

```html
<div id="emit-example-argument">
  <magic-eight-ball v-on:give-advice="showAdvice"></magic-eight-ball>
</div>
```

```js
new Vue({
  el: '#emit-example-argument',
  methods: {
    showAdvice: function (advice) {
      alert(advice)
    }
  }
})
```





























