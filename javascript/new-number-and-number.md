# new Number() 和 Number() 的区别

[StackOverflow 链接](https://stackoverflow.com/questions/4719320/new-number-vs-number)

`new Number(expression)` 创建一个 wrapper object

`Number(expression)` 将 expression 转化为 number primitive value

```js
typeof new Boolean("true"); // "object"
typeof Boolean("true"); // "boolean"

// Note I'm using strict-equals
new Boolean("true") === true; // false
Boolean("true") === true; // true
```

```js
// Generally:
// You don't need those:
new Number();
new String();
new Boolean();

// You can use those for casting:
Number(value);
String(value);
Boolean(value);
```

Note: While the wrapper object will get converted to the primitive automatically when necessary (and vice versa), there is only one case I can think of where you would want to use new Boolean, or any of the other wrappers for primitives - if you want to attach properties to a single value. E.g:

```js
var b = new Boolean(true);
b.relatedMessage = "this should be true initially";
alert(b.relatedMessage); // will work

var b = true;
b.relatedMessage = "this should be true initially";
alert(b.relatedMessage); // undefined
```
