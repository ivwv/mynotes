# 2. 使用

#### 2.1 **在Node HTTP 服务中使用**

**Server(app)，服务端**

```js
const app = require('http').createServer(handler)
const io = require('socket.io')(app)
const fs = require('fs')

app.listen(80)

function handler(req,res){
    fs.readFile(__dirname+'/index.html',(err,data)=>{
        if(err){
            res.writeHead(500);
            return res.end('Error loading index.html,server error!')
        }
        res.writeHead(200);
        res.end(data)
    }),
}

io.on('connection',(socket)=>{
    socket.emit('news',{hello:'world'})//发送个客户端消息
    socket.on('my other event',(data)=>{
        console.log(data)//收到的消息
    })
})
```

**Client(index.html)，客户端**

```js
<script src="/socket.io/socket.io.js"></script>
<script>
    const socket=io('http://localhost');//这里一定要http开头，因为socket.io不是websocket实现的
    socket.on('news',(data)=>{
        console.log(data)//收到服务器emit的消息
        socket.emit('my other event',{my:'data'})//完成了一次消息互换
    })
</script>
```



#### 2.2 **在express中使用Socket.io**

**Server(app.js)**

```js
const app= require('express')()
const server = require('http').Server(app);
const io = require('socket.io')(server)

server.listen(80)
// 警告：app.listen(80)在这里没起作用，可能有端口被占用情况

app.get('/',(req,res)=>{
    res.sendFile(__dirname+'/index.html')
})

io.on('connection',(socket)=>{
    socket.emit('news',{hello:'world'}
    socket.on('my other event',(data)=>{
        console.log(data)
    })
})
```



**Client(index.html)**

```js
<script src="/socket.io/socket.io.js"></script>
<script>
    const socket= io.connect('http://localhost')
    socket.on('news',(data)=>{
        console.log(data)

        socket.emit('my other event',{my:'data'})
    })
</script>
```

#### 2.3 发送和接收事件

**`Socket.io`允许你发送和接收自定义事件，除了`connect`、`message` 和 `disconnect`，你都可以发送自定义事件**

#### 2.4 **发送易失性的消息**

有时可以删除某些消息。 假设您有一个应用程序，显示关键字`bieber`的实时推文。

如果某个客户端尚未准备好接收消息（由于网络速度缓慢或其他问题，或者因为它们通过长轮询连接并处于请求 - 响应周期的中间），如果它没有收到所有推文 与bieber相关的申请不会受到影响。

在这种情况下，您可能希望将这些消息作为易失性消息发送。

**Server**

```js
var io = require('socket.io')(80);

io.on('connection',socket=>{
    const tweets = setInterval(()=>{
        // getBieberTweet??
        getBieberTweet(tweet=>{
            socket.volatile.emit('bieber tweet',tweets)
        })
    },100)
    socket.on('disconnect',()=>{
        clearInterval(tweets)
    })
})
```

#### 2.5 **发送和获取数据(确认)**

**Server(app.js)**

```js
    const io= require('socket.io')(80)
    io.on('connection',socket=>{
        socket.on('ferret',(name,word,fn)=>{
            fn(name+'says'+word)
        })
    })
```



**client(index.html)**

```html
<script>
    const socket= io()
    socket.on('connect',()=>{
        socket.emit('ferrect','tobi','woot',(data)=>{
            console.log(data)//应该是 'tobi says woot'
        })
    })
</script>
```



#### 2.6 **广播消息**

- 
- 广播时不支持回调

**要进行广播，只需添加广播标志即可发出和发送方法调用。 广播意味着向除了启动它的socket之外的所有人发送消息。**

**Server**

```js
const io = require('socket.io')(80)
io.on('connection',(socket)=>{
    socket.broadcast.emit('user connected')
    socket.broadcast.to('socketId').emit('hi',"hi") //给指定人发送
})
```



#### 2.7 **作为跨浏览器使用websocket**

