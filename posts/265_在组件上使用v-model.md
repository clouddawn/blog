## 组件的 v-model

* 前面我们在 `input` 中可以使用 `v-model` 来完成双向绑定：
  * 这个时候往往会非常方便，因为 `v-model` 默认帮助我们完成了两件事；
  * `v-bind:value` 的数据绑定和 `@input` 的事件监听；
*  如果我们现在封装了一个组件，其他地方在使用这个组件时，是否也可以使用 `v-model` 来同时完成这两个功能呢？
  * 也是可以的，vue 也支持在组件上使用 `v-model`；
* 当我们在组件上使用的时候，等价于如下的操作：
  * 我们会发现和 `input` 元素不同的只是属性的名称和事件触发的名称而已；

```html
<Form v-model="message"></Form>
<!-- 相当于 -->
<Form :modelValue="message" @update:model-value="message = $event"></Form>
```

## 组件 v-model 的实现

```html
<!--Form.vue-->
<template>
  <div>
    <input type="text" :value="modelValue" @input="send_message">
  </div>
</template>

<script>
export default {
  name: "Form",
  props: ["modelValue"],
  emits: ["update:model-value"],
  methods: {
    send_message(event) {
      this.$emit("update:model-value", event.target.value);
    }
  }
};
</script>
```

## computed 实现

* 我们依然希望在组件内部按照双向绑定的做法去完成，应该如何操作呢？
  * 可以使用计算属性的 setter 和 getter 来完成。

```html
<!--Form.vue-->
<template>
  <div>
    <input type="text" v-model="cmodelValue">
  </div>
</template>

<script>
export default {
  name: "Form",
  props: ["modelValue"],
  computed: {
    "cmodelValue": {
      set(value) {
        this.$emit("update:model-value", value);
      },
      get() {
        return this.modelValue;
      }
    }
  },
  emits: ["update:model-value"]
};
</script>
```

## 绑定多个属性

* 我们现在通过 v-model 是直接绑定了一个属性，如果我们希望绑定多个属性呢？
  * 也就是我们希望在一个组件上使用多个 v-model 是否可以实现呢？
  * 默认情况下的 `v-model` 其实是绑定了 `modelValue` 属性和 `@update:modelValue` 的事件；
  * 如果我们希望绑定更多，可以给 v-model 传入一个参数，那么这个参数的名称就是我们绑定属性的名称；
* 注意：这里绑定了两个属性

```html
<Form v-model="message" v-model:title="title"></Form>
```

* `v-model:title`  相当于做了两件事：
  * 绑定了 `title` 属性；
  * 监听了 `@update:title` 的事件；

```html
<!--Form.vue-->
<template>
  <div>
    <input type="text" v-model="cmodelValue">
    <input type="text" v-model="ctitle">
  </div>
</template>

<script>
export default {
  name: "Form",
  props: ["modelValue", "title"],
  computed: {
    "cmodelValue": {
      set(value) {
        this.$emit("update:model-value", value);
      },
      get() {
        return this.modelValue;
      }
    },
    ctitle: {
      set(value) {
        this.$emit("update:title", value);
      },
      get() {
        return this.title;
      }
    }
  },
  emits: ["update:model-value", "update:title"],
};
</script>
```



































