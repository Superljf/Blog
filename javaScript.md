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