如果您只想要WebSocket语义，那么您也可以这样做。 只需利用`send`和监听`message`事件：

**Serve(app.js)**

```js
const io = require('socket.io')(80)
io.on('connection',(socket)=>{
    socket.on('message',()=>{})
    socket.on('disconnect',()=>{})
})
```

**Client(index.html)**

```js
<script>
    const socket=io('http://localhost/');
    socket.on('connect',()=>{
        socket.send('hi')
    })
    socket.on('message',(msg)=>{})
</script>
```

**如果您不关心重新连接逻辑等，请查看`Engine.IO`，它是Socket.IO使用的WebSocket语义传输层。**

#### 2.8 **命名空间**

`Socket.io`允许你 “namespace”你的`sockets`，这实际上意味着分配不同的端点或路径。 这是一个有用的功能，可以最大限度地减少资源（TCP连接）的数量，同时通过在通信通道之间引入分离来分离应用程序中的问题。

**默认命名空间**

我们调用默认名称空间`/`它是默认情况下连接到的一个`Socket.IO`客户端，以及默认情况下服务器监听的那个。

此命名空间由`io.sockets`或简单地`io`标识为：

```js
//以下都被emit到所有socket连接
io.sockets.emit('hi','everyone');
io.emit('hi','everyone')//简写
```

**自定义命名空间**

要设置自定义命名空间，可以在服务端调用`of`函数

```js
const nsp= io.of('/my-namespace');
nsp.on('connection',(socket)=>{
    console.log('some connected')
})
nsp.emit('hi','everyone')
```



**在客户端，你告诉`Socket.IO`客户端连接到该命名空间：**

```js
const socket= io('/my-namespace')
```

***重要提示*：命名空间是`Socket.IO`协商的实现细节，与底层传输的实际URL无关，默认为：`/socket.io/...`**

#### 2.9 **房间**

在每个名称空间中，还可以定义`sockets`可以`join(加入/连接)`和`leave(离开)`的任意通道。

**加入或离开**

可以调用`join`来订阅给定通道的 `socket`

```js
io.on('connection',socket=>{
    socket.join("some room")
})
```

然后在广播或者emit时，简单地使用 `to` 或 `in`（两者是相同）：

```js
io.to('some room').emit('some event');
```

离开该频道，请以与`join`的相同的方式调用`leave`:

```js
io.leave("some room")
```

**默认房间**

Socket.io中的每`Socket`都由一个随机的、不可访问的、唯一的标识符`Socket#id`标识。为了方便起见，每个socket都自动加入由该id标识的房间。

这使得向其他socket 广播消息变得容易：

```js
io.on('connection',(socket)=>{
    socket.io('say to someone',(id,msg)=>{
        socket.broadcast.to(id).emit("my message",msg)
    })
})
```

**断开**

断开连接后，sockets 会自动离开它们所属的所有通道，不需要进行特殊处理。

#### 2.10 **给外部发送消息**

在某些情况下，您可能希望从socket.io进程上下文之外向socket.io命名空间/房间中的socket发出事件。有几种方法可以解决这个问题，比如实现自己的通道来向流程发送消息。

为了方便这个用例，我们创建了两个模块：

- **socket.io-redis**
- **socket.io-emitter**

通过实现Redis 适配器：

```js
const io= require('socket.io')(3000);
const redis= require('socket.io-redis');

io.adapter(redis({host:"localhost",port:6379}))
```

然后，您可以从任何其他进程向任何通道发送消息。

```js
const io=require('socket.io-emitter')({host:'127.0.0.1',port:6379});
serInterval(()=>{
    io.emit('time',new Date())
},5000)
```



## 3 

#### 3.1 **身份验证差异**

**Socket.io 现使用中间器件**

可以通过io.use（）为socket.io服务器提供任意函数，该函数在创建socket时运行。查看此示例：

