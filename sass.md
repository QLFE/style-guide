  # sass代码风格
  ## 目录
  - [语法](#syntax)
  - [排序](#ordering-of-property-declarations)
  - [变量](#variables)
  - [Mixins](#mixins)
  - [扩展指令](#extend-directive)
  - [嵌套选择器](#nested-selectors)
  

<a name="syntax"></a>
### 语法

* 使用 `.scss` 的语法，不使用 `.sass` 原本的语法。
* CSS 和 `@include` 声明按照以下逻辑排序（参见下文）

<a name="ordering-of-property-declarations"></a>
### 属性声明的排序

1. 属性声明

    首先列出除去 `@include` 和嵌套选择器之外的所有属性声明。

   ```scss
    .btn-green {
      background: green;
      font-weight: bold;
      // ...
    }
   ```

2. `@include` 声明

    紧随后面的是 `@include`，这样可以使得整个选择器的可读性更高。

   ```scss
    .btn-green {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);
      // ...
    }
   ```

3. 嵌套选择器

    _如果有必要_用到嵌套选择器，把它们放到最后，在规则声明和嵌套选择器之间要加上空白，相邻嵌套选择器之间也要加上空白。嵌套选择器中的内容也要遵循上述指引。

   ```scss
    .btn {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);

      .icon {
        margin-right: 10px;
      }
    }
   ```

<a name="variables"></a>
### 变量

变量名应使用破折号（例如 `$my-variable`）代替 camelCased 和 snake_cased 风格。对于仅用在当前文件的变量，可以在变量名之前添加下划线前缀（例如 `$_my-variable`）。

<a name="mixins"></a>
### Mixins

为了让代码遵循 DRY 原则（Don't Repeat Yourself）、增强清晰性或抽象化复杂性，应该使用 mixin，这与那些命名良好的函数的作用是异曲同工的。虽然 mixin 可以不接收参数，但要注意，假如你不压缩负载（比如通过 gzip），这样会导致最终的样式包含不必要的代码重复。

<a name="extend-directive"></a>
### 扩展指令

应避免使用 `@extend` 指令，因为它并不直观，而且具有潜在风险，特别是用在嵌套选择器的时候。即便是在顶层占位符选择器使用扩展，如果选择器的顺序最终会改变，也可能会导致问题。（比如，如果它们存在于其他文件，而加载顺序发生了变化）。其实，使用 @extend 所获得的大部分优化效果，gzip 压缩已经帮助你做到了，因此你只需要通过 mixin 让样式表更符合 DRY 原则就足够了。

<a name="nested-selectors"></a>
### 嵌套选择器

**请不要让嵌套选择器的深度超过 3 层！**

```scss
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
```

当遇到以上情况的时候，你也许是这样写 CSS 的：

* 与 HTML 强耦合的（也是脆弱的）*—或者—*
* 过于具体（强大）*—或者—*
* 没有重用


再说一遍: **永远不要嵌套 ID 选择器！**

如果你始终坚持要使用 ID 选择器（劝你三思），那也不应该嵌套它们。如果你正打算这么做，你需要先重新检查你的标签，或者指明原因。如果你想要写出风格良好的 HTML 和 CSS，你是**不**应该这样做的。