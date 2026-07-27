# vuex 的 module

* Module是模块的意思, 为什么在Vuex中我们要使用模块呢?
  * Vue使用单一状态树,那么也意味着很多状态都会交给Vuex来管理.
  * 当应用变得非常复杂时，store对象就有可能变得相当臃肿。
  * 为了解决这个问题, Vuex 允许我们将store分割成模块(Module), 而每个模块拥有自己的 state、mutation、action、getters 等。

```js
const moduleA = {
  state: {},
  mutations: {},
  getters: {},
  actions: {}
};

const moduleB = {
  state: {},
  mutations: {},
  getters: {},
  actions: {}
};

export default new Vuex.Store({
  state:{},
  mutations:{},
  getters:{},
  actions:{},
  modules:{
    moduleA,
    moduleB
  }
})
```

* 上面的代码中, 我们已经有了整体的组织结构, 下面我们来看看具体的局部模块中的代码如何书写。
  * 我们在 moduleA 中添加 state、mutations、getters
  * mutation 和 getters 接收的第一个参数是局部状态对象

## state

```js
const moduleA = {
  state: {
    name:'龙文章'
  },
};

export default new Vuex.Store({
  state:{
    name:'孙悟空'
  },
  modules:{
    moduleA,
  }
})
```

.

```html
<template>
  <div>
    <h1>{{$store.state.moduleA.name}}</h1>
  </div>
</template>
```

## mutations

```js
const moduleA = {
  state: {
    name:'龙文章'
  },
  mutations: {
    changeName(state,name){
      state.name = name;
    }
  },
};
```

.

```html
<template>
  <div>
    <h1>{{$store.state.moduleA.name}}</h1>
    <button @click="changeName">改名字</button>
  </div>
</template>

<script>
export default {
  name: "Counter",
  data() {
    return {};
  },
  methods: {
    changeName() {
      this.$store.commit('changeName','孟烦了');
    }
  }
};
</script>
```

## getters

```js
const moduleA = {
  state: {
    name: "龙文章"
  },
  mutations: {
    changeName(state, name) {
      state.name = name;
    }
  },
  getters: {
    fullName(state) {
      return state.name + "-克虏伯";
    },
    fullName2(state, getters) {
      return getters.fullName + "-阿译";
    },
    fullName3(state, getters, rootState) {
      return getters.fullName2 + "-" + rootState.name;
    }
  },
};
```

.

```html
<template>
  <div>
    <h1>{{$store.getters.fullName}}</h1>
    <h1>{{$store.getters.fullName2}}</h1>
    <h1>{{$store.getters.fullName3}}</h1>
    <button @click="changeName">改名字</button>
  </div>
</template>
```

## actions

* 接收一个 context 参数对象
* 局部状态通过 context.state 暴露出来，根节点状态则为 context.rootState

```js
const moduleA = {
  state: {
    name: "龙文章"
  },
  mutations: {
    changeName(state, name) {
      state.name = name;
    }
  },
  actions: {
    aChangeName(context){
      setTimeout(()=>{
        context.commit('changeName','太上老君');
      },1000)
    }
  }
};
```

.

```js
  methods: {
    changeName() {
      this.$store.dispatch('aChangeName','孟烦了');
    }
  }
```





























