# HTML 面试题

## 1. 如何理解 HTML 语义化？

 HTML 语义化是存在一个历史周期的，最开始我们的所有网页都是由后台开发人员使用 table 布局写的，然后是美工人员使用 div+css 来布局，这种方式没什么问题，就是不够语义化，现在前端就是使用正确的标签来进行页面开发，标题就写 h1 到 h6 ,文章就写 article , 时间就用 time 标签，如果是一个画板，就用 canvas 标签。

## 2. meta viewport 是做什么用的，怎么写？

参考资料：

1. [设备像素、设备独立像素、CSS像素、分辨率、PPI、devicePixelRatio 的区别](https://zhuanlan.zhihu.com/p/68563760)
2. [meta viewport 是做什么用的，怎么写？](https://zhuanlan.zhihu.com/p/68539694)
3. [meta viewport 是用来做什么的？怎么用？](https://www.jianshu.com/p/cb1c0f1c71ab)
4. [meta viewport 是做什么用的，怎么写？](https://juejin.cn/post/6844904110873919502)

```html
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1">
```

