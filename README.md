# js-playground

重拾 javascript

## javascript 基本语法

### 语句（statement）

JavaScript 程序的执行单位为行（line），也就是一行一行地执行。一般情况下，每一行就是一个语句。

语句（statement）是为了完成某种任务而进行的操作，比如下面就是一行赋值语句。

```
var a = 1 + 3;
```

`1 + 3` 叫作表达式--为了得到返回值的计算式。
语句和表达式的区别在于，语句主要为了进行某种操作，一般情况下不需要返回值；表达式则是为了得到返回值，一定会返回一个值。凡是 JavaScript 语言中预期为值的地方，都可以使用表达式。比如，赋值语句的等号右边，预期是一个值，因此可以放置各种表达式。

语句以分号结尾，一个分号就表示一个语句结束。多个语句可以写在一行内。

```
var a = 1 + 3 ; var b = 'abc';
```

分号前面可以没有任何内容，JavaScript 引擎将其视为空语句。

```
; ; ;
```

### 变量

> 变量是对“值”的具名引用。变量就是为“值”起名，然后引用这个名字，就等同于引用这个值。变量的名字就是变量名。
> **注意**JavaScript 的变量名区分大小写，A 和 a 是两个不同的变量。

#### 变量提升

> JavaScript 引擎的工作方式是，先解析代码，获取所有被声明的变量，然后再一行一行地运行。这造成的结果，就是所有的变量的声明语句，都会被提升到代码的头部，这就叫做变量提升（hoisting）。

```
console.log(a);  // undefined
var a = 1;
```

上面代码首先使用 console.log 方法，在控制台（console）显示变量 a 的值。这时变量 a 还没有声明和赋值，所以这是一种错误的做法，但是实际上不会报错。因为存在变量提升，真正运行的是下面的代码。

```
var a;
console.log(a);
a = 1;
```

### 标识符

> 标识符（identifier）指的是用来识别各种值的合法名称。最常见的标识符就是变量名，以及后面要提到的函数名。JavaScript 语言的标识符对大小写敏感，所以 a 和 A 是两个不同的标识符。

标识符有一套命名规则:

- 第一个字符，可以是任意 Unicode 字母（包括英文字母和其他语言的字母），以及美元符号（`$`）和下划线（`_`）。
- 第二个字符及后面的字符，除了 Unicode 字母、美元符号和下划线，还可以用数字 0-9。

- 中文是合法的标识符，可以用作变量名。

- JavaScript 有一些保留字，不能用作标识符：
  ```
  arguments、break、case、catch、class、const、continue、debugger、default、delete、do、else、enum、eval、export、extends、false、finally、for、function、if、implements、import、in、instanceof、interface、let、new、null、package、private、protected、public、return、static、super、switch、this、throw、true、try、typeof、var、void、while、with、yield
  ```

### 注释

> 源码中被 JavaScript 引擎忽略的部分就叫做注释，它的作用是对代码进行解释。

```
// 这是单行注释

/*
 这是
 多行
 注释
*/
```

### 区块

> JavaScript 使用大括号，将多个相关的语句组合在一起，称为“区块”（block）。

- 对于 `var` 命令来说，JavaScript 的区块不构成单独的作用域（scope）。对于`let` 和 `const`命令来说，区块会构成单独的作用域。

  ```js
  {
    var a = 1;
    let b = 2;
    const c = 3;
  }

  console.log(a); // 1
  console.log(b); // Uncaught ReferenceError: b is not defined
  console.log(c); //Uncaught ReferenceError: c is not defined
  ```

- 在 JavaScript 语言中，单独使用区块并不常见，区块往往用来构成其他更复杂的语法结构，比如 for、if、while、function 等。

### 条件语句

- JavaScript 提供 if 结构和 switch 结构，完成条件判断，即只有满足预设的条件，才会执行相应的语句。

#### if 语句

```
if (布尔值)
语句;

// 或者
if (布尔值) 语句;
```

