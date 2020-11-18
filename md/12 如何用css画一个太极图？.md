# 如何用css画一个太极图？
## html
```html
    <div class="yin-yang"></div>
```
# css
```css
    .yin-yang {
        width: 196px;
        height: 98px;
        border-color: red;
        border-style: solid;
        border-width: 2px 2px 100px 2px;
        border-radius: 50%;
        position: relative;
        margin: 50px;
    }
    .yin-yang:before {
        content: "";
        position: absolute;
        top: 50%;
        left: 0;
        border: 36px solid red;
        border-radius: 50%;
        width: 24px;
        height: 24px;
        background-color: white;
    }
    .yin-yang::after {
        content: "";
        position: absolute;
        top: 50%;
        left: 50%;
        border: 36px solid white;
        background-color: red;
        border-radius: 50%;
        width: 24px;
        height: 24px;
    }
```
![image](../images/11/yinyang.png)