```js
const srv=require('http').createServer();
const io = require('socket.io')(srv)
let run=0;

io.use((socket,next)=>{
    run++; //0->1
    next()
});

io.use((socket,next)=>{
    run++;// 1->2
    next();
})

const socket=require('socket.io-client')();
socket.io('connect',()=>{
    // run  此时等于2
})
```

**现通过中间件进行身份验证更简单**

旧的`io.set()`和`io.get()`已弃用，只能支持向后兼容。下面是一个将旧的授权示例转换为中间件样式的转换：

```js
io.set('authorization',(handshakeData,callback)=>{
    //确保握手数据看起来不错
    callback(null,true)//出错，'authorized' boolean second
})
```

**新的：**

```js
io.use((socket,next)=>{
    const handshakeData= socket.request;
    // 确保握手数据看起来和以前一样好
    // 如果错误，则执行这个：
    // next(new Error('not authorized'));
    // 否则回调next
    next();
})
```

**命名空间授权?**

```js
io.of('/namespace').use((socket,next)=>{
    const handshakeData= socket.request;
    next()
})
```

#### 3.2 **快捷方式**

一般来说，常见事物有一些新的捷径。旧版本应该仍然有效，但是快捷方式很好。

**向默认命名空间中的所有客户端广播**

**以前:**

```js
io.sockets.emit('eventname',"eventdata");
```

**现在：**

```js
io.emit('eventname','eventdata')
```

**整洁。**

请注意，在这两种情况下，这些消息都会到达连接到默认“/”命名空间的所有客户端，但不会到达其他命名空间中的客户端。



**启动服务端**

**以前：**

```JS
const io = require('socket.io');
const socket=io.listen(80,{/*选项*/});
```



**现在：**

```JS
const io=require('socket.io');
const socket=io({/*选项*/})
`
```

#### 3.3 **配置差异**

**io.set 不见了**

相反，在服务器初始化中进行如下配置：

```JS
const socket= require('socket.io')({
    // 这里是选项
})
```

日志级别等选项已不存在,`io.set('transports')`, `io.set('heartbeat interval')`, `io.set('heartbeat timeout'`, 和 `io.set('resource')` 仍然支持向后兼容性。

**设置资源路径**

上一个`资源`选项等效于新`路径`选项，但在开始时需要一个`/`。例如，以下配置：

```JS
const socket= io.connect('localhost:3000',{
    resource:"path/to/socket.io";
})
```

**变成：**

```JS
const socket= io.connect('localhost:3000',{
    path:'/path/to/socket.io';
})
```

#### 3.4 **解析器/协议差异**

这只与用其他语言更新socket.io实现、自定义socket.io socket等相关。

**差异1 - 数据包编码**

解析现在是基于类和异步的。不是返回单个编码字符串，而是使用一个编码数组作为唯一参数对调用回调进行编码。每个编码都应该按顺序写入传输。这更灵活的让二进制数据传输，下面是一个例子：

```JS
const encoding= parser.encode(packet);
console.log(encoding); //完全编码的数据包
```

**VS:**

```JS
const encoder= new parser.Encoder();
encoder.encode(packet,encodings=>{
    for(let i=0;i<encodings.length;i++){
        console.log(encodings[i]) //包的编码部分
    }
})
```



**差异2 - 数据包解码**

解码将使事情进一步发展，并且是基于事件的。这是因为某些对象（包含二进制）同时在多个部分中进行编码和解码。这个例子应该有助于理解：

```JS
const packet= parser.decode(decoding);
console.log(packet) // 要处理的成型socket.io包
```

**VS:**

```JS
const decoder=  new parser.Decoder();
decoder.on('decoded',(packet)=>{
    console.log(packet) // 要处理的成型socket.io包
})

decoder.add(encodings[0]) // encodings 是从传输接收的两个编码的数组
decoder.add(encodings[1]) // 添加最后一个元素后，解码器将发出“decoded”
```

