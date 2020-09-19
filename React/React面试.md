#### 问题1：什么是虚拟DOM？

> 主题: React
> 难度: ⭐

**虚拟 DOM (VDOM)**是真实 DOM 在内存中的表示。UI 的表示形式保存在内存中，并与实际的 DOM 同步。这是一个发生在渲染函数被调用和元素在屏幕上显示之间的步骤，整个过程被称为**调和**。

#### 问题 5：state 和 props 区别是啥？

> 主题: React
> 难度: ⭐⭐

`props`和`state`是普通的 JS 对象。虽然它们都包含影响渲染输出的信息，但是它们在组件方面的功能是不同的。即

- `state` 是组件自己管理数据，控制自己的状态，可变；

- `props` 是外部传入的数据参数，不可变；

- 没有`state`的叫做无状态组件，有`state`的叫做有状态组件；

- 多用 `props`，少用 `state`，也就是多写无状态组件。

  #### 问题 8：在构造函数调用 `super` 并将 `props` 作为参数传入的作用是啥？

  > 主题: React
  > 难度: ⭐⭐

  在调用 `super()` 方法之前，子类构造函数无法使用`this`引用，ES6 子类也是如此。将 `props` 参数传递给 `super()` 调用的主要原因是在子构造函数中能够通过`this.props`来获取传入的 `props`**传递 props**

  ```
  class MyComponent extends React.Component {
    constructor(props) {
      super(props);
      console.log(this.props);  // { name: 'sudheer',age: 30 }
    }
  }
  ```

```
class MyComponent extends React.Component {
  constructor(props) {
    super();
    console.log(this.props); // undefined
    // 但是 Props 参数仍然可用
    console.log(props); // Prints { name: 'sudheer',age: 30 }
  }

  render() {
    // 构造函数外部不受影响
    console.log(this.props) // { name: 'sudheer',age: 30 }
  }
}
```

#### 问题 13：为什么不直接更新 `state` 呢 ?

> 主题: React
> 难度: ⭐⭐⭐

如果试图直接更新 `state` ，则不会重新渲染组件。

```
 // 错误
 This.state.message = 'Hello world';
```

需要使用`setState()`方法来更新 `state`。它调度对组件`state`对象的更新。当`state`改变时，组件通过重新渲染来响应：

```
// 正确做法
This.setState({message: ‘Hello World’});
```

