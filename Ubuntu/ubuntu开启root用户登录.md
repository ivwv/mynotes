# ubuntu 设置允许root用户登陆

关键词:

黄沙百战穿金甲，不破楼兰终不还。这篇文章主要讲述**ubuntu 设置允许root用户登陆**相关的知识，希望能为你提供帮助。

ubuntu18.04刚装完默认是不允许root用户登陆的，需要进行如下设置：

1、修改配置文件

vim /etc/ssh/sshd_config

把这三行改成这样：（配置项本来存在，改一下值就可以）

[![img](https://img.songbingjia.com/20210512/7ba3a3df70974eabbc296dbf4eeb54c3.jpg)](https://www.songbingjia.com/nginx/show-62702.html)

 

 ```shell
LoginGraceTime 120
PermitRootLogin yes
StrictModes yes
 ```



2、重启ssh

service ssh restart

 

然后就可以用root用户登陆了