# float布局

## 步骤

* 子元素上加`float:left`和`width` ;

* 父元素上加`class = "clearfix"`

  * .clearfix 的写法：

    ```css
    .clearfix::after {
      content:'';
      display:block;
      clear:both;
    }
    ```

* 注意事项
  * 最后一个子元素不设置`width`，或者设置`max-width`
  * 如果图片下面有多余的空白，就在图片上写上 `vertical-align:top`或者`middle`
  * 如果`border`干扰了布局，可以用`outline`代替，`outline`不占用位置
  * 固定宽度的块级元素居中的方法: 写上`margin:0 auto;`或者`margin-left:auto;` `margin-right:auto;` 。后者比前者好，因为不影响上下`margin`
  * 平均布局的关键点：负`margin`

## 示例

https://github.com/clouddawn/float



---



float CSS属性指定一个元素应沿其容器的左侧或右侧放置，允许文本和内联元素环绕它。





































