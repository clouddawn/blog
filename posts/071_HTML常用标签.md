# HTML常用标签

## 完整的HTML结构

一个完整的HTML结构包括哪几部分呢？

* 文档声明
* html 元素
  * head 元素
  * body 元素

```html
<!doctype html>
<html lang="en">
<head>
	<title>Document</title>
</head>
<body>
	<h1>一帆风顺</h1>
</body>
</html>
```

## 文档声明

HTML最上方的一段文本我们称之为**文档类型声明**，用于声明**文档类型**

```html
<!doctype html>
```

* HTML文档声明，告诉浏览器当前页面是HTML5页面；
* 让浏览器用HTML5的标准去解析识别内容；
* 必须放在HTML文档最前面，不能省略，省略了会出现兼容性问题；

## html元素

`<html>` 元素表示一个 HTML 文档的**根**（顶级元素），所以它也被称为**根元素**。

* 所有其他元素必须是此元素的后代。

W3C标准建议为 html 元素增加一个 **lang 属性**，作用是

* 帮助语音合成工具确定要使用的发音；
* 帮助翻译工具确定要使用的翻译规则；

**比如常用的规则：**

* `lang="en"` 表示这个 HTML 文档的语言是英文；
* `lang-"zh-CN"` 表示这个 HTML 文档的语言是中文；

## head 元素

**HTML head 元素** 规定文档相关的**配置信息（也称之为元数据）**，包括文档的标题、引用的文档格式和脚本等。

* 元数据（meta data）即描述数据的数据，可以理解成对整个页面的配置。

一般至少会包含如下两个设置
* 网页的标题：title 元素

  ```html
  <title>网页的标题</title>
  ```

* 网页的编码：meta 元素

  * 可以用于设置网页的字符编码，让浏览器更精准地显示每一个问题，不设置或者设置错误会导致乱码；

  * 一般都使用uft-8编码，涵盖了世界上几乎所有的文字；

    ```html
    <meta charset="utf-8">
    ```

## body 元素

body 元素里面的内容将是你在浏览器窗口中看到的东西，也就是网页的具体内容和结构，大部分HTML元素都是在body中编写呈现的。

## a元素

### 网址

* https://google.com
- http://google.com
* //google.com

### 属性

* **href：**Hypertext Reference 的简称
  * 指定要打开的 URL 地址；
  * 也可以是一个本地地址；
* **target**：该属性指定在何处显示链接的资源。
  * _self：属性值，在当前窗口打开 URL；
  * _blank：在一个新的窗口中打开 URL;

### 伪协议

* javascript: 代码 ;
  * `<a href="javascript:;">啥都不干</a>`
* mailto: 邮箱
  * `<a href="mailto:1256926083@qq.com">举报</a>`
* tel: 手机号
  * `<a href="tel:17756658235">摇人</a>`

* id: href=#id名，可以跳转到id名为Id的标签

1. * `<p id="xxxx"></p>, <a href="#xxx"></a>`就可以定位到这个p标签

## table标签

### thread

### tbody

### tfoot

* tr 
  * table row 一行

* th
  * table head 表头

* td
  * table data 数据

```html
    <table>
        <thead>
            <tr>
                <th></th>
                <th>小明</th>
                <th>小红</th>
                <th>小颖</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <th>数学</th>
                <td>89</td>
                <td>99</td>
                <td>79</td>
            </tr>
            <tr>
                <th>英语</th>
                <td>69</td>
                <td>87</td>
                <td>93</td>
            </tr>
            <tr>
                <th>语文</th>
                <td>89</td>
                <td>87</td>
                <td>49</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <th>总分</th>
                <td>200</td>
                <td>189</td>
                <td>169</td>
            </tr>
        </tfoot>
    </table>
```

![image](../images3/73/01.PNG)

## table的样式

* table-layout：

  * `auto;` 表示根据内容来计算宽度
* `fixed;` 表示定宽，尽可能地让宽度平均

```css
      	/*auto*/
		table {
            width: 600px;
            table-layout: auto;
        } 
         th,td {
            border: 1px solid black;
        }
```

