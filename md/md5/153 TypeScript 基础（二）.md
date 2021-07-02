# TypeScript 基础（三）

```ts
// class 是类型还是值？
class A {

}
const B = A
// 说明 A 可以是值

const a:A = new A()
// 说明 A 是类型

// 所以 A 既是值又是类型
```

---

```ts
// 联合类型与区分联合类型
const f = (n: string | number) => {};
//------
type A = {
  name: 'a';
  age: number;
};
type B = {
  name: 'b';
  gender: string;
};
const fn = (n: A | B) => {
    if(n.name === 'a'){
        n.age
    }else{
        n.gender
    }
};
```

---

```ts
// 交叉类型 &
type A = number & string; // never
//------

type B = { name: string } & { age: number };
const a: B = {
  name: "frank",
  age: 18,
};
//------
```

---

```ts
function min(a: number, b: number): number {
  if (a < b) {
    return a;
  } else {
    return b;
  }
}
var c = min(8, 2);
console.log(c);
```

---

```ts
// 重载
function add(a: string, b: string): string;
function add(a: number, b: number): number;
function add(a: any, b: any): any {
  return a + b;
}

var c = add('3', '4');
console.log(c);
```

---

```ts
enum Gender {
  Male,
  Female,
}

interface Person {
  gender: Gender;
}

function merry(a: Person, b: Person): [Person, Person] {
  if (a.gender !== b.gender) {
    return [a, b];
  } else {
    throw new Error("性别不同才能结婚");
  }
}

let a = { gender: Gender.Male };
let b = { gender: Gender.Male};
console.log(merry(a, b));
```

---



































