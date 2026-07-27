# Composition API

## Options API的弊端

* 在Vue2中，我们编写组件的方式是Options API：
  * Options API的一大特点就是在对应的属性中编写对应的功能模块；
  * 比如data定义数据、methods中定义方法、computed中定义计算属性、watch中监听属性改变，也包括生命周期钩子；
* 但是这种代码有一个很大的弊端：
  * 当我们实现某一个功能时，这个功能对应的代码逻辑会被拆分到各个属性中；
  * 当我们组件变得更大、更复杂时，逻辑关注点的列表就会增长，那么同一个功能的逻辑就会被拆分的很分散；

* 如果能将同一个逻辑关注点相关的代码收集在一起会更
  好。
* 这就是Composition API 要做的事情。
* 也有人把Vue Composition API简称为VCA。

## 认识 Composition API

* 为了开始使用 Composition API，我们需要有一个可以实际使用它（编写代码）的地方；
  * 在Vue组件中，这个位置就是 setup 函数；
* setup其实就是组件的另外一个选项：
  * 只不过这个选项强大到我们可以用它来替代之前所编写的大部分其他选项；
  * 比如methods、computed、watch、data、生命周期等等；

## setup 函数的参数

* setup 有两个参数：props、context。
* props 非常好理解，它其实就是父组件传递过来的属性会被放到 props 对象中，我们在 setup 中如果需要使用，那么就可以直接通过 props 参数获取：
  * 对于定义props的类型，还是和之前的规则是一样的，在props选项中定义；
  * 并且在template中依然是可以正常去使用props中的属性，比如message；
  * 如果我们在setup函数中想要使用props，那么不可以通过 this 去获取；
  * props有直接作为参数传递到setup函数中，直接通过参数来使用即可；
* 另外一个参数是context，我们也称之为是一个SetupContext，它里面包含三个属性：
  * attrs：所有的非 prop 的 attribute；
  * slots：父组件传递过来的插槽；
  * emit：当我们组件内部需要发出事件时会用到 emit（因为不能访问this，所以不可以通过 this.$emit 发出事件）；

```html
<template>
  <h2>
    <slot></slot>
  </h2>
</template>

<script>
export default {
  props: {
    message: {
      type: String,
      required: true
    }
  },
  setup(props, {attrs, slots, emit}) {
    console.log(props.message);
    console.log(attrs.title);
    console.log(slots.default);
    emit('hahaha','hahaha')
  }
};
</script>
```

## setup 函数的返回值

* setup 既然是一个函数，那么它也可以有返回值，它的返回值用来做什么呢？
  * setup 的返回值可以在模板 template 中被使用；
  * 也就是说我们可以通过 setup 的返回值来替代 data 选项；
* 甚至是我们可以返回一个执行函数来代替在 methods 中定义的方法：

```html
<template>
  <div>
    <div>{{ counter }}年</div>
    <button @click="add">一年又过去了</button>
  </div>
</template>

<script>
export default {
  setup(props, {attrs, slots, emit}) {
    let counter = 1;
    const add = () => {
      counter++;
    };
    return {
      counter,
      add
    };
  }
};
</script>
```

* 但是，这种方式无法实现界面的响应式变化。
* 因为对于一个定义的变量来说，默认情况下，Vue并不会跟踪它的变化，来引起界面的响应式操作；

## setup 不可以使用 this

`setup()` 自身并不含对组件实例的访问权，即在 `setup()` 中访问 `this` 会是 `undefined`。

## Reactive API

* 如果想为在 setup 中定义的数据提供响应式的特性，那么我们可以使用 reactive 的函数：

```html
<template>
  <div>
    <h2>
      {{ state.counter }}年了
    </h2>
    <button @click="add">一年又过去了</button>
  </div>
</template>

<script>
import {reactive} from "vue";

export default {
  setup() {
    const state = reactive({
      counter: 1
    });
    const add = () => {
      state.counter++;
    };
    return {
      state,
      add
    };
  }
};
</script>
```

