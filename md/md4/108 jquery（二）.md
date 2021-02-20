# jQuery 概述

## JavaScript 库

* 仓库：可以把很多东西放到这个仓库里面，找东西只需要到仓库里面查找就可以了。
* JavaScript库：即 libraty，是一个封装好的待定的集合（方法和函数）。从封装一大堆函数的角度理解库，就是在这个库中，封装了很多预先定义好的函数在里面，比如动画 amimate、hide、show，比如获取元素等。
* 简单理解：就是一个 JS 文件，里面对我们原生 JS 代码进行了封装，存放到里面，这样我们就可以快速高效的使用这些封装好的功能了。
* 比如 jQuery，就是为了快速方便的操作 DOM，里面基本都是函数（方法）。

### 常见的 JavaScript 库

* jQuery
* Prototype
* YUI
* Dojo
* Ext JS
* 移动端的 zepto

这些库都是对原生 JavaScript 的封装，内部都是用 JavaScript 实现的。

### jQuery 的概念

* jQuery 是一个快速、简介的 JavaScript 库，其设计的宗旨是 "write less, do more" ，即倡导写更少的代码，做更多的事情。
* j 就是 JavaScript；Query 查询；意思就是查询 js，把 js 中的 DOM 操作做了封装，我们可以快速的查询使用里面的功能。
* jQuery 封装了 JavaScript 常用的功能代码，优化了 DOM 操作、事件处理、动画设计和 Ajax 交互。
* 学习 jQuery 的本质就是学习调用这些函数（方法）。
* jQuery 出现的目的是加快前端人员的开发速度，我们可以非常方便的调用和使用它，从而提高开发效率

## jQuery 的优点

* 轻量级。核心文件才几十kb，不会影响页面加载速度
* 跨浏览器兼容。基本兼容了现在主流的浏览器
* 链式编程、隐式迭代
* 对事件、样式、动画支持，大大简化了DOM操作
* 支持插件扩展开发。有着丰富的第三方插件，例如：树形菜单、日期控件、轮播图等
* 免费、开源

## jQuery 的下载

官网地址：https://jquery.com

版本：

* 1x：兼容 IE 678 等低版本浏览器，官网不再更新
* 2x：不兼容 IE 678 等低版本浏览器，官网不再更新
* 3x：不兼容 IE 689 等低版本浏览器，是官方主要更新维护的版本

各个版本的下载：https://code.jquery.com

## jQuery 的使用步骤

* 引入 jQuery 文件
* 使用即可

## jQuery 的入口函数

```js
$(function (){
    ... // 此处是页面 DOM 加载完成的入口
});
```

```js
$(document).ready(function(){
    ... // 此处是页面 DOM 加载完成的入口
});
```

* 等着 DOM 结构渲染完毕即可执行内部代码，不必等到所有外部资源加载完成，jQuery 帮我们完成了封装
* 相当于原生 js 中的 DOMContentLoaded
* 不同于原生 js 中的 load 事件是等页面文档、外部的 js 文件、css 文件、图片加载完毕才执行内部代码
* 更推荐使用第一种方式

































