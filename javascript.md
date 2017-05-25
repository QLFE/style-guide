# JavaScript 代码规范

## 代码风格

### 缩进
switch 下的 case 和 default 必须增加一个缩进层级

```
// not good
switch (variable) {

case '1':
    // do...
    break;

case '2':
    // do...
    break;

default:
    // do...

}

// good
switch (variable) {

    case '1':
        // do...
        break;

    case '2':
        // do...
        break;

    default:
        // do...

}
```

### 分号
以下几种情况需要加分号：

- 变量声明
- 表达式
- return
- throw
- break
- continue
- do-while

```
/* var declaration */
var x = 1;

/* expression statement */
x++;

/* do-while */
do {
    x++;
} while (x < 10);

```

以下几种情况不需要分号：

- 函数定义结束
- for结束
- if/else 结束
- switch 结束

```
// not good
function funcName() {
};

// good
function funcName() {
}

// 如果是函数表达式，分号是不允许省略的。
var funcName = function() {
};
```

### 空格
以下几种情况不需要空格：

- 对象的属性名后
- 前缀一元运算符后
- 后缀一元运算符前
- 函数调用括号前
- 无论是函数声明还是函数表达式，'('前不要空格
- 数组的'['后和']'前
- 对象的'{'后和'}'前
- 运算符'('后和')'前


以下几种情况需要空格：

- 二元运算符前后
- 三元运算符'?:'前后
- 代码块'{'前
- 下列关键字前：else, while, catch, finally
- 下列关键字后：if, else, for, while, do, switch, case, try, catch, finally, with, return, typeof
- 单行注释'//'后（若单行注释和代码同行，则'//'前也需要），多行注释'*'后
- 对象的属性值前
- for循环，分号后留有一个空格，前置条件如果有多个，逗号后留一个空格
- 无论是函数声明还是函数表达式，'{'前一定要有空格
- 函数的参数之间

```
// not good
var a = {
    b :1
};

// good
var a = {
    b: 1
};

// not good
++ x;
y ++;
z = x?1:2;

// good
++x;
y++;
z = x ? 1 : 2;

// not good
var a = [ 1, 2 ];

// good
var a = [1, 2];

// not good
var a = ( 1+2 )*3;

// good
var a = (1 + 2) * 3;

// no space before '(', one space before '{', one space between function parameters
var doSomething = function(a, b, c) {
    // do something
};

// no space before '('
doSomething(item);

// not good
for(i=0;i<6;i++){
    x++;
}

// good
for (i = 0; i < 6; i++) {
    x++;
}

```

### 空行
以下几种情况需要空行：

- 变量声明后（当变量声明在代码块的最后一行时，则无需空行）
- 注释前（当注释在代码块的第一行时，则无需空行）
- 代码块后（在函数调用、数组、对象中则无需空行）
- 文件最后保留一个空行

```
// need blank line after variable declaration
var x = 1;

// not need blank line when variable declaration is last expression in the current block
if (x >= 1) {
    var y = x + 1;
}

var a = 2;

// need blank line before line comment
a++;

function b() {
    // not need blank line when comment is first line of block
    return a;
}

// need blank line after blocks
for (var i = 0; i < 2; i++) {
    if (true) {
        return false;
    }

    continue;
}

var obj = {
    foo: function() {
        return 1;
    },

    bar: function() {
        return 2;
    }
};

// not need blank line when in argument list, array, object
func(
    2,
    function() {
        a++;
    },
    3
);

var foo = [
    2,
    function() {
        a++;
    },
    3
];


var foo = {
    a: 2,
    b: function() {
        a++;
    },
    c: 3
};

```

### 换行
换行的地方，行末必须有','或者运算符；

以下几种情况不需要换行：

- 下列关键字后：else, catch, finally
- 代码块'{'前

以下几种情况需要换行：

- 代码块'{'后和'}'前
- 变量赋值后

```
// not good
function test()
{
    ...
}

// good
function test() {
    ...
}

// not good
var a, foo = 7, b,
    c, bar = 8;

// good
var a,
    foo = 7,
    b, c, bar = 8;
```

### 引号
最外层统一使用单引号

```
// not good
var x = "test";

// good
var y = 'foo',
    z = '<div id="test"></div>';
    
```

### 变量命名
- 标准变量采用驼峰式命名
- 常量全大写，用下划线连接
- 构造函数，大写第一个字母
- jquery对象必须以'$'开头命名
- 函数名使用动宾短语

```
var googID = '';

var MAX_COUNT = 10;

function Person(name) {
    this.name = name;
}

// not good
var body = $('body');

// good
var $body = $('body');

```

### 变量声明
一个函数作用域中所有的变量声明尽量提到函数首部

### 括号
下列关键字后必须有大括号（即使代码块的内容只有一行）：if, else, for, while, do, switch, try, catch, finally, with。

### 数组、对象

对象属性名不需要加引号；

对象以缩进的形式书写，不要写在一行；

数组、对象最后不要有逗号。

```
// not good
var a = {
    'b': 1
};

var a = {b: 1};

var a = {
    b: 1,
    c: 2,
};

// good
var a = {
    b: 1,
    c: 2
};
```

### null

适用场景：

- 初始化一个将来可能被赋值为对象的变量
- 与已经初始化的变量做比较
- 作为一个参数为对象的函数的调用传参
- 作为一个返回对象的函数的返回值


不适用场景：

- 不要用null来判断函数调用时有无传参
- 不要与未初始化的变量做比较

```
// not good
function test(a, b) {
    if (b === null) {
        // not mean b is not supply
        ...
    }
}

var a;

if (a === null) {
    ...
}

// good
var a = null;

if (a === null) {
    ...
}
```

### undefined

永远不要直接使用undefined进行变量判断；

使用typeof和字符串'undefined'对变量进行判断。

```
// not good
if (person === undefined) {
    ...
}

// good
if (typeof person === 'undefined') {
    ...
}
```

### 文档注释


### 其他
对上下文this的引用只能使用'_this', 'that', 'self'其中一个来命名；

switch的falling through和no default的情况一定要有注释特别说明；

```
// good
switch (condition) {
    case 1:
    case 2:
        ...
        break;
    case 3:
        ...
    // why fall through
    case 4
        ...
        break;
    // why no default
}
```