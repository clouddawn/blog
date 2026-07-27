# TypeScript 泛型

```ts
type A = "hi" | 123; // TS
var a = ["hi", 123]; // JS

type F<T> = T | T[];
type FNumber = F<number>;
type FString = F<string>;

var fn = (x: number) => x + 1;
```

---

```ts
// 泛型 = 广泛的类型
// const add = (a: number, b: number) => a + b;
// const add2 = (c: string, d: string) => c + d;

type Add<T> = (a: T, b: T) => T;
// type AddNumber = Add<number>
// type AddString = Add<string>
const addN: Add<number> = (a, b) => a + b;
const addS: Add<string> = (a, b) => a + b;
```

---





























