### servlet 解决中文乱码问题

```java
//response 响应头修改字符编码
//1.
response.setHeader("Content-Type","text/html;charset=utf-8");
//2.
response.setContentType("text/html");
response.setCharacterEncoding("utf-8");
```

