### 启动第一个服务

```js
  var http = require('http');
  var server = http.createServer()
  server.on('request', function () {
    console.log('收到客户端的请求')
  })

  server.listen(3000, function () {
    console.log('服务启动')
  })
```

### 服务启动实例1

```java
app.js
   // 导入 http 内置模块
const http = require('http')
// 这个核心模块，能够帮我们解析 URL地址，从而拿到  pathname  query 
const urlModule = require('url')

// 创建一个 http 服务器
const server = http.createServer()
// 监听 http 服务器的 request 请求
server.on('request', function (req, res) {

  // const url = req.url
  const { pathname: url, query } = urlModule.parse(req.url, true)

  if (url === '/getscript') {
    // 拼接一个合法的JS脚本，这里拼接的是一个方法的调用
    // var scriptStr = 'show()'

    var data = {
      name: 'xjj',
      age: 18,
      gender: '女孩子'
    }

    var scriptStr = `${query.callback}(${JSON.stringify(data)})`
    // res.end 发送给 客户端， 客户端去把 这个 字符串，当作JS代码去解析执行
    res.end(scriptStr)
  } else {
    res.end('404')
  }
})

// 指定端口号并启动服务器监听
server.listen(3008, function () {
  console.log('server listen at http://127.0.0.1:3008', '服务启动了')
}) 
```

```js
客户端JSONP页面
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>

<body>
  <script>
    function showInfo123(data) {
      console.log(data) 
    }
  </script>

<script src="http://127.0.0.1:3008/getscript?callback=showInfo123">
</script>
</body>
</html>
```

### 服务启动实例2

```js
var http = require('http')
// 1. 创建 Server
var server = http.createServer()
// 2. 监听 request 请求事件，设置请求处理函数
server.on('request', function (req, res) {
  console.log('收到请求了，请求路径是：' + req.url)
  console.log('请求我的客户端的地址是：', req.socket.remoteAddress, req.socket.remotePort)
  var url = req.url
  
  if (url === '/') {
    res.end('index page')
  } else if (url === '/login') {
    res.end('login page')
  } else if (url === '/products') {
    var products = [{
        name: '苹果 X',
        price: 8888
      },
      {
        name: '菠萝 X',
        price: 5000
      },
      {
        name: '小辣椒 X',
        price: 1999
      }
    ]
    res.end(JSON.stringify(products))
  } else {
    res.end('404 Not Found.')
  }
})

// 3. 绑定端口号，启动服务
server.listen(3000, function () {
  console.log('服务器启动成功，可以访问了。。。')
})

```

#### node获取机器信息

```js
// 用来获取机器信息的
var os = require('os')

// 用来操作路径的
var path = require('path')
```

#### node.js模块化

```

*// require 是一个方法*

*// 它的作用就是用来加载模块的*

*// 在 Node 中，模块有三种：*

*//  具名的核心模块，例如 fs、http*

*//  用户自己编写的文件模块*

*//   相对路径必须加 ./*

*//   可以省略后缀名*

*//   相对路径中的 ./ 不能省略，否则报错*

*//  在 Node 中，没有全局作用域，只有模块作用域*

*//   外部访问不到内部*

*//   内部也访问不到外部*

*//   默认都是封闭的*

*//  既然是模块作用域，那如何让模块与模块之间进行通信*

*//  有时候，我们加载文件模块的目的不是为了简简单单的执行里面的代码，更重要是为了使用里面的某个成员
```

#### 响应头类型Content-type

```js
// require
// 端口号

var http = require('http')

var server = http.createServer()

server.on('request', function (req, res) {
  // 在服务端默认发送的数据，其实是 utf8 编码的内容
  // 但是浏览器不知道你是 utf8 编码的内容
  // 浏览器在不知道服务器响应内容的编码的情况下会按照当前操作系统的默认编码去解析
  // 中文操作系统默认是 gbk
  // 解决方法就是正确的告诉浏览器我给你发送的内容是什么编码的
  // 在 http 协议中，Content-Type 就是用来告知对方我给你发送的数据内容是什么类型
  // res.setHeader('Content-Type', 'text/plain; charset=utf-8')
  // res.end('hello 世界')

  var url = req.url

  if (url === '/plain') {
    // text/plain 就是普通文本
    res.setHeader('Content-Type', 'text/plain; charset=utf-8')
    res.end('hello 世界')
  } else if (url === '/html') {
    // 如果你发送的是 html 格式的字符串，则也要告诉浏览器我给你发送是 text/html 格式的内容
    res.setHeader('Content-Type', 'text/html; charset=utf-8')
    res.end('<p>hello html <a href="">点我</a></p>')
  }
})

server.listen(3000, function () {
  console.log('Server is running...')
})

```

