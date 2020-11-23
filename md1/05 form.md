# form、input和button标签详解

## form
<font size=3>

**a标签和form标签的区别：**    
a标签跳转页面时发起的是 **http get** 请求。  
form标签跳转页面时发起的请求方式可以通过 **method** 设置；

**注意**：如果form表单里面没有提交按钮，则无法提交。  

**get** 是获取内容；**post** 是上传内容。

## 示例
```html
    <form action="users" method="POST" name="users">
        <input type="text" name="username">
        <input type="password" name="password">
        <input type="submit" value="提交">
    </form>
```
![image](../images/post.png)  

## input
### type:
button 按钮，上面显示 value 属性的值。

## button 
在form表单中，如果button没有加type属性，则默认type为submit。

## radio
```html
        <input type="radio" name="loveme" value="yes">yes
        <input type="radio" name="loveme" value="no">no
```

## checkbox
```html
        喜欢的水果：<label><input type="checkbox" name="fruit" value="apple">苹果</label>
        <label><input type="checkbox" name="fruit" value="orange">橘子</label>
        <label><input type="checkbox" name="fruit" value="pear">梨</label>
```
![image](../images/checkbox0.png)
![image](../images/checkbox.png)

## label

label 元素为鼠标用户改进了可用性。如果你在 label 元素内点击文本，就会触发此控件。就是说，当你选择该标签时，浏览器就会自动将焦点转到和标签相关的表单控件上。

label 标签的 for 属性应当与相关元素的 id 属性相同。

示例：  
```html
<label for="user">用户名：</label>
<input type="text" name="username" id="user">
```
```html
<label>用户名：<input type="text" name="username"></label>
```

## select
```html
        <select name="group" multiple><!--multiple表示可以多选，按住shift或ctrl即可-->
            <option value="" selected>请选择</option><!--selected表示默认选择-->
            <option value="first">第一组</option>
            <option value="second" disabled>第二组</option>
            <option value="third">第三组</option><!--disable表示不能选择-->
        </select>
```
</font>