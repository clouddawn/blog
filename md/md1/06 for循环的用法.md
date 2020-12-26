# for循环
<font size=3>
for语句是一个循环语句，称为for循环。  

在for循环中，为我们提供了专门的位置用来放三个表达式：  
1. 初始化表达式
2. 条件表达式
3. 更新表达式  

## 用法： 

```javascript
    for(初始化表达式;条件表达式;更新表达式){  
        语句...  
    }
```

## 执行流程：

```javascript
    for( 1 初始化表达式; 2 条件表达式; 4 更新表达式){  
        3 语句...  
    }
```
1 执行初始化表达式，初始化变量  
2 执行条件表达式，判断是否执行循环；  
&ensp; 如果为true，则执行循环 3；  
&ensp; 如果为false，则终止循环。  
4 执行更新表达式，更新表达式执行完毕继续重复 2

```javascript
    for(var i=0; i<10; i++){
        alert(i);
    }
```

如果在for循环中不写任何的表达式，只写两个分号（；），此时循环是一个死循环，会一直执行下去，慎用！

```javascript
    for(;;){
        alert("来了，老弟");
    }
```

## 注意

使用while循环做不了的，使用for循环同样也做不到。也就是说，for循环只是把与循环有关的代码集中在了一个位置。

## 示例

```javascript
    //打印1~100之间所有奇数之和。
    var n = 1 , sum = 0;
    for(;n<=100;n++){
        if(n % 2 != 0){
            sum = sum + n;
        }               
    }
    alert(sum);
```
```javascript
    //打印1~100之间所有7的倍数的个数及总和。
    var n = 1 , sum = 0 , count = 0;
    for(;n<=100;n++){
        if(n % 7 == 0){
            sum = sum + n;
            count++;
            document.write(n + "、" +"<br>");
        }               
    }
    document.write("1到100之间所有7的倍数的个数为" + g +"<br>");
    document.write("1到100之间所有7的倍数的总和" + sum +"<br>");
```
```javascript
    /*水仙花数
    水仙花数是一个3位数，它的每个位上的数字的3次幂之和等于它本身，
    （例如：1^3 + 5^3 + 3^3 = 153)，请打印出所有的水仙花数。*/
    var n = 100;
    for(;n<=999;n++){
        var bai = parseInt(n/100);
        var shi = parseInt((n-(bai*100))/10);
        var ge = n % 10;
        if(n == (bai*bai*bai + shi*shi*shi + ge*ge*ge)){
            document.write(n + "、");
        }
    }
```
</font>