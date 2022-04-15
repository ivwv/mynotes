# **socket.io 总结**

简易聊天程序

## 1.初始化

##### 1.1 初始化 nodejs 项目

```shell
npm init
```

##### **1.2 下载 sosket.io 的 npm 包**

```shell
npm install --save express
```

##### 1.3 `express`安装后，我们可以创建一个设置我们的应用程序的 `index.js` 文件

```js
//en 版本提供的例子
const app = require("express")();
const http = require("http").Server(app);

app.get("/", (req, res) => {
  res.send("<h1>Hello world</h1>");
});
http.listen(3000, () => {
  console.log("listening on *:3000");
});

//个人简写如下:

const express = require("express");
const app = express();

app.get("/", (req, res) => {
  res.send("<h1>Hello world</h1>");
});
app.listen(3000, () => {
  console.log("listening on *:3000");
});
```

```shell
node index.js
```

##### 1.4 在 `index.js` 中我们调用了 `res.end`并传递一个 HTML 字符串。

​ **如果我们将整个应用程序的 HTML 放在那里，我们代码看起来会很混乱，相反，我们将创建一个`index.html`文件并提供服务。**

​ **我们重构下，使用`sendFile`替换下路由处理程序：**

```js
app.get("/", (req, res) => {
  res.sendFile(__dirname + "/index.html");
});
```

**在`index.html`补充下内容，如下：**

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Socket.IO chat</title>
    <style>
      * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
      }
      body {
        font: 13px Helvetica, Arial;
      }
      form {
        background: #000;
        padding: 3px;
        position: fixed;
        bottom: 0;
        width: 100%;
      }
      form input {
        border: 0;
        padding: 10px;
        width: 90%;
        margin-right: 0.5%;
      }
      form button {
        width: 9%;
        background: rgb(130, 224, 255);
        border: none;
        padding: 10px;
      }
      #messages {
        list-style-type: none;
        margin: 0;
        padding: 0;
      }
      #messages li {
        padding: 5px 10px;
      }
      #messages li:nth-child(odd) {
        background: #eee;
      }
    </style>
  </head>
  <body>
    <ul id="messages"></ul>
    <form action="">
      <input id="m" autocomplete="off" /><button>Send</button>
    </form>
  </body>
</html>
```

**然后再次运行`node index.js`)进程和刷新页面**

```shell
node index.js
```

##### 1.5 集成 socket.io

socket.io 是由两个部分组成：

- 一个与 node.js HTTP 服务集成的服务器：socket.io
- 一个在浏览器端加载的客户端库：socket.io-client

开发期间，`socket.io` 会自动为我们服务，正如我们将看到的，因为只需安装一个模块：

```shell
npm install --save socket.io
```

**会安装模块并将依赖项添加到`package.json`中，现在，让我们编辑`index.js`来添加它：**

```js
const app = require("express")();
const http = require("http").Server(app); //这里必须绑定在http实例上而不是app上
const io = require("socket.io")(http);

app.get("/", (req, res) => {
  res.sendFile(__dirname + "/index.html");
});

io.on("connection", (socket) => {
  console.log(socket);
  console.log("id", socket.id); //每次connect 的id都不一样
  console.log("a user connected");
});

http.listen(3000, () => {
  console.log("listening on * :3000");
});
```

**请注意，这里通过传递 `http`(HTTP 服务器)对象来初始化 socket.io 的新实例，然后 HTTP 模块监听传入 socket 的`connection`事件，并将其记录到控制台**

**现在在`index.html`文件中，添加了以下内容在 body：**

```js
<script src="/socket.io/socket.io.js"></script>
<script>
const socket=io();//也可以 io("http://xxx")
</script>
```

**思考下：**

```js
let a = 10; //10 100 1000 10000
for (let i = 0; i < a; i++) {
  var socket = io();
}
//会创建10个不同的socket对象
```

**这就是加载`socket.io-client`所需要的，它暴露了一个 io 全局，然后连接。**

**请注意，当调用`io()`时，并没有指定任何 URL，因为它默认尝试连接到为页面提供服务的`HOST`**

**如果现在重新加载服务器和网站，应该看到控制台中打印`a user connected`**

**尝试多打开几个 tab 标签去访问这个 url，将会看到几条消息：**

**![1648274108509](../mdBeforeImg\1648274108509.png)**

**每个`socket`还会触发一个特殊的`disconnect`（断开）事件：**

```js
io.on("connection", (socket) => {
  console.log("a user connected");
  socket.on("disconnect", () => {
    console.log("a user disconnected");
  });
});
```

**然后，你如果刷新 tab 几次，你可以看到如下效果：**

![1648274147007](../mdBeforeImg\1648274147007.png)

##### 1.6 **发送事件(Emiting events)**

**发送事件**

`socket.io`背后的主要思想是：你可以使用你想要的任何数据发送和接受你想要的任何事件，比如可以编码为 json 的对象，甚至也支持二进制数据。

让我们这样做，以便当用户键入消息时，服务器将其作为聊天消息事件获取。 `index.html`中的`scripts`部分现在应该如下所示：

```html
<script src="/socket.io/socket.io.js"></script>
<script src="https://code.jquery.com/jquery-1.11.1.js"></script>
<script>
  $(function () {
    var socket = io();
    $("form").submit(function (e) {
      e.preventDefault(); // prevents page reloading 放置页面重新加载
      socket.emit("chat message", $("#m").val());
      $("#m").val("");
      return false;
    });
  });
</script>
```

**然后， 在`index.js`中，我们打印出来`chat message` 事件：**

```js
io.on("connection", (socket) => {
  socket.on("chat message", (msg) => {
    console.log("message:" + msg);
  });
});
```

**提醒，关于以上代码的路径，是实际开发中，存在偏差，主要是 jquery 的路径，如果是本地文件，则需要做一层设置，以下为笔者的设置：**

在 `index.html`中

```html
<script src="/socket.io/socket.io.js"></script>
<!--这个部分，在node端，会添加一层中间默认路由给它自己-->
<script src="jquery-1.11.1.js"></script>
```

##### 1.7 **广播(Broadcasting)**

**下一个目标是让我们从服务器向其他用户发送事件**

**为了发送一个事件给所有人，`socket.io`给我们提供了`io.emit`:**

```js
io.emit("some event", { for: "hey gay! to everyone" });
```

**如果你想向除了某些`socket`以外的所有人发送消息，我们有`broadcasting`广播标志：**

```js
// 向所有非自己连接的客户端，发送连接数
io.on("connection", (socket) => {
  socket.broadcast.emit("hi");
});
```

如图，刷新中间的窗口，服务器则向左右两侧的窗口推送消息：

![1648274395497](../mdBeforeImg\1648274395497.png)

**在这种情况下。为了简单起见，我们会将消息发送给所有人，包括发件人**

```js
io.on("connection", (socket) => {
  socket.on("chat message", (msg) => {
    io.emit("chat message", msg);
  });
});
```

**在客户端，我们捕获到聊天消息，将其也包含在页面中，现在客户端的 JS 代码如下：**

```html
<script>
  $(function () {
    var socket = io();
    $("form").submit(function (e) {
      e.preventDefault(); // prevents page reloading
      socket.emit("chat message", $("#m").val());
      $("#m").val("");
      return false;
    });
    socket.on("chat message", function (msg) {
      $("#messages").append($("<li>").text(msg));
    });
  });
</script>
```

这就是完成了我们的聊天应用程序，大约 20 行代码!
