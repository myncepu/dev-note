# 1. JavaScript 测试基础

> 记录学习 Kent C. Dodds 的 [Testing JavaScript](https://testingjavascript.com/) 课程时的笔记。

<!-- TOC -->

- [JavaScript 测试基础](#javascript-测试基础)
  - [介绍](#介绍)
  - [抛出错误](#抛出错误)
    - [例子](#例子)
    - [完整代码](#完整代码)
  - [总结](#总结)

<!-- /TOC -->

## 1.1. 介绍

了解一个工具的原理对于更好地使用它十分有用。本课程将创建一个小型的 Jest（JavaScript 测试框架，由 Facebook 开发），进而深入了解 Jest 的原理及用途。

![Jest](https://person-blog-1255441669.cos.ap-beijing.myqcloud.com/images/20191217234417.png)

## 1.2. 抛出错误

首先，我们将了解什么是测试。通过编写一段代码，调用需要测试的代码，比较预期结果和实际结果，并在当两者不符时抛出错误。简单说测试就是用来测试代码是否符合预期的代码。

有时候测试前需要一些设置，例如触发浏览器事件前需要页面组件渲染完成、或者需要读取数据库中的用户数据，这时候测试会变得相对复杂。相对而言，测试纯函数（不依赖外界环境，同样的输入永远获得同样的输出）就简单得多了。

### 1.2.1. 例子

`sum` 函数有个 bug，该函数为两个数相减，而不是相加。修改这个错误很容易，但是我们想写一段自动测试代码，来确保这个错误永远不会再次发生。

```js
// simple.js
const sum = (a, b) => a - b;
const result = sum(3, 7);
```

`sum(3, 7)` 期望输出为 `10`，如果计算值与期望值不同，我们将抛出一个错误："Result is not equal to expected"。

```js
// simple.js
...
const expected = 10
if (result !== expected) {
  throw new Error(`${result} is not equal to ${expected}`)
}
```

`simple.js` 完整代码：

```js
const sum = (a, b) => a - b;
const subtract = (a, b) => a - b;

const result = sum(3, 7);
const expected = 10;
if (result !== expected) {
  throw new Error(`${result} is not equal to ${expected}`);
}
```

运行这段代码：

```bash
node simple.js
```

代码报错：`-4 is not equal to 10`

我们修复 `sum` 函数中减号为加号，重新运行 `node simple.js`，发现代码未抛出错误。

这是一个最基础的测试。接下来，我们来测试 `subtract` 函数。将 `result`，`expected` 由 `const` 改为 `let`，并测试 `subtract` 函数：

```js
// simple.js
...
result = subtract(7, 3);
expected = 4;
if (result !== expected) {
  throw new Error(`${result} is not equal to ${expected}`);
}
```

重新运行脚本，发现脚本未报错。我们故意改错 `sum` 或者 `subtract` 函数，重新运行脚本，发现测试抛出了错误。JavaScript 测试框架会尽可能详尽地阐述这种错误信息，方便我们快速定位和修复问题。

本例子展示了一个最基本的测试，当预期值和实际值不符时抛出错误。

### 1.2.2. 完整代码

```js
// simple.js
const sum = (a, b) => a + b;
const subtract = (a, b) => a - b;

let result = sum(3, 7);
let expected = 10;
if (result !== expected) {
  throw new Error(`${result} is not equal to ${expected}`);
}

result = subtract(7, 3);
expected = 4;
if (result !== expected) {
  throw new Error(`${result} is not equal to ${expected}`);
}
```

## 1.3. 总结

测试是用来判断我们写的代码是否符合预期的代码。
