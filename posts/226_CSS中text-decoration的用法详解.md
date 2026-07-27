# text-decoration

`text-decoration` 这个 CSS 属性是用于设置文本的修饰线外观的（下划线、上划线、贯穿线/删除线 或 闪烁）它是 `text-decoration-line`, `text-decoration-color`, `text-decoration-style`, 和新出现的 `text-decoration-thickness` 属性的缩写。

文本修饰属性会延伸到子元素。这意味着如果祖先元素指定了文本修饰属性，子元素则不能将其删除。

例如，在如下标记中：

```html
<p>This text has <em>some emphasized words</em> in it.</p>
```

应用样式：

```css
p { text-decoration: underline }
```

会对整个段落添加下划线，此时再添加样式：

```css
em { text-decoration: none }
```

则不会引起任何改变，整个段落仍然有下划线修饰。然而，新加样式：

```css
em { text-decoration: overline }
```

则会在`<em>`标记的文字上再添加上这种 `overline `样式。

## text-decoration-line

* 用于设置元素中的文本的修饰类型

`none`

* 表示没有文本修饰效果。

`underline`

* 在文本的下方有一条修饰线。

`overline`

* 在文本的上方有一条修饰线。

`line-through`

* 有一条贯穿文本中间的修饰线。

## text-decoration-style

* 用于设置由 `text-decoration-line` 设定的线的样式。线的样式会应用到所有被 `text-decoration-line` 设定的线，不能为其中的每条线设置不同的样式。

`solid`

* 画一条实线

`double`

* 画一条双实线。

`dotted`

* 画一条点划线。

`dashed`

* 画一条虚线。

`wavy`

* 画一条波浪线。

## text-decoration-thickness

* 用于设置元素中文本所使用的装饰线的笔触厚度。

```css
/* Single keyword */
text-decoration-thickness: auto;
text-decoration-thickness: from-font;

/* length */
text-decoration-thickness: 0.1em;
text-decoration-thickness: 3px;

/* percentage */
text-decoration-thickness: 10%;
```

`auto`

* 由浏览器为文本装饰线选择合适的厚度。

`from-font`

* 如果字体文件中包含了首选的厚度值，则使用字体文件的厚度值。如果字体文件中没有包含首选的厚度值，则效果和设置为 `auto` 一样，由浏览器选择合适的厚度值。

`<length>`

* 将文本装饰线的厚度设置为一个 `length` 类型的值，覆盖掉字体文件建议的值或浏览器默认的值。

```html
<div>
  <div class="text">君不见黄河之水天上来，奔流到海不复回。</div>
  <div class="text">君不见高堂明镜悲白发，朝如青丝暮成雪。</div>
  <div class="text">人生得意须尽欢，莫使金樽空对月。</div>
  <div class="text">天生我材必有用，千金散尽还复来。</div>
</div>
```

.

```css
.text {
  margin: 10px;
}

.text:first-child {
  text-decoration: underline solid red 1px;
}

.text:nth-child(2) {
  text-decoration: line-through double black 0.1em;
}

.text:nth-child(3) {
  text-decoration: overline dotted orange 10%;
}

.text:last-child {
  text-decoration: underline dashed purple auto;
}
```



































