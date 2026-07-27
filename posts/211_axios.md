# Axios 精进

## 发送并发请求

* 有时候, 我们可能需求同时发送两个请求
  * 使用 `axios.all`, 可以放入多个请求的数组.
  * `axios.all([])` 返回的结果是一个数组，使用 `axios.spread` 可将数组 `[res1,res2]` 展开为 `res1, res2`

```js
    both() {
      axios.all([
        axios.post("/people/client/getUserInfo"),
        axios.get("/people/client/getVoucher")
      ])
        .then(axios.spread((res1,res2) => {
          console.log(res1);
          console.log(res2);
        }))
        .catch((error) => {
          console.error(error);
          Dialog.alert({
            message: "调用接口失败",
          }).then(() => {
          });
        });
    },
```

## 全局配置

* 提取固定参数，如 baseURL

```js
axios.defaults.baseURL = '123.207.32.32:8000'
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded'
```

## 常见配置选项

* 请求地址

  ```js
  url: '/user',
  ```

* 请求类型

  ```js
  method: 'get',
  ```

* 请根路径

  ```js
  baseURL: 'http://www.mt.com/api',
  ```

* 自定义的请求头

  ```js
  headers:{'x-Requested-With':'XMLHttpRequest'},
  ```

* URL查询对象

  ```js
  params:{ id: 12 },
  ```

* 超时设置 ms

  ```js
  timeout: 1000,
  ```

* 跨域是否带 Token

  ```js
  withCredentials: false,
  ```

* 响应的数据格式 json / blob /document /arraybuffer / text / stream

  ```js
  responseType: 'json',
  ```

## axios 的实例

* 为什么要创建 axios 的实例呢?
  * 当我们从 axios 模块中导入对象时, 使用的实例是默认的实例。
  * 当给该实例设置一些默认配置时, 这些配置就被固定下来了。
  * 但是后续开发中, 某些配置可能会不太一样。
  * 比如某些请求需要使用特定的 baseURL 或者 timeout 或者 content-Type 等。
  * 这个时候, 我们就可以创建新的实例, 并且传入属于该实例的配置信息。

```js
const axiosInstance = axios.create({
    baseURL: 'http://123.207.32.32:8000',
    timeout: 5000,
    headers: {
        'Content-Type': 'application/x-www-form-urlencoded'
    }
})
```

.

```js
axiosInstance({
    url: '/category',
    method: 'get'
}).then(res => {
    console.log(res);
}).catch(err => {
    console.log(err);
})
```

## 拦截器

* axios提供了拦截器，用于我们在发送每次请求或者得到相应后，进行对应的处理。
* 如何使用拦截器呢？

```js
// 添加请求拦截器
axios.interceptors.request.use(function (config) {
    // 在发送请求之前做些什么
    return config;
  }, function (error) {
    // 对请求错误做些什么
    return Promise.reject(error);
  });

// 添加响应拦截器
axios.interceptors.response.use(function (response) {
    // 2xx 范围内的状态码都会触发该函数。
    // 对响应数据做点什么
    return response;
  }, function (error) {
    // 超出 2xx 范围的状态码都会触发该函数。
    // 对响应错误做点什么
    return Promise.reject(error);
  });
```

* 请求拦截可以做到的事情：
  * 当发送网络请求时，在页面中添加一个 loading 组件，作为动画
  * 某些请求要求用户必须登录，判断用户是否有 token，如果没有 token 跳转到 login 页面
  * 对请求的参数进行序列化
  * 等等

* 请求拦截中错误拦截较少，通常都是配置相关的拦截
  * 可能的错误比如请求超时，可以将页面跳转到一个错误页面中。





































