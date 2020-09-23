####  值到对象的映射

```js
let x='x',y='y'
let obj = {x,y}

console.log(obj) // {x: "x", y: "y"}

```

#### Object.entries()

用于将对象转换为数组

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

用于取出对象中的值

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

用于取出自己想要的键和值

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

字符串截取取出相应的字符，可以说是非常非常的nice

```js
'SampleString'.charAt(0) // S
// 简写
'SampleString'[0]

```

#### 有条件的函数调用

三元运算符去控制函数的调用 nice

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

 ES6 中可以为函数的参数设置默认值，有了这个，我们可以实现一个验证方法参数不能为空的巧妙技巧。

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

#### 如何隐藏所有指定的元素

```js
const hide2 = (el) => Array.from(el).forEach(e => (e.style.display = 'none'));

// 事例:隐藏页面上所有`<img>`元素?
hide(document.querySelectorAll('img'))
```

#### 如何检查元素是否具有指定的类？

页面DOM里的每个节点上都有一个`classList`对象，程序员可以使用里面的方法新增、删除、修改节点上的CSS类。使用`classList`，程序员还可以用它来判断某个节点是否被赋予了某个CSS类。

```js
const hasClass = (el, className) => el.classList.contains(className)

// 事例
hasClass(document.querySelector('p.special'), 'special') // true
```

#### 3.如何切换一个元素的类?

```
const toggleClass = (el, className) => el.classList.toggle(className)

// 事例 移除 p 具有类`special`的 special 类
toggleClass(document.querySelector('p.special'), 'special')
```

#### 4.如何获取当前页面的滚动位置？

```
const getScrollPosition = (el = window) => ({
  x: el.pageXOffset !== undefined ? el.pageXOffset : el.scrollLeft,
  y: el.pageYOffset !== undefined ? el.pageYOffset : el.scrollTop
});

// 事例
getScrollPosition(); // {x: 0, y: 200}
```

#### 6.如何检查父元素是否包含子元素？

```js
const elementContains = (parent, child) => parent !== child && parent.contains(child);

// 事例
elementContains(document.querySelector('head'), document.querySelector('title')); 
// true
elementContains(document.querySelector('body'), document.querySelector('body')); 
// false
```

#### 如何获取元素中的所有图像？

```js
const getImages = (el, includeDuplicates = false) => {
  const images = [...el.getElementsByTagName('img')].map(img => img.getAttribute('src'));
  return includeDuplicates ? images : [...new Set(images)];
};

// 事例：includeDuplicates 为 true 表示需要排除重复元素
getImages(document, true); // ['image1.jpg', 'image2.png', 'image1.png', '...']
getImages(document, false); // ['image1.jpg', 'image2.png', '...']
```

#### How to get the current URL?

```js
const currentURL = () => window.location.href

// 事例
currentURL() // 'https://google.com'
```

#### 11.如何创建一个包含当前URL参数的对象？

```js
const getURLParameters = url =>
  (url.match(/([^?=&]+)(=([^&]*))/g) || []).reduce(
    (a, v) => ((a[v.slice(0, v.indexOf('='))] = v.slice(v.indexOf('=') + 1)), a),
    {}
  );

// 事例
getURLParameters('http://url.com/page?n=Adam&s=Smith'); // {n: 'Adam', s: 'Smith'}
getURLParameters('google.com'); // {}
```

#### 14.`如何在等待指定时间后调用提供的函数？`

```js
const delay = (fn, wait, ...args) => setTimeout(fn, wait, ...args);
delay(
  function(text) {
    console.log(text);
  },
  1000,
  'later'
); 

// 1秒后打印 'later'
```

#### 15.如何在给定元素上触发特定事件且能选择地传递自定义数据？

```js
const triggerEvent = (el, eventType, detail) =>
  el.dispatchEvent(new CustomEvent(eventType, { detail }));

// 事例
triggerEvent(document.getElementById('myId'), 'click');
triggerEvent(document.getElementById('myId'), 'click', { username: 'bob' });
```

#### 18.如何获得两个日期之间的差异（以天为单位）？

```js
const getDaysDiffBetweenDates = (dateInitial, dateFinal) =>
  (dateFinal - dateInitial) / (1000 * 3600 * 24);

// 事例
getDaysDiffBetweenDates(new Date('2017-12-13'), new Date('2017-12-22')); // 9
```

#### setTimeout()接受两个参数，第一个是回调函数，第二个是推迟执行的毫秒数。

> ```javascript
> console.log(1);
> setTimeout(function(){console.log(2);},1000);
> console.log(3);
> ```

上面代码的执行结果是1，3，2，因为setTimeout()将第二行推迟到1000毫秒之后执行。

如果将setTimeout()的第二个参数设为0，就表示当前代码执行完（执行栈清空）以后，立即执行（0毫秒间隔）指定的回调函数。

> ```javascript
> setTimeout(function(){console.log(1);}, 0);
> console.log(2);
> ```

上面代码的执行结果总是2，1，因为只有在执行完第二行以后，系统才会去执行"任务队列"中的回调函数。

总之，setTimeout(fn,0)的含义是，指定某个任务在主线程最早可得的空闲时间执行，也就是说，尽可能早得执行。它在"任务队列"的尾部添加一个事件，因此要等到同步任务和"任务队列"现有的事件都处理完，才会得到执行。

#### 创建对象的几种方式

```js
 //创建对象的几种方式
        //1.字面量
        var obj1 = {name: 'solo obj1'};
        //2.new Object
        var obj2 = new Object({name: 'solo obj2'})
        //3.构造函数创建
        var M = function(name){
            this.name = name;
        }
        var obj3 = new M('solo obj3');
        //4.Object.create
        var p = {name: 'p'};
        var obj4 = Object.create(p);

```

####  instanceof 和 typeof 的区别

typeof 对于基本数据类型（null, undefined, string, number, boolean, symbol），除了 null 都会返回正确的类型。null 会返回 object。
typeof 对于对象类型，除了函数会返回 function，其他的都返回 object。
如果我们想获得一个变量的正确类型，可以通过 `Object.prototype.toString.call(xx)`。这样我们就可以获得类似 `[object Type]` 的字符串。

```js

```

#### Promise 处理错误异常

```js
function toUppercase(string) {
  if (typeof string !== "string") {
    throw TypeError("Wrong type given, expected a string");
  }

  return string.toUpperCase();
}

toUppercase(4);

因为使用了 Promise ，所以可以使用 then 来接收返回的内容，或者用 catch 来捕获出现的错误。
toUppercase(99)
  .then(result => result)
  .catch(error => console.error(error.message));


```



```js


function toUppercase(string) {
  if (typeof string !== "string") {
    return Promise.reject(TypeError("Wrong type given, expected a string"));
  }

  const result = string.toUpperCase();

  return Promise.resolve(result);
}


```

```js
					{@else if it.markState==3} 
										{@if it.statisticalRule == 1} 
											<td>
												<span style="color: #CCCCCC;">&nbsp;
												{@if it.totalConvertMark == ''}
												${it.totalMark}
												{@else}
												${it.totalConvertMark}
												{@/if}
												</span>
											</td>
											<td>--</td>
										{@else} 
										<td><span style="color: #CCCCCC;">&nbsp;不统计</span></td>
										<td>--</td>
										{@/if}					
									{@/if}
```

