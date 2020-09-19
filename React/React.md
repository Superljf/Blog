 

### NPM 命令

1. 1、create-react-app demo  
   2、cnpm init 

2. cnpm install webpack --save-dev

3. npm uninstall webpack-cli

4. cnpm add antd

5. cnpm install --save react-router-dom

6. cnpm i -D react-router react-router-dom

7. npm  add babel-plugin-import --save-dev 
   npm  add antd --save-dev	

   使用dva脚手架构建

8. cnpm i dva-cli -g 

9. dva -v 

10. dva new dva_test

11. npm add redux -saga

12. 

web


```js
  // 监听浏览器点击返回
  if (window.history && window.history.pushState) {
    history.pushState(null, null, document.URL);
    window.addEventListener('popstate', this.handleBack, false);
  }
  
  // 页面销毁取消监听 
  componentWillUnmount () {
    window.removeEventListener('popstate', this.handleBack, false);
  };

```

routes 主要放路由中配置的组件 

components 通用的组件

<img src="C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20191210145455465.png" alt="image-20191210145455465" style="zoom:50%;" />

### Dva

#### 父组件子组件传值

```js
父组件
componentDidMount() {
    this.refs.myTxt.setTxt('报名详情')
  }
  render() {
    return (
      <div>
        <BackDetail ref="myTxt" />
        <div className={styles.main}>
```

```js
子组件
this.state = { 
      txtDetail: "报名详情",
     };
  }
  setTxt = (value) => {
    this.setState({
      txtDetail: value
    })
  }
  render() {
    return (
      <div className={styles.header}>
        <Button size="small" className={styles.btn}>返回</Button>
        <sapn className={styles.txt}>{this.state.txtDetail}</sapn>
```

#### Ref

```js
constructor(props) {
  super(props);
  // 创建ref容器 并保存到组件对象
  this.myRef = React.createRef();
}


// 将容器交给需要标记的标签对象 在解析时会自动将标签对象保存到容器中(属性名： current, 属性值标签： )
<Comp ref={this.myRef} />



 // 收集上传的图片文件路径数组
 const imgs = this.myRef.current.getImgs()
  console.log(imgs)
```



Effects

#### [#](https://dvajs.com/knowledgemap/#put)put

用于触发 action 。

```javascript
yield put({ type: 'todos/add', payload: 'Learn Dva' });
```

#### [#](https://dvajs.com/knowledgemap/#call)call

用于调用异步逻辑，支持 promise 。

```javascript
const result = yield call(fetch, '/todos');
```

#### [#](https://dvajs.com/knowledgemap/#select)select

用于从 state 里获取数据。

```javascript
const todos = yield select(state => state.todos);
```

<img src="C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20191217094939199.png" alt="image-20191217094939199" style="zoom:50%;" />

```js
" Middleware is some code you can put between the framework receiving a request, and the framework generating a response. "
```

<img src="https://gw.alipayobjects.com/zos/rmsportal/YiBKIHevTMjvpIAodsOq.png" alt="img" style="zoom:50%;" />

<img src="https://gw.alipayobjects.com/zos/rmsportal/ZSCxeNAFqHgKXsyjtpxt.png" alt="img" style="zoom:200%;" />

#### Ant Design Pro  

######  npm create umi

+ npm install
+ npm start

###### WithRouter

```
高阶组件中的`withRouter`, 作用是将一个组件包裹进`Route`里面, 然后`react-router`的三个对象`history, location, match`就会被放进这个组件的`props`属性中.

使用<react-router></react-router>

withRouter():包装非路由组件 给其传入history、location/match属性
history:push()/replace()/goBack()
location: pathname属性
match: params属性


```

### 动态菜单路由

```js
// 动态显示路由菜单*

*// 根据指定menu 数据数组生成和的数组*
getMenuNodes = (menuList) => {
 *return* menuList.map(item => {
  *if* (item.children) {
   *return*
​    <Menu.Item={item.key}>
​    <Link *to*={item.key}>
​    <Icon *type*={item.icon}/>
​    <span>{item.title}</span>
​    </Link>
   </Menu.Item>
  } 
  *return* ( *//有下一级菜单
   <SubMeun>
   </SubMeun>
  )
 })
}

*// reduce 方式*2
getMenuNodes2 = (menuList) => {
 *// const array1 = [1, 2, 3, 4];*
 *// const total = array1.reduce()*
 *return* menuList.reduce((pre, item) => {
  *//* 
  *if* (!item.children) {
   pre.push(
​    <Menu.Item={item.key}>
​    <Link *to*={item.key}>
​    <Icon *type*={item.icon}/>
​    <span>{item.title}</span>
​    </Link>
   </Menu.Item>
   )
  } *else* {
   pre.push {
​    <SubMeun>
​     <Menu.item={item.key}/>
​    </SubMeun>
   }
  }
 }
 )
}


```

