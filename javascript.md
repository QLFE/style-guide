# JavaScript代码风格

<a name="table-of-contents"></a>
## 目录

  1. [类型](#types)
  2. [引用](#references)
  3. [对象](#objects)
  4. [数组](#arrays)
  5. [解构](#destructuring)
  6. [字符串](#strings)
  7. [函数](#functions)
  8. [箭头函数](#arrow-functions)
  9. [构造函数](#constructors)
  10. [模块](#modules)
  11. [Iterators & Generators ](#iterators-and-generators)
  12. [属性](#properties)
  13. [变量](#variables)
  14. [提升](#hoisting)
  15. [比较运算符 & 等号](#comparison-operators--equality)
  16. [代码块](#blocks)
  17. [注释](#comments)
  18. [空白](#whitespace)
  19. [逗号](#commas)
  20. [分号](#semicolons)
  21. [类型转换](#type-casting--coercion)
  22. [命名规则](#naming-conventions)
      ​

<a name="types"></a>
##  类型 

- [1.1](#1.1) <a name='1.1'></a> **基本类型**: 直接存取基本类型。

  + `字符串`
  + `数值`
  + `布尔类型`
  + `null`
  + `undefined`

  ```javascript
  const foo = 1
  let bar = foo

  bar = 9

  console.log(foo, bar) // => 1, 9
  ```
- [1.2](#1.2) <a name='1.2'></a> **复制类型**: 通过引用的方式存取复杂类型。

  + `对象`
  + `数组`
  + `函数`

  ```javascript
  const foo = [1, 2]
  const bar = foo

  bar[0] = 9

  console.log(foo[0], bar[0]) // => 9, 9
  ```

**[⬆ 返回目录](#table-of-contents)**

<a name="references"></a>
## 引用

- [2.1](#2.1) <a name='2.1'></a> 对所有的引用使用 `const` ；不要使用 `var`。

  > 为什么？这能确保你无法对引用重新赋值，也不会导致出现 bug 或难以理解。

```javascript
// bad
var a = 1
var b = 2

// good
const a = 1
const b = 2
```

- [2.2](#2.2) <a name='2.2'></a> 如果你一定需要可变动的引用，使用 `let` 代替 `var`。

  > 为什么？因为  `let` 是块级作用域，而 `var` 是函数作用域。

```javascript
// bad
var count = 1
if (true) {
  count += 1
}

// good, use the let.
let count = 1
if (true) {
  count += 1
}
```

- [2.3](#2.3) <a name='2.3'></a> 注意 `let` 和 `const` 都是块级作用域。

  ```javascript
  // const 和 let 只存在于它们被定义的区块内。
  {
    let a = 1
    const b = 1
  }
  console.log(a) // ReferenceError
  console.log(b) // ReferenceError
  ```

**[⬆ 返回目录](#table-of-contents)**

<a name="objects"></a>
## 对象

- [3.1](#3.1) <a name='3.1'></a> 使用字面值创建对象。

  ```javascript
  // bad
  const item = new Object();

  // good
  const item = {};
  ```

- [3.2](#3.2) <a name='3.2'></a> 使用同义词替换需要使用的保留字。

  ```javascript
  // bad
  const superman = {
    class: 'alien',
  }

  // bad
  const superman = {
    klass: 'alien',
  }

  // good
  const superman = {
    type: 'alien',
  }
  ```

- [3.3](#3.6) <a name='3.3'></a> 使用对象属性值的简写。

  > 为什么？因为这样更短更有描述性。

```javascript
const lukeSkywalker = 'Luke Skywalker'

// bad
const obj = {
  lukeSkywalker: lukeSkywalker,
}

// good
const obj = {
  lukeSkywalker
}
```

**[⬆ 返回目录](#table-of-contents)**

<a name="arrays"></a>
## 数组

- [4.1](#4.1) <a name='4.1'></a> 使用字面值创建数组。

  ```javascript
  // bad
  const items = new Array();

  // good
  const items = [];
  ```

  <a name="es6-array-spreads"></a>
- [4.2](#4.2) <a name='4.2'></a> 使用拓展运算符 `...` 复制数组。

  ```javascript
  // bad
  const len = items.length
  const itemsCopy = []
  let i

  for (i = 0; i < len; i++) {
    itemsCopy[i] = items[i]
  }

  // good
  const itemsCopy = [...items]
  ```
- [4.3](#4.3) <a name='4.4'></a> 使用 Array#from 把一个类数组对象转换成数组。

  ```javascript
  const foo = document.querySelectorAll('.foo')
  const nodes = Array.from(foo)
  ```

**[⬆ 返回目录](#table-of-contents)**

<a name="destructuring"></a>
## 解构

- [5.1](#5.1) <a name='5.1'></a> 使用解构存取和使用多属性对象。

  > 为什么？因为解构能减少临时引用属性。

```javascript
// bad
function getFullName(user) {
  const firstName = user.firstName
  const lastName = user.lastName

  return `${firstName} ${lastName}`
}

// good
function getFullName(obj) {
  const { firstName, lastName } = obj
  return `${firstName} ${lastName}`
}

// best
function getFullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`
}
```

- [5.2](#5.2) <a name='5.2'></a> 对数组使用解构赋值。

  ```javascript
  const arr = [1, 2, 3, 4]

  // bad
  const first = arr[0]
  const second = arr[1]

  // good
  const [first, second] = arr
  ```

- [5.3](#5.3) <a name='5.3'></a> 需要回传多个值时，使用对象解构，而不是数组解构。
  > 为什么？增加属性或者改变排序不会改变调用时的位置。

```javascript
// bad
function processInput(input) {
  // then a miracle occurs
  return [left, right, top, bottom];
}

// 调用时需要考虑回调数据的顺序。
const [left, __, top] = processInput(input);

// good
function processInput(input) {
  // then a miracle occurs
  return { left, right, top, bottom };
}

// 调用时只选择需要的数据
const { left, right } = processInput(input);
```


**[⬆ 返回目录](#table-of-contents)**

<a name="strings"></a>
## Strings

- [6.1](#6.1) <a name='6.1'></a> 字符串使用单引号 `''` 。

  ```javascript
  // bad
  const name = "Capt. Janeway"

  // good
  const name = 'Capt. Janeway'
  ```

  <a name="es6-template-literals"></a>
- [6.2](#6.2) <a name='6.2'></a> 程序化生成字符串时，使用模板字符串代替字符串连接。

  > 为什么？模板字符串更为简洁，更具可读性。

```javascript
// bad
function sayHi(name) {
  return 'How are you, ' + name + '?';
}

// bad
function sayHi(name) {
  return ['How are you, ', name, '?'].join();
}

// good
function sayHi(name) {
  return `How are you, ${name}?`;
}
```

**[⬆ 返回目录](#table-of-contents)**

<a name="functions"></a>
## 函数

- [7.1](#7.1) <a name='7.1'></a> 使用函数声明代替函数表达式。

  > 为什么？因为函数声明是可命名的，所以他们在调用栈中更容易被识别。此外，函数声明会把整个函数提升（hoisted），而函数表达式只会把函数的引用变量名提升。这条规则使得[箭头函数](#arrow-functions)可以取代函数表达式。

```javascript
// bad
const foo = function () {
};

// good
function foo() {
}
```

- [7.2](#7.2) <a name='7.2'></a>  **注意:**永远不要在一个非函数代码块（`if`、`while` 等）中声明一个函数，把那个函数赋给一个变量。浏览器允许你这么做，但它们的解析表现不一致。


  <a name="es6-rest"></a>
- [7.3](#7.3) <a name='7.3'></a> 不要使用 `arguments`。可以选择 rest 语法 `...` 替代。

  > 为什么？使用 `...` 能明确你要传入的参数。另外 rest 参数是一个真正的数组，而 `arguments` 是一个类数组。

```javascript
// bad
function concatenateAll() {
  const args = Array.prototype.slice.call(arguments);
  return args.join('')
}

// good
function concatenateAll(...args) {
  return args.join('')
}
```

  <a name="es6-default-parameters"></a>
- [7.4](#7.4) <a name='7.4'></a> 直接给函数的参数指定默认值，不要使用一个变化的函数参数。

  ```javascript
  // really bad
  function handleThings(opts) {
    // 不！我们不应该改变函数参数。
    // 更加糟糕: 如果参数 opts 是 false 的话，它就会被设定为一个对象。
    // 但这样的写法会造成一些 Bugs。
    //（译注：例如当 opts 被赋值为空字符串，opts 仍然会被下一行代码设定为一个空对象。）
    opts = opts || {};
    // ...
  }

  // still bad
  function handleThings(opts) {
    if (opts === void 0) {
      opts = {};
    }
    // ...
  }

  // good
  function handleThings(opts = {}) {
    // ...
  }
  ```

**[⬆ 返回目录](#table-of-contents)**

<a name="arrow-functions"></a>
## 箭头函数

- [8.1](#8.1) <a name='8.1'></a> 当你必须使用函数表达式（或传递一个匿名函数）时，使用箭头函数符号。

  > 为什么?因为箭头函数创造了新的一个 `this` 执行环境（译注：参考 [Arrow functions - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) 和 [ES6 arrow functions, syntax and lexical scoping](http://toddmotto.com/es6-arrow-functions-syntaxes-and-lexical-scoping/)），通常情况下都能满足你的需求，而且这样的写法更为简洁。


  > 为什么不？如果你有一个相当复杂的函数，你或许可以把逻辑部分转移到一个函数声明上。

```javascript
// bad
[1, 2, 3].map(function (x) {
  return x * x
})

// good
[1, 2, 3].map((x) => {
  return x * x
})
```

- [8.2](#8.2) <a name='8.2'></a> 如果一个函数适合用一行写出并且只有一个参数，那就把花括号、圆括号和 `return` 都省略掉。如果不是，那就不要省略。

  > 为什么？语法糖。在链式调用中可读性很高。


  > 为什么不？当你打算回传一个对象的时候。

```javascript
// good
[1, 2, 3].map(x => x * x)

// good
[1, 2, 3].reduce((total, n) => {
  return total + n
}, 0)
```

**[⬆ 返回目录](#table-of-contents)**

<a name="constructors"></a>
## 构造器

- [9.1](#9.1) <a name='9.1'></a> 总是使用 `class`。避免直接操作 `prototype` 。

  > 为什么? 因为 `class` 语法更为简洁更易读。

```javascript
// bad
function Queue(contents = []) {
  this._queue = [...contents]
}
Queue.prototype.pop = function() {
  const value = this._queue[0]
  this._queue.splice(0, 1)
  return value
}
// good
class Queue {
  constructor(contents = []) {
    this._queue = [...contents]
  }
  pop() {
    const value = this._queue[0]
    this._queue.splice(0, 1)
    return value
  }
}
```

- [9.2](#9.2) <a name='9.2'></a> 使用 `extends` 继承。

  > 为什么？因为 `extends` 是一个内建的原型继承方法并且不会破坏 `instanceof`。

```javascript

// bad
const inherits = require('inherits')
function PeekableQueue(contents) {
  Queue.apply(this, contents)
}
inherits(PeekableQueue, Queue)
PeekableQueue.prototype.peek = function() {
  return this._queue[0]
}

// good
class PeekableQueue extends Queue {
  peek() {
    return this._queue[0];
  }
}
```

- [9.3](#9.3) <a name='9.3'></a> 方法可以返回 `this` 来帮助链式调用。

  ```javascript
  // bad
  Jedi.prototype.jump = function() {
    this.jumping = true
    return true
  };

  Jedi.prototype.setHeight = function(height) {
    this.height = height;
  };

  const luke = new Jedi()
  luke.jump() // => true
  luke.setHeight(20) // => undefined

  // good
  class Jedi {
    jump() {
      this.jumping = true
      return this
    }

    setHeight(height) {
      this.height = height
      return this
    }
  }

  const luke = new Jedi()

  luke.jump().setHeight(20)
  ```

**[⬆ 返回目录](#table-of-contents)**

<a name="modules"></a>
## 模块

- [10.1](#10.1) <a name='10.1'></a> 总是使用模组 (`import`/`export`) 而不是其他非标准模块系统。你可以编译为你喜欢的模块系统。

  > 为什么？模块就是未来，让我们开始迈向未来吧。

```javascript
// bad
const AirbnbStyleGuide = require('./AirbnbStyleGuide')
module.exports = AirbnbStyleGuide.es6

// ok
import AirbnbStyleGuide from './AirbnbStyleGuide'
export default AirbnbStyleGuide.es6

// best
import { es6 } from './AirbnbStyleGuide'
export default es6
```

**[⬆ 返回目录](#table-of-contents)**

<a name="iterators-and-generators"></a>
## Iterators and Generators

- [11.1](#11.1) <a name='11.1'></a> 不要使用 iterators。使用高阶函数例如 `map()` 和 `reduce()` 替代 `for-of`。

  > 为什么？这加强了我们不变的规则。处理纯函数的回调值更易读，这比它带来的副作用更重要。

```javascript
const numbers = [1, 2, 3, 4, 5]

// bad
let sum = 0
for (let num of numbers) {
  sum += num
}

sum === 15

// good
let sum = 0
numbers.forEach((num) => sum += num)
sum === 15

// best (use the functional force)
const sum = numbers.reduce((total, num) => total + num, 0)
sum === 15
```

- [11.2](#11.2) <a name='11.2'></a> 现在还不要使用 generators。

  > 为什么？因为它们现在还没法很好地编译到 ES5。 (译者注：目前(2016/03) Chrome 和 Node.js 的稳定版本都已支持 generators)

**[⬆ 返回目录](#table-of-contents)**

<a name="properties"></a>
## 属性

- [12.1](#12.1) <a name='12.1'></a> 使用 `.` 来访问对象的属性。

  ```javascript
  const luke = {
    jedi: true,
    age: 28
  }

  // bad
  const isJedi = luke['jedi']

  // good
  const isJedi = luke.jedi
  ```

- [12.2](#12.2) <a name='12.2'></a> 当通过变量访问属性时使用中括号 `[]`。

  ```javascript
  const luke = {
    jedi: true,
    age: 28
  };

  function getProp(prop) {
    return luke[prop]
  }

  const isJedi = getProp('jedi')
  ```

**[⬆ 返回目录](#table-of-contents)**

<a name="variables"></a>
## 变量

- [13.1](#13.1) <a name='13.1'></a> 一直使用 `const` 来声明变量，如果不这样做就会产生全局变量。我们需要避免全局命名空间的污染。

  ```javascript
  // bad
  superPower = new SuperPower();

  // good
  const superPower = new SuperPower();
  ```

- [13.2](#13.2) <a name='13.2'></a> 使用 `const` 声明每一个变量。

  > 为什么？增加新变量将变的更加容易，而且你永远不用再担心调换错 `;` 跟 `,`。

  ```javascript
  // bad
  const items = getItems(),
      goSportsTeam = true,
      dragonball = 'z'

  // bad
  // (compare to above, and try to spot the mistake)
  const items = getItems(),
      goSportsTeam = true
      dragonball = 'z'

  // good
  const items = getItems()
  const goSportsTeam = true
  const dragonball = 'z'
  ```

- [13.3](#13.3) <a name='13.3'></a> 将所有的 `const` 和 `let` 分组

  > 为什么？当你需要把已赋值变量赋值给未赋值变量时非常有用。

```javascript
// bad
let i, len, dragonball,
    items = getItems(),
    goSportsTeam = true

// bad
let i;
const items = getItems()
let dragonball
const goSportsTeam = true
let len

// good
const goSportsTeam = true
const items = getItems()
let dragonball
let i
let length
```
**[⬆ 返回目录](#table-of-contents)**

<a name="hoisting"></a>
## Hoisting

- [14.1](#14.1) <a name='14.1'></a> `var` 声明会被提升至该作用域的顶部，但它们赋值不会提升。`let` 和 `const` 被赋予了一种称为「[暂时性死区（Temporal Dead Zones, TDZ）](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal_dead_zone_and_errors_with_let)」的概念。这对于了解为什么 [type of 不再安全](http://es-discourse.com/t/why-typeof-is-no-longer-safe/15)相当重要。

  ```javascript
  // 我们知道这样运行不了 
  // （假设 notDefined 不是全局变量）
  function example() {
    console.log(notDefined) // => throws a ReferenceError
  }

  // 由于变量提升的原因，
  // 在引用变量后再声明变量是可以运行的。
  // 注：变量的赋值 `true` 不会被提升。
  function example() {
    console.log(declaredButNotAssigned) // => undefined
    var declaredButNotAssigned = true
  }

  // 编译器会把函数声明提升到作用域的顶层，
  // 这意味着我们的例子可以改写成这样：
  function example() {
    let declaredButNotAssigned
    console.log(declaredButNotAssigned) // => undefined
    declaredButNotAssigned = true
  }

  // 使用 const 和 let
  function example() {
    console.log(declaredButNotAssigned) // => throws a ReferenceError
    console.log(typeof declaredButNotAssigned) // => throws a ReferenceError
    const declaredButNotAssigned = true
  }
  ```

- [14.2](#14.2) <a name='14.2'></a> 匿名函数表达式的变量名会被提升，但函数内容并不会。

  ```javascript
  function example() {
    console.log(anonymous) // => undefined

    anonymous() // => TypeError anonymous is not a function

    var anonymous = function() {
      console.log('anonymous function expression')
    }
  }
  ```

- [14.3](#14.3) <a name='14.3'></a> 命名的函数表达式的变量名会被提升，但函数名和函数函数内容并不会。

  ```javascript
  function example() {
    console.log(named) // => undefined
    named() // => TypeError named is not a function
    superPower() // => ReferenceError superPower is not defined
    var named = function superPower() {
      console.log('Flying');
    };
  }

  // the same is true when the function name
  // is the same as the variable name.
  function example() {
    console.log(named); // => undefined
    named(); // => TypeError named is not a function
    var named = function named() {
      console.log('named');
    }
  }
  ```

- [14.4](#14.4) <a name='14.4'></a> 函数声明的名称和函数体都会被提升。

  ```javascript
  function example() {
    superPower(); // => Flying
    
    function superPower() {
      console.log('Flying')
    }
  }
  ```

- 想了解更多信息，参考 [Ben Cherry](http://www.adequatelygood.com/) 的 [JavaScript Scoping & Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting)。

**[⬆ 返回目录](#table-of-contents)**

<a name="comparison-operators--equality"></a>
## 比较运算符 & 等号

- [15.1](#15.1) <a name='15.1'></a> 优先使用 `===` 和 `!==` 而不是 `==` 和 `!=`.
- [15.2](#15.2) <a name='15.2'></a> 条件表达式例如 `if` 语句通过抽象方法 `ToBoolean` 强制计算它们的表达式并且总是遵守下面的规则：

  + **对象** 被计算为 **true**
  + **Undefined** 被计算为 **false**
  + **Null** 被计算为 **false**
  + **布尔值** 被计算为 **布尔的值**
  + **数字** 如果是 **+0、-0、或 NaN** 被计算为 **false**, 否则为 **true**
  + **字符串** 如果是空字符串 `''` 被计算为 **false**，否则为 **true**

  ```javascript
  if ([0]) {
    // true
    // An array is an object, objects evaluate to true
  }
  ```

- [15.3](#15.3) <a name='15.3'></a> 使用简写。

  ```javascript
  // bad
  if (name !== '') {
    // ...stuff...
  }

  // good
  if (name) {
    // ...stuff...
  }

  // bad
  if (collection.length > 0) {
    // ...stuff...
  }

  // good
  if (collection.length) {
    // ...stuff...
  }
  ```

**[⬆ 返回目录](#table-of-contents)**

<a name="blocks"></a>
## 代码块

- [16.1](#16.1) <a name='16.1'></a> 使用大括号包裹所有的多行代码块。

  ```javascript
  // bad
  if (test)
    return false;

  // good
  if (test) return false;

  // good
  if (test) {
    return false;
  }

  // bad
  function() { return false; }

  // good
  function() {
    return false;
  }
  ```

- [16.2](#16.2) <a name='16.2'></a> 如果通过 `if` 和 `else` 使用多行代码块，把 `else` 放在 `if` 代码块关闭括号的同一行。

  ```javascript
  // bad
  if (test) {
    thing1();
    thing2();
  }
  else {
    thing3();
  }

  // good
  if (test) {
    thing1();
    thing2();
  } else {
    thing3();
  }
  ```


**[⬆ 返回目录](#table-of-contents)**

<a name="comments"></a>
## 注释

- [17.1](#17.1) <a name='17.1'></a> 使用 `/** ... */` 作为多行注释。包含描述、指定所有参数和返回值的类型和值。

  ```javascript
  // bad
  // make() returns a new element
  // based on the passed in tag name
  //
  // @param {String} tag
  // @return {Element} element
  function make(tag) {
    // ...stuff...
    return element;
  }

  // good
  /**
   * make() returns a new element
   * based on the passed in tag name
   *
   * @param {String} tag
   * @return {Element} element
   */
  function make(tag) {
    // ...stuff...
    return element;
  }
  ```

- [17.2](#17.2) <a name='17.2'></a> 使用 `//` 作为单行注释。在评论对象上面另起一行使用单行注释。在注释前插入空行。

  ```javascript
  // bad
  const active = true  // is current tab

  // good
  // is current tab
  const active = true

  // bad
  function getType() {
    console.log('fetching type...');
    // set the default type to 'no type'
    const type = this._type || 'no type'
    return type;
  }

  // good
  function getType() {
    console.log('fetching type...');

    // set the default type to 'no type'
    const type = this._type || 'no type';

    return type;
  }
  ```

**[⬆ 返回目录](#table-of-contents)**

<a name="whitespace"></a>
## 空白

- [18.1](#18.1) <a name='18.1'></a> 使用 2 个空格作为缩进。

  ```javascript
  // bad
  function() {
  ∙∙∙∙const name
  }

  // bad
  function() {
  ∙const name
  }

  // good
  function() {
  ∙∙const name
  }
  ```

- [18.2](#18.2) <a name='18.2'></a> 在花括号前放一个空格。

  ```javascript
  // bad
  function test(){
    console.log('test')
  }

  // good
  function test() {
    console.log('test')
  }

  // bad
  dog.set('attr',{
    age: '1 year',
    breed: 'Bernese Mountain Dog'
  })

  // good
  dog.set('attr', {
    age: '1 year',
    breed: 'Bernese Mountain Dog'
  })
  ```

- [18.3](#18.3) <a name='18.3'></a> 在控制语句（`if`、`while` 等）的小括号前放一个空格。在函数调用及声明中，不在函数的参数列表前加空格。

  ```javascript
  // bad
  if(isJedi) {
    fight ()
  }

  // good
  if (isJedi) {
    fight()
  }

  // bad
  function fight () {
    console.log ('Swooosh!')
  }

  // good
  function fight() {
    console.log('Swooosh!')
  }
  ```

- [18.4](#18.4) <a name='18.4'></a> 使用空格把运算符隔开。

  ```javascript
  // bad
  const x=y+5

  // good
  const x = y + 5
  ```

- [18.5](#18.5) <a name='18.5'></a> 在文件末尾插入一个空行。

  ```javascript
  // bad
  (function(global) {
    // ...stuff...
  })(this)
  ```

  ```javascript
  // bad
  (function(global) {
    // ...stuff...
  })(this)↵
  ↵
  ```

  ```javascript
  // good
  (function(global) {
    // ...stuff...
  })(this)↵
  ```

- [18.6](#18.6) <a name='18.6'></a> 在块末和新语句前插入空行。

  ```javascript
  // bad
  if (foo) {
    return bar
  }
  return baz

  // good
  if (foo) {
    return bar
  }

  return baz

  // bad
  const obj = {
    foo() {
    },
    bar() {
    },
  };
  return obj;

  // good
  const obj = {
    foo() {
    },

    bar() {
    },
  };

  return obj;
  ```


**[⬆ 返回目录](#table-of-contents)**

<a name="commas"></a>
## 逗号

- [19.1](#19.1) <a name='19.1'></a> 行首逗号：**不需要**。

  ```javascript
  // bad
  const story = [
      once
    , upon
    , aTime
  ];

  // good
  const story = [
    once,
    upon,
    aTime
  ]

  // bad
  const hero = {
      firstName: 'Ada'
    , lastName: 'Lovelace'
    , birthYear: 1815
    , superPower: 'computers'
  };

  // good
  const hero = {
    firstName: 'Ada',
    lastName: 'Lovelace',
    birthYear: 1815,
    superPower: 'computers'
  };
  ```


**[⬆ 返回目录](#table-of-contents)**

<a name="type-casting--coercion"></a>
## 类型转换

- [21.1](#21.1) <a name='21.1'></a> 在语句开始时执行类型转换。
- [21.2](#21.2) <a name='21.2'></a> 字符串：

  ```javascript
  //  => this.reviewScore = 9;

  // bad
  const totalScore = this.reviewScore + '';

  // good
  const totalScore = String(this.reviewScore);
  ```

- [21.3](#21.3) <a name='21.3'></a> 对数字使用 `parseInt` 转换，并带上类型转换的基数。

  ```javascript
  const inputValue = '4';

  // bad
  const val = new Number(inputValue);

  // bad
  const val = +inputValue;

  // bad
  const val = inputValue >> 0;

  // bad
  const val = parseInt(inputValue);

  // good
  const val = Number(inputValue);

  // good
  const val = parseInt(inputValue, 10);
  ```

- [21.4](#21.4) <a name='21.4'></a> 布尔:

  ```javascript
  const age = 0;

  // bad
  const hasAge = new Boolean(age);

  // good
  const hasAge = Boolean(age);

  // good
  const hasAge = !!age;
  ```


**[⬆ 返回目录](#table-of-contents)**

<a name="naming-conventions"></a>
## 命名规则

- [22.1](#22.1) <a name='22.1'></a> 避免单字母命名。命名应具备描述性。

  ```javascript
  // bad
  function q() {
    // ...stuff...
  }

  // good
  function query() {
    // ..stuff..
  }
  ```

- [22.2](#22.2) <a name='22.2'></a> 使用驼峰式命名对象、函数和实例。

  ```javascript
  // bad
  const OBJEcttsssss = {};
  const this_is_my_object = {};
  function c() {}

  // good
  const thisIsMyObject = {};
  function thisIsMyFunction() {}
  ```

- [22.3](#22.3) <a name='22.3'></a> 使用帕斯卡式命名构造函数或类。

  ```javascript
  // bad
  function user(options) {
    this.name = options.name;
  }

  const bad = new user({
    name: 'nope',
  });

  // good
  class User {
    constructor(options) {
      this.name = options.name;
    }
  }

  const good = new User({
    name: 'yup',
  });
  ```

- [22.4](#22.4) <a name='22.4'></a> 使用下划线 `_` 开头命名私有属性。

  ```javascript
  // bad
  this.__firstName__ = 'Panda';
  this.firstName_ = 'Panda';

  // good
  this._firstName = 'Panda';
  ```

- [22.5](#22.5) <a name='22.5'></a> 别保存 `this` 的引用。使用箭头函数或 Function#bind。

  ```javascript
  // bad
  function foo() {
    const self = this;
    return function() {
      console.log(self);
    };
  }

  // bad
  function foo() {
    const that = this;
    return function() {
      console.log(that);
    };
  }

  // good
  function foo() {
    return () => {
      console.log(this);
    };
  }
  ```

- [22.6](#22.6) <a name='22.6'></a> 如果你的文件只输出一个类，那你的文件名必须和类名完全保持一致。

  ```javascript
  // file contents
  class CheckBox {
    // ...
  }
  export default CheckBox;

  // in some other file
  // bad
  import CheckBox from './checkBox';

  // bad
  import CheckBox from './check_box';

  // good
  import CheckBox from './CheckBox';
  ```

- [22.7](#22.7) <a name='22.7'></a> 当你导出默认的函数时使用驼峰式命名。你的文件名必须和函数名完全保持一致。

  ```javascript
  function makeStyleGuide() {
  }

  export default makeStyleGuide;
  ```

- [22.8](#22.8) <a name='22.8'></a> 当你导出单例、函数库、空对象时使用帕斯卡式命名。

  ```javascript
  const AirbnbStyleGuide = {
    es6: {
    }
  };

  export default AirbnbStyleGuide;
  ```


**[⬆ 返回目录](#table-of-contents)**


