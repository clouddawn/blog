# iframe和a标签详解
## iframe
<font size=3>

**iframe** 标签规定一个内联框架。一个内联框架被用来在当前 HTML 文档中嵌入另一个文档。
```html
<iframe src="https://www.baidu.com" frameborder="0"></iframe>
```
**frameborder** 规定是否显示 **iframe** 周围的边框。**1**显示，**0**不显示。
## a
a 标签定义超链接，用于从一个页面链接到另一个页面。  
a 标签最重要的属性是 href 属性，它指定链接的目标。  

在所有浏览器中，链接的默认外观如下：
未被访问的链接带有下划线而且是蓝色的；  
已被访问的链接带有下划线而且是紫色的；  
活动链接（点击的时候）带有下划线而且是红色的。  

**target**规定在何处打开链接： 
 
**_blank**：新窗口打开。  
**_parent**：在父窗口中打开链接。  
**_self**：默认，当前页面跳转。  
**_top**：在当前窗体打开链接，并替换当前的整个窗体(框架页)。
