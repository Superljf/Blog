#### 定义

**React Hooks 的意思是，组件尽量写成纯函数，如果需要外部功能和副作用，就用钩子把外部代码"钩"进来。** React Hooks 就是那些钩子。

#### 命名

所有的钩子都是为函数引入外部功能，所以 React 约定，钩子一律使用`use`前缀命名，便于识别。你要使用 xxx 功能，钩子就命名为 usexxx。

## useState()：状态钩子

`useState()`用于为函数组件引入状态（state）。纯函数不能有状态，所以把状态放在钩子里面。

- `useState()` 方法里面唯一的参数就是初始 state。
- 返回值为：当前 state 以及更新 state 的函数
- 当我们使用 `useState` 定义 state 变量时候，它返回一个有两个值的数组。第一个值是当前的 state，第二个值是更新 state 的函数。
- ![image-20200331093626340](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200331093626340.png)
- ![image-20200331093638557](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200331093638557.png)
- ![image-20200331093820104](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200331093820104.png)

```js

import React, { useState } from "react";

export default function  Button()  {
    //buttonText是变量 指向当前的状态值
    // setButtonText 是一个函数  
  const  [buttonText, setButtonText] =  useState("Click me,   please");

  function handleClick()  {
    return setButtonText("Thanks, been clicked!");
  }

  return  <button  onClick={handleClick}>{buttonText}</button>;
}
```

`

useState()`这个函数接受状态的初始值，作为参数，上例的初始值为按钮的文字。该函数返回一个数组，数组的第一个成员是一个变量（上例是`buttonText`），指向状态的当前值。第二个成员是一个函数，用来更新状态，约定是`set`前缀加上状态的变量名（上例是`setButtonText`）。

## useContext()：共享状态钩子

如果需要在组件之间共享状态，可以使用`useContext()`。

```js
 const { username } = useContext(AppContext)
```

现在有两个组件 Navbar 和 Messages，我们希望它们之间共享状态。

> ```markup
> <div className="App">
>   <Navbar/>
>   <Messages/>
> </div>
> ```

第一步就是使用 React Context API，在组件外部建立一个 Context。

> ```javascript
> const AppContext = React.createContext({});
> ```

组件封装代码如下。

> ```markup
> <AppContext.Provider value={{
>   username: 'superawesome'
> }}>
>   <div className="App">
>     <Navbar/>
>     <Messages/>
>   </div>
> </AppContext.Provider>
> ```

上面代码中，`AppContext.Provider`提供了一个 Context 对象，这个对象可以被子组件共享。

Navbar 组件的代码如下。

> ```javascript
> const Navbar = () => {
>   const { username } = useContext(AppContext);
>   return (
>     <div className="navbar">
>       <p>AwesomeSite</p>
>       <p>{username}</p>
>     </div>
>   );
> }
> ```

Message 组件的代码也类似。

> ```javascript
> const Messages = () => {
>   const { username } = useContext(AppContext)
> 
>   return (
>     <div className="messages">
>       <h1>Messages</h1>
>       <p>1 message for {username}</p>
>       <p className="message">useContext is awesome!</p>
>     </div>
>   )
> }
> ```

## useReducer()：action 钩子

React 本身不提供状态管理功能，通常需要使用外部库。这方面最常用的库是 Redux。

Redux 的核心概念是，组件发出 action 与状态管理器通信。状态管理器收到 action 以后，使用 Reducer 函数算出新的状态，Reducer 函数的形式是`(state, action) => newState`。

`useReducers()`钩子用来引入 Reducer 功能。

> ```javascript
> const [state, dispatch] = useReducer(reducer, initialState);
> ```

上面是`useReducer()`的基本用法，它接受 Reducer 函数和状态的初始值作为参数，返回一个数组。数组的第一个成员是状态的当前值，第二个成员是发送 action 的`dispatch`函数。

下面是一个计数器的例子。用于计算状态的 Reducer 函数如下。

> ```javascript
> const myReducer = (state, action) => {
>   switch(action.type)  {
>     case('countUp'):
>       return  {
>         ...state,
>         count: state.count + 1
>       }
>     default:
>       return  state;
>   }
> }
> ```

组件代码如下。

> ```javascript
> function App() {
>   const [state, dispatch] = useReducer(myReducer, { count:   0 });
>   return  (
>     <div className="App">
>       <button onClick={() => dispatch({ type: 'countUp' })}>
>         +1
>       </button>
>       <p>Count: {state.count}</p>
>     </div>
>   );
> }
> ```

## useEffect()：副作用钩子

```text
import React, { useState, useEffect } from 'react'
```

`useEffect()`用来引入具有副作用的操作，最常见的就是向服务器请求数据。以前，放在`componentDidMount`里面的代码，现在可以放在`useEffect()`。

你可以把 `useEffect` 看做 `componentDidMount` ， `componentDidUpdate` 和 `componentWillUnmount` 这三个函数的组合。

### 根据某个状态是否变化来决定要不要重新执行：

```js
const [value, setValue] = useState<string>('I never change')
useEffect(() => {
  switchCount += 1
}, [value])
```

因为 `value` 我们不会去任何地方改变它的值，所以在末尾加了 `[value]` 后， `useEffect` 内的逻辑也只会执行第一次，相当于在 class 组件中执行了 `componentDidMount` ，后续的 `shouldComponentUpdate` 返回全部是 `false` 。

### 组件卸载时处理一些内存问题，比如清除定时器、清除事件监听：

```js
useEffect(() => {
  const handler = () => {
    document.title = Math.random().toString()
  }

  window.addEventListener('resize', handler)

  return () => {
    window.removeEventListener('resize', handler)
  }
}, [])
```





