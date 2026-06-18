# JSON

JSON（JavaScript Object Notation，JavaScript 对象表示法）是一种轻量级的文本数据交换格式。它易于人类阅读和编写，也易于机器解析和生成。虽然名称源自 JavaScript，但 JSON 是独立于语言的标准格式，绝大多数编程语言都提供了对它的支持。

### 核心特点

- **自描述**：数据以键值对的形式组织，结构清晰。
- **紧凑**：比 XML 更简短，减少网络传输开销。
- **易于解析**：可以直接被 JavaScript 的 `JSON.parse()` 处理，其他语言也有对应的库。
- **纯文本**：可用任何文本编辑器打开查看。

### 基本语法规则

- **数据以键值对形式存在**：`"name": "Alice"`
- **键必须是带双引号的字符串**：`"key"`（有些实现允许不加引号，但标准要求双引号）
- **多个键值对用逗号分隔**
- **对象用花括号 {}** 包裹
- **数组用方括号 []** 包裹，数组内可包含多个值（对象、字符串、数字等）

### 支持的数据类型

| 类型   | 示例              |
| :----- | :---------------- |
| 字符串 | `"hello"`         |
| 数字   | `123`, `-3.14`    |
| 布尔值 | `true`, `false`   |
| 空值   | `null`            |
| 对象   | `{"name": "Bob"}` |
| 数组   | `[1, 2, "three"]` |

### 一个完整的 JSON 示例

```json
{
  "name": "张三",
  "age": 28,
  "isStudent": false,
  "hobbies": ["阅读", "游泳"],
  "address": {
    "city": "北京",
    "zipcode": "100000"
  },
  "favoriteNumber": null
}
```

### 常见用途

- **Web API 数据交换**：RESTful 接口广泛使用 JSON 传递请求和响应数据。
- **配置文件**：很多现代工具（如 npm、VS Code、Prettier）用 JSON 作为配置格式。
- **数据存储**：NoSQL 数据库（如 MongoDB）直接使用类似 JSON 的 BSON 格式。
- **前后端通信**：前端通过 `fetch` 或 `axios` 发送 JSON 给后端，后端返回 JSON。

### 注意事项

- JSON 不支持注释（部分实现如 JSON5 支持，但标准不支持）。
- 结尾不能有逗号（no trailing comma）。
- 字符串必须使用**双引号**，单引号不符合标准。
- JSON 没有日期类型，通常用字符串（如 ISO 8601 格式 `"2026-06-10T12:00:00Z"`）或数字时间戳表示。

### 在 JavaScript 中的使用

```javascript
// 解析 JSON 字符串 → 对象
const jsonStr = '{"name":"Tom","age":20}';
const obj = JSON.parse(jsonStr);  // { name: "Tom", age: 20 }

// 将对象 → JSON 字符串
const newJsonStr = JSON.stringify(obj);  // '{"name":"Tom","age":20}'
```

总的来说，JSON 凭借其简洁、通用、高效的特点，已经成为互联网上最主流的数据交换格式之一。如果你需要处理 Web API 的数据或保存配置信息，JSON 几乎总是首选。

