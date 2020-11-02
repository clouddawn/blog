# while和do...while循环的用法与区别
## 循环语句：
<font size= 3>
通过循环语句可以反复执行一段代码。  
</font>

## while循环
### 语法：

<font size=3>

```javascript
while(条件表达式){  
    语句...  
} 
``` 
while语句在执行时，先对条件表达式进行求值判断；  
如果值为true，则执行循环体，循环体执行完毕以后，继续对表达式进行判断；  
如果为true，则继续执行循环体，以此类推；  
如果值为false，则终止循环。 
```javascript
    var n = 1;
    while(true){
        alert(n++);
    }
```
像这种将条件表达式写死为true的循环，叫做死循环。  
该循环不会停止，除非浏览器关闭，因此在开发中要慎用。  
可以使用break，来终止循环。  
```javascript
    var n = 1;
    while(true){
        alert(n++);
        if(n == 10){
            break
        }
    }
```
```javascript
    //创建一个循环，往往需要三个步骤

    //1. 初始化一个变量
    var i = 1;

    //2. 在循环中设置一个条件表达式
     while(i <= 50){

        //3. 定义一个更新表达式，每次更新初始化变量
        document.write(i++ + "<br>");
    }
```
## do...while循环
### 语法：

<font size=3>

```javascript
    do{
        语句...
    }while(条件表达式)
```
### 执行流程：
do...while语句在执行时，会先执行循环体；
循环体执行完毕以后，再对while后的条件表达式进行判断；
如果结果为true，则继续执行循环体，执行完毕继续判断，以此类推；
如果结果为false,则终止循环。  

do...while和while功能类似，不同的是while是先判断后执行，而do...while是先执行，后判断。  

do...while可以保证循环体至少执行一次，而while不能。

```javascript
    var n = 1;
    do{
        alert(n++);
        if(n == 10){
        break;
        }
    }
    while(false)
```

### 小试牛刀
假如投资的年利率为5%，试求从10000块增长到20000块，需要多少年？
```javascript
    var m = 10000, n = 0;
    while(m<20000){
        m = m * 1.05;
        n++;
    }
    alert(n);
```
</font>
