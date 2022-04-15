### HTML 页面

```
<!-- bootstrap 表格 -->
    <div class="container">
      <div class="row">
        <div class="col-md-12">
          <table class="table table-bordered">
            <thead>
              <tr>
                <th>sno</th>
                <th>cno</th>
                <th>degree</th>
              </tr>
            </thead>
            <tbody>
              <!-- <tr>
                <td>1</td>
                <td>Mark</td>
                <td>Otto</td>
                <td>@mdo</td>
              </tr> -->
            </tbody>
          </table>
        </div>
      </div>
    </div>

```

#### 使用 fetch()请求

```js
//使用fetch 获取/getsc 并将数据以key为表头 value为表格内容 动态输出在页面内
fetch("http://localhost:3000/getsc")
  .then((res) => res.json())
  .then((data) => {
    let headStr = "";
    for (var n in Object.keys(data[0])) {
      headStr += `<th>${Object.keys(data[0])[n]}</th>`;
    }
    document.querySelector("thead").innerHTML = headStr;
    //使用双for循环遍历
    let str = "";
    for (var item in data) {
      str += `<tr>`;
      for (var i in Object.keys(data[0])) {
        str += `<td>${Object.values(data[item])[i]}</td>`;
      }
      str += `</tr>`;
    }
    document.querySelector("tbody").innerHTML = str;
  });
```

#### 使用 axios 请求

```js
//使用axios 获取/getsc 并将数据以key为表头 value为表格内容 动态输出在页面内
axios.get("http://localhost:3000/getsc").then((res) => {
  console.log(res.data);
  let headStr = "";
  for (var n in Object.keys(res.data[0])) {
    headStr += `<th>${Object.keys(res.data[0])[n]}</th>`;
  }
  document.querySelector("thead").innerHTML = headStr;
  let str = "";
  for (var item in res.data) {
    str += `<tr>`;
    for (var i in Object.keys(res.data[0])) {
      str += `<td>${Object.values(res.data[item])[i]}</td>`;
    }
    str += `</tr>`;
  }
  document.querySelector("tbody").innerHTML = str;
});
```

#### 使用$.ajax()

```js
//使用$.ajax 获取/getsc 并将数据以key为表头 value为表格内容 动态输出在页面内
$.ajax({
  url: "http://localhost:3000/getsc",
  type: "get",
  success: function (data) {
    console.log(data);
    let headStr = "";
    for (var n in Object.keys(data[0])) {
      headStr += `<th>${Object.keys(data[0])[n]}</th>`;
    }
    document.querySelector("thead").innerHTML = headStr;
    let str = "";
    for (var item in data) {
      str += `<tr>`;
      for (var i in Object.keys(data[0])) {
        str += `<td>${Object.values(data[item])[i]}</td>`;
      }
      str += `</tr>`;
    }
    document.querySelector("tbody").innerHTML = str;
  },
});
```

#### 使用原生 ajax

```js
//使用ajax 获取/getsc 并将数据以key为表头 value为表格内容 动态输出在页面内
let xhr = new XMLHttpRequest();
xhr.open("get", "http://localhost:3000/getsc");
xhr.send();
xhr.onreadystatechange = function () {
  if (xhr.readyState == 4 && xhr.status == 200) {
    let data = JSON.parse(xhr.responseText);
    console.log(data);
    let headStr = "";
    for (var n in Object.keys(data[0])) {
      headStr += `<th>${Object.keys(data[0])[n]}</th>`;
    }
    document.querySelector("thead").innerHTML = headStr;
    let str = "";
    for (var item in data) {
      str += `<tr>`;
      for (var i in Object.keys(data[0])) {
        str += `<td>${Object.values(data[item])[i]}</td>`;
      }
      str += `</tr>`;
    }
    document.querySelector("tbody").innerHTML = str;
  }
};
```

#### 请求数据类型(不是该格式会出现错误)

```js
//表中数据为虚拟数据
```

![1649847300547](../mdBeforeImg/\1649847300547.png)

![1649847475602](../mdBeforeImg/\1649847475602.png)

#### 效果

![1649847498810](../mdBeforeImg/\1649847498810.png)

![1649847521159](../mdBeforeImg/\1649847521159.png)