* 那么这是什么原因呢？为什么就可以变成响应式的呢？
  * 这是因为当我们使用 reactive 函数处理我们的数据之后，数据再次被使用时就会进行依赖收集；
  * 当数据发生改变时，所有收集到的依赖都是进行对应的响应式操作（比如更新界面）；
  * 事实上，我们编写的 data 选项，也是在内部交给了 reactive 函数将其变成响应式对象的；

## Ref API

* reactive API 对传入的类型是有限制的，它要求我们必须传入的是一个对象或者数组类型：
  * 如果我们传入一个基本数据类型（String、Number、Boolean）会报一个警告；

* 这个时候 Vue3 给我们提供了另外一个 API：ref API
  * ref 会返回一个可变的响应式对象，该对象作为一个**响应式的引用**维护着它内部的值，这就是 ref 名称的来源；
  * 它内部的值是在 ref 的 value 属性中被维护的；

```html
<template>
  <div>
    <h1>当前计数：{{ counter }}</h1>
    <button @click="add">+1</button>
  </div>
</template>

<script>
import {ref} from "vue";

export default {
  setup() {
    let counter = ref(1);

    function add() {
      counter.value++;
    }

    return {
      counter,
      add
    };
  }
};
</script>
```

* **这里有两个注意事项：**
  * 在模板中引入 ref 的值时，Vue 会自动帮助我们进行解包操作，所以我们并不需要在模板中通过 `ref.value` 的方式
    来使用；
  * 但是在 setup 函数内部，它依然是一个 ref 引用， 所以对其进行操作时，我们依然需要使用 `ref.value` 的方式；

## 认识 readonly

* 我们通过 reactive 或者 ref 可以获取到一个响应式的对象，但是某些情况下，我们传入给其他地方（组件）的这个响应式对象希望在另外一个地方（组件）被使用，但是不能被修改。
  * Vue3 为我们提供了 readonly 的方法；
  * readonly 会返回原生对象的只读代理（它依然是一个 Proxy，只是 set 方法被劫持）；
* 在开发中常见的 readonly 方法会传入三个类型的参数：
  * 类型一：普通对象；
  * 类型二：reactive 返回的对象；
  * 类型三：ref 的对象；

## readonly 的使用

* readonly 返回的对象都是不允许修改的；
* 但是经过 readonly 处理的原来的对象是允许被修改的；
  * 比如 `const info = readonly(obj)`，info 对象是不允许被修改的；
  * 当 obj 被修改时，readonly 返回的 info 对象也会被修改；
  * 但是我们不能去修改 readonly 返回的对象 info；
* 其实本质上就是 readonly 返回的对象的 setter 方法被劫持了而已；

```js
    // 1. 传入一个普通对象
    const p1 = {
      name: "悟空",
      age: 18
    };
    
    const readonlyP1 = readonly(p1);
    console.log(readonlyP1);

    // 2. 传入 reactive 对象
    const state = reactive({
      name: "八戒",
      age: 20
    });
    const state2 = readonly(state);

    // 3.传入 ref 对象
    const nameRef = ref("骆玉珠");
    const readonlyNameRef = readonly(nameRef);
```

## Reactive 判断的 API

### isProxy

* 检查对象是否是由 `reactive` 或 `readonly` 创建的 `proxy`。

```js
const p1 = {
  name: "孙悟空",
  age: 500
};

const reactiveP1 = reactive(p1);
console.log(isProxy(reactiveP1)); // true

const readonlyP1 = readonly(p1);
console.log(isProxy(readonlyP1)); // true

const refP1 = ref(p1);
console.log(isProxy(refP1)); // false

const proxyP1 = new Proxy(p1, {
  get(target, key, receiver) {
    Reflect.get(target, key, receiver);
  },
  set(target, key, newValue, receiver) {
    Reflect.set(target, key, newValue, receiver);
  }
});
console.log(isProxy(proxyP1)); // false
```

### isReactive

* 检查对象是否是由 `reactive` 创建的响应式代理：
* 如果该代理是 `readonly` 建的，但包裹了由 `reactive` 创建的另一个代理，它也会返回 `true`；

