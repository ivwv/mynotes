# GET 请求

## 1.form 表单

```html
<!-- //get表单 -->
<form action="http://localhost:3000/get" method="get">
  <input type="text" name="name" value="张三" />
  <input type="text" name="age" value="18" />
  <input type="text" name="pwd" value="hello" />
  <input type="submit" value="提交" />
</form>
```

### 服务器端代码

```js
//get 请求 返回数据库中 teacher 表的所有数据
app.get("/get", (req, res) => {
  console.log(req.query);
  let sql = "SELECT * FROM teacher";
  query(sql).then((data) => {
    res.send({
      query: req.query,
      data: data,
    });
  });
});
```

- **服务器响应**

  ![1649999424556](../mdBeforeImg\1649999424556.png)

- **服务器打印**

![1649999451319](../mdBeforeImg\1649999451319.png)

## 2.$.ajax

### @参数对象:data

```js
// $.ajax get
$("#get").submit(function (e) {
  console.log($("#get").serialize());
  e.preventDefault();
  $.ajax({
    url: "http://localhost:3000/get",
    type: "get",
    //data 格式可以是对象格式 也可以是serialize格式

    data: $("#get").serialize(),
    //   data: {
    //     name: $('[name="name"]').val(),
    //     age: $('[name="age"]').val(),
    //     pwd: $('[name="pwd"]').val(),
    //   },
    success: function (res) {
      console.log(res);
    },
  });
});
```

**serialize 打印输出** 为字符串拼接格式

![1650000748617](../mdBeforeImg\1650000748617.png)

### 服务器输出

![1650000313847](../mdBeforeImg\1650000313847.png)

### 客户端输出

![1650000338473](../mdBeforeImg\1650000338473.png)

### 解决办法

- #### 服务器端

- **使用 get 请求 服务器端必须添加以下代码 否则会报错跨域**

  ```js
  //使用cors 解决get跨域
  const cors = require("cors");
  app.use(cors());
  ```

**最终效果**

![1650000497491](../mdBeforeImg\1650000497491.png)

![1650000505788](../mdBeforeImg\1650000505788.png)

## 3.$.get

### @参数：第二个对象/查询字符串

```js
//$.get(url,[data,[callback])
$.get(
  "http://localhost:3000/get",
  {
    name: "张三",
    age: 18,
    pwd: "hello",
  },
  //可以跟上回调函数 打印响应的数据
  function (res) {
    console.log(res);
  }
);
//$.get(url,[callback])
//也可以使用拼接字符串的方法，将上传的参数以查询字符串的方式拼接在url后面
//！注意 由于jq的 serialize()方法没有跟上 '?' 需要我们手动在url后方添加 '?' 号
$.get("http://localhost:3000/get?" + $("#get").serialize(), function (res) {
  console.log(res);
});

//两种方式效果下相同 且服务端不用做任何处理
//但服务端需要添加cors模块 解决跨域问题
```

![1650001188442](../mdBeforeImg\1650001188442.png)

## 4.fetch()

```js
//fetch
//fetch 方法默认为get方式
//由于fetch为Promise对象 所以要使用then(callback)
//fetch不能使用body传参数 否者会报错 'GET/HEAD 不能携带参数'
//fetch 要跟上两个then
//第一个then作用是将响应的数据转换为何种类型
//第二个then为处理函数
$("#get").submit(function (e) {
  e.preventDefault();
  fetch("http://localhost:3000/get")
    .then((res) => res.json())
    .then((res) => {
      console.log(res);
    });
});
```

- **第一个 then 的 res 常用数据转换类型**

`Body.arrayBuffer()`
使 Response 挂起一个流操作并且在完成时读取其值，它返回一个 Promise 对象，其 resolve 参数类型是 ArrayBuffer。
`Body.blob()`
使 Response 挂起一个流操作并且在完成时读取其值，它返回一个 Promise 对象，其 resolve 参数类型是 Blob。
`Body.formData()`
使 Response 挂起一个流操作并且在完成时读取其值，它返回一个 Promise 对象，其 resolve 参数类型是 FormData 表单。
`Body.json()` **常用**
使 Response 挂起一个流操作并且在完成时读取其值，它返回一个 Promise 对象，其 resolve 参数类型是使用 JSON 解析 body 文本的结果。
`Body.text()`
使 Response 挂起一个流操作并且在完成时读取其值，它返回一个 Promise 对象，其 resolve 参数类型是 USVString（文本）。

