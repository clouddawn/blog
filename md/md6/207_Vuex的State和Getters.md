# Vuex的State和Getters

* Vuex有几个比较核心的概念:
  * State
  * Getters
  * Mutation
  * Action
  * Module

## State单一状态树

* Vuex 提出使用单一状态树, 什么是单一状态树呢？
  * 英文名称是Single Source of Truth，也可以翻译成单一数据源。
* 但是，它是什么呢？我们来看一个生活中的例子。
  * OK，我用一个生活中的例子做一个简单的类比。
  * 我们知道，在国内我们有很多的信息需要被记录，比如上学时的个人档案，工作后的社保记录，公积金记录，结婚后的婚姻信息，以及其他相关的户口、医疗、文凭、房产记录等等。
  * 这些信息被分散在很多地方进行管理，有一天你需要办某个业务时(比如入户某个城市)，你会发现你需要到各个对应的工作地点去打印、盖章各种资料信息，最后到一个地方提交证明你的信息无误。
  * 这种保存信息的方案，不仅仅低效，而且不方便管理，以及日后的维护也是一个庞大的工作(需要大量的各个部门的人力来维护)。
* 这个和我们在应用开发中比较类似：
  * 如果你的状态信息是保存到多个Store对象中的，那么之后的管理和维护等等都会变得特别困难。
  * 所以Vuex也使用了单一状态树来管理应用层级的全部状态。
  * 单一状态树能够让我们用最直接的方式找到某个状态的片段，而且在之后的维护和调试过程中，也可以非常方便的管理和维护。

## Getters基本使用

* 有时候，我们需要从 store 中获取一些 state 变异后的状态，比如下面的 Store 中：
  * 获取豆瓣评分最高的剧

```js
export default new Vuex.Store({
  state: {
    teleplays: [
      {
        id: 1,
        name: "大世界扭蛋机",
        score: 6.8
      },
      {
        id: 2,
        name: "破事精英",
        score: 7.6
      },
      {
        id: 3,
        name: "加油！妈妈",
        score: 6.1
      },
      {
        id: 4,
        name: "梦华录",
        score: 8.2
      },
      {
        id: 5,
        name: "警察荣誉",
        score: 8.6
      }
    ]
  },
  getters: {
    great(state) {
      let max = 0, greatTeleplay = "";
      state.teleplays.forEach(item => {
        if (item.score > max) {
          max = item.score;
          greatTeleplay = item.name;
        }
      });
      return greatTeleplay;
    }
  }
});
```

.

```html
<template>
  <div>
    <h2>{{ $store.getters.great }} YYDS</h2>
  </div>
</template>
```

### Getters作为参数和传递参数

* 获取豆瓣评分大于7的列表和个数

```js
  getters: {
    great7(state) {
      return state.teleplays.filter(item => item.score > 7);
    },
    great7Counts(state,getters) {
      return getters.great7.length;
    }
  }
```

.

```html
<template>
  <div>
    <ul>
      <li v-for="item in $store.getters.great7" :key="item.id">{{item.name}}</li>
    </ul>
    <h2>{{$store.getters.great7Counts}}个</h2>
  </div>
</template>
```

* getters 默认是不能传递参数的, 如果希望传递参数, 那么只能让getters 本身返回另一个函数.
  * 比如上面的案例中,我们希望根据ID获取剧集的信息

```js
  getters: {
    select(state) {
      return (id) => {
        return state.teleplays.find(item => item.id = id);
      };
    }
  }
```

.

```html
<h2>{{$store.getters.select(2).name}}</h2>
```





















