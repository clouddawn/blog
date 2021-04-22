# computed 和 watch

## computed - 计算属性

### 用途

* 被计算出来的属性就是计算属性
* 例1：[用户名展示](https://codesandbox.io/s/compassionate-lake-xyjkw)
* 例2：[列表展示](https://codesandbox.io/s/sleepy-brook-721ec)

### 缓存

* 如果依赖的属性没有变化，就不会重新计算
* getter / setter 默认不会做缓存，Vue 做了特殊处理
* 如何缓存？看[示例]() 
* 示例仅供参考，并非 Vue 源码，只是实现的一种方式