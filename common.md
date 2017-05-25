# 通用代码规范
## 文件及目录命名规则
- 一律小写；
- 多个单词用连字符(-)连接；
- 只能出现英文，数字和连字符；
- 该命名规范适用于 html, css, js, swf, xml, png, gif, jpg, ico 等前端维护的所有文件类型和相关目录。

## 文件编码
所有文件编码统一采用 UTF-8 无 Bom 编码。
在HTML模板和文档中使用 ```<meta charset=”utf-8”> ```指定编码。不需要为样式表指定编码，它默认是UTF-8。

参考：[Handling character encodings in HTML and CSS](https://www.w3.org/International/tutorials/tutorial-char-enc/)

## 注释
在**需要时**尽可能去解释你的代码，
用注释去解释你的代码，包括它的应用范围、用途、此方案的选择理由等。

