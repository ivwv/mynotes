

### fetch() 用法

`fetch` 规范与 `jQuery.ajax()` 主要有以下的不同：

- 当接收到一个代表错误的 HTTP 状态码时，从 `fetch()` 返回的 Promise **不会被标记为 reject**，即使响应的 HTTP 状态码是 404 或 500。相反，它会将 Promise 状态标记为 resolve （如果响应的 HTTP 状态码不在 200 - 299 的范围内，则设置 resolve 返回值的 [`ok`](https://developer.mozilla.org/zh-CN/docs/Web/API/Response/ok) 属性为 false ），仅当网络故障时或请求被阻止时，才会标记为 reject。
- `fetch` **不会发送跨域 cookies**，除非你使用了 *credentials* 的[初始化选项](https://developer.mozilla.org/zh-CN/docs/Web/API/fetch#参数)。（自[2018 年 8 月](https://github.com/whatwg/fetch/pull/585)以后，默认的 credentials 政策变更为 `same-origin`。Firefox 也在 61.0b13 版本中进行了修改

##### 一个基本的 fetch 请求设置起来很简单。

```js
//fetch返回的是一个Promise
fetch('https://dog.ceo/api/breeds/image/random')
.then(response => response.json())
.then(data => console.log(data));

```

当然它只是一个 HTTP 响应，而不是真的 JSON。为了获取JSON的内容，我们需要使用 `json()`方法（该方法返回一个将响应 body 解析成 JSON 的 promise）。







```html
<button type="button" class="btn btn-default">button</button>
    <img src="" alt="">
    <script>
        var img = document.querySelector('img');
        var button = document.querySelector('button');

        button.onclick = function () {
            fetch('https://dog.ceo/api/breeds/image/random')
                .then(res => {
                    console.log(res.ok);
                    if (res.ok) {
                        return res.json()
                    }
                    throw new Error("错误")
                })
                .then(data => {
                    console.log(data.message)
                    img.src = data.message
                })
        }
        // fetch('http://124.221.62.120:3001/')
        //     .then(res => res.json())
        //     .then(data => console.log(data.result))
    </script>
```





### fetch() post请求

```js
var data = { name: "张三", age: "18" };
      fetch("http://localhost:3000/addsc", {
        method: "POST",
        body: JSON.stringify(data),
        headers: {
          "Content-Type": "application/json",//正常情况跟上这个值，对应body的类型为转换为字符串类型
          // "Content-Type": "application/x-www-form-urlencoded", 
        },
      })
        .then(function (response) {
          return response.json();
        })
        .then(function (data) {
          console.log(data);
        });
```



```js
//服务器端跟上中间件
var cors = require("cors");
var bodyParser = require("body-parser");
router.use(cors());
router.use(bodyParser.urlencoded({ extended: false }));
router.use(bodyParser.json());
```

```js
//路由
router.post("/addsc", (req, res) => {
    //post为body get为query
  console.log(req.body);
  res.send({
    code: 1,
    msg: "添加成功",
    req: req.body,
  });
```

