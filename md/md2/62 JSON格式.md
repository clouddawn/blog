# JSON 格式

## 是什么

一种用于数据交换的文本格式，在很多配置文件里都能看到 xxx.json

## 格式

- 复合类型的值只能是数组或对象，不能是函数、正则表达式对象、日期对象。
- 简单类型的值只有四种：字符串、数值（必须以十进制表示）、布尔值和 null（不能使用 NaN, Infinity, -Infinity 和 undefined).
- 字符串必须使用双引号表示，不能使用单引号。
- 对象的键名必须放在双引号里面。
- 数组或对象最后一个成员的后面，不能加逗号。

```javascript
        // 合法的 JSON 格式
        ["one", "two", "three"]
        {"one":1,"two":2, "three":3}
        {"names":["王胖子","吴邪"]}
        {[{"name": "张起灵"},{"name": "闷油瓶"}]}
```

.

```javascript
        {name:"张三", 'age':32} // 属性名必须使用双引号
        [32, 64, 128, 0xFFF] // 不能使用十六进制值
        {"name":"张三", "age":undefined} //不能使用 undefined
```

## JS 内置对象

- JSON.stringify  
  用于把一个值变成符合 JSON 格式的字符串

```javascript
let obj = {
  a: 1,
  b: 2,
};
let str = JSON.stringify(obj);
console.log(str);
```

![image](../images2/62/1.png)(1)

- JSON.parse  
  用于把一个符合 JSON 格式的字符串还原对象

```javascript
let obj = {
  a: 1,
  b: 2,
};
let str = JSON.stringify(obj);
console.log(str);

let newObj = JSON.parse(str);
console.log(newObj);
```

![image](../images2/62/2.png)(2)

## JavaScript 对象 VS JSON

JavaScript 对象的字面量写法只是长的像 JSON 格式数据，二者属于不同的范畴，JavaScript 对象中很多类型（函数、正则、Date）JSON 格式的规范并不支持，JavaScript 对象的字面量写法更宽松。
