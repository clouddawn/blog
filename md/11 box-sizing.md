# box-sizing

在 CSS 盒子模型的默认定义里，你对一个元素所设置的 width 与 height 只会应用到这个元素的内容区。如果这个元素有任何的 border 或 padding ，绘制到屏幕上时的盒子宽度和高度会加上设置的边框和内边距值。  

![image](../images/11/box.png)  

box-sizing: border-box 告诉浏览器：你想要设置的边框和内边距的值是包含在width内的。也就是说，如果你将一个元素的width设为100px，那么这100px会包含它的border和padding，内容区的实际宽度是width减去(border + padding)的值。

注: border-box不包含margin

![image](../images/11/ie-box.png)

```html
    <div class="box1"></div>
    <div class="box2"></div>
```
```css
    * {
        margin: 0;
        padding: 0;
    }
    .box1 {
        width: 200px;
        height: 200px;
        border: 10px solid red;
        padding: 20px;
        margin: 50px;
    }
    .box2 {
        width: 200px;
        height: 200px;
        border: 10px solid red;
        padding: 20px;
        margin: 50px;
        box-sizing: border-box;
    }
```
![image](../images/11/ex1.png)