```js
const p1 = {
  name: "孙悟空",
  age: 500
};

const reactiveP1 = reactive(p1);
console.log(isReactive(reactiveP1)); // true

const readonlyP1 = readonly(p1);
console.log(isReactive(readonlyP1)); // false

const refP1 = ref(p1);
console.log(isReactive(refP1)); // false

const proxyP1 = new Proxy(p1, {
  get(target, key, receiver) {
    Reflect.get(target, key, receiver);
  },
  set(target, key, newValue, receiver) {
    Reflect.set(target, key, newValue, receiver);
  }
});
console.log(isReactive(proxyP1)); // false

console.log(isReactive(readonly(reactiveP1))); // true
```

### isReadonly

* 检查对象是否是由 readonly 创建的只读代理

### toRaw

* 返回 `reactive` 或 `readonly` 代理的原始对象（不建议保留对原始对象的持久引用，请谨慎使用）。

```js
    const p1 = {
      name: "孙悟空",
      age: 500
    };

    const reactiveP1 = reactive(p1);

    console.log(toRaw(reactiveP1) === p1); // true
```

### shallowReactive

* 创建一个响应式代理，它跟踪其自身 `property` 的响应性，但不执行嵌套对象的深层响应式转换 (深层还是原生对象)。

### shallowReadonly

* 创建一个 `proxy`，使其自身的 `property` 为只读，但不执行嵌套对象的深度只读转换（深层还是可读、可写的）。

### toRefs

* 如果我们使用 ES6 的解构语法，对 reactive 返回的对象进行解构获取值，那么之后无论是修改解构后的变量，还是修改reactive 返回的 state 对象，数据都不再是响应式的：

```js
    const info = reactive({
      name: "令狐冲",
      age: 29
    });

    let {name,age} =info;
```

* 那么有没有办法让我们解构出来的属性是响应式的呢？
  * Vue 为我们提供了一个 toRefs 的函数，可以将 reactive 返回的对象中的属性都转成 ref；
  * 那么我们再次进行解构出来的 name 和 age 本身都是 ref的；

```js
let {name,age} = toRefs(info);
```

* 这种做法相当于已经在 `info.name` 和 `ref.value` 之间建立了 链接，任何一个修改都会引起另外一个变化；

### toRef

* 如果我们只希望转换一个 reactive 对象中的属性为 ref, 那么可以使用 toRef 的方法：

```js
    const info = reactive({
      name: "令狐冲",
      age: 29
    });

    let {name} = info;
    let age = toRef(info,"age")
```

## ref 其他的 API

### unref

* 如果我们想要获取一个 ref 引用中的value，那么也可以通过 unref 方法：
  * 如果参数是一个 ref，则返回内部值，否则返回参数本身；
  * 这是 `val = isRef(val) ? val.value : val` 的语法糖函数；

```js
    const info = reactive({
      name: "令狐冲",
      age: 29
    });

    let {name} = info;
    let age = toRef(info, "age");

    function sum(num1, num2) {
      return unref(num1) + unref(num2);
    }

    console.log(sum(age, 1)); // 30
```

### isRef

* 判断值是否是一个 ref 对象

### shallowRef

* 创建一个浅层的 ref 对象

### triggerRef

* 手动触发和 `shallowRef` 相关联的副作用：

```js
    let info = shallowRef({
      name: "令狐冲",
      age: 29
    });

    function changeAge() {
      // 下面的修改不是响应式的
      info.value.age++;
      // 手动触发
      triggerRef(info);
    }
```

## customRef

* 创建一个自定义的 ref，并对其依赖项跟踪和更新触发进行显式控制：
  * 它需要一个工厂函数，该函数接受 track 和 trigger 函数作为参数；
  * 并且应该返回一个带有 get 和 set 的对象；
* 这里我们使用一个的案例：
  * 对双向绑定的属性进行 debounce( 防抖) 的操作；

```html
<template>
  <div>
    <input type="text" v-model="inputValue">
    <h1>{{ inputValue }}</h1>
  </div>
</template>

<script>
import debounceRef from "./useDebounceRef.js";

export default {
  name: "Home",
  setup() {
    let inputValue = debounceRef("hello");

    return {
      inputValue
    };
  }
};
</script>
```

.

