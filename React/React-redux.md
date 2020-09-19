## Redux 

![image-20200316142731650](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200316142731650.png)

- store数据仓库 保存数据的地方
- State： state是一个对象 数据仓库里的所有数据都放到一个state里
- Action：1个动作 触发数据改变的方法
- Dispatch: 将动作触发成方法
- Reducer: 是一函数 通过获取动作  改变数据  生成1个新的state， 从而改变页面

![image-20200312142935373](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200312142935373.png)

![image-20200312143037383](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200312143037383.png)

（1）Web 应用是一个状态机，视图与状态是一一对应的。

（2）所有的状态，保存在一个对象里面。

你需要一种机制，可以在同一个地方查询状态、改变状态、传播状态的变化。

- 某个组件的状态，需要共享
- 某个状态需要在任何地方都可以拿到
- 一个组件需要改变全局状态
- 一个组件需要改变另一个组件的状态

![img](http://www.ruanyifeng.com/blogimg/asset/2016/bg2016091801.png)

- redux 是一个独立专门用于做状态管理的JS库

- 集中式管理react 应用中多个组件共享状态

- 单一数据源
   整个应用状态，都应该被存储在单一store的对象树中。

  只读状态
   唯一可以修改状态的方式，就是发送（dispatch）一个动作（Action），通俗来讲，就是说只有getter，没有setter。

  

### Actions ----  model

#### 1、Actions:

Action是唯一可以改变状态的途径，服务器的各种推送、用户自己做的一些操作，最终都会转换成一个个的Action，而且这些Action会按顺序执行，这种简单化的方法用起来非常的方便。Action 是一个对象。其中的type属性是必须的，表示 Action 的名称：



```go
const action = {
  type: 'ADD_TODO',
  payload: 'Learn Redux'
};
```

```jsx
function changeTable(index) {
        return { type: "channgTable",
                data:index 
               }
}
```

#### 2、Reducers :

Store 收到 Action 以后，必须给出一个新的 State，这样 View 才会发生变化。这种 State 的计算过程就叫做 Reducer。

Reducer 是一个函数，它接受 Action 和当前 State 作为参数，返回一个新的 State。

```jsx
const reducer = function (state, action) {
  // ...
  return new_state;
};

const defaultState = 0;
const reducer = (state = defaultState, action) => {
  switch (action.type) {
    case 'ADD':
      return state + action.payload;
    default: 
      return state;
  }
};

const state = reducer(1, {
  type: 'ADD',
  payload: 2
});
```

#### 3、Store:

#### （View层）页面



##### store.dispatch()`是 View 发出 Action 的唯一方法。

```js
import { createStore } from 'redux';
const store = createStore(fn);

store.dispatch({
  type: 'ADD_TODO',
  payload: 'Learn Redux'
});
```

Store 就是保存数据的地方，你可以把它看成一个容器。整个应用只能有一个 Store。

Redux 提供`createStore`这个函数，用来生成 Store。

> ```javascript
> import { createStore } from 'redux';
> const store = createStore(fn);
> ```

上面代码中，`createStore`函数接受另一个函数作为参数，返回新生成的 Store 对象。

```csharp
var store = createStore(reducer);
```

这就是Store了，用来管理state的单一对象。其中有三个方法：

- store.getState()：获取state，如上，经过reducer已经返回了一个新的state，那么就可以用该函数获取；

- store.dispatch(action)：发出操作，更新state。action内有操作的类型，就可以出发不同的对state的更新；

- store.subscribe(listener)：监听变化，当state发生更新时，就可以在这个函数的回调中监听。

  

  > ```javascript
  > 
  > ```

#### 4、 State

`Store`对象包含所有数据。如果想得到某个时点的数据，就要对 Store 生成快照。这种时点的数据集合，就叫做 State。

当前时刻的 State，可以通过`store.getState()`拿到。

> ```javascript
> import { createStore } from 'redux';
> const store = createStore(fn);
> 
> const state = store.getState();
> ```

Redux 规定， 一个 State 对应一个 View。只要 State 相同，View 就相同。你知道 State，就知道 View 是什么样，反之亦然。

## react-redux

**Provider**和**connect**。

#### 1、Provider:



```xml
<Provider store={store}>
    <Router ref="router" history={hashHistory}>
        <Route path='/' component={Index}>
            <IndexRoute  component={MainPage}></IndexRoute>
        </Route>
    </Router>
</Provider>
```

Provider就是把我们用rudux创建的store传递到内部的其他组件。让内部组件可以享有这个store并提供对state的更新。

#### 2、connect:

```cpp
export default connect(mapStateToProps,mapDispatchToProps)(MainPage);
```

connect()一共有四个参数，但我这里只说基本的两个，**mapStateToProps**和**mapDispatchToProps**。

- mapStateToProps：简单来说，就是把状态绑定到组件的属性当中。我们定义的state对象有哪些属性，在我们组件的props都可以查阅和获取。

  

  ```jsx
  const mapStateToProps = (state, ownProps) => {
        return {tableIndex:state.tableIndex}
  }
  ```

- mapDispatchToProps：在redux中介绍过，用store.dispatch(action)来发出操作，那么我们同样可以把这个方法封装起来，即绑定到我们的方法中。

  

  ```tsx
  const mapDispatchToProps = (dispatch, ownProps) => {
      return {
          changeActive:(args)=>dispatch({type:"changeTable",data:args})
      }
  }
  ```

可以看到，这个方法return的就是一个dispatch函数，将该方法绑定到属性上，我们同样可以在props查看和调用。



## React-redux

#### 1、store

- 用来让外界获取Redux的数据（store.getState）

- 外界来修改Redux中的数据（store.dispatch）

- ```
  import { createStore } from 'redux';
  const store = createStore(reducer);
  ```

#### 2、action

- action:描述我要干啥，一般是一个对象的形式，其中有一个type字段是必须要有的，比如：{ type：‘请求增援’ }，还可以带点数据{ type：‘请求增援’，gun:"100" }

#### 3、reducer

- reducer:撸开袖子真刀实枪的就去干了，比如一连长要求增援，增援要求是100杆枪，团长马上就给你加了100杆枪送了过去。

```
const defaultState = 0;
const reducer = (state = defaultState, action) => {
  switch (action.type) {
    case '请求增援':
      return state + action.gun;
    default: 
      return state;
  }
};
```

action和reducer也可以想象成产品经理和程序员的关系。

产品经理：“我要一个按钮，圆角的”

程序员：“嗯，做好了”

产品经理：“换个颜色吧，红色”

程序员：“ok，换好了”

差不多就是这样，产品经理并不操心具体怎么实现的，他只说他想要干什么（type），然后再提点实现的要求（各种其他的数据），程序员就去具体实现（reducer，修改state，然后返回一个**全新的state,**这里注意我们并没有直接返回原来的state，我们返回的是一个全新的state对象，因为reducer函数是一个没有副作用的纯函数）

那怎么去触发这个操作（action）呢，就好比说我一连长发现敌情了，我怎么报告给通讯班，让通讯班来处理呢？

就是上面提到过的store.dispatch，不过还要加一个参数，那就是action

```
store.dispatch({ type：‘请求增援’，gun:"100" })
```

 

这样就可以触发action，执行reducer，得到一个全新的state。

### 获取Redux中的数据

比如说我要在render函数中显示Redux的数据，那么我就可以先获取它的数据：

```
store.getState()
```

然后把这个数据当做props渲染到组件中去就行了。

### 更新Redux中的数据

如果你要修改它的数据，那就在JSX中调用

```
store.dispatch( { type：‘请求增援’，gun:"100" } )
```

### **响应Redux中的变化**

那么这里问题又来了，你调用了store.dispatch之后Redux中的数据确实改变了，可是React并没有什么变化啊。也就是说React中的render函数并没有被触发呀是不是，就好像React中你直接修改React中的state是没有用的而必须调用React的setState才能重新渲染。

因此，为了让Redux的数据一改变我们就重新渲染，Redux自己提供了一个方法叫做

```
store.subscribe(render)
```

这个函数可以**监听Redux中state的变化**，一旦Redux中的state发生了变化，render函数就会被调用，页面就会被重新渲染。

  在React-redux中有两个比较关键的概念：Provider和connect方法。

一般我们都将顶层组件包裹在Provider组件之中，这样的话，所有组件就都可以在react-redux的控制之下了,**但是store必须作为参数放到Provider组件中去**

```
<Provider store = {store}>
    <团长/>
<Provider>
```

这个组件的目的是让所有组件都能够访问到Redux中的数据。

 这个比较简单，我们主要讲connect方法。

### connect方法：

```
connect(mapStateToProps, mapDispatchToProps)(MyComponent)
```

其实connect方法一共有4个参数，这里主要讲前两个。

#### mapStateToProps

哪个组件想接收数据了 

字面含义是把state映射到props中去，意思就是把Redux中的数据映射到React中的props中去。

也就是说你React想把Redux中的哪些数据拿过来用。

比如这里二连这个组件想要渲染自己枪支的数量。就可以直接在二连这个组件中把Redux中的gunOfErlian拿过来用

```
const mapStateToProps = (state) => {
  return {
    gun: state.gunOfErlian
  }
}
```

然后渲染的时候就可以直接使用this.props.gun

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
class Erlian extends Component {
    constructor(props){
        super(props);
    }
    render(){
        return(
            <div>this.props.gun</div>
        )
    }
}
Erlian = connect()(Erlian);
export default Erlian;
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

那么这样就可以实现渲染，就是把Redux中的state变成React中的props。



#### mapDispatchToProps

如果哪个组件想发送action

通过上面的分析，相信这个函数也很好理解，就是把各种dispatch也变成了props让你可以直接使用

然后就到了我们这里最重要的一点了。

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
const mapDispatchToProps = (dispatch) => {
  return {
    onClick: () => {
      dispatch({
        type: '请求增援',　　　　 gun : 100
      });
    }
  };
}
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

更改一下上面的Erlian组件

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
class Erlian extends Component {
    constructor(props){
        super(props);
    }
    render(){
        return(
            <div>this.props.gun</div>
            <button onClick = {this.props.onClick}>请求增援</button>
        )
    }
}
Erlian = connect()(Erlian);
export default Erlian;
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

当我点击请求增援按钮后，Erlian组件的枪支数量会自动的更新，而**不需要**我们手动的去用store.subscribe订阅render函数以达到更新页面的目的。

这样一来我们就不需要一层层的传递store对象了。

这种随处都可以使用、修改Redux中的数据的方式确实很方便，但Redux推荐的最佳实践还是在尽可能少的地方使用connect，把逻辑，数据相关的都放到容器组件中去处理，其他的组件都由容器组件所生成的props一层层传递下去然后渲染（傻瓜组件），这里就不多说了。

## 案例一

![image-20200316165150706](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200316165150706.png)

![image-20200316170213794](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200316170213794.png)

#### comA

```js

/**
 * 导入connect
 * 利用connect 对组件进行加强
 *  我们实现connect 第二个参数   
 *  构建map
 * 
 * 在组件内部就可以通过this.prop拿到这个组件
 */

import React from 'react'

// 导入connect 
import { connect } from 'react-redux'

const mapDispatchToProps = (dispatch) => {
  return {
    sendAction: () => {
      dispatch({
        type: 'add_action'
      })
    }
  }
}


 class Home extends React.Component {
   
  handleClick = () => {
    this.props.sendAction()
  }
  
  render() {
    return (
      <button onClick={this.handleClick}> + </button>
    )
  }
}

export default connect(null, mapDispatchToProps)(Home)


```

#### action 

```js
// 这是action函数

const sendAction = () => {
  // 我们需要返回一个action对象
  return {
    type: 'send_type',
    value: '我是一个action'
  }
}

module.exports = {
  sendAction
}
```



#### Reducer

```jsx
// 接收两个参数 第一个参数是 state 第二个参数是  action 
// 进行逻辑处理
const initState  = {
  count: 0
}
exports.reducer = (state = initState, action) => {

  switch(action.type) {
    case 'add_action': 
      return {
        count: state.count + 1
      }
      default:
        return state;
  }
  return state;
} 
```

#### Store

```js
import { createStore } from "redux";
// 导入我们自己创建好的reducer
import { reducer } from '../reducer/reducer';
// 构建 store
export default createStore(reducer)
// const store = createStore(reducer);

// export default store;

```

#### ComB

```js
import React from 'react'
import { connect } from 'react-redux';
const  mapStateToProps = state => {
    return state;
};

 class ComB extends React.Component {
  render() {
    return (
    <div>{this.props.count}</div>
    )
  }
}

export default connect(mapStateToProps)(ComB)
```

#### App.js

```js
import React from 'react';
import store from "./store/store";
// 导入Provider组件 利用这个组件包裹我们的结构 从而达到统一维护store的效果
import { Provider } from 'react-redux';
import Home from './pages/home/index';
import ComB from './pages/ComB/index';

function App() {
  return (
    <Provider store={store}>
    <Home/>
    <ComB/>
    </Provider>
  )
}

export default App;
```

