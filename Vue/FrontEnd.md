

1、this.setState是异步的
在你调用了this.setState后在他的下面输出他的结果还是没变的状态

2、`indexOf()`方法返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1。

3、https://juejin.im/post/5f032fe3f265da22c75734b8![image-20200708172240960](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200708172240960.png)

```js
function append(arr, item) {
let resArr = [...arr,item]
return resArr
}
```

4、Assign

​                        

```
1. 打开一个新的空白页
2. 输入 www.samanthaming.com (当前页)

3. 使用 `window.location.assign('https://www.w3schools.com')` 载入新页面
4. 按 "返回上一页"
5. 返回到了 👉 www.samanthaming.com
```

#### Replace

​                        

```
1. 打开一个新的空白页
2. 输入 www.samanthaming.com (当前页)

3. 使用 `window.location.assign('https://www.w3schools.com')` 载入新页面
4. 按 "返回上一页"
5. 返回到一个空白页
```