```js
import {customRef} from "vue";

// 自定义 ref
export default function (value, delay = 300) {
  return customRef((track, trigger) => {
    let timerId;
    return {
      get() {
        track();
        return value;
      },
      set(newValue) {
        clearTimeout(timerId);
        timerId = setTimeout(() => {
          value = newValue;
          trigger();
        }, delay);
      }
    };
  });
}
```

## computed

* 如何使用 computed 呢？
  * 方式一：接收一个 getter 函数，并为 getter 函数返回的值，返回一个不变的 ref 对象；
  * 方式二：接收一个具有 get 和 set 的对象，返回一个可变的（可读写）ref 对象；

```js
// 方式一
let firstName = ref("冲");
let lastName = ref("令狐");

const fullName = computed(() => {
  return firstName.value + " · " + lastName.value;
});
```

.

```js
// 方式二
const fullName = computed({
  get() {
    return firstName.value + " · " + lastName.value;
  },
  set(newValue) {
    const names = newValue.split("·");
    firstName.value = names[0];
    lastName.value = names[1];
  }
});

function changeLastName() {
  fullName.value = "冲·陈";
}
```

## 侦听数据的变化

* 在 Options API 中，可以通过 watch 选项来侦听 data 或者 props 的数据变化，当数据变化时执行某一些操作。
* 在 Composition API 中，我们可以使用 watchEffect 和 watch 来完成响应式数据的侦听；
  * watchEffect 用于自动收集响应式数据的依赖；
  * watch 需要手动指定侦听的数据源；

## watchEffect

* 当侦听到某些响应式数据变化时，我们希望执行某些操作，这个时候可以使用 watchEffect。
* 来看一个案例：
  * 首先，watchEffect 传入的函数会被立即执行一次，并且在执行的过程中会收集依赖；
  * 其次，只有收集的依赖发生变化时，watchEffect 传入的函数才会再次执行；

```js
setup() {
  const info = ref({
    name: "林平之",
    age: 19
  });
  watchEffect(() => {
    console.log(`我老了，${info.value.age}`);
  });

  function changeAge() {
    info.value.age++;
  }

  return {
    info,
    changeAge
  };
}
```

## watchEffect 的停止侦听

* 在某些情况下，我们希望停止侦听，这个时候我们可以获取 `watchEffect` 的返回值函数，调用该函数即可。
* 比如在上面的案例中，age 达到 25 的时候就停止侦听：

```js
    const stopWatchAge = watchEffect(() => {
      console.log(`我老了，${info.value.age}`);
    });

    function changeAge() {
      info.value.age++;
      if (info.value.age > 25) {
        stopWatchAge();
      }
    }
```

## watchEffect 清除副作用

* 什么是清除副作用呢？
  * 比如在开发中需要在侦听函数中执行网络请求，但是在网络请求还没有达到的时候，停止了侦听器，或者侦听器侦听函数被再次执行了。
  * 那么上一次的网络请求应该被取消掉，这个时候就应该清除上一次的副作用；
* 在给 `watchEffect` 传入的函数被回调时，其实可以获取到一个参数：`onInvalidate`
  * 当副作用即将重新执行 或者 侦听器被停止 时会执行该函数传入的回调函数；
  * 可以在传入的回调函数中，执行一些清除工作；

```js
watchEffect((onCleanup) => {
    console.log(`我老了，${info.value.age}`);
    const timer = setTimeout(() => {
        console.log("着火了");
    }, 1500);
    onCleanup(() => {
        clearTimeout(timer);
    });
});
```

## setup 中使用 ref

* 在 setup 中如何使用 ref 或者元素或者组件？
  * 需要定义一个 ref 对象，然后绑定到元素或者组件的 ref 属性上；

```html
<template>
  <div>
    <h1 ref="h1Ref">把自己作为方法</h1>
    <button @click="getH1">getH1</button>
  </div>
</template>

<script>
import {ref} from "vue";

export default {
  setup() {
    const h1Ref = ref(null);

    function getH1() {
      console.log(h1Ref.value);
    }

    return {
      h1Ref,
      getH1
    };
  }
};
</script>
```

## watchEffect 的执行时机

