# vuex 的 action

## Action的基本定义

* 我们强调, 不要在 Mutation 中进行异步操作。
  * 但是某些情况, 我们确实希望在 Vuex 中进行一些异步操作, 比如网络请求, 必然是异步的. 这个时候怎么处理呢?
  * Action类似于Mutation, 但是是用来代替Mutation进行异步操作的。

```js
export default new Vuex.Store({
  state: {
    personMessage: {
      name: "孙悟空",
      age: 500,
    }
  },
  mutations: {
    update(state) {
      state.personMessage = {...state.personMessage, "hobby": "吃桃子"};
    }
  },
  actions: {
    aUpdate(context) {
      setTimeout(() => {
          context.commit("update");
        },1000);
    }
  }
});
```

* context 是什么?
  * context 是和 store 对象具有相同方法和属性的对象。
  * 也就是说, 我们可以通过 context 去进行 commit 相关的操作, 也可以获取 context.state 等。
  * 但是注意, 这里它们并不是同一个对象。

## Action的分发

* 在Vue组件中, 如果我们调用action中的方法, 那么就需要使用dispatch

```js
  methods: {
    update() {
      this.$store.dispatch("aUpdate");
    }
  }
```

* 同样的, 也是支持传递payload

```js
  mutations: {
    update(state,payload) {
      state.personMessage = {...state.personMessage, "hobby": payload.hobby};
    }
  },
  actions: {
    aUpdate(context,payload) {
      setTimeout(() => {
          context.commit("update",payload);
        },1000);
    }
  }
```

.

```js
  methods: {
    update() {
      this.$store.dispatch("aUpdate",{"hobby": "吃桃子"});
    }
  }
```

## Action返回的Promise

* 在Action中, 我们可以将异步操作放在一个Promise中, 并且在成功或者失败后, 调用对应的resolve或reject

```js
actions: {
    aUpdate(context,payload) {
      return new Promise((resolve,reject)=>{
        setTimeout(() => {
          context.commit("update",payload);
          resolve();
        },1000);
      })
    }
  }
```

.

```js
methods: {
    update() {
      this.$store.dispatch("aUpdate", {
        "hobby": "吃桃子",
      })
          .then(() => {
            console.log("成功了，开不开心");
          });
    }
  }
```

























