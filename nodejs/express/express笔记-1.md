# Express基本使用

## 路由

定义简单路由。

`Hello World!`在主页回复：

```javascript
app.get('/', function (req, res) {
  res.send('Hello World!')
})
```

响应`/`应用程序主页根路由 ( ) 上的 POST 请求：

```javascript
app.post('/', function (req, res) {
  res.send('Got a POST request')
})
```

响应对`/user`路由的 PUT 请求：

```javascript
app.put('/user', function (req, res) {
  res.send('Got a PUT request at /user')
})
```

响应对`/user`路由的 DELETE 请求：

```javascript
app.delete('/user', function (req, res) {
  res.send('Got a DELETE request at /user')
})
```

### 路由使用

下载相关npm包

```shell
npm install express
```

```js
//导入包
var express = require('express')
var app = express()

// GET method route
app.get('/', function (req, res) {
  res.send('GET request to the homepage')
})

// POST method route
app.post('/', function (req, res) {
  res.send('POST request to the homepage')
})

app.listen(80);
```



### app.all()

有一种特殊的路由方法，`app.all()`用于在*所有*HTTP 请求方法的路径上加载中间件函数。例如，无论使用 GET、POST、PUT、DELETE 还是[http 模块](https://nodejs.org/api/http.html#http_http_methods)中支持的任何其他 HTTP 请求方法，都会对路由“/secret”的请求执行以下处理程序。

```javascript
app.all('/secret', function (req, res, next) {
  console.log('Accessing the secret section ...')
  next() // pass control to the next handler(把控制权交给下一个管理者)
})
```



### app.get()

```javascript
app.get('/', function (req, res) {
  res.send('root')
})
```

此路由路径将匹配到 的请求`/about`。

```javascript
app.get('/about', function (req, res) {
  res.send('about')
})
```

此路由路径将匹配到 的请求`/random.text`。

```javascript
app.get('/random.text', function (req, res) {
  res.send('random.text')
})
```

以下是一些基于字符串模式的路由路径示例。

此路由路径将匹配`acd`和`abcd`。

```javascript
app.get('/ab?cd', function (req, res) {
  res.send('ab?cd')
})
```

此路由路径将匹配`abcd`、`abbcd`、`abbbcd`等。

```javascript
app.get('/ab+cd', function (req, res) {
  res.send('ab+cd')
})
```

此路由路径将匹配`abcd`、`abxcd`、`abRANDOMcd`、`ab123cd`等。

```javascript
app.get('/ab*cd', function (req, res) {
  res.send('ab*cd')
})
```

此路由路径将匹配`/abe`和`/abcde`。

```javascript
app.get('/ab(cd)?e', function (req, res) {
  res.send('ab(cd)?e')
})
```

基于正则表达式的路由路径示例：

此路由路径将匹配其中带有“a”的任何内容。

```javascript
app.get(/a/, function (req, res) {
  res.send('/a/')
})
```

此路由路径将匹配`butterfly`and `dragonfly`，但不匹配`butterflyman`, `dragonflyman`，依此类推。

```javascript
app.get(/.*fly$/, function (req, res) {
  res.send('/.*fly$/')
})
```



### 路由参数

路由参数是命名的 URL 段，用于捕获在 URL 中的位置指定的值。捕获的值填充到`req.params`对象中，路径中指定的路由参数的名称作为它们各自的键。

```
Route path: /users/:userId/books/:bookId
Request URL: http://localhost:3000/users/34/books/8989
req.params: { "userId": "34", "bookId": "8989" }
```

要使用路由参数定义路由，只需在路由的路径中指定路由参数，如下所示。

```javascript
app.get('/users/:userId/books/:bookId', function (req, res) {
  res.send(req.params)
})
```

**路由参数的名称必须由“单词字符”（[A-Za-z0-9_]）组成。**

由于连字符 ( `-`) 和点 ( `.`) 是按字面解释的，因此它们可以与路由参数一起用于有用的目的。

```
Route path: /flights/:from-:to
Request URL: http://localhost:3000/flights/LAX-SFO
req.params: { "from": "LAX", "to": "SFO" }

Route path: /plantae/:genus.:species
Request URL: http://localhost:3000/plantae/Prunus.persica
req.params: { "genus": "Prunus", "species": "persica" }
```

为了更好地控制路由参数可以匹配的确切字符串，您可以在括号 ( `()`) 中附加正则表达式：

```
Route path: /user/:userId(\d+)
Request URL: http://localhost:3000/user/42
req.params: {"userId": "42"}
```

**因为正则表达式通常是文字字符串的一部分，所以一定要`\`使用额外的反斜杠来转义任何字符，例如`\\d+`.**

## 路由处理程序



您可以提供多个回调函数，它们的行为类似于[中间件](https://www.expressjs.com.cn/en/guide/using-middleware.html)来处理请求。唯一的例外是这些回调可能会调用`next('route')`以绕过剩余的路由回调。您可以使用此机制对路由施加先决条件，然后如果没有理由继续当前路由，则将控制权传递给后续路由

路由处理程序的形式可以是函数、函数数组或两者的组合，如以下示例所示。

单个回调函数可以处理路由。例如：

```javascript
app.get('/example/a', function (req, res) {
  res.send('Hello from A!')
})
```

一个以上的回调函数可以处理一个路由（确保你指定了`next`对象）。例如：

```javascript
app.get('/example/b', function (req, res, next) {
  console.log('下一个函数会发送响应 ...')
  next()
}, function (req, res) {
  res.send('Hello from B!')
})
```

一组回调函数可以处理路由。例如：

```javascript
var cb0 = function (req, res, next) {
  console.log('CB0')
  next()
}

var cb1 = function (req, res, next) {
  console.log('CB1')
  next()
}

var cb2 = function (req, res) {
  res.send('Hello from C!')
}

app.get('/example/c', [cb0, cb1, cb2])
```

独立函数和函数数组的组合可以处理路由。例如：

```javascript
var cb0 = function (req, res, next) {
  console.log('CB0')
  next()
}

var cb1 = function (req, res, next) {
  console.log('CB1')
  next()
}

app.get('/example/d', [cb0, cb1], function (req, res, next) {
  console.log('下一个函数会发送响应 ...')
  next()
}, function (req, res) {
  res.send('Hello from D!')
})
```

## 响应方法

下表中响应对象（`res`）上的方法可以向客户端发送响应，并终止请求-响应循环。如果没有从路由处理程序调用这些方法，则客户端请求将被挂起。

| 方法                                                         | 描述                                                 |
| ------------------------------------------------------------ | ---------------------------------------------------- |
| [res.download()](https://www.expressjs.com.cn/en/4x/api.html#res.download) | 提示要下载的文件。                                   |
| [res.end()](https://www.expressjs.com.cn/en/4x/api.html#res.end) | 结束响应过程。                                       |
| [res.json()](https://www.expressjs.com.cn/en/4x/api.html#res.json) | 发送 JSON 响应。                                     |
| [res.jsonp()](https://www.expressjs.com.cn/en/4x/api.html#res.jsonp) | 发送带有 JSONP 支持的 JSON 响应。                    |
| [res.redirect()](https://www.expressjs.com.cn/en/4x/api.html#res.redirect) | 重定向请求。                                         |
| [res.render()](https://www.expressjs.com.cn/en/4x/api.html#res.render) | 渲染视图模板。                                       |
| [res.send()](https://www.expressjs.com.cn/en/4x/api.html#res.send) | 发送各种类型的响应。                                 |
| [res.sendFile()](https://www.expressjs.com.cn/en/4x/api.html#res.sendFile) | 将文件作为八位字节流发送。                           |
| [res.sendStatus()](https://www.expressjs.com.cn/en/4x/api.html#res.sendStatus) | 设置响应状态码并将其字符串表示形式作为响应正文发送。 |

## app.route()

您可以使用`app.route()`. 因为路径是在单个位置指定的，所以创建模块化路由是有帮助的，因为这有助于减少冗余和拼写错误。有关路由的更多信息，请参阅：[Router() 文档](https://www.expressjs.com.cn/en/4x/api.html#router)。

下面是一个使用`app.route()`.

```javascript
app.route('/book')
  .get(function (req, res) {
    res.send('Get a random book')
  })
  .post(function (req, res) {
    res.send('Add a book')
  })
  .put(function (req, res) {
    res.send('Update the book')
  })
```

## express.Router

使用`express.Router`该类创建模块化、可安装的路由处理程序。实例是一个`Router`完整的中间件和路由系统；因此，它通常被称为“迷你应用程序”。

以下示例将路由器创建为模块，在其中加载中间件函数，定义一些路由，并将路由器模块安装在主应用程序的路径上。

`birds.js`在 app 目录下创建一个名为 router 的文件，内容如下：

```javascript
var express = require('express')
var router = express.Router()

// middleware that is specific to this router
router.use(function timeLog (req, res, next) {
  console.log('Time: ', Date.now())
  next()
})
// define the home page route
router.get('/', function (req, res) {
  res.send('Birds home page')
})
// define the about route
router.get('/about', function (req, res) {
  res.send('About birds')
})

module.exports = router
```

然后，在应用程序中加载路由器模块：

```javascript
var birds = require('./birds')

// ...

app.use('/birds', birds)
```

该应用程序现在将能够处理对`/birds`和的请求`/birds/about`，以及调用`timeLog`特定于路由的中间件函数。