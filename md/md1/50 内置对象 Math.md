# 内置对象 Math

## 内置对象

* JS的对象分为3种：自定义对象、内置对象、浏览器对象等。
* **内置对象**就是JS语言自带的一些对象，这些对象供开发者使用，并提供了一些常用的或是最基本而必要的功能（属性和方法）。
* 内置对象最大的优点就是帮助我们快速开发。

## [Math](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math)

* Math 是一个内置对象，它拥有一些数学常数属性和数学函数方法。
* Math 数学对象，不是一个构造器，所以不需要 new 来调用，直接使用里面的属性和方法即可。

### [Math.PI](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/PI)

* Math.PI 表示一个圆的周长与直径的比例，即圆周率 Π

```javascript
    console.log(Math.PI);
```
![image](../images/50/1.png)(1)

### [Math.max](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/max)

* 返回给定的一组数字中的最大值。
* 如果有任一参数不能被转换为数值，则结果为 NaN。
* 如果没有参数，则结果为 - Infinity。

```javascript
    console.log(Math.max(1,34,98)); // 98
```
---
```javascript
    console.log(Math.max(1,34,'你大爷')); 
```
![image](../images/50/2.png)(2)

```javascript
    console.log(Math.max()); 
```
![image](../images/50/3.png)(3)