![image](../images3/73/02.PNG)

```css
        /*fixed*/
		table {
            width: 600px;
            table-layout: fixed;
        } 
         th,td {
            border: 1px solid black;
        }
```

![image](../images3/73/03.PNG)

* border-collapse 和 border-spacing用来调整表格Border的间隔

  * `border-collapse` 属性用来决定表格的边框是分开的还是合并的。在分隔模式下，相邻的单元格都拥有独立的边框。在合并模式下，相邻单元格共享边框。

  * `border-spacing` 属性指定相邻单元格边框之间的距离。

    ```css
            /*border-collapse*/
    		table {
                width: 600px;
                table-layout: fixed;
                border-collapse: collapse;
            } 
             th,td {
                border: 1px solid black;
            }
    ```

  ![image](../images3/73/04.PNG)

  ​		

   ```css
          /*border-spacing*/
          table {
              width: 600px;
              table-layout: fixed;
              border-spacing: 0;
          } 
           th,td {
              border: 1px solid black;
          }
   ```

  ![image](../images3/73/05.PNG)

## img元素

* 我们应该如何告诉浏览器来显示一张图片呢？使用 img 元素。

* img 是一个可替换元素（replaced element）;

### 作用

* 发出 get 请求，展示一张图片

### 属性

* src  图片地址
* alt  如果图片加载失败，会显示 alt 属性的文字
* width / height  宽/高，如果只写其中一个，另一个会自适应。

## 事件

* onload  加载成功
* onerror  加载失败

### 示例

* 在图片加载失败时，加载备用图片

  ```html
      <style>
          img {
              max-width: 100%;
          }
      </style>
      <img id="xxx" src="images/2.PNG" alt="棋魂">
      <img id="yyy" src="images/250.png" alt="250">
      <script>
          xxx.onload = function() {
              console.log('xxx加载成功');
          }
          xxx.onerror = function() {
              console.log('xxx加载失败');
          }
          yyy.onload = function() {
              console.log('yyy加载成功');
          }
          yyy.onerror = function() {
              console.log('yyy加载失败');
              yyy.src="/images/404.png"
          }
      </script>
  ```

  ![image](../images3/73/06.PNG)

 ## 响应式

* max-width: 100%  这样图片就可以自适应不同的屏幕大小。



## form 标签

### 作用

* 发 get 或 post 请求，然后刷新页面

## 属性

* action  往哪里发请求
* method  用哪种方式请求，GET或POST
* autocomplete  自动填充
  * `off`：在每一个用到的输入域里，用户必须显式的输入一个值，浏览器不会自动补全输入。
  * `on`：浏览器能够根据用户之前在表单里输入的值自动补全, 会给出填这个表单的提示。
* target: 在当前页面提交，还是新开一个页面提交

#### input 的 submit 和 button 的 submit 有什么区别？

* input 标签里不能再有其他的标签
* button 标签里可以有其他的标签，可以对提交按钮设置样式



## iframe 元素

* 利用 iframe 元素可以实现：在一个 HTML 文档中嵌入其他 HTML 文档
* frameborder 属性
  * 用于规定是否显示边框
    * 1：显示
    * 0：不显示
* a 元素 target 的其他值：
  * _parent: 在父窗口找那个打开url
  * _top：在顶层窗口中打开url



## HTML 全局属性

某些属性只能设置在特定的元素中：

* 比如 img 元素的 src、a 元素的 href；

也有一些属性是所有 HTML 都可以设置和拥有的，这样的属性我们称之为“全局属性（Global Attrubutes）”。

### 常见的全局属性如下：

* **id**：定义唯一标识符，该标识符在整个文档中必须是唯一的。其目的是在链接（使用片段标识符），脚本或样式（使用CSS）时标识元素。
* **class**：一个以空格分隔的元素的类名（classes）列表，它允许CSS和JS通过类选择器或者DOM方法来选择和访问特定的元素；
* **style**：给元素添加内联样式；
* **title**：包含表示与其所属元素相关信息的文本，这些信息通常可以作为提示呈现给用户，但不是必须的。



