#### 服务端渲染和客户端渲染

![image-20200330172422546](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200330172422546.png)

![image-20200330172509018](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200330172509018.png)

#### 模块化

![image-20200331094820284](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200331094820284.png)

- 优先从缓存中加载



#### 使用模板引擎

```
npm install art-template --save
```

```css
var express = require（'express'）; 
var app = express（）;

//查看引擎设置
 app.engine（'art'，require（'express-art-template'））; 
app.set（'view'，{ 
    调试：process.env.NODE_ENV！== 'production'
 }）; 
app.set（'views'，path.join（__ dirname，'views'））; 
app.set（'view engine'，'art'）;

//路由
 app.get（'/'，function（req，res） { 
    res.render（'index.art'，{ 
        用户：{ 
            名称：'aui'，
            标签：[ 'art'，'template'，' nodejs' ] 
        } 
    }）; 
}）;
```

response.render方法用于渲染网页模板。

```javascript
app.get("/", function(request, response) {
  response.render("index", { message: "Hello World" });
});
```

## Express

接下来在 `myapp` 目录下安装 Express 并将其保存到依赖列表中。如下：

```sh
$ cnpm install express --save
```

如果只是临时安装 Express，不想将它添加到依赖列表中，可执行如下命令：

```sh
$ cnpm install express --no-save
```

```js
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => res.send('Hello World!'))

app.listen(port, () => console.log(`Example app listening on port ${port}!`))
```

#### 应用程序生成器

```js
$ npx express-generator
```

#### 基本路由

*路由*是指确定应用程序如何响应客户端对特定端点的请求，该特定端点是URI（或路径）和特定的HTTP请求方法（GET，POST等）。

每个路由可以具有一个或多个处理程序函数，这些函数在路由匹配时执行。

路由定义采用以下结构：

```javascript
app.METHOD(PATH, HANDLER)
```

- `app`是的实例`express`。
- `METHOD`是小写的[HTTP请求方法](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods)。
- `PATH` 是服务器上的路径。
- `HANDLER` 是当路由匹配时执行的函数。

```javascript
app.get('/', function (req, res) {
  res.send('Hello World!')
})
```

在根路由（`/`）（应用程序的主页）上响应POST请求：

```javascript
app.post('/', function (req, res) {
  res.send('Got a POST request')
})
```

响应对`/user`路由的PUT请求：

```javascript
app.put('/user', function (req, res) {
  res.send('Got a PUT request at /user')
})
```

#### 托管静态文件express.static 

例如，通过如下代码就可以将 `public` 目录下的图片、CSS 文件、JavaScript 文件对外开放访问了：

```javascript
app.use(express.static('public'))
```

```

当以 /public/ 开头的时候，去 ./public/ 目录中找找对应的资源
这种方式更容易辨识，推荐这种方式
app.use('/public/', express.static('./public/'))

必须是 /a/puiblic目录中的资源具体路径
app.use('/abc/d/', express.static('./public/'))

当省略第一个参数的时候，则可以通过 省略 /public 的方式来访问
这种方式的好处就是可以省略 /public/
app.use(express.static('./public/'))
```

现在，你就可以访问 `public` 目录中的所有文件了：

```plain-text
http://localhost:3000/images/kitten.jpg
http://localhost:3000/css/style.css
http://localhost:3000/js/app.js
http://localhost:3000/images/bg.png
http://localhost:3000/hello.html

```

如果要使用多个静态资源目录，请多次调用 `express.static` 中间件函数：

```javascript
app.use(express.static('public'))
app.use(express.static('files'))
```

#### 使用nodemon

```
cnpm install -g nodemon
1
```

#### 安装成功检查版本

```
nodemon --version
nodemon app.js
```

#### 路由

*路由*是指应用程序的端点（URI）如何响应客户端请求。

应用程序“侦听”与指定的路由和方法匹配的请求，并且当它检测到匹配项时，它将调用指定的回调函数。

```javascript
var express = require('express')
var app = express()

// respond with "hello world" when a GET request is made to the homepage
app.get('/', function (req, res) {
  res.send('hello world')
})
```

