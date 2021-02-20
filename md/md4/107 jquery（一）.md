# 浅析jQuery 

## jQuery 有多牛X

* 它是目前前端最长寿的库，2006年发布
* 它是世界上使用最广泛的库，现在仍有80%的网站在用

## jQuery 用到了哪些设计模式

* 不用 new 的构造函数，这个模式没有专门的名字
* $（支持多种参数），这个模式叫做重载
* 用闭包隐藏细节，这个模式没有专门的名字 

## 链式风格

* 也叫 jQuery 风格
* `window.jQuery()` 是我们提供的全局函数

## 特殊函数 jQuery

*  `jQuery(选择器)` 用于获取对应的元素
* 但它却不返回这些元素
* 相反，它返回一个对象，称为 jQuery 构造出来的对象
* 这个对象可以操作对应的元素

## jQuery 是构造函数吗？

### 是

* 因为 jQuery 函数确实构造出了一个对象

## 不是

* 因为不需要写 `new jQuery()` 就能构造一个对象

### 结论

* jQuery 是一个不需要加 new 的构造函数
* jQuery 不是常规意义上的构造函数

## 查

```js
jQuery('#xxx') 返回值并不是元素，而是一个 api 对象

jQuery('#xxx').find('.red') 查找 #xxx 里的 .red 元素

jQuery('#xxx').parent() 获取爸爸

jQuery('#xxx').children() 获取儿子

jQuery('#xxx').siblings() 获取兄弟

jQuery('#xxx').index() 获取排行老几（从0开始）

jQuery('#xxx').next() 获取弟弟

jQuery('#xxx').prev() 获取哥哥

jQuery('.red').each(fn) 遍历并对每个元素执行 fn
```

## jQuery 太长，可以添加一个别名

* `window.$ = window.jQuery`

### 命名风格 

#### 下面的代码令人误解

* `const div = $('div#test')`
* 我们会误以为 div 是一个 DOM
* 实际上 div 是 jQuery 构造的 api 对象
* 怎么避免这种误解呢？

#### 改成这样

* `const $div = $('div#test')`
* `$div.appendChild` 不存在，因为它不是 DOM 对象
* `$div.find` 存在，因为它是 jQuery 对象

