* 默认情况下，组件的更新会在副作用函数执行之前：
  * 如果我们希望在副作用函数中获取到元素，是否可行呢？

```js
  setup() {
    const h1Ref = ref(null);

    function getH1() {
      console.log(h1Ref.value);
    }

    watchEffect(() => {
      console.log(h1Ref.value);
    });

    return {
      h1Ref,
      getH1
    };
  }
```

* 我们会发现打印结果打印了两次：
  * 这是因为 setup 函数在执行时就会立即执行传入的副作用函数，这个时候 DOM 并没有挂载，所以打印为 null；
  * 而当 DOM 挂载时，会给 title 的 ref 对象赋值新的值，副作用函数会再次执行，打印出来对应的元素；

## 调整 watchEffect 的执行时机

* 如何能在第一次的时候就打印出来对应的元素？
  * 这个时候需要改变副作用函数的执行时机；
  * 它的默认值是 pre，它会在元素**挂载**或者**更新**之前执行；
  * 所以我们会先打印出来一个空的，当依赖的 title 发生改变时，就会再次执行一次，打印出元素；
* 我们可以设置副作用函数的执行时机：

```js
watchEffect(() => {
  console.log(h1Ref.value);
}, {
  flush: "post"
});
```

## Watch 的使用

* watch 的 API 完全等同于组件 watch 选项的 Property：
  * watch 需要侦听特定的数据源，并在回调函数中执行副作用；
  * 默认情况下它是惰性的，只有当被侦听的源发生变化时才会执行回调；
* 与 watchEffect 的比较，watch 允许我们：
  * 懒执行副作用（第一次不会直接执行）；
  * 更具体的说明当哪些状态发生变化时，触发侦听器的执行；
  * 访问侦听状态变化前后的值；

## 侦听单个数据源

* watch 侦听函数的数据源有两种类型：
  * 一个 getter 函数：但是该 getter 函数必须引用可响应式的对象（比如 reactive 或者 ref ）；
  * 直接写入一个可响应式的对象，reactive 或者 ref（比较常用的是 ref）；

```js
setup() {
  const info = reactive({
  	name: "林平之",
    age: 19
  });
  watch(() => info.age, (newValue,oldValue) => {
  	console.log('newValue:' + newValue,'oldValue:' + oldValue)
  })
  function changeAge(){
  	info.age++
  }

  return {
  	info,
    changeAge
  };
}
```

-

```js
setup() {
  const info = ref({
  	name: "林平之",
    age: 19
  });
  watch(() => info.value.age, (newValue,oldValue) => {
  	console.log('newValue:' + newValue,'oldValue:' + oldValue)
  })
  function changeAge(){
  	info.value.age++
  }

  return {
  	info,
    changeAge
  };
}
```

## 侦听多个数据源

* 侦听器还可以使用数组同时侦听多个源：

```js
setup() {
    const info = ref({
      name: "林平之",
      age: 19
    });
    watch(() => [info.value.name, info.value.age], (newValues, oldValues) => {
      console.log("newValues:", newValues, "oldValues:", oldValues);
    });

    function changeAge() {
      info.value.age++;
    }

    return {
      info,
      changeAge
    };
  }
}
```

## 侦听响应式对象

*  如果要侦听一个数组或者对象，那么可以使用一个 getter 函数，并且对可响应对象进行解构：

```js
setup() {
    const names = reactive(["令狐冲", "任盈盈", "杨过", "小龙女"]);
    watch(() => [...names], (newValue, oldValue) => {
      console.log(newValue, oldValue);
    });
    const changeNames = () => {
      names.push("李瓶儿");
    };

    return {
      names,
      changeNames
    };
  }
```

## watch 的选项

* 如果我们希望侦听一个深层的侦听，那么依然需要设置 deep 为true：
  * 也可以传入 immediate 立即执行；

```js
const info = reactive({
  name: "令狐冲",
  age: 20,
  friend: {
  	name: "田伯光"
  }
});

watch(() => ({...info}), (newInfo, oldInfo) => {
  console.log(newInfo, oldInfo);
}, {
  deep: true,
  immediate: true
});
```

## 生命周期钩子

