# NodeJs API接口解决跨域(cors)问题，设置跨域访问

#### 方法一

**下载 模块**

```shell
npm install body-parser
npm install cors
```



**导入模块**

```js
const express = require('express');
const app = express()
var bodyParser = require('body-parser');
var cors = require('cors')
```

**使用**

```js
//中间件，所以要在所有路由上方插入
app.use(cors())
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())
```

#### 

