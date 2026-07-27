# onclick、XMLHttpRequest、DOM

## GlobalEventHandlers.onclick

全局事件处理器（GlobalEventHandlers）之一的 `onclick` 属性，是处理当前元素的 `click` 事件的事件处理器。

* **GlobalEventHandlers** 描述了一系列 web worker 的事件接口 `HTMLElement` ，`Document`，`Window`。这里面的每一个接口都可以添加更多的事件句柄。
* GlobalEventHandlers 是一个混入对象（mixin）而不是一个真正的接口，所以无法创建直接基于 GlobalEventHandlers 的对象。

* **click** 当定点设备的按钮（通常是鼠标左键）在一个元素上被按下和放开时，`click` 事件就会被触发。

### 语法

* `element.onclick = functionRef;`

```html
    <p>请随意点击本例子。</p>
    <p id="log"></p>
    <script>
        let log = document.getElementById('log');

        document.onclick = inputChange;

        function inputChange(e) {
        log.textContent = `Position: (${e.clientX}, ${e.clientY})`;
        }  
    </script>
```

*  Document 接口表示任何在浏览器中载入的网页，并作为网页内容的入口，也就是 DOM 树。
* DOM 树包含了像 `<body>`、`<table>` 这样的元素，以及大量其他元素。它向网页文档本身提供了全局操作功能，能解决如何获取页面的 URL ，如何在文档中创建一个新的元素这样的问题。
* Document 的方法 `getElementById()` 返回一个匹配特定 ID 的元素。由于元素的 ID 在大部分情况下要求是独一无二的，这个方法自然而然地成为了一个高效查找特定元素的方法。

 

## XMLHttpRequest

XMLHttpRequest (XHR) 对象用于与服务器交互。通过 XMLHttpRequest 可以在不刷新页面的情况下请求特定 URL，获取数据。这允许网页在不影响用户操作的情况下，更新页面的局部内容。

* **XMLHttpRequest()**  该构造函数用于初始化一个 XMLHttpRequest 实例对象。

### XMLHttpRequest.open()

* 用于初始化一个请求
* `XMLHttpRequest.open(method, url)`
* **method**  要使用的 HTTP 方法，比如 GET、POST、DELETE 等
* **url**  一个 DOMString 表示要向其发送请求的 URL
* DOMString 是一个 UTF-16 字符串，由于 JS 已经使用了这样的字符串，所以 DOMString 直接映射到一个 String 。

### XMLHttpRequest.onload = callback

* **callback** 是请求成功完成时要执行的函数

### XMLHttpRequest.onerror = callback

* 当请求失败时执行的函数

### XMLHttpRequest.response

* 返回响应的正文

### XMLHttpRequest.send()

* 用于发送 HTTP 请求
* 如果是异步请求（默认为异步请求），则此方法会在请求发送后立即返回
* 如果是同步请求，则此方法直到响应达到后才会返回



## DOM

### Document.createElement()

* 用于创建一个由标签名称 tagName 指定的 HTML 元素

#### 语法

```js
var element = document.createElement(tagName);
```

#### 参数

* **tagName**  指定要创建元素类型的字符串，该方法不允许使用限定名称（如：“html:a”）

#### 示例

```js
const style = document.createElement('style');
```



### element.innerHTML

* 设置或获取 HTML 语法表示的元素的后代
* 如果要向一个元素中插入一段 HTML，而不是替换它的内容，那么请使用 `insertAdjacentHTML()` 方法

#### 语法

```js
const content = element.innerHTML;
element.innerHTML = htmlString;
```

#### 值

DOMString 包含元素后代的 HTML 序列，设置元素的 innerHTML 将会删除所有该元素的后代并以上面给出的 htmlString 替代



### Node.appendChild

* `Node.appendChild()` 方法将一个节点附加到指定父节点的子节点列表的**末尾**处。
* 如果将被插入的节点已经存在于当前文档的文档树中，那么 `appendChild()` 只会将它从原先的位置移动到新的位置（不需要事先移除要移动的节点）。
* 这意味着，一个节点不可能同时出现在文档的不同位置。
* 所以，如果某个节点已经拥有父节点，在被传递给此方法后，它首先会被移除，再被插入到新的位置。
* 若要保留已在文档中的节点，可以先使用 `Node.cloneNode()` 方法来为它创建一个副本，再将副本附加到目标父节点下。
* **注意**，用 `cloneNode` 制作的副本不会自动保持同步。

```html
    <h1>静夜思</h1>
    <script>
        const h1 = document.createElement('h1');
        h1.innerHTML = '窗前明月光';
        document.body.appendChild(h1);
        document.body.appendChild(h1);
        const h11 = h1.cloneNode(true);
        document.body.appendChild(h11);
    </script>
```



### Node.cloneNode

* `Node.cloneNode()` 方法返回调用该方法的节点的一个副本

#### 语法

```js
let dupNode = node.cloneNode(deep);
```

* **node**  将要被克隆的节点
* **dupNode**  克隆生成的副本节点
* **deep**  是否采用深度克隆，如果为 **true** ，则该节点的所有后代节点也都会被克隆；      如果为 `false`，则只克隆该节点本身。 















































