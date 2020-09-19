![JavaScript 迁移 TypeScript 的坑](https://pic4.zhimg.com/50/v2-ed0c11740c5bf50f307a38d0262149b1_hd.jpg)

#### 获取TypeScript

- 安装

  ```shell
  npm install -g typescript
  ```

  ```shell
  $ tsc -v
  Version 3.2.2
  ```

- 编译

- ![image-20200402102859242](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200402102859242.png)

  ```powershell
  tsc helloworld.ts
  ```

  在命令行上，运行TypeScript编译器：

  ```shell
  tsc greeter.ts
  ```

```ts
function greeter(person) {
    return "Hello, " + person;
}

let user = "Jane User";

document.body.innerHTML = greeter(user);
```

##### 添加类型注解 ：string类型注解

#### 类型注解

- TypeScript里的类型注解是一种轻量级的为函数或变量添加约束的方式。
- TypeScript提供了静态的代码分析
- TypeScript支持JavaScript的新特性，比如支持基于类的面向对象编程

#### Webpack

Webpack集成非常简单。 你可以使用 `ts-loader`，它是一个TypeScript的加载器，结合`source-map-loader`方便调试。 运行：

```shell
npm install ts-loader source-map-loader
```

```jsx
 	    module: {
        loaders: [
            // All files with a '.ts' or '.tsx' extension will be handled by 'ts-loader'.
            { test: /\.tsx?$/, loader: "ts-loader" }
        ],
```

要注意的是`ts-loader`必须在其它处理`.js`文件的加载器之前运行。

### 获取声明文件

如果你开始做转换到TypeScript导入，你可能会遇到`Cannot find module 'foo'.`这样的错误。 问题出在没有 *声明文件*来描述你的代码库。 幸运的是这非常简单。 如果TypeScript报怨像是没有 `lodash`包，那你只需这样做

```shell
npm install -s @types/lodash
```

### 由模块导出

通常来讲，由模块导出涉及添加属性到`exports`或`module.exports`。 TypeScript允许你使用顶级的导出语句。 比如，你要导出下面的函数：

```js
module.exports.feedPets = function(pets) {
    // ...
}
```

那么你可以这样写：

```ts
export function feedPets(pets) {
    // ...
}
```

有时你会完全重写导出对象。 这是一个常见模式，这会将模块变为可立即调用的模块：

```js
var express = require("express");
var app = express();
```

之前你可以是这样写的：

```js
function foo() {
    // ...
}
module.exports = foo;
```

在TypeScript里，你可以使用`export =`来代替。

```ts
function foo() {
    // ...
}
export = foo;
```

### 连续添加属性

有些人可能会因为代码美观性而喜欢先创建一个对象然后立即添加属性：

```js
var options = {};
options.color = "red";
options.volume = 11;
```

TypeScript会提示你不能给`color`和`volumn`赋值，因为先前指定`options`的类型为`{}`并不带有任何属性。 如果你将声明变成对象字面量的形式将不会产生错误：

```ts
let options = {
    color: "red",
    volume: 11
};
```

你还可以定义`options`的类型并且添加类型断言到对象字面量上。

```ts
interface Options { color: string; volume: number }

let options = {} as Options;
options.color = "red";
options.volume = 11;
```

### `any`，`Object`，和`{}`

### 严格的`null`与`undefined`检查

```
在 JavaScript 中 null 表示 "什么都没有"。

null是一个只有一个值的特殊类型。表示一个空对象引用。

用 typeof 检测 null 返回是 object。
```

默认地，TypeScript把`null`和`undefined`当做属于任何类型。 这就是说，声明为 `number`类型的值可以为`null`和`undefined`。 因为在JavaScript和TypeScript里， `null`和`undefined`经常会导致BUG的产生，所以TypeScript包含了`strictNullChecks`选项来帮助我们减少对这种情况的担忧。

当启用了`strictNullChecks`，`null`和`undefined`获得了它们自己各自的类型`null`和`undefined`。 当任何值 *可能*为`null`，你可以使用联合类型。 比如，某值可能为 `number`或`null`，你可以声明它的类型为`number | null`。

假设有一个值TypeScript认为可以为`null`或`undefined`，但是你更清楚它的类型，你可以使用`!`后缀。

```js
declare var foo: string[] | null;

foo.length;  // error - 'foo' is possibly 'null'

foo!.length; // okay - 'foo!' just has type 'string[]'
```

# React & Webpack

Webpack这个工具可以将你的所有代码和可选择地将依赖捆绑成一个单独的`.js`文件。

现在我们添加React和React-DOM以及它们的声明文件到`package.json`文件里做为依赖：

```shell
npm install --save react react-dom @types/react @types/react-dom
```