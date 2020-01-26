# NPM 换源

作者：nickfox
链接：https://www.jianshu.com/p/f311a3a155ff

## 使用淘宝镜像

- 临时使用

```bash
  npm --registry https://registry.npm.taobao.org install express
```

- 持久使用

```bash
  npm config set registry https://registry.npm.taobao.org
```

- 通过 cnpm

```bash
  npm install -g cnpm --registry=https://registry.npm.taobao.org
```

## 使用官方镜像

```bash
npm config set registry https://registry.npmjs.org/
```

## 查看 npm 源地址

```bash
npm config get registry
```
