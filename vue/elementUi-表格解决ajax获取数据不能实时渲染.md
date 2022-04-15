#### **elementUi-表格解决ajax获取数据不能实时渲染.txt**

```html
<template>
    <!-- tableData 绑定的是数据 -->
  <el-table :data="tableData" style="width: 100%">
       <!-- prop是elementui自定义属性 -->
    <el-table-column prop="book_id" label="日期" width="180"> </el-table-column>
    <el-table-column prop="name" label="姓名" width="180"> </el-table-column>
    <el-table-column prop="author" label="地址"> </el-table-column>   
</template>
```





```js
export default {
  data() {
    return {
        //如果要ajax渲染数据，这个数组最好是空数组
      tableData: [],
    };
  },
  methods: {
    getData() {
      //重要！！！，要修改this指向
      var self = this;
      $.ajax({
        type: "get",
        url: "http://localhost:3000",
        // dataType: jsonp,
        success: function (data) {
  		//将获取过来的数据赋值给self指向的tableData
          self.tableData = data.result;
          console.log(typeof data.result);
        },
      });
    },
  },
    //当页面创建完成后，就执行获取数据到页面上
  created() {
    this.getData();
  }
```