### Function1前台登录表单验证

###### Async/await 

-  async /*await* 的理解和使用

   理解： 

    简化promice对象的使用 不再使用then()来指定回调函数

    能同步编码方式实现异步流程

   使用： 

    哪里使用await 

  - 在返回promise对象的表达式左侧： 左侧得到的不再是

    promise 而是promise异步成功的值

    哪里使用async

  -  *await* 所在最近函数定义的左侧 

###### 高阶组件

```js
 /*理解Form组件
  高阶函数： 
    定义： 接收的参数是函数或者返回值是函数
    实现一个更加强大 动态的功能
   *高阶组件：
      本质是一个函数
      函数接收一个组件 返回一个新的组件
      Form.create()返回的就是一个高阶组件
   
   */
  const WrapperForm = Form.create()(Login)

  export default WrapperForm
```



### 登录表单事件处理

```js
  handleSubmit = e => {
// 方法是一个特别的属性
// 属性值是一个函数
// 阻止事件的默认行为 阻止表单的提交

  e.preventDefault()
   // 对表单所有的字段进行验证
  this.props.form.validateFields(async (err, { username, password }) => {
    if (!err) {
      const result = await reqLogin(username, password)
      /**
       * async await 的理解和使用
       * 理解： 
       *  简化promise 对象的使用 不再使用then()来指定回调函数
       *  能同步编码方式实现异步流程  
       * 使用 哪里使用async 哪里使用await
       *  
       * 
       */
      if (result.status === 0) {
        this.props.history.replace()
        // 将user信息保存到local 
        const user = result.data
        localStorage.setItem('user_key', JSON.stringify(user))
      } else {
        MessageChannel.error()
      }
    } else {

    }
  })

  }
  
```



### 读取保存的user数据 如果数据不存在 直接跳转到登录页面

```
 // 读取保存的user 如果不存在  直接跳转到登录界面
   const user = JSON.parse(localStorage.getItem('user_key')|| '{}')
   if (!user._id) {
      // this.props.history.replace('/login')
      return <Redirect to="/login"/>  //自动跳转到指定的路径

   }
```



###### 封装LocalStorage方法

```js
// 操作local数据的工具函数模块

export default {
  saveUser(user) {
    localStorage.setItem('user_key', JSON.stringify(user))
  },

  // 返回一个user 对象  如果没有返回一个{}
  getUser() {
    return JSON.parse(localStorage.getItem('user_key') || '{}')
  },

  removeUser() {
    localStorage.removeItem('user_key')
  },
}


```

### 拼接url

```js
${idCardNo}&validateUrl&url=${url}`;
```

### 定时器

```js

// 动态显示时间
componentDidMount() {
  // 启动循环定时器
 this.setIntervalId = setinterval(() => {
   this.setState({
      currentTime: FormData(Date.now())
   })
 }, 1000);
//  发送jsonp方式
 this.getWeather()
};
componentWillMount() {
  clearInterval(this.setIntervalId)
}
```

### {...props}

```js
return <button {...props}>  </button>
  // {...props}将接收的所有属性传给子标签
```

### **Fuction2获取分类列表页面** 

- 写出静态页面
- 向接口发送请求
- 传入数据进行显示

```js
// 获取分类列表
export const reqCategorys = () => ajax.get(BASE + '/manage/category/list') 

```



###### 在同一组件存储接口的数据并取出

```js
  state = {
    categorys: [], // 所有分类的数组
     loading: false,
      // 自定义状态显示 显示隐藏 
     showStatus: 0, // 0: 不显示 1：显示添加 2：显示修改
  }
  render() {

    // 取出状态数据
    const { categorys } = this.state.categorys
```

###### 数据渲染放置问题

```js

initColumns = () => {
    this.colums = [
        // 数据
    ]
  }
  // 挂载代码不放全代码
  componentDidMount() {
    this.initColumns()
  }
  // 列表渲染
  <span>{this.colums}</span>
```

###### 异步获取分类列表显示

```js
 // 异步获取分类列表显示
  getCategorys = async () => {
    // 发异步ajax请求
    const result =  await reqCategorys()
    if (result.status === 0) {
      // 成功 取出分类列表
      const categorys = result.data
      // 更新状态category 数据
      this.setState({
        categorys
      })
    } else {
      MessageChannel.error('获取失败')
    }
  }
```

#### 添加-更新分类

###### API

