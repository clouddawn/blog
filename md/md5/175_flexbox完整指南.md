# flexbox （弹性盒子）完整指南

弹性盒子是一种用于按行或按列布局元素的一维布局方法 。元素可以膨胀以填充额外的空间, 收缩以适应更小的空间。 

## 为什么是弹性盒子？

长久以来，CSS 布局中唯一可靠且跨浏览器兼容的创建工具只有 [floats](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/CSS_layout/Floats) 和 [positioning](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/CSS_layout/Positioning)。这两个工具大部分情况下都很好使，但是在某些方面它们具有一定的局限性。

以下简单的布局需求是难以或不可能用这样的工具（ [floats](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/CSS_layout/Floats) 和 [positioning](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/CSS_layout/Positioning)）方便且灵活的实现的：

- 在父内容里面垂直居中一个块内容。
- 使容器的所有子项占用等量的可用宽度/高度，而不管有多少宽度/高度可用。
- 使多列布局中的所有列采用相同的高度，即使它们包含的内容量不同。

## 一个简单的例子

[点击查看](https://codesandbox.io/embed/stupefied-margulis-yb3zk?fontsize=14&hidenavigation=1&theme=dark)

你可以看到这个页面有一个含有顶级标题的 `<header>` 元素，和一个包含三个 `<article>` 的 `<section>` 。我们将使用这些来创建一个非常标准的三列布局，如下所示：

![image](../images5/175/01.png)

首先，我们需要选择将哪些元素将设置为柔性的盒子。我们需要给这些 flexible 元素的父元素 `display` 设置一个特定值。在本例中，我们想要设置 `<article>` 元素，因此我们给 `<section>` 设置 display：

```css
section {
  display:flex
}
```

结果如下：

![image](../images5/175/01.png)

所以，就这样一个简单的声明就给了我们所需要的一切—非常不可思议，对吧？ 我们的多列布局具有大小相等的列，并且列的高度都是一样。 这是因为这样的 flex 项（flex容器的子项）的默认值是可以解决这些的常见问题的。 

## flex 模型说明

当元素表现为 flex 框时，它们沿着两个轴来布局：

- **主轴（main axis）**是沿着 flex 元素放置的方向延伸的轴（比如页面上的横向的行、纵向的列）。该轴的开始和结束被称为 **main start** 和 **main end**。
- **交叉轴（cross axis）**是垂直于 flex 元素放置方向的轴。该轴的开始和结束被称为 **cross start** 和 **cross end**。
- 设置了 `display: flex` 的父元素（在本例中是 `<section> `）被称之为 **flex 容器（flex container）。**
- 在 flex 容器中表现为柔性的盒子的元素被称之为 **flex 项**（**flex item**）（本例中是`<article>` 元素）

## 弹性盒属性

![image](../images5/175/02.svg)

### 父级（弹性容器）的属性

```css
.container {
  display: flex; /* or inline-flex */
}
```

这定义了一个 flex 容器，内联或块取决于给定的值，它为其所有直接子级启用 flex 上下文。



### flex-direction

![image](../images5/175/03.svg)

这建立了主轴，从而定义了 flex 项目在 flex 容器中的放置方向。

```css
.container {
  flex-direction: row | row-reverse | column | column-reverse;
}
```



### flex-wrap

![image](../images5/175/04.svg)

默认情况下，弹性项目都将尝试适应一行。您可以更改它并允许项目根据需要使用此属性进行包装。

```css
.container {
  flex-wrap: nowrap | wrap | wrap-reverse;
}
```

- `nowrap` （默认）：所有弹性项目都在一行上
- `wrap`: flex 项目将从上到下包裹到多行上。
- `wrap-reverse`: flex 项目将从下到上包裹在多行上。



### flex-flow

```css
.container {
  flex-flow: column wrap;
}
```

这是 `flex-direction` 和 `flex-wrap` 属性的简写。



### justify-content

```css
.container {
  justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;
}
```

![image](../images5/175/05.svg)



这定义了沿主轴的对齐方式。当一行中的所有 flex 项目都固定或灵活但已达到其最大大小时，它有助于分配剩余的额外可用空间。当项目溢出行时，它还可以对项目的对齐方式施加一些控制。



### align-items

```css
.container {
  align-items: stretch | flex-start | flex-end | center | baseline;
}
```

![image](../images5/175/06.svg)



### align-content

```css
.container {
  align-content: flex-start | flex-end | center | space-between | space-around;
}
```

![image](../images5/175/07.svg)



## 子项（弹性项目）的属性

![image](../images5/175/08.svg)

## order

```css
.item {
  order: 5; /* default is 0 */
}
```

![image](../images5/175/09.svg)



## flex-grow

```css
.item {
  flex-grow: 4; /* default 0 */
}
```

![image](../images5/175/10.svg)

* 负数无效



[Flex 青蛙游戏](https://flexboxfroggy.com/#zh-cn)











































