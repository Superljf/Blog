#### 模板字符串

```js
onst name = 'kris'
const age = 24
const info = `My name is ${name}, I am ${age}`
```

#### async   await  

- async 用于申明一个 function 是异步的

- await 用于等待一个异步方法执行完成。
- await 等待的是一个表达式，这个表达式的计算结果是 Promise 对象或者其它值（换句话说，就是没有特殊限定）。

```html
const优于let有几个原因。一个是const可以提醒阅读程序的人，这个变量不应该改变；另一个是const比较符合函数式编程思想，运算不改变值，只是新建值，而且这样也有利于将来的分布式运算；最后一个原因是 JavaScript 编译器会对const进行优化，所以多使用const，有利于提高程序的运行效率，也就是说let和const的本质区别，其实是编译器内部的处理不同。
```

```js
函数的参数如果是对象的成员，优先使用解构赋值。

// bad
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;
}

// good
function getFullName(obj) {
  const { firstName, lastName } = obj;
}

// best
function getFullName({ firstName, lastName }) {
}
```

```js
数组
使用扩展运算符（...）拷贝数组。

// bad
const len = items.length;
const itemsCopy = [];
let i;

for (i = 0; i < len; i++) {
  itemsCopy[i] = items[i];
}

// good
const itemsCopy = [...items];
使用 Array.from 方法，将类似数组的对象转为数组。

const foo = document.querySelectorAll('.foo');
const nodes = Array.from(foo);
```

```js
那些使用匿名函数当作参数的场合，尽量用箭头函数代替。因为这样更简洁，而且绑定了 this。

// bad
[1, 2, 3].map(function (x) {
  return x * x;
});

// good
[1, 2, 3].map((x) => {
  return x * x;
});

// best
[1, 2, 3].map(x => x * x);
```

```js
// ES6的写法
import React from 'react';

class Breadcrumbs extends React.Component {
  render() {
    return <nav />;
  }
};

export default Breadcrumbs;
```

```js
上面代码也展示了一种去除数组重复成员的方法。

// 去除数组的重复成员
[...new Set(array)]
上面的方法也可以用于，去除字符串里面的重复字符。

[...new Set('ababbc')].join('')
// "abc"
```

```
“Same-value-zero equality”，它类似于精确相等运算符（`===`），主要的区别是向 Set 加入值时认为`NaN`等于自身，而精确相等运算符认为`NaN`不等于自身。
```

```js
Set 结构的实例与数组一样，也拥有forEach方法，用于对每个成员执行某种操作，没有返回值。

let set = new Set([1, 4, 9]);
set.forEach((value, key) => console.log(key + ' : ' + value))
// 1 : 1
// 4 : 4
// 9 : 9
```

```js
扩展运算符和 Set 结构相结合，就可以去除数组的重复成员。

let arr = [3, 5, 2, 2, 5, 5];
let unique = [...new Set(arr)];
// [3, 5, 2]
```

```js
而且，数组的map和filter方法也可以间接用于 Set 了。

let set = new Set([1, 2, 3]);
set = new Set([...set].map(x => x * 2));
// 返回Set结构：{2, 4, 6}

let set = new Set([1, 2, 3, 4, 5]);
set = new Set([...set].filter(x => (x % 2) == 0));
// 返回Set结构：{2, 4}
```

```
!! 运算符可以将右侧的值强制转换为布尔值，这也是将值转换为布尔值的一种简单方法。
```

```js
转换为布尔值（调用Boolean()方法）
转换为数字（调用Number()、parseInt()和parseFloat()方法）
转换为字符串（调用.toString()或者String()方法）
```

