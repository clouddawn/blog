# React

## React 简介

React 是一个将数据渲染为HTML视图的开源 JS 库。

### 原生 JS 开发痛点

* 操作 DOM 繁琐、效率低（**DOM-API 操作 UI**）
* 直接操作 DOM，浏览器会进行大量的**重绘重排**。

* 没有**组块化**编码方案，代码复用率低

### React 的特点

* 采用**组件化**模式、**声明式编码**，提高开发效率及组件复用率
* 使用**虚拟DOM** + 优秀的 **Diffing** 算法，尽量减少与真实DOM的交互

### 虚拟DOM

* 相比真实DOM比较“轻”，因为虚拟DOM是React内部在用，无需真实DOM上那么多的属性。
* 最终会被React转化为真实DOM，呈现在页面上。

### JSX

* 全称:  JavaScript XML

* react定义的一种类似于XML的JS扩展语法: 本质是JS + XML

#### 语法规则

* 标签中混入js表达式时要用 {}
* 样式的类名指定要用className，不要用class
* 内联样式，要用 style={{key:value}} 的形式去写
* 只有一个根标签
* 标签必须闭合
* 标签首字母
  * 若小写字母开头，react会将该标签转为html中同名元素，若html中无该标签对应的同名元素，则报错
  * 若大写字母开头，react就去渲染对应的组件，若组件没有定义，则报错

#### js语句 vs js表达式

* 表达式：一个表达式会产生一个值，可以放在任何需要值的地方
  * a
  * a + b
  * demo(1)
  * arr.map()
  * function test(){}
* 语句(代码)
  * if(){}
  * for(){}
  * switch(){case:xxxx}

### 模块与组件
#### 模块

* 理解：向外提供特定功能的js程序, 一般就是一个js文件

* 为什么要拆成模块：随着业务逻辑增加，代码越来越多且复杂。

* 作用：复用js, 简化js的编写, 提高js运行效率

#### 组件

* 理解：用来实现局部功能效果的代码和资源的集合(html/css/js/image等等)

* 为什么要用组件： 一个界面的功能更复杂

* 作用：复用编码, 简化项目编码, 提高运行效率

### 模块化与组件化


#### 模块化

* 当应用的js都以模块来编写的, 这个应用就是一个模块化的应用

#### 组件化

* 当应用是以多组件的方式实现, 这个应用就是一个组件化的应用

### 函数式组件

```jsx
<script type="text/babel">
  function MyComponent(){
    console.log(this); // 此处的this是undefined，因为babel编译后开启了严格模式
    return <h1>陈铭的《有聊》全是泛泛之谈，深度不够，没啥干货</h1>
	}
  ReactDOM.render(<MyComponent/>, document.getElementById('test'));
  /*
  * 执行了ReactDOM.render(<MyComponent/>, ...)之后，发生了什么？
  * 1. React解析组件标签，找到了MyComponent组件。
  * 2. 发现组件是使用函数定义的，随后调用该函数，将返回的虚拟DOM转为真实DOM，随后呈现在页面中。
  * */
</script>
```

### 类式组件

```jsx
<script type="text/babel">
	// 1. 创建类式组件
	class MyComponent extends React.Component {
    render(){
      // render是放在哪里的？-- MyComponent的原型对象上，供实例使用。
			// render中的this是谁？-- MyComponent的实例对象 <=> MyComponent组件实例对象。
      console.log('render中的this:', this);
      return <h1>喜人奇妙夜，真好看</h1>
		}
	}
  // 2. 渲染组件到页面
  ReactDOM.render(<MyComponent />, document.querySelector('#test'));
  // 执行了 ReactDOM.render(<MyComponent />, ...) 之后，发生了什么？
	// 1. React解析组件标签，找到了MyComponent组件。
	// 2. 发现组件是使用类定义的，随后new出来该类的实例，并通过该实例调用到原型上的render方法。
	// 3. 将render返回的虚拟DOM转为真实DOM，随后呈现在页面中。
</script>
```

#### 注意

* 组件名首字母必须大写
* 虚拟DOM元素只能有一个根元素
* 虚拟DOM元素必须有结束标签

#### 渲染类组件标签的基本流程

* React 内部会创建组件实例对象
* 调用 render() 得到虚拟 DOM，并解析为真实 DOM
* 插入到指定的页面元素内部

### state

* state 是组件对象最重要的属性, 值是对象(可以包含多个 key-value 的组合)

* 组件被称为"状态机", 通过更新组件的 state 来更新对应的页面显示(重新渲染组件)

#### 注意

* 组件中 render 方法中的 this 为组件实例对象

* 组件自定义的方法中 this 为 undefined，如何解决？
  * 强制绑定 this: 通过函数对象的 bind()
  * 箭头函数

* 状态数据，不能直接修改或更新

























