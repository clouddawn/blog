# 如何用css画一个太极图？
## 方法一
### html
```html
    <div class="yin-yang">
        <div class="bsc">
            <div class="bssc"></div>
        </div>
        <div class="wsc">
            <div class="wssc"></div>
        </div>
    </div>
```
### css
```css
.yin-yang {
    width: 200px;
    height: 200px;
    border-radius: 50%;
    margin: 100px;
    background: linear-gradient(180deg, rgba(255,255,255,1) 0%, rgba(255,255,255,1) 50%, rgba(0,0,0,1) 50%, rgba(0,0,0,1) 100%);
    position: relative;
}
.yin-yang .bsc {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    background-color: black;
    position: absolute;
    top: 50px;
    left: 0;
}
.yin-yang .bsc .bssc {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background-color: white;
    position: absolute;
    top: 50px;
    left: 40px;
}
.yin-yang .wsc {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    background-color: white;
    position: absolute;
    top: 50px;
    right: 0;
}
.yin-yang .wsc .wssc {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background-color: black;
    position: absolute;
    top: 50px;
    right: 40px;
}
```
![image](../images/12/ptyy.png)

## 方法二

### html
```html
    <div class="yin-yang"></div>
```
### css
```css
    .yin-yang {
        width: 196px;
        height: 98px;
        border-style: solid;
        border-width: 2px 2px 100px 2px;
        border-color: black;
        border-radius: 50%;
        position: relative;
        margin: 100px;
    }
    .yin-yang:before {
        content: "";
        position: absolute;
        top: 50%;
        left: 0;
        border: 37px solid black;
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
        border: 37px solid white;
        background-color: black;
        border-radius: 50%;
        width: 24px;
        height: 24px;
    }
```
![image](../images/12/yinyang.png)

## 方法三

### html

```html
    <div class="yin-yang"></div>
```

### css

```css
body {
    background-color: #555555;
}
.yin-yang {
    width: 200px;
    height: 200px;
    border-radius: 50%;
    margin: 100px;
    background: linear-gradient(180deg, rgba(255,255,255,1) 0%, rgba(255,255,255,1) 50%, rgba(0,0,0,1) 50%, rgba(0,0,0,1) 100%);
    position: relative;
    margin: 100px;
}
.yin-yang::before {
    content: "";
    width: 100px;
    height: 100px;
    border-radius: 50%;
    position: absolute;
    top: 50px;
    left: 0;
    background: radial-gradient(circle, rgba(255,255,255,1) 0%, rgba(255,255,255,1) 24%, rgba(0,0,0,1) 24%);
}
.yin-yang::after {
    content: "";
    width: 100px;
    height: 100px;
    border-radius: 50%;
    position: absolute;
    top: 50px;
    right: 0;
    background: radial-gradient(circle, rgba(0,0,0,1) 0%, rgba(0,0,0,1) 24%, rgba(255,255,255,1) 24%);
}
```
![image](../images/12/three.png)

## 方法四 会动的太极图

### html
```html
    <div class="yin-yang"></div>
```

### css
```css
* {
    margin: 0;
    padding: 0;
}
body {
    background-color: #555555;
}
.yin-yang {
    width: 200px;
    height: 200px;
    border-radius: 50%;
    margin: 100px;
    background: linear-gradient(180deg, rgba(255,255,255,1) 0%, rgba(255,255,255,1) 50%, rgba(0,0,0,1) 50%, rgba(0,0,0,1) 100%);
    position: relative;
    margin: 100px;
    animation-name: spin;
    animation-duration: 3s;
    animation-iteration-count: infinite;
    animation-timing-function: linear;
}
.yin-yang::before {
    content: "";
    width: 100px;
    height: 100px;
    border-radius: 50%;
    position: absolute;
    top: 50px;
    left: 0;
    background: radial-gradient(circle, rgba(255,255,255,1) 0%, rgba(255,255,255,1) 24%, rgba(0,0,0,1) 24%);
}
.yin-yang::after {
    content: "";
    width: 100px;
    height: 100px;
    border-radius: 50%;
    position: absolute;
    top: 50px;
    right: 0;
    background: radial-gradient(circle, rgba(0,0,0,1) 0%, rgba(0,0,0,1) 24%, rgba(255,255,255,1) 24%);
}
@keyframes spin {
    form {
        transform: rotate(0deg);
    }
    to {
        transform: rotate(360deg);
    }
}
```
![image](../images/12/ayin.png)