```
// 添加分类 
export const reqAddCategory = ({categoryName, categoryId}) => ajax.post(BASE + '', {
    categoryName,
    categoryId,
})

```



###### 三元运算符

```js
title={ showStatus === 1 ? "添加分类" : "修改分类" }
```

###### 代码顺序 

+ state {}

+ 自定义方法 function() {}

+ 生命周期函数 

###### 点击事件绑定函数处理 只有点击时触发 

控制模态框的 显示隐藏

```js
 <Button onClick={() => { this.setState({showStatus: 1}) }}>
```

###### Protypes 声明接收的属性值（父子组件传值进行验证）

###### 修改分类

```js

//子组件
  componentWillMount () {
    // 将当前子组件中的form对象的值传入父组件中的setForm
    this.props.setForm(this.props.form)
  }

  render() {

    const { getFieldDecorator } = this.props.form

   // 父组件得到form对象的值后可进行表单验证
 {/* 将子组件传递的form 对象保存到当前组件的对象 */}
      <AddUpdateForm setForm={form => this.form = form} />
      

//或子组件中声明  
 static proTypes = {
    setForm: this.proTypes.func.isRequired,
     cateforyName: PropTypes.string,
  }

```

###### 添加分类 handleOk（）

```js
import React, { Component } from 'react'
import {

}
import { reqCategorys } from '../../services/api'
const columns = [
  {
    title: '分类的名称',
    dataIndex: 'name',
  },
  {
    title: '操作',
    render: () => <LinkButton>修改分类</LinkButton>
  },
]
export default class category extends Component {
  state = {
    categorys: [], // 所有分类的数组
    loading: false,
    showStatus: 0, // 0: 不显示 1：显示添加 2：显示修改
  }

  // 初始化table 所有列信息数组
  initColumns = () => {

  }
  getCategorys = async () => {
    const result = await reqCategorys ()
    if (result === 0 ) {
      // 取出分类列表
      const categoeys = result.data
      // 更新状态数据
      this.setState({
        categorys
      })
    }
  }
  handleOk = async () => {
    // 进行表单验证
    this.form.validateFields(async (err, value) => {
      if (!err) {
        // 重置输入数据
        this.form.resetFields;
        // 验证通过后 得到输入数据
          const { categoryName } = values
          let result 
        if (showStatus === 1) {  
          //  发添加分类的请求
        const result = await reqAddCategory(categoryName)
        } else { 
          // 修改
          this.categoeys = this.category._id
          const result = await reqUpdateCategory({categoryName, categoryId}) 
        }
        this.setState({ showStatus: 0 })
        // 根据响应结果 做不同处理
          const action = showStatus === 1 ? '添加' : '修改'
        if (result.status === 0) {
          // 重新获取分类列表显示
          this.getCategorys()
          MessageChannel.success( action + '分类成功')
        } else {
          MessageChannel.error(action + '分类失败')
        }
      }
    })
  handleCancel = () => {
    // 重置数据
    this.form.resetFields;
    this.setState({
      showStatus: 0
    })
  }
}
  componentWillMount() {
    this.initColumns()
  }
  componentDidMount() {
    this.getCategorys()
  }

  render() {
    const { categorys } = this.state

    // Card 右上角的结构
    const extra = (
      <Button type="primary" onClick={ this.setState({showStatus : 1}) }>
        <Icon type="plus">

        </Icon>
      </Button>
    )
    return (
      <Card title="Default size card" extra={extra} style={{ width: 300 }}>
        <Table>
          bordered={true}
          rowKey="_id"
          columns={this.columns}
          dataSource={data}
          pagination={{ defaultPageSize: 2, showQuickJumper: true }}
        </Table>

        <Modal>
          title={ showStatus === 1 ? "添加分类" : "修改分类" }
          visible={}
          onOk={this.handleOk}
          onCancel={this.handleCancel}
        </Modal>
    </Card>
    )
  }
}
```

### 前台分页

### 后台分页

##### 获取接口数据

```
// 获取商品分页列表
export const reqProducts = (pageNum, pageSize) => ajax(BASE + '/mannage/product/list', {
    params: { // 包含所有query 参数对象
        pageNum,
        pageSize,
    }
})
```

##### 添加响应拦截器  添加请求拦截器