### fetch 向服务器传数据

### @参数：查询字符串

```js
//fetch serialize 传参数
//同样 fetch传参数也需要在url地后面添加查询字符串
$("#get").submit(function (e) {
  e.preventDefault();
  fetch("http://localhost:3000/get?" + $("#get").serialize())
    .then((res) => res.json())
    .then((res) => {
      console.log(res);
    });
});
```

## 5.axios()

### @axios.get() 参数对象：params/查询字符串

```js
//   axios get
//axios.get() 传参数使用 params 传递对象形式的参数
$("#get").submit(function (e) {
  e.preventDefault();
  axios
    .get("http://localhost:3000/get", {
      //也可使用添加查询字符串请求
      //.get("http://localhost:3000/get?" + $("#get").serialize(), {
      params: {
        name: $('[name="name"]').val(),
        age: $('[name="age"]').val(),
        pwd: $('[name="pwd"]').val(),
      },
    })
    .then((res) => {
      console.log(res);
    })
    .catch((err) => {
      console.log(err);
    });
});
```

### @axios() 参数：params/查询字符串

```js
$("#get").submit(function (e) {
  e.preventDefault();
  axios({
    method: "get",
    url: "http://localhost:3000/get",
    params: {
      name: $('[name="name"]').val(),
      age: $('[name="age"]').val(),
      pwd: $('[name="pwd"]').val(),
    },
  })
    .then((res) => {
      console.log(res);
    })
    .catch((err) => {
      console.log(err);
    });
});

//-------------
$("#get").submit(function (e) {
  e.preventDefault();
  axios({
    method: "get",
    url: "http://localhost:3000/get?" + $("#get").serialize(),
  })
    .then((res) => {
      console.log(res);
    })
    .catch((err) => {
      console.log(err);
    });
});
```

## 总结

- **众多方法默认请求方式为 Get**
- **服务器端必须处理跨域问题**
  - **可以在服务器端使用 cors 中间件**
- **传递参数时 form 表单直接点击 submit**
- **$.ajax get 方式传递参数可以使用对象`data` 传递对象形式 **

  - **也可跟上查询字符串格式**

- **$.get 可以在第二个参数跟上一个对象格式 也可传参数**

- **fetch 不可携带对象格式参数，必须使用查询字符串格式方式拼接在 url 后方 记得加 '?'**

- **axios 使用 对象`params`传递对象形式参数**

  - **也可使用查询字符串格式**

# POST 请求

## 1.form 表单

```html
<!-- //post表单 -->
<form action="http://localhost:3000/post" method="post">
  <input type="text" name="name" value="张三" />
  <input type="text" name="age" value="18" />
  <input type="text" name="pwd" value="hello" />
  <input type="submit" value="提交" />
</form>
```

### 服务器端代码

```js
//post 请求，返回用户上传的数据
app.post("/post", (req, res) => {
  log(req.body);
  res.send({
    body: req.body,
  });
});
```

- **服务器响应**

![1649999522639](../mdBeforeImg\1649999522639.png)

- **服务器打印**
- ![1649999545114](../mdBeforeImg\1649999545114.png)

### undefind 解决方法

#### 服务器端

```js
//导入body-parser模块
const bodyParser = require("body-parser");
app.use(bodyParser.json()); //只有这一个 服务器端输出req.body的值为     {}
app.use(bodyParser.urlencoded({ extended: false })); //只有这一个 服务器端输出如下图
```

![1649999867980](../mdBeforeImg\1649999867980.png)

## 2.$.ajax

### @参数对象：data:对象/data:查询字符串

```js
//$.ajax post
//传递参数使用data对象
$("#post").submit(function (e) {
  e.preventDefault();
  $.ajax({
    url: "http://localhost:3000/post",
    type: "post",
    //data: $("#post").serialize(),
    data: {
      name: $('[name="name"]').val(),
      age: $('[name="age"]').val(),
      pwd: $('[name="pwd"]').val(),
    },
    success: function (res) {
      console.log(res);
    },
  });
});
```

### 服务器端解决跨域问题 所有 post 方法都要使用

```js
//使用cors 处理get post请求跨域问题
const cors = require("cors");
// body-parser
const bodyParser = require("body-parser");
app.use(cors());
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: false }));
```