有一种特殊的路由方法，`app.all()`用于为*所有* HTTP请求方法的路径加载中间件功能。例如，无论是使用GET，POST，PUT，DELETE还是[http模块](https://nodejs.org/api/http.html#http_http_methods)支持的任何其他HTTP请求方法，都会对路由“ / secret”的请求执行以下处理程序。

```javascript
app.all('/secret', function (req, res, next) {
  console.log('Accessing the secret section ...')
  next() // pass control to the next handler
})
```

##### 路由转义

```
如果您需要$在路径字符串中使用美元字符（），请将其转义为([和])。例如，“ /data/$book” 处用于请求的路径字符串将为“ /data/([\$])book”。
```

##### 路线参数

路由参数被命名为URL段，用于捕获URL中在其位置处指定的值。捕获的值将填充到`req.params`对象中，并将路径中指定的route参数的名称作为其各自的键。

```
Route path: /users/:userId/books/:bookId
Request URL: http://localhost:3000/users/34/books/8989
req.params: { "userId": "34", "bookId": "8989" }
```

要使用路由参数定义路由，只需在路由路径中指定路由参数，如下所示。

```javascript
app.get('/users/:userId/books/:bookId', function (req, res) {
  res.send(req.params)
})
http://localhost:8087/users/34/books/8989
```

##### 多个回调函数 路线处理程序

您可以提供行为类似于[中间件的](https://www.expressjs.com.cn/en/guide/using-middleware.html)多个回调函数来处理请求。唯一的例外是这些回调可能会调用`next('route')`以绕过其余的路由回调。您可以使用此机制在路由上施加先决条件，然后在没有理由继续使用当前路由的情况下将控制权传递给后续路由。

```js
app.get('/example/b', function (req, res, next) {
  console.log('the response will be sent by the next function ...')
  next()
}, function (req, res) {
  res.send('Hello from B!')
})
```

#### 编写用于Express应用程序的中间件

*中间件*功能是可以访问[请求对象](https://www.expressjs.com.cn/en/4x/api.html#req) （`req`），[响应对象](https://www.expressjs.com.cn/en/4x/api.html#res)（`res`）和`next`应用程序的请求-响应周期中的功能的功能。该`next`功能是Express路由器中的功能，当调用该功能时，将在当前中间件之后执行中间件。

中间件功能可以执行以下任务：

- 执行任何代码。
- 更改请求和响应对象。
- 结束请求-响应周期。
- 调用堆栈中的下一个中间件。

要加载中间件功能，请调用`app.use()`，指定中间件功能

```javascript
var express = require('express')
var app = express()

var myLogger = function (req, res, next) {
  console.log('LOGGED')
  next()
}

app.use(myLogger)

app.get('/', function (req, res) {
  res.send('Hello World!')
})

app.listen(3000)
```

```js

var requestTime = function (req, res, next) {
  req.requestTime = Date.now()
  next()
}

app.use(requestTime)

app.get('/', function (req, res) {
  var responseText = 'Hello World'
  responseText += 'ss' + req.requestTime
  res.send(responseText)
  console.log(responseText)
})
```

##### 使用中间件

##### 应用层中间件

##### 路由器级中间件

路由器级中间件与应用程序级中间件的工作方式相同，只不过它绑定到的实例`express.Router()`。

```javascript
var router = express.Router()
```

使用`router.use()`和`router.METHOD()`函数加载路由器级中间件。

##### 错误处理中间件

```javascript
app.use(function (err, req, res, next) {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})
```

##### 第三方中间件

使用第三方中间件向Express应用程序添加功能。

安装Node.js模块以获得所需的功能，然后在应用程序级别或路由器级别将其加载到您的应用程序中。

以下示例说明了如何安装和加载cookie解析中间件功能`cookie-parser`。

```sh
$ npm install cookie-parser
var express = require('express')
var app = express()
var cookieParser = require('cookie-parser')

// load the cookie-parsing middleware
app.use(cookieParser())
```

##### body-parse

body-parser是一个HTTP`请求体解析中间件`，使用这个模块可以解析JSON、Raw、文本、URL-encoded格式的请求体，Express框架中就是使用这个模块做为请求体解析中间件。

```css
1. bodyParser.json(options): 解析json数据
2. bodyParser.raw(options): 解析二进制格式(Buffer流数据)
3. bodyParser.text(options): 解析文本数据
4. bodyParser.urlencoded(options): 解析UTF-8的编码的数据。
```

bodyParser 解析json数据

```jsx
var bodyParser = require('body-parser')
```

```css
var express = require('express')
var bodyParser = require('body-parser')
 
var app = express()
 
// parse application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: false }))
 
// parse application/json
app.use(bodyParser.json())
 
app.use(function (req, res) {
  res.setHeader('Content-Type', 'text/plain')
  res.write('you posted:\n')
  res.end(JSON.stringify(req.body, null, 2))
})
```

#### __dirname   __filename

```js
app.use('/tour/auth', require(__dirname + '/module/auth'));

app.use('/tour/user', require(__dirname + '/module/user'));
```



#### MongoDB 

```
$ cnpm install mongodb
```

```js
## 创建连接

var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/runoob";
 
MongoClient.connect(url, { useNewUrlParser: true }, function(err, db) {
  if (err) throw err;
  console.log("数据库已创建!");
  db.close();
});
```



#### mySql

```
cnpm install mysql
```

```css
mysql -u root -p
#接着输入你的密码
解决：
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '123456';
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123456';
SELECT plugin FROM mysql.user WHERE User = 'root';

```

```js
var mysql      = require('mysql');
var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'root',
  password : '123456',
  database : 'test'
});
 
connection.connect();
 
var  sql = 'SELECT * FROM websites';
//查
connection.query(sql,function (err, result) {
        if(err){
          console.log('[SELECT ERROR] - ',err.message);
          return;
        }
 
       console.log('--------------------------SELECT----------------------------');
       console.log(result);
       console.log('------------------------------------------------------------\n\n');  
});


var  addSql = 'INSERT INTO websites(Id,name,url,alexa,country) VALUES(0,?,?,?,?)';
var  addSqlParams = ['菜鸟工具', 'https://c.runoob.com','23453', 'CN'];
//增
connection.query(addSql,addSqlParams,function (err, result) {
        if(err){
         console.log('[INSERT ERROR] - ',err.message);
         return;
        }        
 
       console.log('--------------------------INSERT----------------------------');
       //console.log('INSERT ID:',result.insertId);        
       console.log('INSERT ID:',result);        
       console.log('-----------------------------------------------------------------\n\n');  
});


var modSql = 'UPDATE websites SET name = ?,url = ? WHERE Id = ?';
var modSqlParams = ['菜鸟移动站', 'https://m.runoob.com',6];
//改
connection.query(modSql,modSqlParams,function (err, result) {
   if(err){
         console.log('[UPDATE ERROR] - ',err.message);
         return;
   }        
  console.log('--------------------------UPDATE----------------------------');
  console.log('UPDATE affectedRows',result.affectedRows);
  console.log('-----------------------------------------------------------------\n\n');
});



var delSql = 'DELETE FROM websites where id=6';
//删
connection.query(delSql,function (err, result) {
        if(err){
          console.log('[DELETE ERROR] - ',err.message);
          return;
        }        
 
       console.log('--------------------------DELETE----------------------------');
       console.log('DELETE affectedRows',result.affectedRows);
       console.log('-----------------------------------------------------------------\n\n');  
});
```



#### 实例

##### 登录

```js
/**
 * 登录
 */
router.post('/loginForm', async (req, res) => {
	const md5 = crypto.createHash('md5');
	const loginMsg = req.body;
	const phone = loginMsg.phone;
	const pwd = md5.update(loginMsg.pwd).digest('hex');

	try {
		const result = await db('select id from tour_user where user_phone="' + phone + '" and user_pwd="' + pwd + '"');
		const [item] = result;
		if (!item) res.json({ code: -1, data: null, message: '用户不存在或密码错误' });
		else res.json({ code: 0, data: item.id, message: '' });
	} catch (err) {
		res.json({ code: -1, data: null, message: '登录失败，请重新操作' });
	}
});

```

vue请求接口  

```js
   login(this.phone, this.pwd)
      .then(res => {
        const { code, data, message } = res.data;
        if (code === 0) {
          window.sessionStorage.uid = data;
          this.$router.back();
        } else {
          this.$dialog.alert({ message });
        }
      })
      .catch(error => {
        this.$dialog.alert({ message: "登录失败" });
      });
```

##### 连接MySql

```js
const mysql = require('mysql');

const db = mysql.createConnection({
	host: '127.0.0.1',
	user: 'root',
	password: '123456',
	database: 'test'
});
db.connect();

module.exports = (sql, callback) => {
	return new Promise((resolve, reject) => {
		db.query(sql, (err, data) => {
			if (err) reject(err);
			else resolve(data);
		});
	});
};
```

