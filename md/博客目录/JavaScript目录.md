# JavaScript

[114_对象的方法补充](https://github.com/clouddawn/blog/blob/main/md/md7/235_JS%E5%8E%9F%E5%9E%8B%E5%86%85%E5%AE%B9%E8%A1%A5%E5%85%85.md)

* `hasOwnProperty`
* `in/for in` 操作符
* `instanceof`
* `isPrototypeOf`

[113_如何访问和修改对象的原型](https://github.com/clouddawn/blog/blob/main/md/md7/234_%E5%A6%82%E4%BD%95%E8%AE%BF%E9%97%AE%E5%92%8C%E4%BF%AE%E6%94%B9%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%8E%9F%E5%9E%8B.md)

* `Object.getPrototypeOf()`
* `Object.setPrototypeOf()`
* `Object.create()`

[112_JS 如何实现 Number.prototype.toString 方法？](https://github.com/clouddawn/blog/blob/main/md/md7/233_JS%E5%A6%82%E4%BD%95%E5%AE%9E%E7%8E%B0toString%E6%96%B9%E6%B3%95.md)

[111_深入JS面向对象继承](https://github.com/clouddawn/blog/blob/main/md/md7/232_%E6%B7%B1%E5%85%A5JS%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E7%BB%A7%E6%89%BF.md)

* JavaScript 中的类和对象
* 面向对象的特性 - 继承
* JavaScript 原型链
* Object 的原型
* 原型链关系的内存图
* Object 是所有类的父类
* 通过原型链实现继承
* 继承创建对象的内存图
* 原型链继承的弊端
* 借用构造函数继承
* 原型式继承函数
* 寄生式继承函数
* 寄生组合式继承

[110_JS创建多个对象的方案](https://github.com/clouddawn/blog/blob/main/md/md7/231_JS%E5%88%9B%E5%BB%BA%E5%A4%9A%E4%B8%AA%E5%AF%B9%E8%B1%A1%E7%9A%84%E6%96%B9%E6%A1%88.md)

* 字面量创建的方式
* 工厂模式
* 构造函数
* new 操作符调用的作用
* 对象的原型
* 函数的原型 prototype
* 创建对象的内存表现
* 赋值为新的对象
* prototype 添加属性
* constructor 属性
* 重写原型对象
* 原型对象的 constructor
* 创建对象 - 构造函数和原型结合

[109_Object方法对对象限制](https://github.com/clouddawn/blog/blob/main/md/md6/230_Object%E6%96%B9%E6%B3%95%E5%AF%B9%E5%AF%B9%E8%B1%A1%E9%99%90%E5%88%B6.md)

* `Object.preventExtensions()` 不可扩展
* `Object.seal()` 封闭对象
* `Object.freeze()` 冻结对象

[108_获取属性描述符](https://github.com/clouddawn/blog/blob/main/md/md6/229_%E8%8E%B7%E5%8F%96%E5%B1%9E%E6%80%A7%E6%8F%8F%E8%BF%B0%E7%AC%A6.md)

* `Object.defineProperties`
* `Object.getOwnPropertyDescriptor`
* `Object.getOwnPropertyDescriptors`

[107_JS 函数的 this 指向](https://github.com/clouddawn/blog/blob/main/md/md6/217_JS%E5%87%BD%E6%95%B0%E7%9A%84this%E6%8C%87%E5%90%91.md)

* 为什么需要 this ？
* this 指向什么呢？
* this 到底指向什么呢？
* 规则一：默认绑定
* 规则二：隐式绑定
* 规则三：显式绑定
* call、apply、bind
* 内置函数的绑定思考
* new 绑定
* 规则优先级

[106_call、apply、bind](https://github.com/clouddawn/blog/blob/main/md/md6/218_call_apply_bind.md)

[105_JS函数式编程](https://github.com/clouddawn/blog/blob/main/md/md6/219_JS%E5%87%BD%E6%95%B0%E5%BC%8F%E7%BC%96%E7%A8%8B.md)

* 实现 apply、call、bind
* 认识 arguments
* arguments 转成 array
* 箭头函数不绑定 arguments
* 理解 JavaScript 纯函数
* JavaScript 柯里化
* 理解组合函数

[104_JS额外知识补充](https://github.com/clouddawn/blog/blob/main/md/md6/221_JS%E9%A2%9D%E5%A4%96%E7%9F%A5%E8%AF%86%E8%A1%A5%E5%85%85.md)

* with 语句
* eval 函数
* 严格模式

[103_深入 JS 面向对象](https://github.com/clouddawn/blog/blob/main/md/md6/222_%E6%B7%B1%E5%85%A5JS%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.md)

* Object.defineProperty

[102_Object.keys 和 Object.getOwnPropertyNames 的区别](https://github.com/clouddawn/blog/blob/main/md/md6/223_Object_keys_getOwnPropertyNames.md)

[101_JS 中如何禁止对象添加新的属性？](https://github.com/clouddawn/blog/blob/main/md/md6/224_JS%E4%B8%AD%E5%A6%82%E4%BD%95%E7%A6%81%E6%AD%A2%E5%AF%B9%E8%B1%A1%E6%B7%BB%E5%8A%A0%E6%96%B0%E7%9A%84%E5%B1%9E%E6%80%A7.md)

* Object.preventExtensions()

[100_js实现所有单词首字母大写，其余字母小写](https://github.com/clouddawn/blog/blob/main/md/md6/228_JS%E5%AE%9E%E7%8E%B0%E6%89%80%E6%9C%89%E5%8D%95%E8%AF%8D%E9%A6%96%E5%AD%97%E6%AF%8D%E5%A4%A7%E5%86%99.md)

[99_方法](https://github.com/clouddawn/blog/blob/main/md/md1.5/25%20%E6%96%B9%E6%B3%95.md)

[98 JavaScript运行原理](https://github.com/clouddawn/blog/blob/main/md/md6/213%20JS%E8%BF%90%E8%A1%8C%E5%8E%9F%E7%90%86.md)

* 高级编程语言
* 浏览器的工作原理、内核、渲染过程
* JS引擎

[97 TypeScript会取代JavaScript吗](https://github.com/clouddawn/blog/blob/main/md/md6/212%20TypeScript%E4%BC%9A%E5%8F%96%E4%BB%A3JavaScript%E5%90%97%20.md)

* 类型约束

[96 JS引擎和代码执行](https://zhuanlan.zhihu.com/p/336562695)

[95 window](https://zhuanlan.zhihu.com/p/336570433)

[94 JS世界](https://zhuanlan.zhihu.com/p/336612395)

[93 倒计时案例](https://zhuanlan.zhihu.com/p/337166183)

[92 getter](https://zhuanlan.zhihu.com/p/407291302)

[91 String.prototype.slice()](https://zhuanlan.zhihu.com/p/407512625)

* 截取字符串

[90 String.prototype.substring()](https://zhuanlan.zhihu.com/p/407521858)

* 截取字符串

[89 for...in](https://zhuanlan.zhihu.com/p/407657059)

[88 Object.keys()](https://zhuanlan.zhihu.com/p/407657793)

[87 跨源资源共享（CORS）](https://zhuanlan.zhihu.com/p/407831284)

[86 async / await](https://zhuanlan.zhihu.com/p/408363923)

[85 Object.assign()](https://zhuanlan.zhihu.com/p/408510453)

[84 展开语法](https://zhuanlan.zhihu.com/p/408659399)

* ...

[83 Object.defineProperty()](https://zhuanlan.zhihu.com/p/408687633)

[82 JS 浅拷贝与深拷贝](https://zhuanlan.zhihu.com/p/409122020)

[81 如何用正则实现 trim()](https://zhuanlan.zhihu.com/p/409209516)

[80 不用 class 如何实现继承？用 class 又如何实现？](https://zhuanlan.zhihu.com/p/409215040)

[79 JS的解析过程与变量提升](https://zhuanlan.zhihu.com/p/302714610)

[78 break 和 continue 语句](https://zhuanlan.zhihu.com/p/307417839)

[77 质数练习的优化](https://zhuanlan.zhihu.com/p/307849929)

* 对象

[76 对象简介](https://zhuanlan.zhihu.com/p/307913392)

[75 对象的基本操作](https://zhuanlan.zhihu.com/p/308290178)

[74 属性名和属性值](https://zhuanlan.zhihu.com/p/311190216)

* 对象

[73 基本数据类型和引用数据类型](https://zhuanlan.zhihu.com/p/311540685)

* 堆/栈

[72 对象字面量](https://zhuanlan.zhihu.com/p/311602473)

[71 函数的简介](https://zhuanlan.zhihu.com/p/313965406)

[70 函数的参数](https://zhuanlan.zhihu.com/p/314038421)

[69 立即执行函数](https://zhuanlan.zhihu.com/p/316071291)

[68 什么是数组以及数组的创建方式](https://zhuanlan.zhihu.com/p/317180573)

[67 访问数组元素](https://zhuanlan.zhihu.com/p/317267189)

* for ... in

[66 遍历数组练习](https://zhuanlan.zhihu.com/p/319905240)

[65 数组中新增元素](https://zhuanlan.zhihu.com/p/320252836)

[64 for循环的用法](https://zhuanlan.zhihu.com/p/274764026)

[63 while和do...while循环的用法与区别](https://zhuanlan.zhihu.com/p/272505976)

[62 switch语句的用法](https://zhuanlan.zhihu.com/p/270310342?)

[61 Array.from()](https://github.com/clouddawn/blog/blob/main/md/md6/220_Array.form.md)

[60 事件参考](https://zhuanlan.zhihu.com/p/412771985)

[59 正则表达式测试题](https://zhuanlan.zhihu.com/p/416572232)

[58 DOM与BOM](https://github.com/clouddawn/blog/blob/main/md/md5/182%20DOM%E4%B8%8EBOM.md)

[57 Axios 是什么？怎么用？](https://zhuanlan.zhihu.com/p/424978482)

[56 正则测试题](https://zhuanlan.zhihu.com/p/375596721)

[55 FormData 是什么？怎么用？](https://zhuanlan.zhihu.com/p/425155791)

[54 JS 中的 Image() 怎么用？](https://zhuanlan.zhihu.com/p/434074559)

[53 JS 中的 XMLHttpRequest 对象怎么用？](https://zhuanlan.zhihu.com/p/435420620)

* ajax

[52 JS 中 XMLHttpRequest 的实例属性有哪些？](https://zhuanlan.zhihu.com/p/435430612)

* ajax

[51 JS 中 XMLHttpRequest 实例的方法有哪些？](https://zhuanlan.zhihu.com/p/435542501)

* ajax

[50 JS 中 XMLHttpRequest 实例的事件有哪些？](https://zhuanlan.zhihu.com/p/435547312)

* ajax

[49 JS 中的 Navigator.sendBeacon() 是干什么的？](https://zhuanlan.zhihu.com/p/435549202)

* ajax

[48 JS 中的 this 是用来干什么的？怎么用？](https://zhuanlan.zhihu.com/p/441408073)

[47 JS 获取时间戳与时间戳转换](https://zhuanlan.zhihu.com/p/441555310)

[46 JS 如何删除数组中的某一项？](https://zhuanlan.zhihu.com/p/442469214)

* splice

[45 如何使用 JS 将数组中的某一项移到第一位？](https://zhuanlan.zhihu.com/p/442927338)

[44 如何用 JS 禁止视频快进？](https://zhuanlan.zhihu.com/p/443314203)

[43 如何解决动态 rem 页面在微信浏览器中样式错乱？](https://zhuanlan.zhihu.com/p/443319104)

[43 JS 中的 onclick 怎么用？](https://zhuanlan.zhihu.com/p/446357411)

* 点击事件

[41 JS 中的 new 运算符怎么用？](https://zhuanlan.zhihu.com/p/452421922)

[40 如何理解 JS 中的闭包？](https://zhuanlan.zhihu.com/p/452629581)

[39 前端学习阶段性知识总结（一）](https://zhuanlan.zhihu.com/p/452824167)

* loader 和 plugin 的区别
* node require

[38 JS 中的构造函数是怎么用的？](https://zhuanlan.zhihu.com/p/463188810)

[37 浏览器渲染的机制？](https://zhuanlan.zhihu.com/p/455655385)

* 重绘
* 回流

[36 阻塞解析与阻塞渲染](https://zhuanlan.zhihu.com/p/458148110)

* css加载阻塞
* js加载阻塞

[35 JS 中点击事件的三种写法](https://zhuanlan.zhihu.com/p/463036941)

* 事件监听
* 捕获
* 冒泡

[34 JS 中的原型是什么？](https://zhuanlan.zhihu.com/p/463342900)

[33 JS 中 in 运算符的用法？](https://zhuanlan.zhihu.com/p/463469813)

* 判断属性是否在对象中

[32 JS 中 this 的三种情况？](https://zhuanlan.zhihu.com/p/463164020)

[31 JS 中的原型链是什么？](https://zhuanlan.zhihu.com/p/463493359)

[30 JS 中的垃圾回收？](https://zhuanlan.zhihu.com/p/464111503)

[29 JS 中的页面加载完成事件监听](https://zhuanlan.zhihu.com/p/464125152)

[28 JS 中 innerHTML 的用法？](https://zhuanlan.zhihu.com/p/464147284)

[27 JS中如何判断一个变量是否为数组？](https://zhuanlan.zhihu.com/p/466504843)

[26 如何用 JS 生成一个 h2 标签并插入到 div 中？](https://zhuanlan.zhihu.com/p/466636275)

* 原生 JS 操作 DOM

[25 js 如何实现点击按钮，显示按钮的文本？](https://zhuanlan.zhihu.com/p/467904693)

* js/jquery 点击事件

[24 JS 中 filter 的用法？](https://zhuanlan.zhihu.com/p/472088389)

* 筛选数组中的元素

[23 JS 中 for...in 和 for...of 的用法](https://zhuanlan.zhihu.com/p/472726315)

* 遍历对象的key
* 遍历对象

[22 原生 js 如何阻止事件冒泡？](https://zhuanlan.zhihu.com/p/475507871)

[21 JS 中 parseInt 的用法？](https://zhuanlan.zhihu.com/p/477138529)

* 取整

[20 JS 中字符串、数字的相互转换方法？](https://zhuanlan.zhihu.com/p/477491058)

[19 JS中的 Promise 怎么用？](https://zhuanlan.zhihu.com/p/435555341)

[18 JS 中 apply 的用法？](https://zhuanlan.zhihu.com/p/482252372)

[17 JS 中合并两个数组的办法？](https://zhuanlan.zhihu.com/p/482256286)

[16 JS 数组中 pop 和 shift 的用法？](https://zhuanlan.zhihu.com/p/482287647)

* 从数组中删除最后一个元素
* 从数组中删除第一个元素

[15 JS 数组中 unshift 的用法？](https://zhuanlan.zhihu.com/p/485627934)

* 将元素添加到数组开头

[14 JS 数组中 splice 的用法？](https://zhuanlan.zhihu.com/p/485655249)

* 替换数组中的元素

[13 JS 如何找出数组最大值？](https://zhuanlan.zhihu.com/p/486349743)

[12 JS 如何将数组中的元素倒序排列？](https://zhuanlan.zhihu.com/p/487825442)

[11 JS 不用 pop() 如何实现删除数组中最后一个元素？](https://zhuanlan.zhihu.com/p/487889054)

[10 JS 不用 unshift() 如何实现在数组的最前面添加任意个元素？](https://zhuanlan.zhihu.com/p/488464746)

* reset参数/三个点

[9 JS 中 toFixed() 的用法？](https://zhuanlan.zhihu.com/p/489156440)

* 指定取小数点后几位

[8 JS 中遍历数组的四种方法](https://zhuanlan.zhihu.com/p/491119682)

[7 JS 数组中 filter/map/reduce 的用法?](https://github.com/clouddawn/blog/blob/main/md/md5/181%20JS%20%E6%95%B0%E7%BB%84%E4%B8%AD%20filtermapreduce%20%E7%9A%84%E7%94%A8%E6%B3%95.md)

[6 Day.js](https://zhuanlan.zhihu.com/p/493982695)

* 处理日期、时间戳

[5 JS 实现数组去重的两个方法？](https://zhuanlan.zhihu.com/p/501240670)

[4 JS 如何实现数组排序？](https://zhuanlan.zhihu.com/p/501616981)

[3 ES5 如何实现模块化？](https://zhuanlan.zhihu.com/p/509084381)

- es5
- 匿名函数

[2 ES6：Module 的语法](https://zhuanlan.zhihu.com/p/509137259)

- import
- export
- 导入、导出

[1 如何用 JS 操作 Cookie?](https://zhuanlan.zhihu.com/p/509830488)

- cookie