- **不使用中间件处理跨域问题**

  - ![1650004817679](../mdBeforeImg\1650004817679.png)

- **仅使用**`app.use(cors());`

  - 出现一个空对象
  - ![1650004850300](../mdBeforeImg\1650004850300.png)

- ```js
  //一下两个单独使用，不使用 app.use(cors());
  // app.use(bodyParser.json());
  //app.use(bodyParser.urlencoded({ extended: false }));
  ```

  - ![1650005000140](../mdBeforeImg\1650005000140.png)

- **使用**

  - ```js
    app.use(cors());
    app.use(bodyParser.json());
    ```

  - ![1650005098684](../mdBeforeImg\1650005098684.png)

- **使用**

  - ```js
    app.use(cors());
    // app.use(bodyParser.json());
    app.use(bodyParser.urlencoded({ extended: false }));
    ```

  - ![1650005153567](../mdBeforeImg\1650005153567.png)

- **正常使用**

  - ```js
    //都使用
    app.use(cors());
    app.use(bodyParser.json());
    app.use(bodyParser.urlencoded({ extended: false }));
    ```

## 3.$.post()

### @参数：第二个参数为对象/查询字符串

```js
//   $.post
//直接使用对象形式添加在第二个参数位置
$("#post").submit(function (e) {
  e.preventDefault();
  $.post(
    "http://localhost:3000/post",
    //$("#post").serialize(),
    {
      name: $('[name="name"]').val(),
      age: $('[name="age"]').val(),
      pwd: $('[name="pwd"]').val(),
    },
    function (res) {
      console.log(res);
    }
  );
});
```

![1650005608666](../mdBeforeImg\1650005608666.png)

## 4.fetch()

- **官方文档**

```js
// Example POST method implementation:
async function postData(url = "", data = {}) {
  // Default options are marked with *
  const response = await fetch(url, {
    method: "POST", // *GET, POST, PUT, DELETE, etc.
    mode: "cors", // no-cors, *cors, same-origin
    cache: "no-cache", // *default, no-cache, reload, force-cache, only-if-cached
    credentials: "same-origin", // include, *same-origin, omit
    headers: {
      "Content-Type": "application/json",
      // 'Content-Type': 'application/x-www-form-urlencoded',
    },
    redirect: "follow", // manual, *follow, error
    referrerPolicy: "no-referrer", // no-referrer, *no-referrer-when-downgrade, origin, origin-when-cross-origin, same-origin, strict-origin, strict-origin-when-cross-origin, unsafe-url
    body: JSON.stringify(data), // body data type must match "Content-Type" header
  });
  return response.json(); // parses JSON response into native JavaScript objects
}

postData("https://example.com/answer", { answer: 42 }).then((data) => {
  console.log(data); // JSON data parsed by `data.json()` call
});
```

### 使用

### @参数：body:对象/body:查询字符串

```js
//fetch post
$("#post").submit(function (e) {
  e.preventDefault();
  fetch("http://localhost:3000/post", {
    method: "post",
    //   body: $("#post").serialize(),
    body: JSON.stringify({
      name: $('[name="name"]').val(),
      age: $('[name="age"]').val(),
      pwd: $('[name="pwd"]').val(),
    }),
    headers: {
      "Content-Type": "application/json",
      // "Content-Type": "application/x-www-form-urlencoded",
    },
  })
    .then((res) => res.json())
    .then((res) => {
      console.log(res);
    });
});

//-----------------------
//fetch post
$("#post").submit(function (e) {
  e.preventDefault();
  fetch("http://localhost:3000/post", {
    method: "post",
    body: $("#post").serialize(),
    //   body: JSON.stringify({
    //     name: $('[name="name"]').val(),
    //     age: $('[name="age"]').val(),
    //     pwd: $('[name="pwd"]').val(),
    //   }),
    headers: {
      // "Content-Type": "application/json",
      "Content-Type": "application/x-www-form-urlencoded",
    },
  })
    .then((res) => res.json())
    .then((res) => {
      console.log(res);
    });
});
```

**以上两种结果都一样，能正常输出结果**

![1650008554038](../mdBeforeImg\1650008554038.png)

### 注意事项

- 使用

  - ```js
    body: $("#post").serialize(),
    headers: {
                "Content-Type": "application/x-www-form-urlencoded",
              },
    ```

  - **由于 body 的值为查询字符串格式，headers 要设置为以上代码**

  - **服务器端才会检测**

