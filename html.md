# HTML 代码规范
## 文档类型(DOCTYPE)
采用 HTML5 的 doctype 来启用标准模式， 建议使用大写的DOCTYPE。
```
<!DOCTYPE html>
```
参考：
- [<!DOCTYPE html> and older browsers](http://stackoverflow.com/questions/5384625/doctype-html-and-older-browsers)
- [Activating Browser Modes with Doctype](https://hsivonen.fi/doctype/)

## lang 属性
根据HTML5规范：
> 应在html标签上加上lang属性。这会给语音工具和翻译工具帮助，告诉它们应当怎么去发音和翻译。
更多关于 lang 属性的说明[在这里](http://w3c.github.io/html/semantics.html#the-html-element)；
```
<html lang="zh-CN">
```
参考：[网页头部的声明应该是用 lang="zh" 还是 lang="zh-cn"？](https://www.zhihu.com/question/20797118)

## 编码
页面必须使用**精简形式**，明确指定字符编码。指定字符编码的 meta 必须是 head 的第一个直接子元素

```
<html>
    <head>
        <meta charset="UTF-8">
        ......
    </head>
    <body>
        ......
    </body>
</html>
```

参考：[HTML5 charset能用么？](https://www.qianduan.net/html5-charset-can-it/)

## IE兼容模式
```
<meta http-equiv="X-UA-Compatible" content="IE=Edge">
```
参考：[What's the difference if \<meta http-equiv=“X-UA-Compatible” content=“IE=edge”> exists or not?](http://stackoverflow.com/questions/6771258/whats-the-difference-if-meta-http-equiv-x-ua-compatible-content-ie-edge-e)

## CSS 和 JavaScript 引入
引入CSS是必须指明```rel=stylesheet```

引入CSS和JS时不需要指明 type，因为 text/css 和 text/javascript 分别是他们的默认值

HTML5 规范链接：

- [使用link](https://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-link-element)
- [使用style](https://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-style-element)
- [使用script](https://www.w3.org/TR/2011/WD-html5-20110525/scripting-1.html#the-script-element)

```
<!-- External CSS -->
<link rel="stylesheet" href="code_guide.css">

<!-- In-document CSS -->
<style>
    ...
</style>

<!-- External JS -->
<script src="code_guide.js"></script>

<!-- In-document JS -->
<script>
    ...
</script>
```

## 缩进
缩进采用**soft tab(4个空格)**。

对每个块、列表、表格元素都另起一行，每个子元素都缩进。

## 协议

嵌入式资源省略协议头。

省略图片、媒体文件、样式表以及脚本的URL协议头部分（http:、https:），不使用这两个协议的文件则不省略。 省略协议头，即让URL变成相对地址，可以避免协议混合及小文件重复下载

使用 protocol-relative URL 引入 CSS，在 IE7/8 下，会发两次请求。是否使用 protocol-relative URL 应充分考虑页面针对的环境。

移动环境或只针对现代浏览器设计的 Web 应用，如果引用外部资源的 URL 协议部分与页面相同，建议省略协议前缀

```
<!-- 不推荐 -->
<script src="http://www.google.com/js/gweb/analytics/autotrack.js"></script>

<!-- 推荐 -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>

```

参考：[URI starting with two slashes … how do they behave?](http://stackoverflow.com/questions/4071117/uri-starting-with-two-slashes-how-do-they-behave)

## 命名
id 和 class 必须小写，单词间以连字符(-)分隔。

class 必须代表相应模块或部件的内容或功能，不得以样式信息进行命名。

尽量避免为了 hook 脚本，创建无样式信息的 class,使用 id、属性选择作为 hook 是更好的方式。

## 标签
标签名必须使用小写字母
**对于无需自闭合的标签，不允许自闭合**
```
<!-- good -->
<input type="text" name="title">

<!-- bad -->
<input type="text" name="title" />
```
标签使用遵循语义化原则
在编写HTML代码时，需要尽量避免多余的父节点，减少标签数量

## 属性
属性名必须使用小写字母
属性值必须用双引号包围
**boolean属性值不需要声明取值**，XHTML需要每个属性声明取值，但是HTML5并不需要；

更多内容可以参考 [WhatWG section on boolean attributes](https://html.spec.whatwg.org/multipage/infrastructure.html#boolean-attributes)：

>boolean属性的存在表示取值为true，不存在则表示取值为false。

```
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
    <option value="1" selected>1</option>
</select>
```
自定义属性建议以 data- 为前缀

## 属性排序
属性应该按照特定的顺序出现以保证易读性；
- class
- id
- name
- data-*
- src, for, type, href, value , max-length, max, min, pattern
- placeholder, title, alt
- aria-*, role
- required, readonly, disabled

## 文档模板
```
<!DOCTYPE html>
<html lang="zh-CN">
    <head>
        <meta charset="utf-8">
        <meta http-equiv="x-ua-compatible" content="ie=edge">
        <title></title>
        <meta name="description" content="">
        <meta name="keyword" content="">
        <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
    ...
    </body>
</html>

```