#### if...else 结构

```js
if (m === 0) {
  // ...
} else if (m === 1) {
  // ...
} else if (m === 2) {
  // ...
} else {
  // ...
}
```

#### switch 结构

多个 if...else 连在一起使用的时候，可以转为使用更方便的 switch 结构。

```js
switch (fruit) {
  case "banana":
    // ...
    break;
  case "apple":
    // ...
    break;
  default:
  // ...
}
```

上面代码根据变量 fruit 的值，选择执行相应的 case。如果所有 case 都不符合，则执行最后的 default 部分。需要注意的是，每个 case 代码块内部的 break 语句不能少，否则会接下去执行下一个 case 代码块，而不是跳出 switch 结构。

#### 三语运算符 `?:`

JavaScript 还有一个三元运算符（即该运算符需要三个运算子）`?:`，也可以用于逻辑判断。

```
(条件) ? 表达式1 : 表达式2
```

**例子：**如果 n 可以被 2 整除，则 even 等于 true，否则等于 false。它等同于下面的形式。

```js
// 常规写法
var even;
if (n % 2 === 0) {
  even = true;
} else {
  even = false;
}

// 三元表达式
var even = n % 2 === 0 ? true : false;
```

### 循环语句

> 循环语句用于重复执行某个操作，它有多种形式。

#### while 循环

While 语句包括一个循环条件和一段代码块，只要条件为真，就不断循环执行代码块。

```js
var i = 0;

while (i < 100) {
  console.log("i 当前为：" + i);
  i = i + 1;
}

console.log(`while循环结束后的i为${i}`); // 100
```

#### for 循环

for 语句是循环命令的另一种形式，可以指定循环的起点、终点和终止条件。它的格式如下。

```js
for (初始化表达式; 条件; 递增表达式) 语句;

// 或者

for (初始化表达式; 条件; 递增表达式) {
  语句;
}
```

for 语句后面的括号里面，有三个表达式。

- 初始化表达式（initialize）：确定循环变量的初始值，只在循环开始时执行一次。
- 条件表达式（test）：每轮循环开始时，都要执行这个条件表达式，只有值为真，才继续进行循环。
- 递增表达式（increment）：每轮循环的最后一个操作，通常用来递增循环变量。

```js
var x = 3;
for (var i = 0; i < x; i++) {
  console.log(i);
}

console.log(`for循环结束后i为${i}`);
// 0
// 1
// 2
// for循环结束后i为3
```

#### `do ... while` 循环

`do...while`循环与 `while`循环类似，唯一的区别就是先运行一次循环体，然后判断循环条件。

```js
do 语句;
while (条件);

// 或者
do {
  语句;
} while (条件);
```

**示例：**

```js
var x = 3;
var i = 0;

do {
  console.log(i);
  i++;
} while (i < x);
console.log(`while 循环结束后i为${i}`); // 3

do {
  console.log("do 执行了"); // 会输出在控制台
} while (false);
```

#### break 语句和 continue 语句

break 语句和 continue 语句都具有跳转作用，可以让代码不按既有的顺序执行。

break 语句用于跳出代码块或循环。

```js
var i = 0;

while (i < 100) {
  console.log("i 当前为：" + i);
  i++;
  if (i === 1) break;
}
```

上面代码只会执行 1 次循环，一旦 i 等于 1，就会跳出循环。

for 循环也可以使用 break 语句跳出循环。

```js
for (var i = 0; i < 5; i++) {
  console.log(i);
  if (i === 3) break;
}
// 0
// 1
// 2
// 3
```

**`continue`**语句用于立即终止本轮循环，返回循环结构的头部，开始下一轮循环。

```js
var i = 0;

while (i < 100) {
  i++;
  if (i % 2 === 0) continue;
  console.log("i 当前为：" + i);
}
```

