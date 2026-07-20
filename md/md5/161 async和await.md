# async & await

`async` 和 `await` 是 JavaScript 中处理**异步操作**的终极语法糖，它的核心价值在于**让异步代码写得像同步代码一样直观**，彻底告别“回调地狱”和复杂的 `Promise` 链式调用。

### 1. 基本概念

- **async**：放在函数声明前面。它会把该函数的返回值自动包装成一个 **Promise** 对象。
- **await**：只能用在 `async` 函数内部。它会暂停当前函数的执行，等待右侧的 Promise 对象状态变为 `resolved`（成功）或 `rejected`（失败），然后**返回结果**。

------

### 2. 基础用法示例

假设我们有一个模拟网络请求的函数：

```javascript
// 模拟一个异步任务，1秒后返回 "数据"
function fetchData() {
  return new Promise((resolve) => {
    setTimeout(() => resolve("数据"), 1000);
  });
}
```

**传统 Promise 写法**（链式调用）：

```javascript
function getInfo() {
  fetchData()
    .then(result => {
      console.log(result); // 1秒后输出 "数据"
    });
}
```

**改用 async/await 写法**（同步写法）：

```javascript
async function getInfo() {
  const result = await fetchData(); // 等待 Promise 完成
  console.log(result); // 1秒后输出 "数据"
}
```

------

### 3. 串行与并行

- **串行（顺序执行）**：使用 `await` 逐行等待，前一个完成才执行后一个（耗时 = 两者之和）。

  ```javascript
  async function serial() {
    const data1 = await fetchData(); // 等待 1s
    const data2 = await fetchData(); // 再等待 1s
    console.log(data1, data2); // 总共耗时 2s
  }
  ```

- **并行（同时执行）**：如果两个任务互不依赖，先用 `Promise.all` 创建任务，再统一 `await`（耗时 ≈ 最慢的那个）。

  ```javascript
  async function parallel() {
    // 同时发起两个请求（不阻塞彼此）
    const [data1, data2] = await Promise.all([fetchData(), fetchData()]);
    console.log(data1, data2); // 总共耗时约 1s
  }
  ```

------

### 4. 错误处理

如果 Promise 失败（`rejected`），`await` 会抛出异常。**必须用 try...catch 包裹**，否则错误会被静默吞噬。

```javascript
async function getInfo() {
  try {
    const result = await fetchData(); 
    // 假设 fetchData 有时会报错
    console.log(result);
  } catch (error) {
    console.error("请求失败了：", error.message);
    // 在这里做降级处理，比如展示错误提示
  }
}
```

如果不喜欢 `try...catch` 的缩进，也可以用 Promise 的 `.catch` 捕获：

```javascript
async function getInfo() {
  const result = await fetchData().catch(err => console.log(err));
  // 如果出错，result 是 undefined，但不会阻塞后续代码
}
```

------

### 5. 循环中的用法

`await` 在 `for`、`while` 循环中表现完美，可以顺序执行：

```javascript
async function processArray(urls) {
  for (const url of urls) {
    const data = await fetch(url); // 逐个等待，按顺序执行
    console.log(data);
  }
}
```

**特别注意**：`forEach` 不支持 `await`（会并发执行且无法等待），如果需要并发请使用 `for...of` 或 `Promise.all`。

------

### 6. 高级避坑指南

- **忘记写 await**：如果没有 `await`，你拿到的是 **Promise 对象**，而不是实际值，会导致后续操作错乱。

  ```javascript
  const result = fetchData(); // ❌ result 是 Promise，不是 "数据"
  ```

- **await 会阻塞当前函数**：它只阻塞 `async` 函数内部的后续代码，**不会阻塞主线程**（浏览器依然可以响应点击、渲染等操作）。

- **返回值**：`async` 函数永远返回 Promise。如果你想直接拿到最终值，必须用 `await` 调用它，或者 `.then`。



## await 返回值

在 JavaScript 中，`await` 的核心作用就是**暂停** `async` 函数的执行，并**等待**一个 `Promise` 的决议（settled）。

### 1. 最核心的规则

**await 表达式的返回值，永远是 Promise 对象被解决（resolve）时传出的那个值。**

- 如果 `await` 后面的 `Promise` 成功（fulfilled），`await` 就返回该成功结果。
- 如果 `await` 后面的 `Promise` 失败（rejected），`await` **不会返回值**，而是直接**抛出异常**（Throw）。

------

### 2. 分场景详解返回值

#### 场景一：`await` 一个成功兑现的 Promise

这是最标准的用法，返回值就是 Promise 中 `resolve(...)` 传递的参数。

```javascript
function fetchData() {
  return new Promise((resolve) => {
    setTimeout(() => resolve('Hello, World!'), 1000);
  });
}

async function test() {
  const result = await fetchData(); 
  console.log(result); // 输出: 'Hello, World!'
  console.log(typeof result); // 输出: string
}
test();
```

**结论**：`result` 的类型是 `string`，而不是 `Promise`。`await` 帮你把 Promise 给“剥”开了。

