# Date对象（二）

### 封装一个函数，返回当前的时分秒 格式：08:08:08

```javascript
        function getTime(){
            let time = new Date();
            let h = time.getHours();
            h = h < 10 ? '0' + h : h;
            let m = time.getMinutes();
            m = m < 10 ? '0' + m : m;
            let s = time.getSeconds();
            s = s < 10 ? '0' + s : s;
            return h + ':' + m + ':' + s;
        }
        console.log(getTime());
```

### 获取日期总的毫秒形式 （时间戳） 
Date 对象是基于1970年1月1日（世界标准时间）起的毫秒数，我们经常利用总的毫秒数来计算时间，因为它更精确。

* valueOf()

```javascript
        var date = new Date();
        console.log(date.valueOf());
```

* getTime()

```javascript
        var date = new Date();
        console.log(date.getTime());
```
* 简单的写法，也是最常用的

```javascript
        var date = +new Date();
        console.log(date); 
```

* H5新增的

```javascript
        console.log(Date.now());
```



