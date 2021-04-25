# computed 和 watch

## computed - 计算属性

### 用途

* 被计算出来的属性就是计算属性
* 例1：[用户名展示](https://codesandbox.io/s/compassionate-lake-xyjkw)
* 例2：[列表展示](https://codesandbox.io/s/sleepy-brook-721ec)
  * [不用 computed 筛选男女](https://codesandbox.io/s/modest-matsumoto-pd03w)
  * [用 computed 筛选男女](https://codesandbox.io/s/little-breeze-hdx44)

### 缓存

* 如果依赖的属性没有变化，就不会重新计算
* getter / setter 默认不会做缓存，Vue 做了特殊处理
* 如何缓存？看[示例]() 
* 示例仅供参考，并非 Vue 源码，只是实现的一种方式

## watch - 监听/侦听

### 用途

* 当数据变化时，执行一个函数
* 例1：[撤销](https://codesandbox.io/s/lucid-shamir-cpcw3)
* 例2：[模拟computed](https://codesandbox.io/s/objective-star-vu2h3)

### 何谓变化？

* 看[示例](https://codesandbox.io/s/still-snowflake-m62t1)
* obj 原本是 `{a:'a'}`，现在`obj={a:'a'}`，请问
* obj 变了没有？obj.a 变了没有
* obj 变了，obj.a 没变
* 简单类型看值，复杂类型（对象）看地址
* 这其实就是 === 的规则

### watch语法一 文档

* 类型：`{[key:string]:string | Function | Object | Array}`

* 详细：

  一个对象，键是需要观察的表达式，值是对应回调函数。值也可以是方法名，或者包含选项的对象。Vue 实例将会在实例化时调用`$watch()`，遍历 watch 对象的每一个 property 。

* 示例：

```js
var vm = new Vue({
    data:{
        a:1,
        b:2,
        c:3,
        d:4,
        e:{
            f:{
                g:5
            }
        }
    },
    watch:{
        a:function(val,oldVal){
            console.log('new:%s, old:%s',val,oldVla)
        },
        //方法名
        b:'someMethod',
        //该回调会在任何被侦听的对象的 property 改变是被调用，不论起被嵌套多深
        c:{
            handler:function(val,oldVal){
                /*...*/
            },
            deep:true
        },
        //该回调将会在侦听开始之后被立即调用
        d:{
            handler:'someMethod',
            immediate:true
        },
        //你可以传入回调数组，它们会被逐一调用
        e:[
            'handle1',
            function handle2(val,oldVal){
                /*...*/
            },
            {
                handler:function handle3(val,oldVal){
                    /**/
                },
            },
        ],
        //watch vm.e.f's value:{g:5}
        'e.f':function (val,oldVal){
            /*...*/
        }
    }
})
vm.a = 2 // => new:2,old:1
```

* 注意，不应该使用箭头函数来定义 watcher 函数（例如`searchQuery: newValue => this.updateAutocomplete(newValue)`）。理由是箭头函数绑定了父级作用域的上下文，所以`this`将不会按照期望指向 Vue 实例，`this.updateAutocomplete`将是 undefined 。

### 语法2

```js
vm.$watch('xxx',fn,{deep:.., immediate:..})
```

* 其中 'xxx' 可以改为一个返回字符串的函数

#### deep: true 是干什么的？

* 如果 object.a 变了，请问 object 算不算也变了
* 如果你需要答案是**也变了**，那么就用 deep:true
* 如果你需要答案是**没有变**，那么就用 deep:false
* deep 的意思是，监听 object 的时候是否往深了看

### computed 和 watch的区别

- computed是计算属性，watch是侦听属性
- computed是用来计算某个值的，计算出来的值在使用时不需要加括号，直接作为属性使用；且computed会缓存计算结果，只要依赖属性不发生变化，就不会重新计算，直接返回已计算出来的结果
- watch是用于监听属性变化的，当监听的属性变化了会执行相应的函数；其中immediate为true表示第一次渲染也要执行函数；deep为true表示对象内部属性如果变化也认为对象变化，要执行对应的函数
- 如果一个属性依赖于其他属性变化，用computed；如果需要在一个属性发生变化时进行某些操作，用watch

