#### 场景二：`await` 一个被拒绝的 Promise（异常）

此时没有“返回值”可言，你必须用 `try...catch` 捕获它，否则函数会直接终止并将错误冒泡给调用者。

```javascript
function failPromise() {
  return new Promise((resolve, reject) => {
    reject(new Error('出错了'));
  });
}

async function test() {
  try {
    const result = await failPromise(); 
    // 这行代码永远不会执行
    console.log(result);
  } catch (error) {
    console.log(error.message); // 输出: '出错了'
    // 在这里，error 就是 reject 传递出来的值
  }
}
test();
```

**重要补充**：如果你没有用 `try...catch`，这个错误会变成未捕获的异常，相当于 `promise.catch()` 没写。

#### 场景三：`await` 一个非 Promise 值（普通值）

如果 `await` 后面跟的不是 Promise（比如数字、字符串、普通对象），JavaScript 会**自动将其包装成一个立即成功（fulfilled）的 Promise**。

```javascript
async function test() {
  const a = await 42;
  const b = await 'Hello';
  const c = await { name: 'Jack' };
  
  console.log(a); // 42
  console.log(b); // 'Hello'
  console.log(c); // { name: 'Jack' }
}
test();
```

**结论**：返回值就是该值本身。这其实和 `Promise.resolve(42)` 的效果一样。

#### 场景四：`await` 一个 Thenable 对象（拥有 then 方法的对象）

只要一个对象拥有 `then` 方法，`await` 就会将其当作 Promise 来处理，返回值取决于 `then` 方法中回调传入的参数。

```javascript
const thenable = {
  then(resolve) {
    resolve('来自thenable的值');
  }
};

async function test() {
  const result = await thenable;
  console.log(result); // 输出: '来自thenable的值'
}
test();
```

------

### 3. 进阶硬核知识点

#### （1）关于“微任务”与“宏任务”的时机

虽然 `await` 看起来阻塞了代码，但它**并不阻塞主线程**（引擎依然在处理其他任务）。

```javascript
async function test() {
  console.log(1);
  const result = await 100; // 注意：这里虽然是普通值，但依然会触发微任务
  console.log(result); 
  console.log(3);
}

test();
console.log(2);

// 输出顺序：1, 2, 100, 3
```

**解释**：`await 100` 等价于 `await Promise.resolve(100)`。`await` 右侧的执行是同步的（立即执行），但**等待返回值并继续执行后续代码**，会被放入微任务队列。所以 `await` 后面的代码总是晚于当前同步代码执行。

#### （2）`await` 返回值的类型推导（TypeScript 场景）

在 TS 中，如果你 `await` 一个 `Promise<T>`，返回值的类型会被推导为 `T`（解除包裹）。但如果你 `await` 一个联合类型（比如 `Promise<string> | number`），TS 会推导为 `string | number`。

#### （3）如果 Promise 中 `resolve` 了另一个 Promise

如果 `resolve` 的参数本身又是一个 Promise，`await` 会递归地展开（扁平化）直到拿到最终的非 thenable 值。

```javascript
const p1 = Promise.resolve(Promise.resolve(Promise.resolve('最终值')));

async function test() {
  const result = await p1;
  console.log(result); // 输出: '最终值'（自动展平）
}
test();
```

------

### 5. 常见误区：`await` 并不总是返回 Promise 的 `resolve` 值

很多初学者会误以为 `await` 返回的一定是成功值，从而忘记捕获错误。**必须牢记：**

> 如果你不包裹 `try...catch`，`await` 在遇到 reject 时根本不会执行到赋值语句，它会直接“跳出”整个 async 函数，相当于把错误抛给了上层。

**对比代码：**

```javascript
// 错误写法（未捕获）
async function bad() {
  const data = await Promise.reject('炸了'); // 这里直接抛出异常，data 不会被赋值
  console.log(data); // 这行永远执行不到
}

// 正确写法
async function good() {
  const data = await Promise.reject('炸了').catch(err => err); // 返回 '炸了'
  console.log(data); // 输出: '炸了'
}
```

------

### 总结

| 场景               | `await` 后面的值                      | 返回值表现                        |
| :----------------- | :------------------------------------ | :-------------------------------- |
| **成功的 Promise** | `Promise.resolve('ok')`               | 返回 `'ok'`                       |
| **失败的 Promise** | `Promise.reject('err')`               | 抛出异常 `'err'`（需捕获）        |
| **普通值**         | `123` / `'abc'` / `{}`                | 返回该普通值本身                  |
| **Thenable 对象**  | `{ then: ... }`                       | 返回 `then` 回调中 `resolve` 的值 |
| **嵌套 Promise**   | `Promise.resolve(Promise.resolve(1))` | 自动展平，返回 `1`                |

**一句话终极概括**：`await` 本质上就是**取出 Promise 这个“盒子”里的内容**。如果盒子是好的（fulfilled），你就得到内容；如果盒子是坏的（rejected），它就会在原地“爆炸”（throw），你必须接住它。


















