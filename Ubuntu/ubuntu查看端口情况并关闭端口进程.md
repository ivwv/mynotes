# Ubuntu查看端口占用及关闭终端命令



Ubuntu查看端口使用情况，使用netstat命令：

> 查看已经连接的服务端口（ESTABLISHED） netstat -a 查看所有的服务端口（LISTEN，ESTABLISHED） netstat -ap

查看指定端口，可以结合grep命令：

> netstat -ap | grep 8080

 也可以使用lsof命令：

> lsof -i:8888

若要关闭使用这个端口的程序，使用kill + 对应的pid

> kill -9 PID号

**实例命令：**

- **1.查看已连接的服务端口 (ESTABLISHED)**

```js
netstat有一个快捷键【ss】
```

复制

![img](https://ask.qcloudimg.com/http-save/yehe-5005176/daedb72475f0ecba976983afec6596a2.png?imageView2/2/w/1620)

```js
netstat -a ss -a
```

复制

**2.查看所有的服务端口(LISTEN,ESTABLISHED)**

```js
netstat -ap ss -ap
```

复制

**3.查看指定端口，可以结合grep命令**

```js
netstat -apn | grep 8080  ss -apn | grep 8080 或  lsof -i:8080
```

复制

**4.查询进程详情**

```js
ps -aux | grep pid
```

复制

**5.关闭使用这个端口的程序，使用kill + 对应的pid**

```js
kill -9 PID
```