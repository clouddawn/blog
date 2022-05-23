# DOM与BOM

## DOM

DOM 全称是 Document Object Model ，翻译过来就是 文档对象模型，将 web 页面与到脚本连接起来。

DOM模型用一个逻辑树来表示一个文档，树的每个分支的终点都是一个节点(node)，每个节点都包含着对象(objects)。

DOM的方法(methods)让你可以用特定方式操作这个树，用这些方法你可以改变文档的结构、样式或者内容。节点可以关联上事件处理器，一旦某一事件被触发了，那些事件处理器就会被执行。

##  BOM

BOM 的核心是 window，而 window 对象又具有双重角色，它既是通过 js 访问浏览器窗口的一个接口，又是一个 Global（全局）对象。这意味着在网页中定义的任何对象，变量和函数，都以 window 作为其  global 对象。

```js
window.close(); // 关闭窗口
```



**D**ocument **O**bject **M**odel（文档对象模型），就是把「文档」当做一个「对象」来看待。

相应的，**B**rowser **O**bject **M**odel（浏览器对象模型）,即把「浏览器」当做一个「对象」来看待。

在 DOM 中，文档中的各个组件（component），可以通过 object.attribute 这种形式来访问。一个 DOM 会有一个根对象，这个对象通常就是 document。

而 BOM 除了可以访问文档中的组件之外，还可以访问浏览器的组件，比如问题描述中的 navigator（导航条）、history（历史记录）等等。

在这种 「XOM」的模型中，最应该理解的就是 Object Model。Object Model 就表示你可以通过像操作对象一样，来操作这个 X。

再解释一下什么是对象（Object）。

在编程领域中，对象就是指的一种拥有具体数据（Data）并且具有（并不总是）特定行为（Behavior）的东西。例如，一个人 ，就可以看做一个对象。人的年龄、性别、身高、体重就是上文说的具体「数据」，通常将对象拥有的具体数据称作对象的「属性（Attribute）」；而人吃饭，睡觉，行走等能力，就是上文所说的「行为」，通常，我们把对象的行为称作对象的「方法（Method）」。另外，对象是可以嵌套的，也就是是说，一个对象的属性也可以是对象。

上文所说的「像操作对象一样」，最主要就是指访问对象的属性和调用对象的方法。对象的属性可以通过 object.attribute 这种形式来访问，对象的方法可以通过 object.method(arguments) 这种形式来调用。

对应到 DOM 中，document 这个根对象就有很多属性，例如 title 就是 document 的一个属性，可以通过 document.title 访问；document 对象也有很多方法，例如 getElementById，可以通过 document.getElementById(nodeId) 调用。

