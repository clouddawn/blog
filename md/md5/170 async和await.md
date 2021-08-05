# async 函数

* **async** 函数是使用 `async` 关键字声明的函数
* async 函数是 `AsyncFunction` 构造函数的实例，并且其中允许使用 `await` 关键字
* `async` 和 `await` 关键字让我们可以用一种更简洁的方式写出基于 `Promise` 的异步行为，而无需刻意地链式调用 `promise`

### 语法

```js
async function name([param[, param[, ... param]]]) {
    statements 
}
```

* `name` 函数名称
* `param` 要传递给函数的参数的名称
* `statements` 包含函数主体的表达式，可以使用 `await` 机制

### 描述

* `async`  函数可能包含 0 个或者多个 `await` 表达式。
* `await`  表达式会暂停整个 `async` 函数的执行进程并出让其控制权，只有当其等待的基于 `promise` 的异步操作被兑现或被拒绝之后才会恢复进程。
* `promise` 的解决值会被当做该 `await` 表达式的返回值。
* 使用 `async` / `await` 关键字就可以在异步代码中使用普通的 `try` / `catch` 代码块。
* `await` 关键字只在 `async` 函数内有效，如果你在 `async` 函数体之外使用它，就会抛出语法错误。



```js
function 摇色子(){
    return new Promise((resolve,reject) => {
        setTimeout(()=>{
            let n = parseInt(Math.random()*6+1,10);
            resolve(n);
        },2000)
    })
}

摇色子().then(
    x => {
        console.log("色子的点数是" + x)
    },
    () => {
        console.log("摇色子还能失败？")
    }
)
```

--------------

---------------

```js
function 摇色子(){
    return new Promise((resolve,reject) => {
        setTimeout(()=>{
            let n = parseInt(Math.random()*6+1,10);
            resolve(n);
        },2000)
    })
}

async function test(){
    let n = await 摇色子();
    console.log(n)
}
test()
```

----------------------

-------------

```js
function 猜大小(猜测){
    return new Promise((resolve,reject) => {
        setTimeout(()=>{
            let n = parseInt(Math.random()*6+1,10);
            if(n>3){
                if(猜测 === '大'){
                    resolve(n);
                }else{
                    reject(n);
                }
            }else{
                if(猜测 === '小'){
                    resolve(n);
                }else{
                    reject(n);
                }
            }
            resolve(n);
        },1000)
    })
}

async function test(){
    try{
        let n = await 猜大小('大');
        console.log('赢了赢了：' + n)
    }catch(error){
        console.log('输了输了：' + error)
    }
}

test()
```

-------

------------------

```js
function 猜大小(猜测){
    return new Promise((resolve,reject) => {
        setTimeout(()=>{
            let n = parseInt(Math.random()*6+1,10);
            if(n>3){
                if(猜测 === '大'){
                    resolve(n);
                }else{
                    console.log('error')
                    reject(n);
                }
            }else{
                if(猜测 === '小'){
                    resolve(n);
                }else{
                    console.log('error')
                    reject(n);
                }
            }
            resolve(n);
        },1000)
    })
}

// Promise.all([猜大小('大'),猜大小('大')])
// 	.then((x)=>{console.log(x)},(y)=>{console.log(y)})

async function test(){
    try{
        let n = await Promise.all([猜大小('大'),猜大小('大')]);
        console.log('赢了赢了：' + n)
    }catch(error){
        console.log('输了输了：' + error)
    }
}
test()
```

























