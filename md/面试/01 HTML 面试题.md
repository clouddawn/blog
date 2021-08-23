# HTML 面试题

## 1. 如何理解 HTML 语义化？

 HTML 语义化是存在一个历史周期的，最开始我们的所有网页都是由后台开发人员使用 table 布局写的，然后是美工人员使用 div+css 来布局，这种方式没什么问题，就是不够语义化，现在前端就是使用正确的标签来进行页面开发，标题就写 h1 到 h6 ,段落就用 p 标签，文章就用 article 。

语义化有利于SEO，有助于搜索引擎的爬虫抓取更多的有效信息，爬虫是依赖于标签来确定上下文和各个关键字的权重；

语义化的HTML在没有CSS的情况下也能呈现较好的内容结构与代码结构；

语义化的HTML便于开发者阅读与维护；

## 2. meta viewport 是做什么用的，怎么写？

参考资料：

1. [设备像素、设备独立像素、CSS像素、分辨率、PPI、devicePixelRatio 的区别](https://zhuanlan.zhihu.com/p/68563760)
2. [meta viewport 是做什么用的，怎么写？](https://zhuanlan.zhihu.com/p/68539694)
3. [meta viewport 是用来做什么的？怎么用？](https://www.jianshu.com/p/cb1c0f1c71ab)
4. [meta viewport 是做什么用的，怎么写？](https://juejin.cn/post/6844904110873919502)

meta viewport 是用来做移动端适配的，让网页可以在移动端上得到很好的呈现。

meta 标签里面有两个属性，name 和 content 。name 里面写 viewport ，content 里面写 width = device-width ，宽度等于设备宽度；initial-scale = 1 ，页面的初始缩放比例为 1 ;  minimum-scale = 1 , maximum-scale = 1 ，用户能够放大和缩小的比例都为1，这是用来禁止用户缩放的；user-scalable = no ，也是用来禁止用户缩放的。之所以重复禁止用户缩放，是因为在有些浏览器上其中一个可能会失效。

```html
<meta name="viewport" content="width=device-width,initial-scale=1,minimum-scale=1,maximum-scale=1,user-scalable=no">
```

## 3. 你用过哪些 HTML 5 标签？
header main footer article audio video canvas

## 4. H5 是什么？
H5 泛指那些在移动端网络社交媒体，例如微信，中传播的，带有交互体验、动态效果以及音效的 Web 页面。