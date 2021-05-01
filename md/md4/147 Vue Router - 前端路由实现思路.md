# Vue Router - 前端路由实现思路

## 路由是什么

* 路由的功能就是 1 对多分发请求

![image](../images4/147/01.png)

![image](../images4/147/02.png)

* 原生 html 中访问网页 url 通过 window.location.hash 获取
* 原生 html 中监听 hashchange 事件可针对不同 url  做出对应操作

## 路由表

* 表驱动编程 --> key - hash，value - 对应页面
* 嵌套路由：多层 url 使用多层路由表引导访问页面

## 路由的模式

* 对于 vue 这类渐进式前端开发框架，为了构建 SPA（单页面应用），需要引入前端路由系统，这也就是 Vue-Router 存在的意义。前端路由的核心，就在于 —— 改变视图的同时不会向后端发出请求。

### Hash 模式

* [hash 示例](https://codesandbox.io/s/x3nxq950ko) 

* 形如 “/#/内容” 的 url 访问，hash —— 即地址栏 URL 中的 # 符号（此 hash 不是密码学里的散列运算）。比如这个 URL：http://www.abc.com/#/hello  hash 的值为 #/hello。它的特点在于：hash 虽然出现在 URL 中，但不会被包括在 HTTP 请求中，对后端完全没有影响，因此改变 hash 不会重新加载页面。
* 任何情况下都可以用 hash 做前端路由
* 缺点是 SEO 不友好，因为服务器收不到 hash（#后的内容），浏览器会自动删掉 # 后的内容，不会发给服务器
* 上面这个 bug 的解决方案是 hashbang，须使用 "#!内容"

### History 模式

* [history 示例](https://codesandbox.io/s/oqjvqm6w05) 

* 形如 "/内容" 的 url 访问，history —— 利用了 HTML5 History Interface 中新增的 pushState() 和 replaceState() 方法。（需要特定浏览器支持）这两个方法应用于浏览器的历史记录栈，在当前已有的 back、forward、go 的基础之上，他们提供了对历史记录进行修改的功能。只是当它们执行修改时，虽然改变了当前的 URL，但浏览器不会立即向后端发送请求。
* 通过 window.location.pathname 获取路径
* 只有后端将所有前端路由都渲染至同一页面时才能使用（这个页面不能是 404），即不管用户访问服务器下的任何 url 都会默认访问主页
* 缺点：IE8 以下不支持，且用户体验差，（每次切换 url 都会刷新页面）

#### 使用 window.history.pushState() 在不刷新页面的情况下切换 url

* 首先在跳转链接处（如 a 标签）使用 e.preventDefault 阻止跳转和刷新页面
* window.history.pushState  方法接受三个参数，依次为：
  * state：一个与指定网址相关的状态对象，popstate 事件触发时，该对象会传入回调函数。如果不需要这个对象，此处可以填 null。
  * title：新页面的标题，但是所有浏览器目前都忽略这个值，因此这里可以填 null。
  * url：新的网址，必须与当前页面处在同一个域，浏览器的地址将显示这个网址。
* 进行 window.history.pushState() 后接其他操作更改页面元素即可。

### Memory 模式（一般不用）

* 将用户访问的路径使用 setItem 存入 localStorage 中并进行跳转，每次刷新使用 getItem 获取当前的路径跳转至之前访问的页面
* 适合没有路径的应用，适合非浏览器，比如在 app 中利用 localStorage 进行跳转
* 缺点：单机版的路由，因为同一个 url，因为用户的 localStorage 不一样，访问到的页面不一样，因为无法分享 url

### 总结

* hash 和 history 都利用 url 存取路径，前者使用 hash，后者使用 pathname; 而 memory 通过 localStorage 存取路径，适合非浏览器
* hash 和 history 可分享 url，因为两者都能从 url 中读取信息，而 memory 是单机版路由，根据用户的 localStorage 不同将访问不同页面
* hash 模式下，仅 hash 符号之前的内容会被包含在请求中，如 http://www.abc.com，因此对于后端来说，即使没有做到对路由的全覆盖，也不会返回 404 错误。
* history 模式下，前端的 URL 必须和实际向后端发起请求的 URL 一致，如 http://www.abc.com/book/id 如果后端缺少对 /book/id 的路由处理，将返回 404 错误。Vue-Router 官网里如此描述：“不过这种模式要玩好，还需要后台配置支持……所以呢，你要在服务端增加一个覆盖所有情况的候选资源：如果 URL 匹配不到任何静态资源，则应该返回同一个 index.html 页面，这个页面就是你 app 依赖的页面。”































