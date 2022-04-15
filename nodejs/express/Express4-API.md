# 4.x API

## 表示（）

创建一个 Express 应用程序。该函数是模块`express()`导出的顶级函数。`express`

```javascript
var express = require('express')
var app = express()
```

### 方法

### express.json([选项])

此中间件在 Express v4.16.0 及更高版本中可用。

这是 Express 中内置的中间件功能。它使用 JSON 有效负载解析传入的请求，并基于 [body-parser](https://www.expressjs.com.cn/resources/middleware/body-parser.html)。

返回仅解析 JSON 并且仅查看`Content-Type`标头与`type`选项匹配的请求的中间件。此解析器接受正文的任何 Unicode 编码，并支持自动膨胀`gzip`和 `deflate`编码。

```
body`包含已解析数据的新对象`request` 在中间件（ie）之后填充到对象上，如果没有要解析的主体、不匹配或发生错误，则填充`req.body`空对象（ ）。`{}``Content-Type
```

由于`req.body`的形状基于用户控制的输入，因此该对象中的所有属性和值都是不受信任的，应该在信任之前进行验证。例如，`req.body.foo.toString()`可能以多种方式失败，例如 `foo`可能不存在或可能不是字符串，并且`toString`可能不是函数而是字符串或其他用户输入。

下表描述了可选`options`对象的属性。

| 财产      | 描述                                                         | 类型   | 默认                 |
| --------- | ------------------------------------------------------------ | ------ | -------------------- |
| `inflate` | 启用或禁用处理放气（压缩）的身体；当禁用时，瘪的身体会被拒绝。 | 布尔值 | `true`               |
| `limit`   | 控制最大请求正文大小。如果这是一个数字，则该值指定字节数；如果是字符串，则将该值传递给[字节](https://www.npmjs.com/package/bytes)库进行解析。 | 混合   | `"100kb"`            |
| `reviver` | 该选项作为第二个参数`reviver`直接传递给。[您可以在有关 JSON.parse 的 MDN 文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse#Example.3A_Using_the_reviver_parameter)`JSON.parse`中找到有关此参数的更多信息。 | 功能   | `null`               |
| `strict`  | 启用或禁用仅接受数组和对象；禁用时将接受任何`JSON.parse`接受。 | 布尔值 | `true`               |
| `type`    | 这用于确定中间件将解析的媒体类型。此选项可以是字符串、字符串数组或函数。如果不是函数，`type`则选项直接传递给[type-is](https://www.npmjs.org/package/type-is#readme)库，它可以是扩展名（like `json`）、mime 类型（like `application/json`）或带有通配符的 mime 类型（like `*/*`or `*/json`）。如果是函数，`type`则调用该选项`fn(req)`，如果请求返回真值，则解析请求。 | 混合   | `"application/json"` |
| `verify`  | 此选项（如果提供）称为`verify(req, res, buf, encoding)`，其中`buf`是`Buffer`原始请求正文的 a 并且`encoding`是请求的编码。可以通过抛出错误来中止解析。 | 功能   | `undefined`          |

### express.raw([选项])

此中间件在 Express v4.17.0 及更高版本中可用。

这是 Express 中内置的中间件功能。它将传入的请求有效负载解析为 a`Buffer`并基于 [body-parser](https://www.expressjs.com.cn/resources/middleware/body-parser.html)。

返回将所有主体解析为 a`Buffer`并仅查看`Content-Type`标头与`type`选项匹配的请求的中间件。此解析器接受正文的任何 Unicode 编码，并支持自动膨胀`gzip`和 `deflate`编码。

在中间件（即）之后`body` `Buffer`的对象上填充一个包含解析数据的新对象，如果没有要解析的主体、不匹配或发生错误，则填充一个空对象（ ）。`request``req.body``{}``Content-Type`

由于`req.body`的形状基于用户控制的输入，因此该对象中的所有属性和值都是不受信任的，应该在信任之前进行验证。例如，`req.body.toString()`可能以多种方式失败，例如堆叠多个解析器`req.body`可能来自不同的解析器。建议在调用缓冲区方法之前进行`req.body`测试。`Buffer`

下表描述了可选`options`对象的属性。

| 财产      | 描述                                                         | 类型   | 默认                         |
| --------- | ------------------------------------------------------------ | ------ | ---------------------------- |
| `inflate` | 启用或禁用处理放气（压缩）的身体；当禁用时，瘪的身体会被拒绝。 | 布尔值 | `true`                       |
| `limit`   | 控制最大请求正文大小。如果这是一个数字，则该值指定字节数；如果是字符串，则将该值传递给[字节](https://www.npmjs.com/package/bytes)库进行解析。 | 混合   | `"100kb"`                    |
| `type`    | 这用于确定中间件将解析的媒体类型。此选项可以是字符串、字符串数组或函数。如果不是函数，`type`则选项直接传递给[type-is](https://www.npmjs.org/package/type-is#readme)库，它可以是扩展名（like `bin`）、mime 类型（like `application/octet-stream`）或带有通配符的 mime 类型（like `*/*`or `application/*`）。如果是函数，`type`则调用该选项`fn(req)`，如果请求返回真值，则解析请求。 | 混合   | `"application/octet-stream"` |
| `verify`  | 此选项（如果提供）称为`verify(req, res, buf, encoding)`，其中`buf`是`Buffer`原始请求正文的 a 并且`encoding`是请求的编码。可以通过抛出错误来中止解析。 | 功能   | `undefined`                  |

### express.Router([选项])

创建一个新的[路由器](https://www.expressjs.com.cn/4x/api.html#router)对象。

```javascript
var router = express.Router([options])
```

可选`options`参数指定路由器的行为。

| 财产            | 描述                                                         | 默认                                              | 可用性 |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------- | ------ |
| `caseSensitive` | 启用区分大小写。                                             | 默认禁用，将“/Foo”和“/foo”视为相同。              |        |
| `mergeParams`   | 保留`req.params`来自父路由器的值。如果父项和子项的参数名称冲突，则子项的值优先。 | `false`                                           | 4.5.0+ |
| `strict`        | 启用严格路由。                                               | 默认情况下禁用，“/foo”和“/foo/”被路由器视为相同。 |        |

您可以像应用程序一样添加中间件和 HTTP 方法路由（例如`get`、`put`、`post`等） 。`router`

有关详细信息，请参阅[路由器](https://www.expressjs.com.cn/4x/api.html#router)。

### express.static（根，[选项]）

这是 Express 中内置的中间件功能。它提供静态文件并基于 [serve-static](https://www.expressjs.com.cn/resources/middleware/serve-static.html)。

注意：为获得最佳结果，请[使用反向代理](https://www.expressjs.com.cn/en/advanced/best-practice-performance.html#use-a-reverse-proxy)缓存来提高提供静态资产的性能。

该`root`参数指定提供静态资产的根目录。该函数通过结合`req.url`提供的`root`目录来确定要服务的文件。当找不到文件时，它不会发送 404 响应，而是调用`next()` 以继续下一个中间件，从而允许堆叠和回退。

下表描述了`options`对象的属性。另请参见[下面的示例](https://www.expressjs.com.cn/4x/api.html#example.of.express.static)。

| 财产           | 描述                                                         | 类型   | 默认        |
| -------------- | ------------------------------------------------------------ | ------ | ----------- |
| `dotfiles`     | 确定如何处理点文件（以点“.”开头的文件或目录）。  请参阅[下面](https://www.expressjs.com.cn/4x/api.html#dotfiles)的点文件。 | 细绳   | “忽视”      |
| `etag`         | 启用或禁用 etag 生成  注意：`express.static`始终发送弱 ETag。 | 布尔值 | `true`      |
| `extensions`   | 设置文件扩展名后备：如果找不到文件，则搜索具有指定扩展名的文件并提供找到的第一个文件。示例：`['html', 'htm']`。 | 混合   | `false`     |
| `fallthrough`  | 让客户端错误作为未处理的请求通过，否则转发客户端错误。  请参阅下面的[失败](https://www.expressjs.com.cn/4x/api.html#fallthrough)。 | 布尔值 | `true`      |
| `immutable`    | 启用或禁用响应标头`immutable`中的指令。`Cache-Control`如果启用，`maxAge`还应指定该选项以启用缓存。该`immutable`指令将阻止受支持的客户端在选项的生命周期内发出条件请求`maxAge`以检查文件是否已更改。 | 布尔值 | `false`     |
| `index`        | 发送指定的目录索引文件。设置为`false`禁用目录索引。          | 混合   | “索引.html” |
| `lastModified` | 将`Last-Modified`标题设置为操作系统上文件的最后修改日期。    | 布尔值 | `true`      |
| `maxAge`       | 以毫秒为单位设置 Cache-Control 标头的 max-age 属性或[ms 格式](https://www.npmjs.org/package/ms)的字符串。 | 数字   | 0           |
| `redirect`     | 当路径名是目录时，重定向到结尾的“/”。                        | 布尔值 | `true`      |
| `setHeaders`   | 用于设置 HTTP 标头以与文件一起服务的功能。  请参阅下面的[setHeaders](https://www.expressjs.com.cn/4x/api.html#setHeaders)。 | 功能   |             |

有关更多信息，请参阅[在 Express 中提供静态文件](https://www.expressjs.com.cn/starter/static-files.html)。和[使用中间件 - 内置中间件](https://www.expressjs.com.cn/en/guide/using-middleware.html#middleware.built-in)。

##### 点文件

此选项的可能值为：

- “allow” - 对点文件没有特殊处理。
- “deny” - 拒绝对 dotfile 的请求，用 响应`403`，然后调用`next()`.
- “忽略” - 就好像点文件不存在一样，用 响应`404`，然后调用`next()`.

**注意**：使用默认值，它不会忽略以点开头的目录中的文件。

##### 失败

当此选项为`true`时，客户端错误（例如错误请求或对不存在文件的请求）将导致此中间件简单地调用`next()`以调用堆栈中的下一个中间件。当为 false 时，这些错误（甚至是 404）将调用`next(err)`.

将此选项设置为，`true`以便您可以将多个物理目录映射到同一个 Web 地址或路由以填充不存在的文件。

如果您已将此中间件安装在严格设计为单个文件系统目录的路径上，则使用`false`该路径，这允许短路 404 以减少开销。这个中间件也会回复所有的方法。

##### 设置标题

对于此选项，指定一个函数来设置自定义响应标头。对标头的更改必须同步发生。

该函数的签名是：

```javascript
fn(res, path, stat)
```

论据：

- `res`，[响应对象](https://www.expressjs.com.cn/4x/api.html#res)。
- `path`，正在发送的文件路径。
- `stat`，`stat`正在发送的文件的对象。

#### express.static 示例

下面是一个将`express.static`中间件函数与精心设计的选项对象一起使用的示例：

```javascript
var options = {
  dotfiles: 'ignore',
  etag: false,
  extensions: ['htm', 'html'],
  index: false,
  maxAge: '1d',
  redirect: false,
  setHeaders: function (res, path, stat) {
    res.set('x-timestamp', Date.now())
  }
}

app.use(express.static('public', options))
```

### express.text([选项])

此中间件在 Express v4.17.0 及更高版本中可用。

这是 Express 中内置的中间件功能。它将传入的请求有效负载解析为字符串，并基于 [body-parser](https://www.expressjs.com.cn/resources/middleware/body-parser.html)。

返回将所有主体解析为字符串并仅查看`Content-Type`标头与`type`选项匹配的请求的中间件。此解析器接受正文的任何 Unicode 编码，并支持自动膨胀`gzip`和 `deflate`编码。

```
body`包含解析数据的新字符串`request` 在中间件（ie）之后填充到对象上，如果没有要解析的主体、不匹配或发生错误，则填充`req.body`空对象（ ）。`{}``Content-Type
```

由于`req.body`的形状基于用户控制的输入，因此该对象中的所有属性和值都是不受信任的，应该在信任之前进行验证。例如，`req.body.trim()`可能以多种方式失败，例如堆叠多个解析器`req.body`可能来自不同的解析器。`req.body`建议在调用字符串方法之前测试字符串。

下表描述了可选`options`对象的属性。

| 财产             | 描述                                                         | 类型   | 默认           |
| ---------------- | ------------------------------------------------------------ | ------ | -------------- |
| `defaultCharset` | `Content-Type`如果请求标头中未指定字符集，请为文本内容指定默认字符集。 | 细绳   | `"utf-8"`      |
| `inflate`        | 启用或禁用处理放气（压缩）的身体；当禁用时，瘪的身体会被拒绝。 | 布尔值 | `true`         |
| `limit`          | 控制最大请求正文大小。如果这是一个数字，则该值指定字节数；如果是字符串，则将该值传递给[字节](https://www.npmjs.com/package/bytes)库进行解析。 | 混合   | `"100kb"`      |
| `type`           | 这用于确定中间件将解析的媒体类型。此选项可以是字符串、字符串数组或函数。如果不是函数，`type`则选项直接传递给[type-is](https://www.npmjs.org/package/type-is#readme)库，它可以是扩展名（like `txt`）、mime 类型（like `text/plain`）或带有通配符的 mime 类型（like `*/*`or `text/*`）。如果是函数，`type`则调用该选项`fn(req)`，如果请求返回真值，则解析请求。 | 混合   | `"text/plain"` |
| `verify`         | 此选项（如果提供）称为`verify(req, res, buf, encoding)`，其中`buf`是`Buffer`原始请求正文的 a 并且`encoding`是请求的编码。可以通过抛出错误来中止解析。 | 功能   | `undefined`    |

### express.urlencoded（[选项]）

此中间件在 Express v4.16.0 及更高版本中可用。

这是 Express 中内置的中间件功能。它使用 urlencoded 有效负载解析传入的请求，并基于[body-parser](https://www.expressjs.com.cn/resources/middleware/body-parser.html)。

返回仅解析 urlencoded 正文并仅查看`Content-Type`标头与`type`选项匹配的请求的中间件。此解析器仅接受正文的 UTF-8 编码，并支持自动膨胀`gzip`和`deflate`编码。

```
body`包含已解析数据的新对象`request` 在中间件（ie）之后填充到对象上，如果没有要解析的主体、不匹配或发生错误，则填充`req.body`空对象（ ）。该对象将包含键值对，其中值可以是字符串或数组（when is ）或任何类型（when is ）。`{}``Content-Type``extended``false``extended``true
```

由于`req.body`的形状基于用户控制的输入，因此该对象中的所有属性和值都是不受信任的，应该在信任之前进行验证。例如，`req.body.foo.toString()`可能以多种方式失败，例如 `foo`可能不存在或可能不是字符串，并且`toString`可能不是函数而是字符串或其他用户输入。

下表描述了可选`options`对象的属性。

| 财产             | 描述                                                         | 类型   | 默认                                  |
| ---------------- | ------------------------------------------------------------ | ------ | ------------------------------------- |
| `extended`       | 此选项允许在使用`querystring`库 (when `false`) 或`qs`库 (when `true`) 解析 URL 编码数据之间进行选择。“扩展”语法允许将丰富的对象和数组编码为 URL 编码格式，从而提供类似 JSON 的 URL 编码体验。有关详细信息，请[参阅 qs 库](https://www.npmjs.org/package/qs#readme)。 | 布尔值 | `true`                                |
| `inflate`        | 启用或禁用处理放气（压缩）的身体；当禁用时，瘪的身体会被拒绝。 | 布尔值 | `true`                                |
| `limit`          | 控制最大请求正文大小。如果这是一个数字，则该值指定字节数；如果是字符串，则将该值传递给[字节](https://www.npmjs.com/package/bytes)库进行解析。 | 混合   | `"100kb"`                             |
| `parameterLimit` | 此选项控制 URL 编码数据中允许的最大参数数。如果请求包含的参数多于该值，则会引发错误。 | 数字   | `1000`                                |
| `type`           | 这用于确定中间件将解析的媒体类型。此选项可以是字符串、字符串数组或函数。如果不是函数，`type`则选项直接传递给[type-is](https://www.npmjs.org/package/type-is#readme)库，它可以是扩展名（like `urlencoded`）、mime 类型（like `application/x-www-form-urlencoded`）或带有通配符的 mime 类型（like `*/x-www-form-urlencoded`）。如果是函数，`type`则调用该选项`fn(req)`，如果请求返回真值，则解析请求。 | 混合   | `"application/x-www-form-urlencoded"` |
| `verify`         | 此选项（如果提供）称为`verify(req, res, buf, encoding)`，其中`buf`是`Buffer`原始请求正文的 a 并且`encoding`是请求的编码。可以通过抛出错误来中止解析。 | 功能   | `undefined`                           |

## 应用

该`app`对象通常表示 Express 应用程序。`express()`通过调用Express 模块导出的顶级函数来创建它：

```javascript
var express = require('express')
var app = express()

app.get('/', function (req, res) {
  res.send('hello world')
})

app.listen(3000)
```

该`app`对象具有用于

- 路由 HTTP 请求；例如，请参见[app.METHOD](https://www.expressjs.com.cn/4x/api.html#app.METHOD)和[app.param](https://www.expressjs.com.cn/4x/api.html#app.param)。
- 配置中间件；见[app.route](https://www.expressjs.com.cn/4x/api.html#app.route)。
- 渲染 HTML 视图；见[app.render](https://www.expressjs.com.cn/4x/api.html#app.render)。
- 注册模板引擎；见[app.engine](https://www.expressjs.com.cn/4x/api.html#app.engine)。

它还具有影响应用程序行为方式的设置（属性）；有关详细信息，请参阅[应用程序设置](https://www.expressjs.com.cn/4x/api.html#app.settings.table)。

Express 应用程序对象可以从[请求对象](https://www.expressjs.com.cn/4x/api.html#req)和[响应对象](https://www.expressjs.com.cn/4x/api.html#res)中分别引用为`req.app`、 和`res.app`。

### 特性

### 应用程序.locals

该`app.locals`对象的属性是应用程序中的局部变量。

```javascript
console.dir(app.locals.title)
// => 'My App'

console.dir(app.locals.email)
// => 'me@myapp.com'
```

设置后，`app.locals`属性的值将在应用程序的整个生命周期中保持不变，而[res.locals](https://www.expressjs.com.cn/4x/api.html#res.locals)属性仅在请求的生命周期内有效。

您可以访问应用程序中呈现的模板中的局部变量。这对于为模板以及应用程序级数据提供帮助函数很有用。局部变量在中间件中可用`req.app.locals`（参见[req.app](https://www.expressjs.com.cn/4x/api.html#req.app)）

```javascript
app.locals.title = 'My App'
app.locals.strftime = require('strftime')
app.locals.email = 'me@myapp.com'
```

### 应用程序挂载路径

该`app.mountpath`属性包含一个或多个安装子应用程序的路径模式。

子应用程序是`express`可用于处理对路由的请求的实例。

```javascript
var express = require('express')

var app = express() // the main app
var admin = express() // the sub app

admin.get('/', function (req, res) {
  console.log(admin.mountpath) // /admin
  res.send('Admin Homepage')
})

app.use('/admin', admin) // mount the sub app
```

它类似于对象的[baseUrl](https://www.expressjs.com.cn/4x/api.html#req.baseUrl)属性`req`，只是`req.baseUrl` 返回匹配的 URL 路径，而不是匹配的模式。

如果子应用挂载在多个路径模式上，`app.mountpath`则返回其挂载的模式列表，如下例所示。

```javascript
var admin = express()

admin.get('/', function (req, res) {
  console.dir(admin.mountpath) // [ '/adm*n', '/manager' ]
  res.send('Admin Homepage')
})

var secret = express()
secret.get('/', function (req, res) {
  console.log(secret.mountpath) // /secr*t
  res.send('Admin Secret')
})

admin.use('/secr*t', secret) // load the 'secret' router on '/secr*t', on the 'admin' sub app
app.use(['/adm*n', '/manager'], admin) // load the 'admin' router on '/adm*n' and '/manager', on the parent app
```

### 活动

### app.on('mount', 回调(父))

当子应用安装在父应用上时，该`mount`事件会在子应用上触发。父应用程序被传递给回调函数。

**笔记**

子应用程序将：

- 不继承具有默认值的设置值。您必须在子应用程序中设置该值。
- 继承设置的值，没有默认值。

有关详细信息，请参阅[应用程序设置](https://www.expressjs.com.cn/en/4x/api.html#app.settings.table)。

```javascript
var admin = express()

admin.on('mount', function (parent) {
  console.log('Admin Mounted')
  console.log(parent) // refers to the parent app
})

admin.get('/', function (req, res) {
  res.send('Admin Homepage')
})

app.use('/admin', admin)
```

### 方法

### app.all（路径，回调 [，回调 ...]）

此方法类似于标准的[app.METHOD()](https://www.expressjs.com.cn/4x/api.html#app.METHOD)方法，不同之处在于它匹配所有 HTTP 动词。

#### 论据

| 争论       | 描述                                                         | 默认          |
| ---------- | ------------------------------------------------------------ | ------------- |
| `path`     | 调用中间件函数的路径；可以是以下任何一种：表示路径的字符串。路径模式。匹配路径的正则表达式模式。以上任何一种组合的数组。有关示例，请参阅[路径示例](https://www.expressjs.com.cn/4x/api.html#path-examples)。 | '/'（根路径） |
| `callback` | 回调函数；可：一个中间件功能。一系列中间件功能（以逗号分隔）。一组中间件函数。以上所有的组合。您可以提供多个回调函数，其行为类似于中间件，但这些回调可以调用`next('route')`以绕过剩余的路由回调。您可以使用此机制对路由施加先决条件，然后如果没有理由继续当前路由，则将控制权传递给后续路由。由于[路由器](https://www.expressjs.com.cn/4x/api.html#router)和[应用程序](https://www.expressjs.com.cn/4x/api.html#application)实现了中间件接口，因此您可以像使用任何其他中间件功能一样使用它们。有关示例，请参阅[中间件回调函数示例](https://www.expressjs.com.cn/4x/api.html#middleware-callback-function-examples)。 | 没有任何      |

#### 例子

`/secret`对于使用 GET、POST、PUT、DELETE 或任何其他 HTTP 请求方法的请求，都会执行以下回调：

```javascript
app.all('/secret', function (req, res, next) {
  console.log('Accessing the secret section ...')
  next() // pass control to the next handler
})
```

该`app.all()`方法对于为特定路径前缀或任意匹配映射“全局”逻辑很有用。例如，如果您将以下内容放在所有其他路由定义的顶部，则要求从该点开始的所有路由都需要身份验证，并自动加载用户。请记住，这些回调不必充当端点：`loadUser` 可以执行任务，然后调用`next()`以继续匹配后续路由。

```javascript
app.all('*', requireAuthentication, loadUser)
```

或等价物：

```javascript
app.all('*', requireAuthentication)
app.all('*', loadUser)
```

另一个例子是列入白名单的“全局”功能。该示例与上面的示例类似，但它仅限制以“/api”开头的路径：

```javascript
app.all('/api/*', requireAuthentication)
```

### app.delete（路径，回调 [，回调 ...]）

使用指定的回调函数将 HTTP DELETE 请求路由到指定路径。有关详细信息，请参阅[路由指南](https://www.expressjs.com.cn/guide/routing.html)。

#### 论据

| 争论       | 描述                                                         | 默认          |
| ---------- | ------------------------------------------------------------ | ------------- |
| `path`     | 调用中间件函数的路径；可以是以下任何一种：表示路径的字符串。路径模式。匹配路径的正则表达式模式。以上任何一种组合的数组。有关示例，请参阅[路径示例](https://www.expressjs.com.cn/4x/api.html#path-examples)。 | '/'（根路径） |
| `callback` | 回调函数；可：一个中间件功能。一系列中间件功能（以逗号分隔）。一组中间件函数。以上所有的组合。您可以提供多个回调函数，其行为类似于中间件，但这些回调可以调用`next('route')`以绕过剩余的路由回调。您可以使用此机制对路由施加先决条件，然后如果没有理由继续当前路由，则将控制权传递给后续路由。由于[路由器](https://www.expressjs.com.cn/4x/api.html#router)和[应用程序](https://www.expressjs.com.cn/4x/api.html#application)实现了中间件接口，因此您可以像使用任何其他中间件功能一样使用它们。有关示例，请参阅[中间件回调函数示例](https://www.expressjs.com.cn/4x/api.html#middleware-callback-function-examples)。 | 没有任何      |

#### 例子

```javascript
app.delete('/', function (req, res) {
  res.send('DELETE request to homepage')
})
```

### app.disable（名称）

将布尔设置设置`name`为`false`，其中`name`是[应用设置表](https://www.expressjs.com.cn/4x/api.html#app.settings.table)中的属性之一。调用`app.set('foo', false)`布尔属性与调用相同`app.disable('foo')`。

例如：

```javascript
app.disable('trust proxy')
app.get('trust proxy')
// => false
```

### app.disabled（名称）

如果禁用`true`布尔设置( )，则返回，其中是[应用设置表](https://www.expressjs.com.cn/4x/api.html#app.settings.table)中的属性之一。`name``false``name`

```javascript
app.disabled('trust proxy')
// => true

app.enable('trust proxy')
app.disabled('trust proxy')
// => false
```

### 应用程序启用（名称）

将布尔设置设置`name`为`true`，其中`name`是[应用设置表](https://www.expressjs.com.cn/4x/api.html#app.settings.table)中的属性之一。调用`app.set('foo', true)`布尔属性与调用相同`app.enable('foo')`。

```javascript
app.enable('trust proxy')
app.get('trust proxy')
// => true
```

### app.enabled（名称）

返回是否启用`true`了设置( )，其中是[应用设置表](https://www.expressjs.com.cn/4x/api.html#app.settings.table)中的属性之一。`name``true``name`

```javascript
app.enabled('trust proxy')
// => false

app.enable('trust proxy')
app.enabled('trust proxy')
// => true
```

### app.engine(ext, 回调)

将给定的模板引擎注册`callback`为`ext`.

默认情况下，Express 将`require()`引擎基于文件扩展名。例如，如果您尝试渲染“foo.pug”文件，Express 会在内部调用以下内容，并缓存`require()`后续调用以提高性能。

```javascript
app.engine('pug', require('pug').__express)
```

将此方法用于不提供`.__express`开箱即用的引擎，或者如果您希望将不同的扩展“映射”到模板引擎。

例如，要将 EJS 模板引擎映射到“.html”文件：

```javascript
app.engine('html', require('ejs').renderFile)
```

在这种情况下，EJS 提供了一个`.renderFile()`与 Express 所期望的签名相同的方法：`(path, options, callback)`，但请注意，它将此方法作为`ejs.__express`内部别名，因此如果您使用“.ejs”扩展名，则无需执行任何操作。

一些模板引擎不遵循这个约定。[consolidate.js](https://github.com/tj/consolidate.js)库 映射 Node 模板引擎以遵循此约定，因此它们可以与 Express 无缝协作。

```javascript
var engines = require('consolidate')
app.engine('haml', engines.haml)
app.engine('html', engines.hogan)
```

### app.get(名称)

返回应用设置的值`name`，其中`name`是 [应用设置表](https://www.expressjs.com.cn/4x/api.html#app.settings.table)中的字符串之一。例如：

```javascript
app.get('title')
// => undefined

app.set('title', 'My Site')
app.get('title')
// => "My Site"
```

### app.get(路径，回调 [，回调 ...])

使用指定的回调函数将 HTTP GET 请求路由到指定路径。

#### 论据

| 争论       | 描述                                                         | 默认          |
| ---------- | ------------------------------------------------------------ | ------------- |
| `path`     | 调用中间件函数的路径；可以是以下任何一种：表示路径的字符串。路径模式。匹配路径的正则表达式模式。以上任何一种组合的数组。有关示例，请参阅[路径示例](https://www.expressjs.com.cn/4x/api.html#path-examples)。 | '/'（根路径） |
| `callback` | 回调函数；可：一个中间件功能。一系列中间件功能（以逗号分隔）。一组中间件函数。以上所有的组合。您可以提供多个回调函数，其行为类似于中间件，但这些回调可以调用`next('route')`以绕过剩余的路由回调。您可以使用此机制对路由施加先决条件，然后如果没有理由继续当前路由，则将控制权传递给后续路由。由于[路由器](https://www.expressjs.com.cn/4x/api.html#router)和[应用程序](https://www.expressjs.com.cn/4x/api.html#application)实现了中间件接口，因此您可以像使用任何其他中间件功能一样使用它们。有关示例，请参阅[中间件回调函数示例](https://www.expressjs.com.cn/4x/api.html#middleware-callback-function-examples)。 | 没有任何      |

有关详细信息，请参阅[路由指南](https://www.expressjs.com.cn/guide/routing.html)。

#### 例子

```javascript
app.get('/', function (req, res) {
  res.send('GET request to homepage')
})
```

### app.listen（路径，[回调]）

启动一个 UNIX 套接字并侦听给定路径上的连接。此方法与 Node 的[http.Server.listen()](https://nodejs.org/api/http.html#http_server_listen)相同。

```javascript
var express = require('express')
var app = express()
app.listen('/tmp/sock')
```

### app.listen([port[, host[, backlog]]][, callback])

绑定并监听指定主机和端口上的连接。此方法与 Node 的[http.Server.listen()](https://nodejs.org/api/http.html#http_server_listen)相同。

如果端口被省略或为 0，操作系统将分配一个任意未使用的端口，这对于自动化任务（测试等）等情况很有用。

```javascript
var express = require('express')
var app = express()
app.listen(3000)
```

`app`返回的实际上`express()`是一个 JavaScript `Function`，旨在作为回调传递给 Node 的 HTTP 服务器以处理请求。这使得为您的应用程序的 HTTP 和 HTTPS 版本提供相同的代码库变得很容易，因为应用程序不会从这些版本继承（它只是一个回调）：

```javascript
var express = require('express')
var https = require('https')
var http = require('http')
var app = express()

http.createServer(app).listen(80)
https.createServer(options, app).listen(443)
```

该`app.listen()`方法返回一个[http.Server](https://nodejs.org/api/http.html#http_class_http_server)对象，并且（对于 HTTP）是以下的便捷方法：

```javascript
app.listen = function () {
  var server = http.createServer(this)
  return server.listen.apply(server, arguments)
}
```

注意：Node 的 [http.Server.listen()](https://nodejs.org/api/http.html#http_server_listen) 方法的所有形式实际上都得到了支持。

### app.METHOD（路径，回调 [，回调 ...]）

路由 HTTP 请求，其中 METHOD 是请求的 HTTP 方法，如 GET、PUT、POST 等，小写。因此，实际的方法是`app.get()`、 `app.post()`、`app.put()`等。有关完整列表，请参阅下面的[路由方法。](https://www.expressjs.com.cn/4x/api.html#routing-methods)

#### 论据

| 争论       | 描述                                                         | 默认          |
| ---------- | ------------------------------------------------------------ | ------------- |
| `path`     | 调用中间件函数的路径；可以是以下任何一种：表示路径的字符串。路径模式。匹配路径的正则表达式模式。以上任何一种组合的数组。有关示例，请参阅[路径示例](https://www.expressjs.com.cn/4x/api.html#path-examples)。 | '/'（根路径） |
| `callback` | 回调函数；可：一个中间件功能。一系列中间件功能（以逗号分隔）。一组中间件函数。以上所有的组合。您可以提供多个回调函数，其行为类似于中间件，但这些回调可以调用`next('route')`以绕过剩余的路由回调。您可以使用此机制对路由施加先决条件，然后如果没有理由继续当前路由，则将控制权传递给后续路由。由于[路由器](https://www.expressjs.com.cn/4x/api.html#router)和[应用程序](https://www.expressjs.com.cn/4x/api.html#application)实现了中间件接口，因此您可以像使用任何其他中间件功能一样使用它们。有关示例，请参阅[中间件回调函数示例](https://www.expressjs.com.cn/4x/api.html#middleware-callback-function-examples)。 | 没有任何      |

#### 路由方法

Express 支持以下与 HTTP 同名方法对应的路由方法：

| `checkout``copy``delete``get``head``lock``merge``mkactivity` | `mkcol``move``m-search``notify``options``patch``post` | `purge``put``report``search``subscribe``trace``unlock``unsubscribe` |
| ------------------------------------------------------------ | ----------------------------------------------------- | ------------------------------------------------------------ |
|                                                              |                                                       |                                                              |

API 文档仅针对最流行的 HTTP 方法`app.get()`、 `app.post()`、`app.put()`和`app.delete()`. 但是，上面列出的其他方法的工作方式完全相同。

要路由转换为无效 JavaScript 变量名的方法，请使用方括号表示法。例如，`app['m-search']('/', function ...`。

除了之前没有为路径调用过的 方法之外，还会`app.get()`自动为 HTTP`HEAD`方法调用该函数。`GET``app.head()``app.get()`

方法 ,`app.all()`不是从任何 HTTP 方法派生的，而是在*所有*HTTP 请求方法的指定路径中加载中间件。有关详细信息，请参阅[app.all](https://www.expressjs.com.cn/4x/api.html#app.all)。

有关路由的更多信息，请参阅[路由指南](https://www.expressjs.com.cn/guide/routing.html)。

### app.param（[名称]，回调）

[为路由参数](https://www.expressjs.com.cn/en/guide/routing.html#route-parameters)添加回调触发器，其中`name`为参数名称或参数数组，`callback`为回调函数。回调函数的参数依次是请求对象、响应对象、下一个中间件、参数的值和参数的名称。

如果`name`是一个数组，`callback`则为其中声明的每个参数注册触发器，按照它们声明的顺序。此外，对于除最后一个之外的每个声明的参数，`next`回调内部的调用将调用下一个声明参数的回调。对于最后一个参数，调用`next`将调用当前正在处理的路由的下一个中间件，就像它`name`只是一个字符串一样。

例如，当`:user`出现在路由路径中时，您可以映射用户加载逻辑以自动提供`req.user`给路由，或对参数输入执行验证。

```javascript
app.param('user', function (req, res, next, id) {
  // try to get the user details from the User model and attach it to the request object
  User.find(id, function (err, user) {
    if (err) {
      next(err)
    } else if (user) {
      req.user = user
      next()
    } else {
      next(new Error('failed to load user'))
    }
  })
})
```

参数回调函数在定义它们的路由器上是本地的。它们不会被安装的应用程序或路由器继承。因此，在 上定义的参数回调`app`将仅由在路由上定义的路由参数触发`app`。

所有参数回调将在参数出现的任何路由的任何处理程序之前调用，并且它们在请求-响应周期中仅被调用一次，即使参数在多个路由中匹配，如下例所示。

```javascript
app.param('id', function (req, res, next, id) {
  console.log('CALLED ONLY ONCE')
  next()
})

app.get('/user/:id', function (req, res, next) {
  console.log('although this matches')
  next()
})

app.get('/user/:id', function (req, res) {
  console.log('and this matches too')
  res.end()
})
```

在 上`GET /user/42`，打印以下内容：

```
CALLED ONLY ONCE
although this matches
and this matches too
app.param(['id', 'page'], function (req, res, next, value) {
  console.log('CALLED ONLY ONCE with', value)
  next()
})

app.get('/user/:id/:page', function (req, res, next) {
  console.log('although this matches')
  next()
})

app.get('/user/:id/:page', function (req, res) {
  console.log('and this matches too')
  res.end()
})
```

在 上`GET /user/42/3`，打印以下内容：

```
CALLED ONLY ONCE with 42
CALLED ONLY ONCE with 3
although this matches
and this matches too
```

以下部分描述`app.param(callback)`，从 v4.11.0 起已弃用。

该`app.param(name, callback)`方法的行为可以通过只传递一个函数来完全改变`app.param()`。这个函数是一个应该如何表现的自定义实现`app.param(name, callback)`——它接受两个参数并且必须返回一个中间件。

此函数的第一个参数是应捕获的 URL 参数的名称，第二个参数可以是任何可能用于返回中间件实现的 JavaScript 对象。

函数返回的中间件决定了捕获 URL 参数时发生的行为。

在此示例中，`app.param(name, callback)`签名被修改为`app.param(name, accessId)`。`app.param()`现在将接受名称和数字，而不是接受名称和回调。

```javascript
var express = require('express')
var app = express()

// customizing the behavior of app.param()
app.param(function (param, option) {
  return function (req, res, next, val) {
    if (val === option) {
      next()
    } else {
      next('route')
    }
  }
})

// using the customized app.param()
app.param('id', 1337)

// route to trigger the capture
app.get('/user/:id', function (req, res) {
  res.send('OK')
})

app.listen(3000, function () {
  console.log('Ready')
})
```

在此示例中，`app.param(name, callback)`签名保持不变，但没有使用中间件回调，而是定义了自定义数据类型检查函数来验证用户 ID 的数据类型。

```javascript
app.param(function (param, validator) {
  return function (req, res, next, val) {
    if (validator(val)) {
      next()
    } else {
      next('route')
    }
  }
})

app.param('id', function (candidate) {
  return !isNaN(parseFloat(candidate)) && isFinite(candidate)
})
```

' `.`' 字符不能用于在捕获正则表达式中捕获字符。例如，您不能使用`'/user-.+/'`to capture `'users-gami'`、 use `[\\s\\S]`or `[\\w\\W]`instead (如`'/user-[\\s\\S]+/'`.

例子：

```javascript
// captures '1-a_6' but not '543-azser-sder'
router.get('/[0-9]+-[[\\w]]*', function (req, res, next) { next() })

// captures '1-a_6' and '543-az(ser"-sder' but not '5-a s'
router.get('/[0-9]+-[[\\S]]*', function (req, res, next) { next() })

// captures all (equivalent to '.*')
router.get('[[\\s\\S]]*', function (req, res, next) { next() })
```

### 应用程序路径（）

返回应用程序的规范路径，一个字符串。

```javascript
var app = express()
var blog = express()
var blogAdmin = express()

app.use('/blog', blog)
blog.use('/admin', blogAdmin)

console.dir(app.path()) // ''
console.dir(blog.path()) // '/blog'
console.dir(blogAdmin.path()) // '/blog/admin'
```

在挂载应用程序的复杂情况下，此方法的行为可能会变得非常复杂：通常最好使用[req.baseUrl](https://www.expressjs.com.cn/4x/api.html#req.baseUrl)来获取应用程序的规范路径。

### app.post（路径，回调 [，回调 ...]）

使用指定的回调函数将 HTTP POST 请求路由到指定路径。有关详细信息，请参阅[路由指南](https://www.expressjs.com.cn/guide/routing.html)。

#### 论据

| 争论       | 描述                                                         | 默认          |
| ---------- | ------------------------------------------------------------ | ------------- |
| `path`     | 调用中间件函数的路径；可以是以下任何一种：表示路径的字符串。路径模式。匹配路径的正则表达式模式。以上任何一种组合的数组。有关示例，请参阅[路径示例](https://www.expressjs.com.cn/4x/api.html#path-examples)。 | '/'（根路径） |
| `callback` | 回调函数；可：一个中间件功能。一系列中间件功能（以逗号分隔）。一组中间件函数。以上所有的组合。您可以提供多个回调函数，其行为类似于中间件，但这些回调可以调用`next('route')`以绕过剩余的路由回调。您可以使用此机制对路由施加先决条件，然后如果没有理由继续当前路由，则将控制权传递给后续路由。由于[路由器](https://www.expressjs.com.cn/4x/api.html#router)和[应用程序](https://www.expressjs.com.cn/4x/api.html#application)实现了中间件接口，因此您可以像使用任何其他中间件功能一样使用它们。有关示例，请参阅[中间件回调函数示例](https://www.expressjs.com.cn/4x/api.html#middleware-callback-function-examples)。 | 没有任何      |

#### 例子

```javascript
app.post('/', function (req, res) {
  res.send('POST request to homepage')
})
```

### app.put（路径，回调 [，回调 ...]）

使用指定的回调函数将 HTTP PUT 请求路由到指定路径。

#### 论据

| 争论       | 描述                                                         | 默认          |
| ---------- | ------------------------------------------------------------ | ------------- |
| `path`     | 调用中间件函数的路径；可以是以下任何一种：表示路径的字符串。路径模式。匹配路径的正则表达式模式。以上任何一种组合的数组。有关示例，请参阅[路径示例](https://www.expressjs.com.cn/4x/api.html#path-examples)。 | '/'（根路径） |
| `callback` | 回调函数；可：一个中间件功能。一系列中间件功能（以逗号分隔）。一组中间件函数。以上所有的组合。您可以提供多个回调函数，其行为类似于中间件，但这些回调可以调用`next('route')`以绕过剩余的路由回调。您可以使用此机制对路由施加先决条件，然后如果没有理由继续当前路由，则将控制权传递给后续路由。由于[路由器](https://www.expressjs.com.cn/4x/api.html#router)和[应用程序](https://www.expressjs.com.cn/4x/api.html#application)实现了中间件接口，因此您可以像使用任何其他中间件功能一样使用它们。有关示例，请参阅[中间件回调函数示例](https://www.expressjs.com.cn/4x/api.html#middleware-callback-function-examples)。 | 没有任何      |

#### 例子

```javascript
app.put('/', function (req, res) {
  res.send('PUT request to homepage')
})
```

### app.render（视图，[本地]，回调）

`callback`通过该函数返回视图的呈现 HTML 。它接受一个可选参数，该参数是一个包含视图局部变量的对象。它就像[res.render()](https://www.expressjs.com.cn/4x/api.html#res.render)，除了它不能自己将渲染视图发送给客户端。

将`app.render()`其视为生成渲染视图字符串的实用程序函数。内部`res.render()`用于`app.render()`渲染视图。

局部变量`cache`保留用于启用视图缓存。设置为`true`，如果你想在开发过程中缓存视图；默认情况下，视图缓存在生产中启用。

```javascript
app.render('email', function (err, html) {
  // ...
})

app.render('email', { name: 'Tobi' }, function (err, html) {
  // ...
})
```

### app.route(路径)

返回单个路由的实例，然后您可以使用它来处理带有可选中间件的 HTTP 动词。用于`app.route()`避免重复的路由名称（以及因此的拼写错误）。

```javascript
var app = express()

app.route('/events')
  .all(function (req, res, next) {
    // runs for all HTTP verbs first
    // think of it as route specific middleware!
  })
  .get(function (req, res, next) {
    res.json({})
  })
  .post(function (req, res, next) {
    // maybe add a new event...
  })
```

### app.set（名称，值）

将设置分配`name`给`value`。您可以存储任何您想要的值，但某些名称可用于配置服务器的行为。这些特殊名称列在[应用设置表中](https://www.expressjs.com.cn/4x/api.html#app.settings.table)。

调用`app.set('foo', true)`布尔属性与调用相同 `app.enable('foo')`。同样，调用`app.set('foo', false)`布尔属性与调用相同`app.disable('foo')`。

使用 检索设置的值[`app.get()`](https://www.expressjs.com.cn/4x/api.html#app.get)。

```javascript
app.set('title', 'My Site')
app.get('title') // "My Site"
```

#### 应用程序设置

下表列出了应用程序设置。

请注意，子应用程序将：

- 不继承具有默认值的设置值。您必须在子应用程序中设置该值。
- 继承设置的值，没有默认值；这些在下表中明确指出。

例外：子应用将继承 的值，`trust proxy`即使它具有默认值（为了向后兼容）；子应用不会继承`view cache`in production 的值（什么时候`NODE_ENV`是“production”）。

| 财产                     | 类型         | 描述                                                         | 默认                                                         |
| ------------------------ | ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `case sensitive routing` | 布尔值       | 启用区分大小写。启用后，“/Foo”和“/foo”是不同的路由。禁用时，“/Foo”和“/foo”被视为相同。**注意**：子应用将继承此设置的值。 | 不适用（未定义）                                             |
| `env`                    | 细绳         | 环境模式。一定要在生产环境中设置为“生产”；请参阅[生产最佳实践：性能和可靠性](https://www.expressjs.com.cn/advanced/best-practice-performance.html#env)。 | `process.env.NODE_ENV`（`NODE_ENV`环境变量）或“开发”如果`NODE_ENV`未设置。 |
| `etag`                   | 多变         | 设置 ETag 响应标头。有关可能的值，请参阅[`etag`选项表](https://www.expressjs.com.cn/4x/api.html#etag.options.table)。[有关 HTTP ETag 标头的更多信息](http://en.wikipedia.org/wiki/HTTP_ETag)。 | `weak`                                                       |
| `jsonp callback name`    | 细绳         | 指定默认 JSONP 回调名称。                                    | “打回来”                                                     |
| `json escape`            | 布尔值       | 启用从 、 和 API 转义`res.json`JSON`res.jsonp`响应`res.send`。这会将字符`<`、`>`和`&`转义为 JSON 中的 Unicode 转义序列。这样做的目的是在客户端嗅探 HTML 响应时帮助[减轻某些类型的持久性 XSS 攻击。](https://blog.mozilla.org/security/2017/07/18/web-service-audits-firefox-accounts/)**注意**：子应用将继承此设置的值。 | 不适用（未定义）                                             |
| `json replacer`          | 多变         | [`JSON.stringify` 使用](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify#The_replacer_parameter)的'replacer' 参数。**注意**：子应用将继承此设置的值。 | 不适用（未定义）                                             |
| `json spaces`            | 多变         | [`JSON.stringify` 使用](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify#The_space_argument)的'space' 参数。这通常设置为用于缩进美化 JSON 的空格数。**注意**：子应用将继承此设置的值。 | 不适用（未定义）                                             |
| `query parser`           | 多变         | 通过将值设置为 禁用查询解析`false`，或将查询解析器设置为使用“简单”或“扩展”或自定义查询字符串解析功能。简单查询解析器基于 Node 的本机查询解析器[querystring](http://nodejs.org/api/querystring.html)。扩展查询解析器基于[qs](https://www.npmjs.org/package/qs)。自定义查询字符串解析函数将接收完整的查询字符串，并且必须返回查询键及其值的对象。 | “扩展”                                                       |
| `strict routing`         | 布尔值       | 启用严格路由。启用后，路由器将“/foo”和“/foo/”视为不同。否则，路由器将“/foo”和“/foo/”视为相同。**注意**：子应用将继承此设置的值。 | 不适用（未定义）                                             |
| `subdomain offset`       | 数字         | 要删除以访问子域的主机的点分隔部分的数量。                   | 2                                                            |
| `trust proxy`            | 多变         | 指示应用程序位于前端代理之后，并使用`X-Forwarded-*`标头来确定客户端的连接和 IP 地址。注意：`X-Forwarded-*`标头很容易被欺骗，并且检测到的 IP 地址不可靠。启用后，Express 会尝试确定通过前端代理或一系列代理连接的客户端的 IP 地址。`req.ips` 属性，然后包含客户端连接通过的 IP 地址数组。要启用它，请使用[信任代理选项表](https://www.expressjs.com.cn/4x/api.html#trust.proxy.options.table)中描述的值。`trust proxy` 设置是使用[proxy-addr](https://www.npmjs.org/package/proxy-addr)包实现的。有关更多信息，请参阅其文档。**注意**：子应用程序*将*继承此设置的值，即使它具有默认值。 | `false`（已禁用）                                            |
| `views`                  | 字符串或数组 | 应用程序视图的目录或目录数组。如果是数组，则按照它们在数组中出现的顺序查找视图。 | `process.cwd() + '/views'`                                   |
| `view cache`             | 布尔值       | 启用视图模板编译缓存。**注意**：子应用在生产中不会继承此设置的值（当 `NODE_ENV` 为“生产”时）。 | `true`在生产中，否则未定义。                                 |
| `view engine`            | 细绳         | 省略时使用的默认引擎扩展。**注意**：子应用将继承此设置的值。 | 不适用（未定义）                                             |
| `x-powered-by`           | 布尔值       | 启用“X-Powered-By: Express”HTTP 标头。                       | `true`                                                       |

##### `trust proxy` 设置的选项

阅读[代理背后的 Express](https://www.expressjs.com.cn/guide/behind-proxies.html)以获取更多信息。

| 类型                                      | 价值                                                         |
| ----------------------------------------- | ------------------------------------------------------------ |
| 布尔值                                    | 如果`true`，则客户端的 IP 地址被理解为标头中最左侧的条目`X-Forwarded-*`。如果`false`，则该应用程序被理解为直接面向 Internet 并且客户端的 IP 地址来源于`req.connection.remoteAddress`。这是默认设置。 |
| 字符串 包含逗号分隔值 的字符串 字符串数组 | 要信任的 IP 地址、子网或 IP 地址数组和子网。预配置的子网名称为：环回 - `127.0.0.1/8`,`::1/128`链接本地 - `169.254.0.0/16`,`fe80::/10`uniquelocal - `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`,`fc00::/7`通过以下任一方式设置 IP 地址：指定单个子网：`app.set('trust proxy', 'loopback') `指定子网和地址：`app.set('trust proxy', 'loopback, 123.123.123.123') `将多个子网指定为 CSV：`app.set('trust proxy', 'loopback, linklocal, uniquelocal') `将多个子网指定为数组：`app.set('trust proxy', ['loopback', 'linklocal', 'uniquelocal']) `指定时，IP 地址或子网将被排除在地址确定过程之外，并将离应用服务器最近的不受信任的 IP 地址确定为客户端的 IP 地址。 |
| 数字                                      | 信任来自前端代理服务器的第*n*个跃点作为客户端。              |
| 功能                                      | 自定义信任实现。仅当您知道自己在做什么时才使用它。`app.set('trust proxy', function (ip) {   if (ip === '127.0.0.1' || ip === '123.123.123.123') return true // trusted IPs   else return false }) ` |

##### `etag` 设置的选项

**注意**：这些设置仅适用于动态文件，不适用于静态文件。[express.static](https://www.expressjs.com.cn/4x/api.html#express.static)中间件忽略这些设置 。

ETag 功能是使用 [etag](https://www.npmjs.org/package/etag)包实现的。有关更多信息，请参阅其文档。

| 类型   | 价值                                                         |
| ------ | ------------------------------------------------------------ |
| 布尔值 | `true`启用弱 ETag。这是默认设置。 `false`完全禁用 ETag。     |
| 细绳   | 如果为“强”，则启用强 ETag。 如果“弱”，则启用弱 ETag。        |
| 功能   | 自定义 ETag 函数实现。仅当您知道自己在做什么时才使用它。`app.set('etag', function (body, encoding) {   return generateHash(body, encoding) // consider the function is defined }) ` |

### app.use([路径,]回调[,回调...])

在指定路径挂载指定的[中间件](https://www.expressjs.com.cn/guide/using-middleware.html)函数或函数：中间件函数在请求路径的基匹配时执行`path`。

#### 论据

| 争论       | 描述                                                         | 默认          |
| ---------- | ------------------------------------------------------------ | ------------- |
| `path`     | 调用中间件函数的路径；可以是以下任何一种：表示路径的字符串。路径模式。匹配路径的正则表达式模式。以上任何一种组合的数组。有关示例，请参阅[路径示例](https://www.expressjs.com.cn/4x/api.html#path-examples)。 | '/'（根路径） |
| `callback` | 回调函数；可：一个中间件功能。一系列中间件功能（以逗号分隔）。一组中间件函数。以上所有的组合。您可以提供多个回调函数，其行为类似于中间件，但这些回调可以调用`next('route')`以绕过剩余的路由回调。您可以使用此机制对路由施加先决条件，然后如果没有理由继续当前路由，则将控制权传递给后续路由。由于[路由器](https://www.expressjs.com.cn/4x/api.html#router)和[应用程序](https://www.expressjs.com.cn/4x/api.html#application)实现了中间件接口，因此您可以像使用任何其他中间件功能一样使用它们。有关示例，请参阅[中间件回调函数示例](https://www.expressjs.com.cn/4x/api.html#middleware-callback-function-examples)。 | 没有任何      |

#### 描述

路由将匹配紧随其路径的任何路径，并带有“ `/`”。例如：`app.use('/apple', ...)`将匹配“/apple”、“/apple/images”、“/apple/images/news”等。

由于`path`默认为“/”，对于应用程序的每个请求，都会执行没有路径安装的中间件。
例如，这个中间件函数将为应用程序的*每个*请求执行：

```javascript
app.use(function (req, res, next) {
  console.log('Time: %d', Date.now())
  next()
})
```

**笔记**

子应用程序将：

- 不继承具有默认值的设置值。您必须在子应用程序中设置该值。
- 继承设置的值，没有默认值。

有关详细信息，请参阅[应用程序设置](https://www.expressjs.com.cn/en/4x/api.html#app.settings.table)。

中间件功能是按顺序执行的，因此中间件包含的顺序很重要。

```javascript
// this middleware will not allow the request to go beyond it
app.use(function (req, res, next) {
  res.send('Hello World')
})

// requests will never reach this route
app.get('/', function (req, res) {
  res.send('Welcome')
})
```

**错误处理中间件**

错误处理中间件总是需要*四个*参数。您必须提供四个参数以将其标识为错误处理中间件函数。即使您不需要使用该`next`对象，您也必须指定它来维护签名。否则，该`next`对象将被解释为常规中间件并且无法处理错误。有关错误处理中间件的详细信息，请参阅：[错误处理](https://www.expressjs.com.cn/en/guide/error-handling.html)。

以与其他中间件函数相同的方式定义错误处理中间件函数，除了使用四个参数而不是三个参数，特别是使用签名`(err, req, res, next)`)：

```javascript
app.use(function (err, req, res, next) {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})
```

#### 路径示例

下表提供了一些`path`用于挂载中间件的有效值的简单示例。

| 类型       | 例子                                                         |
| ---------- | ------------------------------------------------------------ |
| 小路       | 这将匹配以 开头的路径`/abcd`：`app.use('/abcd', function (req, res, next) {   next() }) ` |
| 路径模式   | `/abcd`这将匹配以and开头的路径`/abd`：`app.use('/abc?d', function (req, res, next) {   next() }) ``/abcd`这将匹配以、`/abbcd`、等开头的路径`/abbbbbcd`：`app.use('/ab+cd', function (req, res, next) {   next() }) ``/abcd`这将匹配以, `/abxcd`, `/abFOOcd`,等开头的路径`/abbArcd`：`app.use('/ab*cd', function (req, res, next) {   next() }) ``/ad`这将匹配以and开头的路径`/abcd`：`app.use('/a(bc)?d', function (req, res, next) {   next() }) ` |
| 正则表达式 | `/abc`这将匹配以and开头的路径`/xyz`：`app.use(/\/abc|\/xyz/, function (req, res, next) {   next() }) ` |
| 大批       | `/abcd`这将匹配以、`/xyza`、`/lmn`和开头的路径`/pqr`：`app.use(['/abcd', '/xyza', /\/lmn|\/pqr/], function (req, res, next) {   next() }) ` |

#### 中间件回调函数示例

下表提供了可用作 、 和 的参数的中间件函数的一些简单`callback`示例。即使这些示例适用于，它们也适用于、和。`app.use()``app.METHOD()``app.all()``app.use()``app.use()``app.METHOD()``app.all()`

| 用法       | 例子                                                         |
| ---------- | ------------------------------------------------------------ |
| 单一中间件 | 您可以在本地定义和挂载中间件函数。`app.use(function (req, res, next) {   next() }) `路由器是有效的中间件。`var router = express.Router() router.get('/', function (req, res, next) {   next() }) app.use(router) `Express 应用程序是有效的中间件。`var subApp = express() subApp.get('/', function (req, res, next) {   next() }) app.use(subApp) ` |
| 系列中间件 | 您可以在同一挂载路径中指定多个中间件函数。`var r1 = express.Router() r1.get('/', function (req, res, next) {   next() })  var r2 = express.Router() r2.get('/', function (req, res, next) {   next() })  app.use(r1, r2) ` |
| 大批       | 使用数组对中间件进行逻辑分组。`var r1 = express.Router() r1.get('/', function (req, res, next) {   next() })  var r2 = express.Router() r2.get('/', function (req, res, next) {   next() })  app.use([r1, r2]) ` |
| 组合       | 您可以结合上述所有挂载中间件的方式。`function mw1 (req, res, next) { next() } function mw2 (req, res, next) { next() }  var r1 = express.Router() r1.get('/', function (req, res, next) { next() })  var r2 = express.Router() r2.get('/', function (req, res, next) { next() })  var subApp = express() subApp.get('/', function (req, res, next) { next() })  app.use(mw1, [mw2, r1, r2], subApp) ` |

[以下是在 Express 应用程序中使用express.static](https://www.expressjs.com.cn/guide/using-middleware.html#middleware.built-in) 中间件的一些示例。

从应用程序目录中的“公共”目录为应用程序提供静态内容：

```javascript
// GET /style.css etc
app.use(express.static(path.join(__dirname, 'public')))
```

仅当请求路径以“/static”为前缀时，将中间件安装在“/static”以提供静态内容：

```javascript
// GET /static/style.css etc.
app.use('/static', express.static(path.join(__dirname, 'public')))
```

通过在静态中间件之后加载记录器中间件来禁用静态内容请求的日志记录：

```javascript
app.use(express.static(path.join(__dirname, 'public')))
app.use(logger())
```

提供来自多个目录的静态文件，但“./public”优先于其他目录：

```javascript
app.use(express.static(path.join(__dirname, 'public')))
app.use(express.static(path.join(__dirname, 'files')))
app.use(express.static(path.join(__dirname, 'uploads')))
```

## 要求

该`req`对象表示 HTTP 请求，并具有请求查询字符串、参数、正文、HTTP 标头等的属性。在本文档中，按照惯例，该对象始终称为`req`（并且 HTTP 响应为`res`），但其实际名称由您正在使用的回调函数的参数确定。

例如：

```javascript
app.get('/user/:id', function (req, res) {
  res.send('user ' + req.params.id)
})
```

但你也可以拥有：

```javascript
app.get('/user/:id', function (request, response) {
  response.send('user ' + request.params.id)
})
```

该`req`对象是 Node 自己的请求对象的增强版，支持所有[内置的字段和方法](https://nodejs.org/api/http.html#http_class_http_incomingmessage)。

### 特性

在 Express 4 中，默认情况下`req.files`不再在对象上可用。`req`要访问`req.files`对象上上传的文件，请使用多部分处理中间件，例如[busboy](https://www.npmjs.com/package/busboy)、[multer](https://www.npmjs.com/package/multer)、 [formidable](https://www.npmjs.com/package/formidable)、 [multiparty](https://www.npmjs.com/package/multiparty)、 [connect-multiparty](https://www.npmjs.com/package/connect-multiparty)或[pez](https://www.npmjs.com/package/pez)。

### req.app

此属性包含对使用中间件的 Express 应用程序实例的引用。

如果您遵循创建仅导出中间件函数并将`require()`其导出到主文件中的模块的模式，则中间件可以通过以下方式访问 Express 实例`req.app`

例如：

```javascript
// index.js
app.get('/viewdirectory', require('./mymiddleware.js'))
// mymiddleware.js
module.exports = function (req, res) {
  res.send('The views directory is ' + req.app.get('views'))
}
```

### req.baseUrl

安装路由器实例的 URL 路径。

该`req.baseUrl`属性类似于对象的[mountpath](https://www.expressjs.com.cn/4x/api.html#app.mountpath)属性`app`，除了`app.mountpath`返回匹配的路径模式。

例如：

```javascript
var greet = express.Router()

greet.get('/jp', function (req, res) {
  console.log(req.baseUrl) // /greet
  res.send('Konichiwa!')
})

app.use('/greet', greet) // load the router on '/greet'
```

即使您使用路径模式或一组路径模式来加载路由器，该`baseUrl`属性也会返回匹配的字符串，而不是模式。在以下示例中，`greet`路由器加载在两个路径模式上。

```javascript
app.use(['/gre+t', '/hel{2}o'], greet) // load the router on '/gre+t' and '/hel{2}o'
```

当向 发出请求时`/greet/jp`，`req.baseUrl`是“/greet”。当向 发出请求时`/hello/jp`，`req.baseUrl`是“/hello”。

### 请求正文

包含在请求正文中提交的数据键值对。默认情况下，它是`undefined`，并且在您使用主体解析中间件（例如[`express.json()`](https://www.expressjs.com.cn/4x/api.html#express.json)或）时填充[`express.urlencoded()`](https://www.expressjs.com.cn/4x/api.html#express.urlencoded)。

由于`req.body`的形状基于用户控制的输入，因此该对象中的所有属性和值都是不受信任的，应该在信任之前进行验证。例如，`req.body.foo.toString()`可能以多种方式失败，例如`foo`可能不存在或可能不是字符串，并且`toString`可能不是函数而是字符串或其他用户输入。

下面的例子展示了如何使用 body-parsing 中间件来填充`req.body`.

```javascript
var express = require('express')

var app = express()

app.use(express.json()) // for parsing application/json
app.use(express.urlencoded({ extended: true })) // for parsing application/x-www-form-urlencoded

app.post('/profile', function (req, res, next) {
  console.log(req.body)
  res.json(req.body)
})
```

### 请求.cookies

使用[cookie-parser](https://www.npmjs.com/package/cookie-parser)中间件时，该属性是一个包含请求发送的 cookie 的对象。如果请求不包含 cookie，则默认为`{}`.

```javascript
// Cookie: name=tj
console.dir(req.cookies.name)
// => 'tj'
```

如果 cookie 已签名，则必须使用[req.signedCookies](https://www.expressjs.com.cn/4x/api.html#req.signedCookies)。

有关更多信息、问题或疑虑，请参阅[cookie-parser](https://github.com/expressjs/cookie-parser)。

### req.fresh

当客户端缓存中的响应仍然“新鲜”时`true`返回，否则`false`返回以指示客户端缓存现在已过时并且应该发送完整的响应。

当客户端发送`Cache-Control: no-cache`请求头以指示端到端重新加载请求时，该模块将返回`false`以使处理这些请求变得透明。

有关缓存验证如何工作的更多详细信息，请参阅 [HTTP/1.1 缓存规范](https://tools.ietf.org/html/rfc7234)。

```javascript
console.dir(req.fresh)
// => true
```

### 请求主机名

`Host`包含从HTTP 标头派生的主机名。

当[`trust proxy`设置](https://www.expressjs.com.cn/4x/api.html#trust.proxy.options.table) 未计算为 时`false`，此属性将改为从`X-Forwarded-Host`标头字段中获取值。此标头可以由客户端或代理设置。

如果请求中有多个`X-Forwarded-Host`标头，则使用第一个标头的值。这包括一个带有逗号分隔值的标头，其中使用了第一个值。

在 Express v4.17.0 之前，`X-Forwarded-Host`不能包含多个值或多次出现。

```javascript
// Host: "example.com:3000"
console.dir(req.hostname)
// => 'example.com'
```

### 请求.ip

包含请求的远程 IP 地址。

当[`trust proxy`设置](https://www.expressjs.com.cn/4x/api.html#trust.proxy.options.table)未计算为`false`时，此属性的值派生自标头中最左侧的条目 `X-Forwarded-For`。此标头可以由客户端或代理设置。

```javascript
console.dir(req.ip)
// => '127.0.0.1'
```

### 请求.ips

当[`trust proxy`设置](https://www.expressjs.com.cn/4x/api.html#trust.proxy.options.table)未计算为 时，此属性包含请求标头`false`中指定的 IP 地址数组。`X-Forwarded-For`否则，它包含一个空数组。此标头可以由客户端或代理设置。

例如，如果`X-Forwarded-For`是`client, proxy1, proxy2`，`req.ips`将是 ，最下游`["client", "proxy1", "proxy2"]`在哪里。`proxy2`

### 请求方法

包含与请求的 HTTP 方法对应的字符串： `GET`、`POST`、`PUT`等。

### req.originalUrl

`req.url`不是原生的 Express 属性，它继承自 Node 的[http 模块](https://nodejs.org/api/http.html#http_message_url)。

这个属性很像`req.url`；但是，它保留了原始请求 URL，允许您`req.url`出于内部路由目的自由重写。例如，[app.use()](https://www.expressjs.com.cn/4x/api.html#app.use)的“挂载”功能将重写`req.url`以剥离挂载点。

```javascript
// GET /search?q=something
console.dir(req.originalUrl)
// => '/search?q=something'
```

`req.originalUrl`在中间件和路由器对象中都可用，并且是 和 的`req.baseUrl`组合`req.url`。考虑以下示例：

```javascript
app.use('/admin', function (req, res, next) { // GET 'http://www.example.com/admin/new?sort=desc'
  console.dir(req.originalUrl) // '/admin/new?sort=desc'
  console.dir(req.baseUrl) // '/admin'
  console.dir(req.path) // '/new'
  next()
})
```

### 请求参数

该属性是一个包含映射到[命名路由“参数”](https://www.expressjs.com.cn/en/guide/routing.html#route-parameters)的属性的对象。例如，如果您有 route `/user/:name`，则“name”属性可用作`req.params.name`。此对象默认为`{}`.

```javascript
// GET /user/tj
console.dir(req.params.name)
// => 'tj'
```

当您对路由定义使用正则表达式时，捕获组在数组中使用 提供`req.params[n]`，其中`n`是第 n个捕获组。此规则适用于带有字符串路由的未命名通配符匹配，例如`/file/*`：

```javascript
// GET /file/javascripts/jquery.js
console.dir(req.params[0])
// => 'javascripts/jquery.js'
```

如果您需要更改 中的键`req.params`，请使用[app.param](https://www.expressjs.com.cn/en/4x/api.html#app.param)处理程序。更改仅适用于已在路由路径中定义的[参数。](https://www.expressjs.com.cn/en/guide/routing.html#route-parameters)

`req.params`对中间件或路由处理程序中的对象所做的任何更改都将被重置。

注意：Express 自动解码`req.params`（使用`decodeURIComponent`）中的值。

### 请求路径

包含请求 URL 的路径部分。

```javascript
// example.com/users?sort=desc
console.dir(req.path)
// => '/users'
```

从中间件调用时，挂载点不包含在`req.path`. 有关更多详细信息，请参阅[app.use()](https://www.expressjs.com.cn/4x/api.html#app.use)。

### 请求协议

包含请求协议字符串：要么`http`或（对于 TLS 请求）`https`。

当[`trust proxy`设置](https://www.expressjs.com.cn/4x/api.html#trust.proxy.options.table)未计算为 时`false`，此属性将使用`X-Forwarded-Proto`标头字段的值（如果存在）。此标头可以由客户端或代理设置。

```javascript
console.dir(req.protocol)
// => 'http'
```

### 请求查询

此属性是一个对象，其中包含路由中每个查询字符串参数的属性。当[查询解析器](https://www.expressjs.com.cn/4x/api.html#app.settings.table)设置为禁用时，它是一个空对象`{}`，否则它是配置的查询解析器的结果。

由于`req.query`的形状基于用户控制的输入，因此该对象中的所有属性和值都是不受信任的，应该在信任之前进行验证。例如，`req.query.foo.toString()`可能以多种方式失败，例如`foo`可能不存在或可能不是字符串，并且`toString`可能不是函数而是字符串或其他用户输入。

### 请求资源

此属性包含对 与此请求对象相关的[响应对象的引用。](https://www.expressjs.com.cn/4x/api.html#res)

### 请求路由

包含当前匹配的路由，一个字符串。例如：

```javascript
app.get('/user/:id?', function userIdHandler (req, res) {
  console.log(req.route)
  res.send('GET')
})
```

上一个片段的示例输出：

```
{ path: '/user/:id?',
  stack:
   [ { handle: [Function: userIdHandler],
       name: 'userIdHandler',
       params: undefined,
       path: undefined,
       keys: [],
       regexp: /^\/?$/i,
       method: 'get' } ],
  methods: { get: true } }
```

### req.secure

如果建立了 TLS 连接，则为 true 的布尔属性。相当于：

```javascript
console.dir(req.protocol === 'https')
// => true
```

### req.signedCookies

使用[cookie-parser](https://www.npmjs.com/package/cookie-parser)中间件时，此属性包含请求发送的已签名 cookie，未签名且可供使用。签名的 cookie 驻留在不同的对象中以显示开发人员的意图；否则，可能会对 `req.cookie`值进行恶意攻击（这很容易被欺骗）。请注意，签署 cookie 不会使其“隐藏”或加密；但只是防止篡改（因为用于签名的秘密是私人的）。

如果未发送签名 cookie，则该属性默认为`{}`.

```javascript
// Cookie: user=tobi.CP7AWaXDfAKIRfH49dQzKJx7sKzzSoPq7/AcBBRVwlI3
console.dir(req.signedCookies.user)
// => 'tobi'
```

有关更多信息、问题或疑虑，请参阅[cookie-parser](https://github.com/expressjs/cookie-parser)。

### req.stale

指示请求是否“过时”，与`req.fresh`. 有关更多信息，请参阅[req.fresh](https://www.expressjs.com.cn/4x/api.html#req.fresh)。

```javascript
console.dir(req.stale)
// => true
```

### 请求子域

请求域名中的子域数组。

```javascript
// Host: "tobi.ferrets.example.com"
console.dir(req.subdomains)
// => ['ferrets', 'tobi']
```

应用程序属性`subdomain offset`，默认为 2，用于确定子域段的开始。要更改此行为，请使用[app.set](https://www.expressjs.com.cn/en/4x/api.html#app.set)更改其值。

### 请求.xhr

一个布尔属性，`true`如果请求的`X-Requested-With`标头字段是“XMLHttpRequest”，则表明请求是由客户端库（如 jQuery）发出的。

```javascript
console.dir(req.xhr)
// => true
```

### 方法

### req.accepts(类型)

`Accept`根据请求的HTTP 标头字段检查指定的内容类型是否可接受。该方法返回最佳匹配，或者如果指定的内容类型都不可接受，则返回 `false`（在这种情况下，应用程序应以 响应`406 "Not Acceptable"`）。

该`type`值可以是单个 MIME 类型字符串（例如“application/json”）、扩展名（例如“json”）、逗号分隔的列表或数组。对于列表或数组，该方法返回*最佳*匹配（如果有）。

```javascript
// Accept: text/html
req.accepts('html')
// => "html"

// Accept: text/*, application/json
req.accepts('html')
// => "html"
req.accepts('text/html')
// => "text/html"
req.accepts(['json', 'text'])
// => "json"
req.accepts('application/json')
// => "application/json"

// Accept: text/*, application/json
req.accepts('image/png')
req.accepts('png')
// => false

// Accept: text/*;q=.5, application/json
req.accepts(['html', 'json'])
// => "json"
```

如需更多信息，或者如果您有问题或疑虑，请参阅[接受](https://github.com/expressjs/accepts)。

### req.acceptsCharsets(charset [, ...])

根据请求的`Accept-Charset`HTTP 标头字段返回指定字符集的第一个接受的字符集。如果不接受任何指定的字符集，则返回`false`.

如需更多信息，或者如果您有问题或疑虑，请参阅[接受](https://github.com/expressjs/accepts)。

### req.acceptsEncodings(编码 [, ...])

`Accept-Encoding`根据请求的HTTP 标头字段，返回指定编码的第一个接受的编码。如果不接受任何指定的编码，则返回`false`.

如需更多信息，或者如果您有问题或疑虑，请参阅[接受](https://github.com/expressjs/accepts)。

### req.acceptsLanguages(lang [, ...])

`Accept-Language`根据请求的HTTP 标头字段，返回指定语言的第一个接受的语言。如果不接受任何指定的语言，则返回`false`。

如需更多信息，或者如果您有问题或疑虑，请参阅[接受](https://github.com/expressjs/accepts)。

### req.get(字段)

返回指定的 HTTP 请求头字段（不区分大小写的匹配）。`Referrer`和`Referer`字段是可互换的。

```javascript
req.get('Content-Type')
// => "text/plain"

req.get('content-type')
// => "text/plain"

req.get('Something')
// => undefined
```

别名为`req.header(field)`.

### req.is(类型)

如果传入请求的“Content-Type”HTTP 标头字段与参数指定的 MIME 类型匹配，则返回匹配的内容类型`type`。如果请求没有正文，则返回`null`。`false`否则返回。

```javascript
// With Content-Type: text/html; charset=utf-8
req.is('html')
// => 'html'
req.is('text/html')
// => 'text/html'
req.is('text/*')
// => 'text/*'

// When Content-Type is application/json
req.is('json')
// => 'json'
req.is('application/json')
// => 'application/json'
req.is('application/*')
// => 'application/*'

req.is('html')
// => false
```

有关更多信息，或者如果您有问题或疑虑，请参阅[type-is](https://github.com/expressjs/type-is)。

### req.param(name [, defaultValue])

已弃用。根据需要使用`req.params`或。`req.body``req.query`

存在时返回 param 的值`name`。

```javascript
// ?name=tobi
req.param('name')
// => "tobi"

// POST name=tobi
req.param('name')
// => "tobi"

// /user/tobi for /user/:name
req.param('name')
// => "tobi"
```

查找按以下顺序执行：

- `req.params`
- `req.body`
- `req.query`

`defaultValue`或者，如果在任何请求对象中都找不到参数，您可以指定设置默认值。

为清楚起见，应优先使用直接访问`req.body`、`req.params`和—— 除非您真正接受来自每个对象的输入。`req.query`

必须加载正文解析中间件才能`req.param()`以可预测的方式工作。有关详细信息，请参阅[req.body](https://www.expressjs.com.cn/4x/api.html#req.body)。

### req.range(大小[, 选项])

`Range`头解析器。

该`size`参数是资源的最大大小。

`options`参数是一个可以具有以下属性的对象。

| 财产      | 类型   | 描述                                                         |
| --------- | ------ | ------------------------------------------------------------ |
| `combine` | 布尔值 | 指定是否应合并重叠和相邻范围，默认为`false`. 当 时`true`，范围将被组合并返回，就好像它们在标题中以这种方式指定一样。 |

将返回一个范围数组或指示解析错误的负数。

- `-2`表示格式错误的标头字符串
- `-1`表示无法满足的范围

```javascript
// parse header from request
var range = req.range(1000)

// the type of the range
if (range.type === 'bytes') {
  // the ranges
  range.forEach(function (r) {
    // do something with r.start and r.end
  })
}
```

## 回复

该`res`对象表示 Express 应用程序在收到 HTTP 请求时发送的 HTTP 响应。

在本文档中，按照惯例，该对象始终称为`res`（并且 HTTP 请求是`req`），但其实际名称由您正在使用的回调函数的参数确定。

例如：

```javascript
app.get('/user/:id', function (req, res) {
  res.send('user ' + req.params.id)
})
```

但你也可以拥有：

```javascript
app.get('/user/:id', function (request, response) {
  response.send('user ' + request.params.id)
})
```

该`res`对象是 Node 自己的响应对象的增强版，支持所有[内置的字段和方法](https://nodejs.org/api/http.html#http_class_http_serverresponse)。

### 特性

### res.app

此属性包含对使用中间件的 Express 应用程序实例的引用。

`res.app`[与请求对象中的req.app](https://www.expressjs.com.cn/4x/api.html#req.app)属性相同。

### res.headersSent

指示应用程序是否为响应发送 HTTP 标头的布尔属性。

```javascript
app.get('/', function (req, res) {
  console.dir(res.headersSent) // false
  res.send('OK')
  console.dir(res.headersSent) // true
})
```

### res.locals

一个对象，其中包含范围为请求的响应局部变量，因此仅可用于在该请求/响应周期（如果有）期间呈现的视图。否则，此属性与[app.locals](https://www.expressjs.com.cn/4x/api.html#app.locals)相同。

此属性对于公开请求级信息（例如请求路径名、经过身份验证的用户、用户设置等）很有用。

```javascript
app.use(function (req, res, next) {
  res.locals.user = req.user
  res.locals.authenticated = !req.user.anonymous
  next()
})
```

### 方法

### res.append（字段 [，值]）

`res.append()`Express v4.11.0+ 支持

将指定附加`value`到 HTTP 响应标头`field`。如果尚未设置标头，则会创建具有指定值的标头。参数可以是`value`字符串或数组。

注意：调用`res.set()`after`res.append()`将重置先前设置的标头值。

```javascript
res.append('Link', ['<http://localhost/>', '<http://localhost:3000/>'])
res.append('Set-Cookie', 'foo=bar; Path=/; HttpOnly')
res.append('Warning', '199 Miscellaneous warning')
```

### res.attachment([文件名])

将 HTTP 响应`Content-Disposition`头字段设置为“附件”。如果`filename`给定了 a ，那么它会根据扩展名通过 设置 Content-Type `res.type()`，并设置`Content-Disposition`“filename=”参数。

```javascript
res.attachment()
// Content-Disposition: attachment

res.attachment('path/to/logo.png')
// Content-Disposition: attachment; filename="logo.png"
// Content-Type: image/png
```

### res.cookie（名称，值 [，选项]）

将cookie 设置`name`为`value`. `value`参数可以是字符串或转换为 JSON 的对象。

`options`参数是一个可以具有以下属性的对象。

| 财产       | 类型           | 描述                                                         |
| ---------- | -------------- | ------------------------------------------------------------ |
| `domain`   | 细绳           | cookie 的域名。默认为应用的域名。                            |
| `encode`   | 功能           | 用于 cookie 值编码的同步函数。默认为`encodeURIComponent`.    |
| `expires`  | 日期           | 格林威治标准时间 cookie 的到期日期。如果未指定或设置为 0，则创建会话 cookie。 |
| `httpOnly` | 布尔值         | 将 cookie 标记为只能由 Web 服务器访问。                      |
| `maxAge`   | 数字           | 方便的选项，用于设置相对于当前时间的到期时间（以毫秒为单位）。 |
| `path`     | 细绳           | cookie 的路径。默认为“/”。                                   |
| `secure`   | 布尔值         | 将 cookie 标记为仅与 HTTPS 一起使用。                        |
| `signed`   | 布尔值         | 指示是否应该对 cookie 进行签名。                             |
| `sameSite` | 布尔值或字符串 | “SameSite” **Set-Cookie**属性的值。更多信息，请访问<https://tools.ietf.org/html/draft-ietf-httpbis-cookie-same-site-00#section-4.1.1>。 |

所做的只是使用提供的选项设置`res.cookie()`HTTP标头。`Set-Cookie`任何未指定的选项默认为[RFC 6265](http://tools.ietf.org/html/rfc6265)中规定的值。

例如：

```javascript
res.cookie('name', 'tobi', { domain: '.example.com', path: '/admin', secure: true })
res.cookie('rememberme', '1', { expires: new Date(Date.now() + 900000), httpOnly: true })
```

您可以通过多次调用在单个响应中设置多个 cookie `res.cookie`，例如：

```javascript
res
  .status(201)
  .cookie('access_token', 'Bearer ' + token, {
    expires: new Date(Date.now() + 8 * 3600000) // cookie will be removed after 8 hours
  })
  .cookie('test', 'test')
  .redirect(301, '/admin')
```

该`encode`选项允许您选择用于 cookie 值编码的函数。不支持异步函数。

示例用例：您需要为组织中的另一个站点设置域范围的 cookie。此其他站点（不受您的管理控制）不使用 URI 编码的 cookie 值。

```javascript
// Default encoding
res.cookie('some_cross_domain_cookie', 'http://mysubdomain.example.com', { domain: 'example.com' })
// Result: 'some_cross_domain_cookie=http%3A%2F%2Fmysubdomain.example.com; Domain=example.com; Path=/'

// Custom encoding
res.cookie('some_cross_domain_cookie', 'http://mysubdomain.example.com', { domain: 'example.com', encode: String })
// Result: 'some_cross_domain_cookie=http://mysubdomain.example.com; Domain=example.com; Path=/;'
```

该`maxAge`选项是一个方便的选项，用于设置相对于当前时间的“过期”（以毫秒为单位）。以下等效于上面的第二个示例。

```javascript
res.cookie('rememberme', '1', { maxAge: 900000, httpOnly: true })
```

您可以传递一个对象作为`value`参数；然后将其序列化为 JSON 并由`bodyParser()`中间件解析。

```javascript
res.cookie('cart', { items: [1, 2, 3] })
res.cookie('cart', { items: [1, 2, 3] }, { maxAge: 900000 })
```

当使用[cookie-parser](https://www.npmjs.com/package/cookie-parser)中间件时，该方法还支持签名的 cookie。只需将`signed`选项设置为`true`. 然后`res.cookie()`将使用传递给的秘密`cookieParser(secret)`对值进行签名。

```javascript
res.cookie('name', 'tobi', { signed: true })
```

稍后您可以通过[req.signedCookie](https://www.expressjs.com.cn/4x/api.html#req.signedCookies)对象访问此值。

### res.clearCookie（名称 [，选项]）

清除 指定的 cookie `name`。有关`options`对象的详细信息，请参阅[res.cookie()](https://www.expressjs.com.cn/4x/api.html#res.cookie)。

Web 浏览器和其他兼容的客户端只会在给定的 cookie 与[res.cookie()](https://www.expressjs.com.cn/4x/api.html#res.cookie)`options`相同的情况下清除 cookie ，不包括 and 。`expires``maxAge`

```javascript
res.cookie('name', 'tobi', { path: '/admin' })
res.clearCookie('name', { path: '/admin' })
```

### res.download(路径 [, 文件名] [, 选项] [, fn])

`options`Express v4.16.0 及更高版本支持可选参数。

将文件`path`作为“附件”传输。通常，浏览器会提示用户下载。默认情况下，`Content-Disposition`标题“filename=”参数是`path`（这通常出现在浏览器对话框中）。使用参数覆盖此默认值`filename`。

当发生错误或传输完成时，该方法调用可选的回调函数`fn`。此方法使用[res.sendFile()](https://www.expressjs.com.cn/4x/api.html#res.sendFile)来传输文件。

可选`options`参数传递到底层[res.sendFile()](https://www.expressjs.com.cn/4x/api.html#res.sendFile) 调用，并采用完全相同的参数。

```javascript
res.download('/report-12345.pdf')

res.download('/report-12345.pdf', 'report.pdf')

res.download('/report-12345.pdf', 'report.pdf', function (err) {
  if (err) {
    // Handle error, but keep in mind the response may be partially-sent
    // so check res.headersSent
  } else {
    // decrement a download credit, etc.
  }
})
```

### res.end([数据] [, 编码])

结束响应过程。这个方法其实来自 Node 核心，具体来说[就是 http.ServerResponse 的 response.end() 方法](https://nodejs.org/api/http.html#http_response_end_data_encoding_callback)。

用于在没有任何数据的情况下快速结束响应。如果您需要使用数据进行响应，请改用[res.send()](https://www.expressjs.com.cn/4x/api.html#res.send)和[res.json()](https://www.expressjs.com.cn/4x/api.html#res.json)等方法。

```javascript
res.end()
res.status(404).end()
```

### res.format（对象）

对请求对象的 HTTP 标头执行内容协商`Accept`（如果存在）。它使用[req.accepts()](https://www.expressjs.com.cn/4x/api.html#req.accepts)根据质量值排序的可接受类型为请求选择处理程序。如果未指定标头，则调用第一个回调。当未找到匹配项时，服务器以 406“不可接受”响应，或调用`default`回调。

选择`Content-Type`回调时设置响应标头。但是，您可以在回调中使用`res.set()`或等方法更改它`res.type()`。

以下示例将响应`{ "message": "hey" }`头`Accept`字段设置为“application/json”或“*/json”（但是如果它是“*/*”，则响应将是“hey”）。

```javascript
res.format({
  'text/plain': function () {
    res.send('hey')
  },

  'text/html': function () {
    res.send('<p>hey</p>')
  },

  'application/json': function () {
    res.send({ message: 'hey' })
  },

  default: function () {
    // log the request and respond with 406
    res.status(406).send('Not Acceptable')
  }
})
```

除了规范化的 MIME 类型之外，您还可以使用映射到这些类型的扩展名来实现稍微不那么冗长的实现：

```javascript
res.format({
  text: function () {
    res.send('hey')
  },

  html: function () {
    res.send('<p>hey</p>')
  },

  json: function () {
    res.send({ message: 'hey' })
  }
})
```

### res.get(字段)

返回由 指定的 HTTP 响应标头`field`。匹配不区分大小写。

```javascript
res.get('Content-Type')
// => "text/plain"
```

### res.json([正文])

发送 JSON 响应。[此方法发送一个响应（具有正确的内容类型），该响应是使用JSON.stringify()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)转换为 JSON 字符串的参数。

参数可以是任何 JSON 类型，包括对象、数组、字符串、布尔值、数字或 null，您也可以使用它来将其他值转换为 JSON。

```javascript
res.json(null)
res.json({ user: 'tobi' })
res.status(500).json({ error: 'message' })
```

### res.jsonp([正文])

发送带有 JSONP 支持的 JSON 响应。此方法与 相同`res.json()`，只是它选择加入 JSONP 回调支持。

```javascript
res.jsonp(null)
// => callback(null)

res.jsonp({ user: 'tobi' })
// => callback({ "user": "tobi" })

res.status(500).jsonp({ error: 'message' })
// => callback({ "error": "message" })
```

默认情况下，JSONP 回调名称只是`callback`. [使用jsonp 回调名称](https://www.expressjs.com.cn/4x/api.html#app.settings.table)设置覆盖它 。

以下是使用相同代码的 JSONP 响应的一些示例：

```javascript
// ?callback=foo
res.jsonp({ user: 'tobi' })
// => foo({ "user": "tobi" })

app.set('jsonp callback name', 'cb')

// ?cb=foo
res.status(500).jsonp({ error: 'message' })
// => foo({ "error": "message" })
```

### res.links（链接）

加入`links`作为参数提供的属性以填充响应的 `Link`HTTP 标头字段。

例如，以下调用：

```javascript
res.links({
  next: 'http://api.example.com/users?page=2',
  last: 'http://api.example.com/users?page=5'
})
```

产生以下结果：

```
Link: <http://api.example.com/users?page=2>; rel="next",
      <http://api.example.com/users?page=5>; rel="last"
```

### res.location（路径）

将响应`Location`HTTP 标头设置为指定`path`参数。

```javascript
res.location('/foo/bar')
res.location('http://example.com')
res.location('back')
```

“back”的`path`值有一个特殊的含义，它指`Referer`的是请求头中指定的URL。如果`Referer`没有指定标头，它指的是“/”。

对 URL 进行编码后，如果尚未编码，Express 会将指定的 URL 在`Location`标头中传递给浏览器，而不进行任何验证。

浏览器负责从当前 URL 或引用 URL 以及`Location`标头中指定的 URL 导出预期 URL；并相应地重定向用户。

### res.redirect（[状态，] 路径）

重定向到派生自指定的 URL `path`，指定`status`的正整数对应于[HTTP 状态代码](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)。如果未指定，则`status`默认为“302“找到”。

```javascript
res.redirect('/foo/bar')
res.redirect('http://example.com')
res.redirect(301, 'http://example.com')
res.redirect('../login')
```

重定向可以是用于重定向到不同站点的完全限定 URL：

```javascript
res.redirect('http://google.com')
```

重定向可以相对于主机名的根目录。例如，如果应用程序打开`http://example.com/admin/post/new`，则以下内容将重定向到 URL `http://example.com/admin`：

```javascript
res.redirect('/admin')
```

重定向可以相对于当前 URL。例如，从`http://example.com/blog/admin/`（注意尾部斜杠），以下将重定向到 URL `http://example.com/blog/admin/post/new`。

```javascript
res.redirect('post/new')
```

重定向到`post/new`from `http://example.com/blog/admin`（没有尾部斜杠），将重定向到`http://example.com/blog/post/new`.

如果您发现上述行为令人困惑，请将路径段视为目录（带有尾部斜杠）和文件，这将开始有意义。

路径相关的重定向也是可能的。如果您在 `http://example.com/admin/post/new`，以下内容将重定向到 `http://example.com/admin/post`：

```javascript
res.redirect('..')
```

`back`重定向将请求重定向回引用[者](http://en.wikipedia.org/wiki/HTTP_referer)，默认为`/`引用者丢失时。

```javascript
res.redirect('back')
```

### res.render(view [, locals] [, callback])

渲染 a`view`并将渲染后的 HTML 字符串发送到客户端。可选参数：

- `locals`, 一个对象，其属性定义视图的局部变量。
- `callback`，一个回调函数。如果提供，该方法将返回可能的错误和呈现的字符串，但不执行自动响应。当发生错误时，该方法在`next(err)`内部调用。

参数是一个字符串，它`view`是要渲染的视图文件的文件路径。这可以是绝对路径，也可以是相对于`views`设置的路径。如果路径不包含文件扩展名，则`view engine`设置确定文件扩展名。如果路径确实包含文件扩展名，那么 Express 将加载指定模板引擎的模块（通过）并使用加载的模块的函数`require()`呈现它。`__express`

有关更多信息，请参阅[将模板引擎与 Express 一起使用](https://www.expressjs.com.cn/guide/using-template-engines.html)。

**注意：**该`view`参数执行文件系统操作，例如从磁盘读取文件和评估 Node.js 模块，因此出于安全原因，不应包含来自最终用户的输入。

局部变量`cache`启用视图缓存。设置为`true`, 开发时缓存视图；默认情况下，视图缓存在生产中启用。

```javascript
// send the rendered view to the client
res.render('index')

// if a callback is specified, the rendered HTML string has to be sent explicitly
res.render('index', function (err, html) {
  res.send(html)
})

// pass a local variable to the view
res.render('user', { name: 'Tobi' }, function (err, html) {
  // ...
})
```

### 资源请求

此属性包含对与此响应对象相关的

请求对象

的引用 。

### res.send([正文])

发送 HTTP 响应。

`body`参数可以是`Buffer`对象、a 、`String`对象`Boolean`、或`Array`。例如：

```javascript
res.send(Buffer.from('whoop'))
res.send({ some: 'json' })
res.send('<p>some html</p>')
res.status(404).send('Sorry, we cannot find that!')
res.status(500).send({ error: 'something blew up' })
```

此方法对简单的非流式响应执行许多有用的任务：例如，它自动分配`Content-Length`HTTP 响应头字段（除非先前定义）并提供自动 HEAD 和 HTTP 缓存新鲜度支持。

当参数为`Buffer`对象时，该方法将`Content-Type` 响应头字段设置为“application/octet-stream”，除非之前定义如下所示：

```javascript
res.set('Content-Type', 'text/html')
res.send(Buffer.from('<p>some html</p>'))
```

当参数为 a`String`时，该方法将其设置`Content-Type`为“text/html”：

```javascript
res.send('<p>some html</p>')
```

当参数为`Array`or`Object`时，Express 以 JSON 表示形式响应：

```javascript
res.send({ user: 'tobi' })
res.send([1, 2, 3])
```

### res.sendFile(路径 [, 选项] [, fn])

`res.sendFile()`从 Express v4.8.0 开始支持。

传输给定的文件`path`。`Content-Type`根据文件名的扩展名设置响应 HTTP 标头字段。除非`root`选项在选项对象中设置，否则`path`必须是文件的绝对路径。

此 API 提供对正在运行的文件系统上的数据的访问。确保 (a) 如果`path`参数包含用户输入，则将参数构造为绝对路径的方式是安全的，或者 (b) 将`root`选项设置为目录的绝对路径以包含其中的访问权限。

`root`提供选项时，`path`参数允许为相对路径，包括包含`..`. Express 将验证提供的相对路径`path`是否将在给定`root`选项中解析。

下表提供了有关`options`参数的详细信息。

| 财产           | 描述                                                         | 默认    | 可用性 |
| -------------- | ------------------------------------------------------------ | ------- | ------ |
| `maxAge`       | 以毫秒为单位设置标头的 max-age 属性`Cache-Control`或以[ms 格式设置字符串](https://www.npmjs.org/package/ms) | 0       |        |
| `root`         | 相对文件名的根目录。                                         |         |        |
| `lastModified` | 将`Last-Modified`标题设置为操作系统上文件的最后修改日期。设置`false`为禁用它。 | 启用    | 4.9.0+ |
| `headers`      | 包含与文件一起服务的 HTTP 标头的对象。                       |         |        |
| `dotfiles`     | 提供点文件的选项。可能的值是“允许”、“拒绝”、“忽略”。         | “忽视”  |        |
| `acceptRanges` | 启用或禁用接受范围请求。                                     | `true`  | 4.14+  |
| `cacheControl` | 启用或禁用设置`Cache-Control`响应标头。                      | `true`  | 4.14+  |
| `immutable`    | 启用或禁用响应标头`immutable`中的指令。`Cache-Control`如果启用，`maxAge`还应指定该选项以启用缓存。该`immutable`指令将阻止受支持的客户端在选项的生命周期内发出条件请求`maxAge`以检查文件是否已更改。 | `false` | 4.16+  |

`fn(err)`该方法在传输完成或发生错误时调用回调函数。如果指定了回调函数并且发生错误，则回调函数必须通过结束请求-响应循环或将控制权传递给下一个路由来显式处理响应过程。

这是一个使用`res.sendFile`其所有参数的示例。

```javascript
app.get('/file/:name', function (req, res, next) {
  var options = {
    root: path.join(__dirname, 'public'),
    dotfiles: 'deny',
    headers: {
      'x-timestamp': Date.now(),
      'x-sent': true
    }
  }

  var fileName = req.params.name
  res.sendFile(fileName, options, function (err) {
    if (err) {
      next(err)
    } else {
      console.log('Sent:', fileName)
    }
  })
})
```

以下示例说明了使用 `res.sendFile`为服务文件提供细粒度支持：

```javascript
app.get('/user/:uid/photos/:file', function (req, res) {
  var uid = req.params.uid
  var file = req.params.file

  req.user.mayViewFilesFrom(uid, function (yes) {
    if (yes) {
      res.sendFile('/uploads/' + uid + '/' + file)
    } else {
      res.status(403).send("Sorry! You can't see that.")
    }
  })
})
```

如需更多信息，或者如果您有问题或疑虑，请参阅[发送](https://github.com/pillarjs/send)。

### res.sendStatus（状态码）

将响应 HTTP 状态代码设置为`statusCode`并将注册的状态消息作为文本响应正文发送。如果指定了未知状态代码，则响应正文将只是代码编号。

```javascript
res.sendStatus(404)
```

`res.statusCode`当设置为无效的 HTTP 状态代码（超出`100`to的范围）时，某些版本的 Node.js 会抛出异常`599`。请查阅 HTTP 服务器文档以了解所使用的 Node.js 版本。

[更多关于 HTTP 状态码](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)

### res.set（字段 [，值]）

将响应的 HTTP 标头设置`field`为`value`. 要一次设置多个字段，请将对象作为参数传递。

```javascript
res.set('Content-Type', 'text/plain')

res.set({
  'Content-Type': 'text/plain',
  'Content-Length': '123',
  ETag: '12345'
})
```

别名为`res.header(field [, value])`.

### res.status（代码）

设置响应的 HTTP 状态。它是 Node 的[response.statusCode](http://nodejs.org/api/http.html#http_response_statuscode)的可链接别名。

```javascript
res.status(403).end()
res.status(400).send('Bad Request')
res.status(404).sendFile('/absolute/path/to/404.png')
```

### res.type(类型)

将`Content-Type`HTTP 标头设置为由指定的`type`. 如果`type`包含“/”字符，则将 设置`Content-Type`为 的确切值，否则假定为文件扩展名并使用该方法`type`在映射中查找 MIME 类型。`express.static.mime.lookup()`

```javascript
res.type('.html')
// => 'text/html'
res.type('html')
// => 'text/html'
res.type('json')
// => 'application/json'
res.type('application/json')
// => 'application/json'
res.type('png')
// => 'image/png'
```

### res.vary（字段）

将字段添加到`Vary`响应标头（如果尚不存在）。

```javascript
res.vary('User-Agent').render('docs')
```

## 路由器

`router`对象是中间件和路由的隔离实例。您可以将其视为“迷你应用程序”，仅能够执行中间件和路由功能。每个 Express 应用程序都有一个内置的应用程序路由器。

路由器的行为类似于中间件本身，因此您可以将其用作 [app.use()](https://www.expressjs.com.cn/4x/api.html#app.use)的参数或用作另一个路由器的 [use()](https://www.expressjs.com.cn/4x/api.html#router.use)方法的参数。

顶级`express`对象有一个创建新对象的[Router()](https://www.expressjs.com.cn/4x/api.html#express.router)`router`方法。

一旦你创建了一个路由器对象，你就可以像应用程序一样向它添加中间件和 HTTP 方法路由（例如`get`、`put`、等）。`post`例如：

```javascript
// invoked for any requests passed to this router
router.use(function (req, res, next) {
  // .. some logic here .. like any other middleware
  next()
})

// will handle any request that ends in /events
// depends on where the router is "use()'d"
router.get('/events', function (req, res, next) {
  // ..
})
```

然后，您可以将路由器用于特定的根 URL，以这种方式将您的路由分成文件甚至迷你应用程序。

```javascript
// only requests to /calendar/* will be sent to our "router"
app.use('/calendar', router)
```

### 方法

### router.all（路径，[回调，...]回调）

此方法与`router.METHOD()`方法一样，只是它匹配所有 HTTP 方法（动词）。

此方法对于为特定路径前缀或任意匹配映射“全局”逻辑非常有用。例如，如果您将以下路由放在所有其他路由定义的顶部，则要求从该点开始的所有路由都需要身份验证，并自动加载用户。请记住，这些回调不必充当端点；`loadUser` 可以执行一个任务，然后调用`next()`以继续匹配后续路由。

```javascript
router.all('*', requireAuthentication, loadUser)
```

或等价物：

```javascript
router.all('*', requireAuthentication)
router.all('*', loadUser)
```

另一个例子是列入白名单的“全局”功能。这里的例子很像以前的例子，但它只限制了以“/api”为前缀的路径：

```javascript
router.all('/api/*', requireAuthentication)
```

### router.METHOD（路径，[回调，...]回调）

这些`router.METHOD()`方法在 Express 中提供路由功能，其中 METHOD 是 HTTP 方法之一，例如 GET、PUT、POST 等，以小写形式显示。因此，实际的方法是`router.get()`、`router.post()`、 `router.put()`等。

除了之前没有为路径调用过的方法之外，还会`router.get()`自动为 HTTP`HEAD`方法调用该函数。`GET``router.head()``router.get()`

您可以提供多个回调，并且所有回调都被平等对待，并且表现得就像中间件一样，除了这些回调可能会调用`next('route')` 以绕过剩余的路由回调。您可以使用此机制对路由执行前置条件，然后在没有理由继续匹配路由时将控制权传递给后续路由。

以下片段说明了可能的最简单的路由定义。Express 将路径字符串转换为正则表达式，在内部用于匹配传入的请求。*执行这些匹配时不*考虑查询字符串，例如“GET /”将匹配以下路由，“GET /?name=tobi”也将匹配。

```javascript
router.get('/', function (req, res) {
  res.send('hello world')
})
```

您还可以使用正则表达式——如果您有非常具体的约束，这很有用，例如，以下将匹配“GET /commits/71dbb9c”以及“GET /commits/71dbb9c..4c084f9”。

```javascript
router.get(/^\/commits\/(\w+)(?:\.\.(\w+))?$/, function (req, res) {
  var from = req.params[0]
  var to = req.params[1] || 'HEAD'
  res.send('commit range ' + from + '..' + to)
})
```

### router.param（名称，回调）

为路由参数添加回调触发器，其中`name`为参数名称，`callback`为回调函数。尽管`name`在技术上是可选的，但从 Express v4.11.0 开始不推荐使用这种方法（见下文）。

回调函数的参数为：

- `req`，请求对象。
- `res`，响应对象。
- `next`，表示下一个中间件功能。
- 参数的值`name`。
- 参数的名称。

与, 不同`app.param()`，`router.param()`不接受路由参数数组。

例如，当`:user`出现在路由路径中时，您可以映射用户加载逻辑以自动提供`req.user`给路由，或对参数输入执行验证。

```javascript
router.param('user', function (req, res, next, id) {
  // try to get the user details from the User model and attach it to the request object
  User.find(id, function (err, user) {
    if (err) {
      next(err)
    } else if (user) {
      req.user = user
      next()
    } else {
      next(new Error('failed to load user'))
    }
  })
})
```

参数回调函数在定义它们的路由器上是本地的。它们不会被安装的应用程序或路由器继承。因此，在 上定义的参数回调`router`将仅由在路由上定义的路由参数触发`router`。

一个参数回调在请求-响应周期中只会被调用一次，即使该参数在多个路由中匹配，如下例所示。

```javascript
router.param('id', function (req, res, next, id) {
  console.log('CALLED ONLY ONCE')
  next()
})

router.get('/user/:id', function (req, res, next) {
  console.log('although this matches')
  next()
})

router.get('/user/:id', function (req, res) {
  console.log('and this matches too')
  res.end()
})
```

在 上`GET /user/42`，打印以下内容：

```
CALLED ONLY ONCE
although this matches
and this matches too
```

以下部分描述`router.param(callback)`，从 v4.11.0 起已弃用。

该`router.param(name, callback)`方法的行为可以通过只传递一个函数来完全改变`router.param()`。这个函数是一个应该如何表现的自定义实现`router.param(name, callback)`——它接受两个参数并且必须返回一个中间件。

此函数的第一个参数是应捕获的 URL 参数的名称，第二个参数可以是任何可能用于返回中间件实现的 JavaScript 对象。

函数返回的中间件决定了捕获 URL 参数时发生的行为。

在此示例中，`router.param(name, callback)`签名被修改为`router.param(name, accessId)`。`router.param()`现在将接受名称和数字，而不是接受名称和回调。

```javascript
var express = require('express')
var app = express()
var router = express.Router()

// customizing the behavior of router.param()
router.param(function (param, option) {
  return function (req, res, next, val) {
    if (val === option) {
      next()
    } else {
      res.sendStatus(403)
    }
  }
})

// using the customized router.param()
router.param('id', '1337')

// route to trigger the capture
router.get('/user/:id', function (req, res) {
  res.send('OK')
})

app.use(router)

app.listen(3000, function () {
  console.log('Ready')
})
```

在此示例中，`router.param(name, callback)`签名保持不变，但没有使用中间件回调，而是定义了自定义数据类型检查函数来验证用户 ID 的数据类型。

```javascript
router.param(function (param, validator) {
  return function (req, res, next, val) {
    if (validator(val)) {
      next()
    } else {
      res.sendStatus(403)
    }
  }
})

router.param('id', function (candidate) {
  return !isNaN(parseFloat(candidate)) && isFinite(candidate)
})
```

### router.route(路径)

返回单个路由的实例，然后您可以使用该实例处理带有可选中间件的 HTTP 动词。用于`router.route()`避免重复的路线命名，从而避免输入错误。

在上面的`router.param()`示例的基础上，以下代码显示了如何使用 `router.route()`来指定各种 HTTP 方法处理程序。

```javascript
var router = express.Router()

router.param('user_id', function (req, res, next, id) {
  // sample user, would actually fetch from DB, etc...
  req.user = {
    id: id,
    name: 'TJ'
  }
  next()
})

router.route('/users/:user_id')
  .all(function (req, res, next) {
    // runs for all HTTP verbs first
    // think of it as route specific middleware!
    next()
  })
  .get(function (req, res, next) {
    res.json(req.user)
  })
  .put(function (req, res, next) {
    // just an example of maybe updating the user
    req.user.name = req.params.name
    // save user ... etc
    res.json(req.user)
  })
  .post(function (req, res, next) {
    next(new Error('not implemented'))
  })
  .delete(function (req, res, next) {
    next(new Error('not implemented'))
  })
```

这种方法重用单一`/users/:user_id`路径并为各种 HTTP 方法添加处理程序。

注意：当您使用 时`router.route()`，中间件排序基于*路由*创建的时间，而不是方法处理程序添加到路由的时间。为此，您可以认为方法处理程序属于添加它们的路由。

### router.use([路径], [函数, ...]函数)

使用指定的中间件函数或函数，带有可选的挂载路径`path`，默认为“/”。

此方法类似于[app.use()](https://www.expressjs.com.cn/4x/api.html#app.use)。下面描述了一个简单的示例和用例。有关更多信息，请参阅[app.use()](https://www.expressjs.com.cn/4x/api.html#app.use)。

中间件就像一个管道：请求从定义的第一个中间件函数开始，并为它们匹配的每个路径“向下”处理中间件堆栈。

```javascript
var express = require('express')
var app = express()
var router = express.Router()

// simple logger for this router's requests
// all requests to this router will first hit this middleware
router.use(function (req, res, next) {
  console.log('%s %s %s', req.method, req.url, req.path)
  next()
})

// this will only be invoked if the path starts with /bar from the mount point
router.use('/bar', function (req, res, next) {
  // ... maybe some additional /bar logging ...
  next()
})

// always invoked
router.use(function (req, res, next) {
  res.send('Hello World')
})

app.use('/foo', router)

app.listen(3000)
```

“挂载”路径被剥离并且对中间件函数*不*可见。此功能的主要效果是挂载的中间件函数可以在不更改代码的情况下运行，而不管其“前缀”路径名如何。

定义中间件的顺序`router.use()`非常重要。它们按顺序调用，因此顺序定义了中间件优先级。例如，通常记录器是您将使用的第一个中间件，以便记录每个请求。

```javascript
var logger = require('morgan')
var path = require('path')

router.use(logger())
router.use(express.static(path.join(__dirname, 'public')))
router.use(function (req, res) {
  res.send('Hello')
})
```

现在假设您想忽略对静态文件的日志记录请求，但继续记录在`logger()`. 在添加记录器中间件之前，您只需将调用移至`express.static()`顶部：

```javascript
router.use(express.static(path.join(__dirname, 'public')))
router.use(logger())
router.use(function (req, res) {
  res.send('Hello')
})
```

另一个例子是从多个目录提供文件，“./public”优先于其他目录：

```javascript
router.use(express.static(path.join(__dirname, 'public')))
router.use(express.static(path.join(__dirname, 'files')))
router.use(express.static(path.join(__dirname, 'uploads')))
```

该`router.use()`方法还支持命名参数，以便您的其他路由器的挂载点可以从使用命名参数的预加载中受益。

**注意**：虽然这些中间件功能是通过特定路由器添加的，但它们运行*时* 由它们所连接的路径（而不是路由器）定义。因此，如果路由匹配，通过一个路由器添加的中间件可以为其他路由器运行。例如，此代码显示了安装在同一路径上的两个不同路由器：

```javascript
var authRouter = express.Router()
var openRouter = express.Router()

authRouter.use(require('./authenticate').basic(usersdb))

authRouter.get('/:user_id/edit', function (req, res, next) {
  // ... Edit user UI ...
})
openRouter.get('/', function (req, res, next) {
  // ... List users ...
})
openRouter.get('/:user_id', function (req, res, next) {
  // ... View user ...
})

app.use('/users', authRouter)
app.use('/users', openRouter)
```

即使身份验证中间件是通过添加的，`authRouter`它也会在由 定义的路由上运行，`openRouter`因为两个路由器都安装在`/users`. 为避免此行为，请为每个路由器使用不同的路径。****