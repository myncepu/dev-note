# 如何在 Node.js 中使用 TypeScript

[视频链接](https://www.youtube.com/watch?v=1UcLoOD1lRM)

## 新建一个 Node.js 项目

运行

```shell
npm init -y
```

该命令会在当前目录下创建一个 package.json 文件，文件内容为

```json
{
  "name": "<current-folder-name></current-folder-name>",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

## 项目中添加 TypeScript

```shell
yarn add -D typescript
```

使用 `tsc --init` 创建 tsconfig.json ，用来存储 TypeScript compiler 设置选项

```shell
npx tsc --init
```

## 写一些 ts 代码

新建 src/index.ts 文件

```shell
# shell command
mkdir src
touch src/index.ts
echo "console.log('Hello from TypeScript')" > src/index.ts
```

编译 ts 为 js，修改 package.json scripts:

```json
{
  ...
  "script": {
    "build": "tsc"
  }
  ...
}
```

tsc 会将 ts 编译为 js,运行

```shell
yarn build
```

该命令会生成 index.js:

```js
// src/index.js
'use strict'
console.log('Hello from TypeScript')
```

可以使用 `node src/index.js`来运行编译后的 `src/index.js`

```shell
node src/index.js
```

输出

```shell
Hello from TypeScript
```

如果每次修改代码都需要手动编译在运行的话，就太麻烦了！可以安装 `ts-node` 来直接运行 ts 代码:

```shell
yarn add -D ts-node
```

修改 `package.json`，在 script 中添加命令:

```json
"script" {
  ...
  "start": "ts-node src/index.ts"
  ...
}
```

运行 `yarn start`

```shell
yarn run v1.12.3
$ ts-node src/index.ts
Hello from TypeScript
✨  Done in 1.99s.
```

可以发现 ts 可以直接运行了！但是还有一个问题，开发过程中我们需要不停修改源码，如果每次修改后都手动运行 `yarn start` 就太麻烦了，这时候我们可以借助 `ts-node-dev` 或者 `nodemon` 包，在我们修改代码后重新启动我们的程序。

### ts-node-dev

安装 `ts-node-dev`

```shell
yarn add -D ts-node-dev
```

修改 `package.json`

```json
"script" {
  ...
  "start": "ts-node-dev --respawn src/index.ts"
  ...
}
```

运行

```shell
yarn start
```

修改 `index.ts` 为

```ts
console.log('Hello from VS Code')
```

发现程序重新启动，控制台输出：

```shell
Hello from VS Code
```

### nodemon

```shell
yarn add -D nodemon
```

修改 package.json:

```json
"script" {
  ...
  "dev": "nodemon --exec ts-node src/index.ts"
  ...
}
```

nodemon 会监控文件变化，发现文件变化之后运行 `ts-node src/index.ts`

两种方法都可以使用，具体到某些项目，有时其中一种会快些。

## 使用其他 ts 和 js libraries

比如使用 express:

```shell
yarn add express
```

`express` 是一个 js library，幸运的是，已经有人为 `express` 写好了类型库，我们可以通过 `yarn add -D @types/express` 来安装 `express` 类型库。

```shell
yarn add -D @types/express
```

还有一个非常好的 package 叫做 `@types/node`

```shell
yarn add -D @types/node
```

这些类型库会在我们使用这些库时提供很大的帮助。如果碰到一些没有类型的包时，我们可以通过一些其他方法来解决。
比如，`shortid` 没有对应类型包

```shell
yarn add shortid
```

`tsc` 报错：

```shell
无法找到模块“short-id”的声明文件。
```

可以通过手动申明 `shortid` 类型订阅来消除错误:

```shell
mkdir src/@types
touch src/@types/shortid.d.ts
```

shortid.d.tx

```ts
declare module 'shortid'
```

## 问题

1. 重启 ts 服务器来解决

   有时候 TypeScript 报一些奇怪的错误，可以通过重启 ts 服务器来解决。
   按 `cmd + shift + p` ，输入 `typescript`，在下拉框中选择“重启 ts 服务器"。

2. cast ts 变量类型

   ```ts
   req.name = 'little rabbit'
   ```

   报错 req 上不存在 name 属性, cast req 为 any。

   ```ts
   ;(req as any).name = 'little rabbit'
   ```

3. 函数可选变量

   ```ts
   const add = (a: number, b? number) => { }
   ```

   b 为可选参数。

   ```ts
   const add = (a: number, b? number) => a + b
   ```

   报错： b 可能为 undefined,可以通过在 b 后加感叹号来告诉 tsc 我们会确保 b 不会是 undefined

   ```ts
   const add = (a: number, b? number) => a + b!
   ```

4. ! 和 (variable as any) 都应该尽量减少使用或者不用，可以通过 `@ts-ignore` 或者 variable cast 来告诉 tsc 忽略错误。

   ```ts
   const add = (a: number, b? number) => {
     // @ts-ignore
     return a + b
   }

   const add = (a: number, b? number) => {
     // 或者 cast b 为 number
     return a + (b as number)
   }
   ```

5. TypeScript 中 type 和 interface 区别

   结论： object 使用 interface ，其他使用 type，仅供参考。
