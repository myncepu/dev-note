# TypeScript 3.0: unknown 类型

[原文链接](https://github.com/xitu/gold-miner/blob/master/TODO1/typescript-3-0-the-unknown-type.md)

自从 TypeScript 在 2012 年发布第一个版本以来 any 类型就一直存在。它代表所有可能的 JavaScript 值 — 基本类型，对象，数组，函数，Error，Symbol，以及任何你可能定义的值。

TypeScript 允许我们对 any 类型的值执行任何操作，而无需事先执行任何形式的检查。使用 any 类型，可以很容易地编写类型正确但是执行异常的代码。如果我们使用 any 类型，就无法享受 TypeScript 大量的保护机制。

这是 unknown 类型的主要价值主张：TypeScript 不允许我们对类型为 unknown 的值执行任意操作。相反，我们必须首先执行某种类型检查以缩小我们正在使用的值的类型范围。