上面代码只有在 i 为奇数时，才会输出 i 的值。如果 i 为偶数，则直接进入下一轮循环。
如果存在多重循环，不带参数的 break 语句和 continue 语句都只针对最内层循环。

#### 标签（label）

JavaScript 语言允许，语句的前面有标签（label），相当于定位符，用于跳转到程序的任意位置，标签的格式如下。

```js
label: 语句;
```

- **标签可以是任意的标识符，但不能是保留字，语句部分可以是任意语句。**
- **标签通常与 break 语句和 continue 语句配合使用，跳出特定的循环。**
- **标签也可以用于跳出代码块。**

```js
// 标签配合break 跳出双层 for 循环
top: for (var i = 0; i < 3; i++) {
  for (var j = 0; j < 3; j++) {
    if (i === 1 && j === 1) break top;
    console.log("i=" + i + ", j=" + j);
  }
}
// i=0, j=0
// i=0, j=1
// i=0, j=2
// i=1, j=0
```

上面代码为一个双重循环区块，break 命令后面加上了 top 标签（注意，top 不用加引号），满足条件时，直接跳出双层循环。如果 break 语句后面不使用标签，则只能跳出内层循环，进入下一次的外层循环。

```js
// 标签配合for 跳过当前循环
top: for (var i = 0; i < 3; i++) {
  for (var j = 0; j < 3; j++) {
    if (i === 1 && j === 1) continue top;
    console.log("i=" + i + ", j=" + j);
  }
}
// i=0, j=0
// i=0, j=1
// i=0, j=2
// i=1, j=0
// i=2, j=0
// i=2, j=1
// i=2, j=2
```

上面代码中，continue 命令后面有一个标签名，满足条件时，会跳过当前循环，直接进入下一轮外层循环。如果 continue 语句后面不使用标签，则只能进入下一轮的内层循环。

```js
// 使用
foo: {
  console.log(1);
  break foo;
  console.log("本行不会输出");
}
console.log(2);
// 1
// 2
```

## 数据类型

### 数据类型概述

- JavaScript 语言的每一个值，都属于某一种数据类型。JavaScript 的数据类型，共有六种。（ES6 又新增了第七种 Symbol 类型的值。）
  - 数值（number）：整数和小数（比如 1 和 3.14）
  - 字符串（string）：文本（比如 Hello World）。
  - 布尔值（boolean）：表示真伪的两个特殊值，即 true（真）和 false（假）
  - undefined：表示“未定义”或不存在，即由于目前没有定义，所以此处暂时没有任何值
  - null：表示空值，即此处的值为空。
  - 对象（object）：各种值组成的集合。

通常，数值、字符串、布尔值这三种类型，合称为原始类型（primitive type）的值，即它们是最基本的数据类型，不能再细分了。对象则称为合成类型（complex type）的值，因为一个对象往往是多个原始类型的值的合成，可以看作是一个存放各种值的容器。至于 undefined 和 null，一般将它们看成两个特殊值。

对象是最复杂的数据类型，又可以分成三个子类型。

- 狭义的对象（object）
- 数组（array）
- 函数（function）

狭义的对象和数组是两种不同的数据组合方式，函数其实是处理数据的方法，JavaScript 把它当成一种数据类型，可以赋值给变量，这为编程带来了很大的灵活性，也为 JavaScript 的“函数式编程”奠定了基础。

### typeof 运算符

```js
typeof 123; // number
typeof "124"; // string
typeof false; // boolean
typeof undefined; // undefined
typeof null; // object
typeof {}; // object
typeof []; // object
typeof new Function(); // function
```

**注意：**
null 的类型是 object，这是由于历史原因造成的。1995 年的 JavaScript 语言第一版，只设计了五种数据类型（对象、整数、浮点数、字符串和布尔值），没考虑 null，只把它当作 object 的一种特殊值。后来 null 独立出来，作为一种单独的数据类型，为了兼容以前的代码，typeof null 返回 object 就没法改变了。
