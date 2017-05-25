# CSS 代码规范

## 代码风格
### 分号
每个属性声明末尾都要加分号

### 空格
以下情况不需要空格：

- 属性名后，```:```前
- 多个规则的分隔符```,```前
- 属性值中```(```后和```)```前
- ```!important``` ```!```后

以下情况需要空格：

- 属性值前，即```:```后
- 关系选择符```>```,```+```,```~```前后
- ```{```前
- ```!important```'!'前
- 属性值中```,```后
- 注释```/*```后和```\*/```前

```
/* not good */
.element {
    color :red! important;
    background-color: rgba( 0 ,0 ,0 ,.5 );
}

/* good */
.element {
    color: red !important;
    background-color: rgba(0, 0, 0, .5);
}

/* not good */
.element>.dialog{
    ...
}

/* good */
.element > .dialog {
    ...
}

```

### 空行
- ```}```后跟一个空行
- 属性不同分类之间需要适当空行

```
/* not good */
.element {
    color: red;
    width: 200px;
}
.dialog {
    ...
}

/* good */
.element {
    color: red;
    
    width: 200px;
}

.dialog {
	...
}

```

### 换行
以下情况不需要换行：
- ```{```前

以下情况不需要换行

- ```{```后和```}```前
- 多个规则的分隔符```{```后
- 每个属性独占一行


### 引号
统一使用双引号

url的内容不需要引号

属性选择器中的属性值需要引号

```
.element:after {
    content: "";
    background-image: url(./img/logo.png);
}

li[data-type="single"] {
    ...
}
```

### 值与单位
当数值为0 -1 之间的小数时，省略整数部分的0

```
/* not good */
panel {
    opacity: 0.8;
}

/* good */
panel {
    opacity: .8;
}

```

长度为 0 时需省略单位

```
/* not good */
body {
    padding: 0px 5px;
}

/* good */
body {
    padding: 0 5px;
}

```

颜色值全部用小写，可以缩写时，需要缩写

```
/* not good */
.element {
    color: #ABCDEF;
    background-color: #001122;
}

/* good */
.element {
    color: #abcdef;
    background-color: #012;
}
```

### 属性简写

在需要显示地设置所有值的情况下，应当尽量限制使用简写形式的属性声明。常见的滥用简写属性声明的情况如下：

padding

margin

background

border

border-radius

大部分情况下，我们不需要为简写形式的属性声明指定所有值。例如，HTML 的 heading 元素只需要设置上、下边距（margin）的值，因此，在必要的时候，只需覆盖这两个值就可以。过度使用简写形式的属性声明会导致代码混乱，并且会对属性值带来不必要的覆盖从而引起意外的副作用。

参考：[Shorthand properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties)

### 属性声明顺序
相关的属性声明应当归为一组，并按照下面的顺序排列：

Positioning(position / top / right / bottom / left / float / display / overflow 等)

Box model(border / margin / padding / width / height 等)

Typographic(font / line-height / text-align / word-wrap)

Visual(background / color / transition / list-style)

## 最佳实践