- 使用

  - ```js
    body: JSON.stringify({
        name: $('[name="name"]').val(),
        age: $('[name="age"]').val(),
        pwd: $('[name="pwd"]').val(),
        }),
       headers: {
          "Content-Type": "application/json",
              },
    ```

  - **由于 body 是一个对象格式**

  - **因此服务器能够解析**

### 错误使用

```js
body: JSON.stringify({
            name: $('[name="name"]').val(),
            age: $('[name="age"]').val(),
            pwd: $('[name="pwd"]').val(),
}),
headers: {
      "Content-Type": "application/x-www-form-urlencoded",
  },
```

**此为错误方式**

- 由于 body 的值和 headers 的值不匹配

- 向服务器发送的参数会出现 body 对象里面的内容被服务器解析为

  - ```js
    //服务器解析输出
    [Object: null prototype] {
      '{"name":"张三","age":"18","pwd":"hello"}': ''
    }
    ```

  - ![1650009274764](../mdBeforeImg\1650009274764.png)

  - 此格式会将向服务器端发送的 value 转为 key 而 解析后的 value 则为空

## 5.axios

### @参数：data:对象/data:查询字符串

```js
//   axios post
//使用data对象传参数
      $("#post").submit(function (e) {
        e.preventDefault();
        axios({
          method: "post",
          url: "http://localhost:3000/post",
          //   data: $("#post").serialize(),
          data: {
            name: $('[name="name"]').val(),
            age: $('[name="age"]').val(),
            pwd: $('[name="pwd"]').val(),
          },
        })
          .then((res) => {
            console.log(res);
          })
          .catch((err) => {
            console.log(err);
          });
      });

//-------------------------
//axiox.post
//第二个参数可以是对象形式
//使用axios.post不用指明headers
//会自动适配
      $("#post").submit(function (e) {
        e.preventDefault();
        axios
          .post("http://localhost:3000/post", {
            name: $('[name="name"]').val(),
            age: $('[name="age"]').val(),
            pwd: $('[name="pwd"]').val(),
          })
          .then((res) => {
            console.log(res);
          })
          .catch((err) => {
            console.log(err);
          });
      });
//服务器端输出
{ name: '张三', age: '18', pwd: 'hello' }

//---------------

//axiox.post
//第二个参数可以是查询字符串格式
//使用axios.post不用指明headers
//会自动适配
//axiox.post
      $("#post").submit(function (e) {
        e.preventDefault();
        axios
          .post("http://localhost:3000/post", $("#post").serialize())
          .then((res) => {
            console.log(res);
          })
          .catch((err) => {
            console.log(err);
          });
      });

//服务器端输出
[Object: null prototype] { name: '张三', age: '18', pwd: 'hello' }

注意！
axios.post两种数据格式都能以json格式输出且看起来不一样，但不影响实际数据调用
```

### 注意

- **axios 跟 fetch 一样 可以指定响应头**

- **但是 axios 传递的参数不用跟 fetch 一样使用 JSON._stringify_()转换**

  - ```js
    data: {
          name: $('[name="name"]').val(),
          age: $('[name="age"]').val(),
          pwd: $('[name="pwd"]').val(),
     }
    ```

  - 使用 JSON._stringify_()转换为被服务器端解析错误

  - ```js
    //data使用JSON.stringify()转换后解析为
    [Object: null prototype] {
      '{"name":"张三","age":"18","pwd":"hello"}': ''
    }
    ```

- **axios 默认响应头为**

  - ```js
    headers: {
           "Content-Type": "application/json",
    },
    ```

  - **当然也可以不用添加响应头**

### 错误示范

```js
//错误示范
data: {
            name: $('[name="name"]').val(),
            age: $('[name="age"]').val(),
            pwd: $('[name="pwd"]').val(),
          },
          headers: {
            "Content-Type": "application/x-www-form-urlencoded",
          },
```

- 返回结果错误
- ![1650010268965](../mdBeforeImg\1650010268965.png)

- 服务器端输出结果错误
- ![1650010297105](../mdBeforeImg\1650010297105.png)

## 总结

- **服务器端需要使用 cors 和 body-parser 解析 json 格式和查询字符串格式**
- **只有 fetch 需要添加数据对应响应头 headrs**