```js
// 封装能发ajax 请求的函数
import axios from 'axios';
// 添加请求拦截器 让post 请求的请求格式为urlcodeed格式 a=1&b2
// 在真正发请求前 
axios.interceptors.request.use(function (config) {
  //得到请求方式和请求体数据 
  const { method, data } = config;
  // 处理post请求 将data对象转换成query参数格式字符串
  if (method.toLowerCase() === 'post' && typeof data === 'object') {
    config.data = qs.stringfy(data)
  }

  return config;
});

// 添加响应的拦截器
// 接收到响应后的一些操作 例如服务器返回登录状态失效  
// 需要重新登录的时候 跳到登录页  
axios.interceptors.response.use(fuction(response) {

  return response;

}, function (error) {
  // 对响应错误做点什么
  return Promise.reject(error);
})
export default axios;

```

##### 在Http.js中封装axios拦截器 Vue

```js
import axios from 'axios' //引入axios组件
import router from '../router'; //引入vue-router组件
import url from './serviceAPI.config' //引入serviceAPI接口

// request拦截器：对请求参数做监听和处理
axios.interceptors.request.use(

    config => {
        //从session storage中获取token
        let token = sessionStorage.getItem("token"); 
        //在每一个接口的请求头上增加一个token
        if (config.url == url.URL.login[0].loginOn) {
        } else {
   
            config.headers = {
                'Authorization': token
            }
        }
        return config;
    },
    error => {//请求错误处理
        return Promise.reject(error.response);
    }
);

// 添加response响应拦截器
axios.interceptors.response.use(function (response) {
    // console.log(response.headers.authorization);
    //如果token值发生改变的时候，替换token值
    if (response.headers.authorization) {
        sessionStorage.setItem("token", response.headers.authorization);
    }
    
    // 对响应数据做点什么
    return response;
}, function (error) {
    // 响应头发生错误发生的操作
    if (error.response.status) {
        switch (error.response.status) {
            // 在登录成功后返回当前页面，这一步需要在登录页操作。                
            // 401 token过期                
            // 登录过期对用户进行提示                
            // 清除本地token和清空sessionStorage的             
            // // 跳转登录页面                
            case 401:
                // 清除token                    
                localStorage.removeItem('token');
                // this.$message.error="token已过期";
                // store.commit('loginSuccess', null);                    
                // 跳转登录页面，并将要浏览的页面fullPath传过去，登录成功后跳转需要访问的页面
                router.replace({
                    path: '/login',
                    query: {
                        redirect: router.currentRoute.fullPath
                    }
                });
                this.$message.error("登入已经过期")

                break;
            // 404请求不存在                /*  */
            case 403:  
                Toast({
                    message: '没有当前操作的权限',
                    duration: 1500,
                    forbidClick: true
                });
                
                // 跳转登录页面，并将要浏览的页面fullPath传过去，登录成功后跳转需要访问的页面
                setTimeout(() => {
                    router.replace({
                        path: '/',
                        query: {
                            redirect: router.currentRoute.fullPath
                        }
                    });
                }, 1000);
                break;
            case 400:
                Toast({
                    message: '参数错误',
                    duration: 1500,
                    forbidClick: true
                });
                // localStorage.removeItem('token');                    
                // store.commit('loginSuccess', null);                    
                // 跳转登录页面，并将要浏览的页面fullPath传过去，登录成功后跳转需要访问的页面
                setTimeout(() => {
                    router.replace({
                        path: '/',
                        query: {
                            redirect: router.currentRoute.fullPath
                        }
                    });
                }, 1000);
                break;
            // 其他错误，直接抛出错误提示                
            default:
        }
        return Promise.reject(error.response);
    }
});
export default axios;
```

###### 封装axios的get方法



```js
export function get(url,params) {
    return new Promise( (resolve,reject)=>{
        axios.get( url, {
           params:params
        } ).then( res => {
            resolve(res.data);
        }).catch( err => {
            reject(err.data);
        })
    } )
   }
```

###### 封装axios的post方法

```js
/*
 *axios:post方法封装
 *@param {string} url [请求接口的地址]
 * @param {object} params [请求时携带的参数]
 * QS.stringify(params) 序列化请求时携带的参数
 * 
*/ 
export function post (url,params){
    return new Promise( (resolve,reject) =>{
        axios.post( url, QS.stringify(params) )
        .then( res => {
            resolve(res.data);
        } )
        .catch( err => {
            reject(err.data)
        } )
    } );
}
```

#####  利用两个'！!'运算符

第一个'!'将值转换成布尔值并取其值的非值，第二个'!'将其布尔值还原，类似于“负负得正”的道理。

```
// 将一个数据强制转换成对应的布尔值
    this.isUpadate = !!product._id
```

##### map方法 获取所有已上传图片文件名的数组

```js
  getImgs = () => this.state.fileList.map(file => file.name)
```

### 富文本编辑器

#### 角色管理

#### 用户管理

### React Hooks

两个常见的api 

useState 

useEffect 















