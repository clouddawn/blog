# 表单与 v-model

## 表单

* 双向绑定是指：修改内存中的变量会使网页中对应的变量变化，而在网页中显示修改变量也会使内存中对应的变量变化。

### Input

* 使用 v-model 实现双向绑定 Input

```html
<template>
  <div id="app">
    <input v-model="message" placeholder="edit me" />
    <p>Message is: {{ message }}</p>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      message: undefined,
    };
  },
};
</script>
```

### textarea

* 类似 input 的方式绑定表单，能够显示更改内存中 message 的值

```html
<textarea v-model="message" placeholder="edit me" />
<p>Message is: {{ message }}</p>
```

### checkbox

* 类似 input，v-model 绑定的容器为数组
* 属性 value 确定选择的值（string），:value 可赋值其他类型

```html
<template>
  <div id="app">
    <input type="checkbox" id="jack" value="Jack" v-model="checkedNames" />
    <label for="jack">Jack</label>
    <input type="checkbox" id="john" value="John" v-model="checkedNames" />
    <label for="john">John</label>
    <input type="checkbox" id="mike" value="Mike" v-model="checkedNames" />
    <label for="mike">Mike</label>
    <br />
    <span>Checked names: {{ checkedNames }}</span>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      checkedNames: [],
    };
  },
};
</script>
```

### radio

* 多个选一个，需要 v-model 绑定同一个变量才能实现几个选项为一组
* 属性 value 确定选择的值（string），:value 可赋值其他类型

```html
<template>
  <div id="app">
    <input type="radio" id="jack" value="Jack" v-model="checkedNames" />
    <label for="jack">Jack</label>
    <input type="radio" id="john" value="John" v-model="checkedNames" />
    <label for="john">John</label>
    <input type="radio" id="mike" value="Mike" v-model="checkedNames" />
    <label for="mike">Mike</label>
    <br />
    <span>Checked names: {{ checkedNames }}</span>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      checkedNames: undefined,
    };
  },
};
</script>
```

### select-option

* 下拉选单，属性 value 确定选择的值（string)，:value 可赋值其他类型

```html
<template>
  <div id="app">
  <select v-model="selected">
    <option disabled value="">请选择</option>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <span>Selected: {{ selected }}</span>
</div>
    
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      selected: undefined,
    };
  },
};
</script>
```

* 还可以使用 v-for 写成数组的形式

```html
<template>
  <div id="app">
    <select v-model="selected">
      <option disabled value="">请选择</option>
      <option v-for="(u, index) in selectArr" :key="index" :value="u.value">
        {{ u.id }}
      </option>
    </select>
    <span>Selected: {{ selected }}</span>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      selected: undefined,
      selectArr: [
        { id: "A", value: "A-Jack" },
        { id: "B", value: "B-Bob" },
        { id: "C", value: "C-Mike" },
      ],
    };
  },
};
</script>
```

* 在 select 标签加入 multiple 属性，v-model 绑定一个数组可实现多选

### form

* form 表单含若干 input 和一个 submit button
* 让用户按回车时提交表单并刷新页面
* 可用 @submit.prevent = 'fn' 监听并阻止提交表单和刷新页面并执行 fn

```html
<template>
  <div id="app">
    <form @submit.prevent="onSubmit">
      <h2>Sign In</h2>
      <label>
        <span>用户名：</span>
        <input
          v-model="user.username"
          type="text"
          placeholder="please input user name"
        />
      </label>
      <br />
      <label>
        <span>密码：</span>
        <input
          v-model="user.password"
          type="password"
          placeholder="please input pwd"
        />
      </label>
      <br />
      <br />
      <button type="submit">登录</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      user: {
        username: "",
        password: "",
      },
    };
  },
  methods: {
    onSubmit() {
      console.log(
        `username is ${this.user.username}, pwd is ${this.user.password}`
      );
    },
  },
};
</script>
```

## 三个 v-model 的修饰符

### .lazy

* input 事件：通过鼠标、键盘等任何输入设备进行输入时触发
* change 事件：input 结束，元素失去焦点时触发
* .lazy 使得在 input 结束，change 时才触发内存更新，而不是每次用户输入内存就立即更新 ---> 适合大量文字不频繁更新的文本框

### .number

* v-model 绑定变量为数字类型时使用，会自动 parseInt 取有效数字（前面的 0 去掉）

### .trim

* 将字符串前后的空格去掉

## v-model

### 原理

* 双向绑定原理：将 value 属性绑定一个变量，再监听 input 事件用接收到的 value 改变绑定变量的值

```html
v-model = "x" 
// 等价于
<input :value="x" @input="x = $event.target.value" />
```

* 下面这个例子可以看出 v-model 是监听 input 事件 $event（value），并对应更改内存中的绑定变量

App.vue

```html
<template>
  <div id="app">
    New Message: {{ message }}
    <hr />
    <NewInput v-model="message" />
  </div>
</template>

<script>
import NewInput from "./components/NewInput.vue";
export default {
  name: "App",
  components: { NewInput },
  data() {
    return {
      message: "",
    };
  },
};
</script>
```

NewInput.vue

```html
<template>
  <input :value="value" @input="OnInput" />
</template>

<script>
export default {
  props: {
    value: {
      type: String,
    },
  },
  methods: {
    OnInput(e) {
      this.$emit("input", e.target.value);
    },
  },
};
</script>
```

### 小结

* 双向绑定是指：用户更改 UI 会引起内存对应数据变化，而修改内存数据也会使对应 UI 发生变化
* v-model 是从 Angular 的 ngModel 借鉴来的
* v-model 本质是 :value 和 @input 的语法糖
* v-model="x" 等价于：

原生组件

```html
<input :value="x" @input="x = $event.target.value" />
```

自定义组件：自定义组件需使用 $emit

```html
<input :value="x" @input="x = $event" />
```

























