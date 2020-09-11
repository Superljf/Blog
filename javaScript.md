####  值到对象的映射

```js
let x='x',y='y'
let obj = {x,y}

console.log(obj) // {x: "x", y: "y"}

```

#### Object.entries()

##### 用于将对象转换为数组

```js
const credits = {
  producer: '大迁世界',
  name: '前端小智',
  rating: 9
}
const arr = Object.entries(credits)
console.log(arr)

*** 输出 ***
[ [ 'producer', '大迁世界' ], [ 'name', '前端小智' ], [ 'rating', 9 ] ]


```

####  Object.values()

##### 用于取出对象中的值

```js
const credits = {
  producer: '大迁世界',
  name: '前端小智',
  rating: 9
}
const arr = Object.values(credits)
console.log(arr)

*** 输出 ***

[ '大迁世界', '前端小智', 9 ]

```

#### 多行字符串

```js
let multiLineString = `some string\n
with multi-line of\n
characters\n`

console.log(multiLineString)

```

#### Array.find 简写

###### 用于取出自己想要的键和值

```
const pets = [{
    type: 'Dog',
    name: 'Max'
  },
  {
    type: 'Cat',
    name: 'Karl'
  },
  {
    type: 'Dog',
    name: 'Tommy'
  }
]
pet = pets.find(pet => pet.type === 'Dog' && pet.name === 'Tommy')

console.log(pet) // { type: 'Dog', name: 'Tommy' }

```

#### charAt() 简写

###### 字符串截取取出相应的字符，可以说是非常非常的nice

```js
'SampleString'.charAt(0) // S
// 简写
'SampleString'[0]

```

#### 有条件的函数调用

###### 三元运算符去控制函数的调用 nice

![image-20200911100449139](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200911100449139.png)

#### 将字符串转换为数字

```js
const num1 = parseInt('100')
// 简写
console.log(+"100")
console.log(+"100.2")

```

#### toString简写

```js
let someNumber = 123
console.log(someNumber.toString()) // "123"
// 简写
console.log(`${someNumber}`) // "123"

```

#### 方法参数验证

######  ES6 中可以为函数的参数设置默认值，有了这个，我们可以实现一个验证方法参数不能为空的巧妙技巧。

```

const isRequired = () => { 
  throw new Error('param is required')
}
 
const print = (num = isRequired()) => { 
  console.log(`printing ${num}`) 
}
 
print(2) //printing 2
print() // error
print(null) //printing null

```

#### 格式化JSON代码

`stringify` 方法有三个参数：`value`，`replacer`和`space`。其中，后两个是可选参数，这也是我们很少知道它的原因。要缩进JSON，必须使用`space`参数。

```js
console.log(JSON.stringify({name:"John",Age:23},null,'\t'));
>>> 
{
 "name": "John",
 "Age": 23
}
```

#### 从数组中获取惟一的值

```js
let uniqueArray = [...new Set([1, 2, 3, 3,3,"school","school",'ball',false,false,true,true])];
 
>>> [1, 2, 3, "school", "ball", false, true]
```

#### 排序数字数组

```js
[0,10,4,9,123,54,1].sort((a,b) => a-b)
 
>>> [0, 1, 4, 9, 10, 54, 123]
```

#### 在解构中使用别名

```js
const object = { number: 10 }
 
const { number } = object
 
// 使用别名
const { number: otherNumber } = object
 
console.log(otherNumber) //10
```

#### 获取数组中的最后一项

```js 
 let array = [0, 1, 2, 3, 4, 5, 6, 7] 
console.log(array.slice(-1))
>>>[7]
 
console.log(array.slice(-2))
>>>[6, 7]
 
console.log(array.slice(-3))
>>>[5, 6, 7]
 
```

