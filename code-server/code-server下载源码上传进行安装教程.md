# 腾讯云服务器安装VS code-server

![img](https://p26-passport.byteacctimg.com/img/user-avatar/0234ea548a715e0b35794de71f6ecc83~300x300.image)

[vEth_xin ![lv-1](https://lf3-cdn-tos.bytescm.com/obj/static/xitu_juejin_web/636691cd590f92898cfcda37357472b8.svg)](https://juejin.cn/user/4125023359481671)

2020年08月18日 21:27 ·  阅读 1627

笔者环境： 1.腾讯云服务器 2.ubuntu 18.04

万能安装方法：

1.下载安装包到本地

https://github.com/coder/code-server/releases

2.通过winscp上传压缩包到/home/ubuntu/ ![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/28958e4e7c104f41af405a99a45225f9~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)

3.访问腾讯云服务器，解压文件

tar -xvzf code-server-3.4.1-linux-amd64.tar.gz

cd code-server-3.4.1-linux-amd64

4.启动服务 ./code-server --bind-addr 0.0.0.0:8888

5.登录尝试 在本地浏览器输入云服务器公网IP：8888，如：

172.16.0.5：8888

初次登录，会要求输入密码。

在shell中输入 cat ~/.config/code-server/config.yaml 查看密码

6.将进程挂在后台

nohup ./code-server --bind-addr 0.0.0.0:8888 >/dev/null 2>&1 &