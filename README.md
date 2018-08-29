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

## 变量

> 变量是对“值”的具名引用。变量就是为“值”起名，然后引用这个名字，就等同于引用这个值。变量的名字就是变量名。
> **注意**JavaScript 的变量名区分大小写，A 和 a 是两个不同的变量。

### 变量提升

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

## 标识符

> 标识符（identifier）指的是用来识别各种值的合法名称。最常见的标识符就是变量名，以及后面要提到的函数名。JavaScript 语言的标识符对大小写敏感，所以 a 和 A 是两个不同的标识符。

标识符有一套命名规则:

- 第一个字符，可以是任意 Unicode 字母（包括英文字母和其他语言的字母），以及美元符号（`$`）和下划线（`_`）。
- 第二个字符及后面的字符，除了 Unicode 字母、美元符号和下划线，还可以用数字 0-9。

- 中文是合法的标识符，可以用作变量名。

- JavaScript 有一些保留字，不能用作标识符：
  ```
  arguments、break、case、catch、class、const、continue、debugger、default、delete、do、else、enum、eval、export、extends、false、finally、for、function、if、implements、import、in、instanceof、interface、let、new、null、package、private、protected、public、return、static、super、switch、this、throw、true、try、typeof、var、void、while、with、yield
  ```

## 注释

> 源码中被 JavaScript 引擎忽略的部分就叫做注释，它的作用是对代码进行解释。

```
// 这是单行注释

/*
 这是
 多行
 注释
*/
```

## 区块

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

## 条件语句

- JavaScript 提供 if 结构和 switch 结构，完成条件判断，即只有满足预设的条件，才会执行相应的语句。

### if 语句

```
if (布尔值)
语句;

// 或者
if (布尔值) 语句;
```

### if...else 结构

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

### switch 结构

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

### 三语运算符 `?:`

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

## 循环语句

> 循环语句用于重复执行某个操作，它有多种形式。

### while 循环

While 语句包括一个循环条件和一段代码块，只要条件为真，就不断循环执行代码块。

```js
var i = 0;

while (i < 100) {
  console.log("i 当前为：" + i);
  i = i + 1;
}

console.log(`while循环结束后的i为${i}`); // 100
```

### for 循环

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

### `do ... while` 循环

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

### break 语句和 continue 语句

break 语句和 continue 语句都具有跳转作用，可以让代码不按既有的顺序执行。

break 语句用于跳出代码块或循环。

```js
var i = 0;

while (i < 100) {
  console.log("i 当前为：" + i);
  i++;
  if (i === 10) break;
}
```