* setup 中如何使用生命周期函数呢？
  * 可以使用直接导入的 onX 函数注册生命周期钩子；

```js
import {onMounted, onUnmounted, onUpdated, ref} from "vue";

export default {
  setup() {
    let name = ref("小飞机");
    setTimeout(() => {
      name.value = "大炮仗";
    }, 1500);

    onMounted(() => {
      console.log("onMounted");
    });
    onUpdated(() => {
      console.log("onUpdated");
    });
    onUnmounted(() => {
      console.log("onUnmounted");
    });

    return {
      name
    };
  }
};
```

## Provide 函数

* Composition API 也可以替代 Provide 和 Inject 的选项。
* 可以通过 provide 来提供数据：
  * 通过 provide 方法来定义每个 Property；
  * provide 可以传入两个参数：
    * name：提供的属性名称；
    * value：提供的属性值；

```js
let counter = 100;
let info = {
  name: "宋万博",
  age: 33
};

provide("counter", counter);
provide("info", info);
```

## Inject 函数

* 在**后代组件**中可以通过**inject**来注入需要的属性和对应的值：
  * inject 可以传入两个参数：
    * 要 inject 的 property 的 name；
    * 默认值；

```js
setup() {
  const counter = inject("counter");
  const info = inject("info");

  return {
  	counter,
    info
  };
}
```

## 数据的响应式

* 为了增加 provide 值和 inject 值之间的响应性，可以在 provide 值时使用 ref 和 reactive。

```js
let counter = ref(100);
let info = reactive({
  name: "宋万博",
  age: 33
});

provide("counter", counter);
provide("info", info);
```

## 修改响应式 Property

* 如果我们修改可响应的数据，那么最好在数据提供的位置来修改：
  * 然后将修改方法进行共享，在后代组件中进行调用；

```js
let counter = ref(100);
let info = reactive({
  name: "宋万博",
  age: 33
});

function changeInfo() {
  info.name = "刘旸";
}

provide("counter", counter);
provide("info", info);
provide("changeInfo", changeInfo);
```

.

```js
setup() {
  const counter = inject("counter");
  const info = inject("info");
  const changeInfo = inject("changeInfo");

  return {
    counter,
    info,
    changeInfo
  };
}
```

## useCounter

* 计数器逻辑抽取

```js
import {ref, computed} from "vue";
export default function (){
  const counter = ref(0);
  const doubleCounter = computed(() => counter.value * 2);

  function increment() {
    counter.value++;
  }

  function decrement() {
    counter.value--;
  }

  return {
    counter,
    doubleCounter,
    increment,
    decrement
  };
}
```

## useTitle

* 编写一个修改 title 的 Hook

```js
import {ref, watch} from "vue";

export default function (title) {
  const refTitle = ref(title);
  watch(refTitle, (newValue) => {
    document.title = newValue;
  }, {
    immediate: true
  });
  return {
    refTitle
  };
}
```

## useScrollPosition

* 监听界面滚动位置的 Hook

```js
import {ref} from "vue";

export default function () {
  const scrollX = ref(0);
  const scrollY = ref(0);

  document.addEventListener("scroll", () => {
    scrollX.value = window.scrollX;
    scrollY.value = window.scrollY;
  });

  return {
    scrollX,
    scrollY
  };
}
```

## useMousePosition

* 监听鼠标的位置

```js
import {ref} from "vue";

export default function () {
  const mouseX = ref(0);
  const mouseY = ref(0);

  window.addEventListener("mousemove", (event) => {
    mouseX.value = event.pageX;
    mouseY.value = event.pageY;
  });

  return {
    mouseX,
    mouseY
  };
}
```

## useLocalStorage

* 使用 localStorage 存储和获取数据的Hook

```js
import {ref, watch} from "vue";

export default function (key, value) {
  const data = ref(value);
  if (value) {
    window.localStorage.setItem(key, JSON.stringify(value));
  } else {
    data.value = JSON.parse(window.localStorage.getItem(key));
  }

  watch(data, (newValue) => {
    window.localStorage.setItem(key, JSON.stringify(newValue));
  });
  return data;
}
```































