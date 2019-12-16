# 变量申明

## var

var 声明语句声明一个变量，并且可选地将其初始化为一个值。

```js
// var 申明语句
var x;

// var 申明变量 y，并初始化
var y = "Hello World";
```

## 变量提升

使用 var 申明的变量可以在声明之前使用，这个行为叫做 hoisting，hoisting 就像是把所有的变量声明移动到函数或者全局代码的开头位置

```js
bla = 2;
var bla;
// ...

// 可以隐式地（implicitly）将以上代码理解为：

var bla;
bla = 2;
```

提升将影响变量声明，而不会影响其值的初始化

```js
function do_something() {
  console.log(bar); // undefined
  var bar = 111;
  console.log(bar); // 111
}

// is implicitly understood as:
function do_something() {
  var bar;
  console.log(bar); // undefined
  bar = 111;
  console.log(bar); // 111
}
```

使用 let 创建的变量，不存在变量提升。只有在 let 申明语句之后，变量才能使用。不然会报 ReferenceError 错误

```js
console.log(x); // 错误：Uncaught ReferenceError ...
let x = "Hello World";
// 这里就可以安全使用 x
```

> ES6 明确规定，如果区块中存在 let 和 const 命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。 总之，在代码块内，使用 let 命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称 TDZ）。
