# CSS 面试题

## 两种盒模型分别说一下

content-box 和 border-box  ，也就是标准盒模型和怪异盒模型。content-box 的 宽度为内容的宽度，border-box 的宽度为内容的宽度加上内边距的宽度，再加上边框的宽度。

我平时喜欢用 border-box ，因为他更符合我的感觉。

## 如何垂直居中？
背代码 https://www.yuque.com/docs/share/708bd899-0c46-47ea-a94c-d7a189c0f7dc?# 《七种方式实现垂直居中》

## flex 怎么用，常用属性有哪些？
看 MDN，背代码。

## BFC 是什么？

BFC 全称是 Block Formatting Context，翻译过来就是块级格式化上下文。用BFC可以[包住浮动元素](http://js.jirengu.com/rozaxufetu/1/edit?html,css,output)，也可以用 [float + div 做左右自适应布局](http://js.jirengu.com/felikenuve/1/edit?html,css,output)。

在浮动元素的父元素上加一个 overflow: hidden ，父元素就可以包住浮动元素；在与 float 元素并列的元素上加一个 overflow: hidden，就可以做自适应的布局。

 BFC 触发条件有：

1. 浮动元素（元素的 float 不是 none）
2. 绝对定位元素（元素的 position 为 absolute 或 fixed）
3. 行内块元素 display: inline-block
4. overflow 值不为 visible 的块元素
5. 弹性元素（display为 flex 或 inline-flex元素的直接子元素）

## CSS 选择器优先级

1. 背人云亦云的答案（错答案、已过时）：https://www.cnblogs.com/xugang/archive/2010/09/24/1833760.html

2. 正确答案

   * 越具体优先级越高

   * 同样优先级写在后面的覆盖写在前面的

   * !important 优先级最高，但是要少用

## 清除浮动说一下

```css
 .clearfix:after{
     content: '';
     display: block; /*或者 table*/
     clear: both;
 }
 .clearfix{ // 加到容器上，里面的子元素的浮动就被清除了
     zoom: 1; /* IE 兼容*/
 }
```