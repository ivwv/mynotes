nodemailer 简介
Nodemailer 是 Node.js 应用程序的一个模块，可以方便地发送电子邮件。

该项目于 2010 年开始，至今已经相当稳定，这也是如今大多数 Node.js 用户默认情况下发送邮件的解决方案。



使用
# 初始化 pageage.json 文件
$ npm init

# 安装依赖
$ npm install nodemailer --save

# 运行
node app.js
1
2
3
4
5
6
7
8
app.js

const nodemailer = require('nodemailer');

// 开启一个 SMTP 连接池
let transporter = nodemailer.createTransport({
    host: 'smtp.qq.com',
    secureConnection: true, // use SSL
    port: 465,
    secure: true, // secure:true for port 465, secure:false for port 587
    auth: {
        user: '80583600@qq.com',
        pass: 'xxx' // QQ邮箱需要使用授权码
    }
});

// 设置邮件内容（谁发送什么给谁）
let mailOptions = {
    from: '"白小明 ��" <80583600@qq.com>', // 发件人
    to: 'xx1@qq.com, xx2@qq.com', // 收件人
    subject: 'Hello ✔', // 主题
    text: '这是一封来自 Node.js 的测试邮件', // plain text body
    html: '<b>这是一封来自 Node.js 的测试邮件</b>', // html body
    // 下面是发送附件，不需要就注释掉
    attachments: [{
            filename: 'test.md',
            path: './test.md'
        },
        {
            filename: 'content',
            content: '发送内容'
        }
    ]
};

// 使用先前创建的传输器的 sendMail 方法传递消息对象
transporter.sendMail(mailOptions, (error, info) => {
    if (error) {
        return console.log(error);
    }
    console.log(`Message: ${info.messageId}`);
    console.log(`sent: ${info.response}`);
});
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
效果预览



踩坑细节
实践的时候遇到许多问题，现在列举如下，若未详尽，敬请留言交流。

POP3/SMTP服务、获取授权码（以QQ为例）
首先需要开启邮箱的 POP3/SMTP 服务。

QQ邮箱需要使用授权码，而不是QQ密码；163 邮箱直接使用163邮箱密码就行。

进入QQ邮箱，设置-账户-开启服务 POP3/SMTP 服务，并生成授权码，现在获取授权码需要验证手机短信。



支持邮箱
理论上支持所有主流邮箱，但我只测试了 QQ 和 163，都成功了。若其他邮箱出问题请留言交流。

535 错误
Error: Invalid login: 535 Error: authentication failed

认证失败：

可能是账号密码错误
链接资源池时加 ssl：secureConnection: true,
QQ 的 host 是 smtp.qq.com；163 的 host 是 smtp.163.com
553 错误
Error: Mail command failed: 553 Mail from must equal authorized user

发件人和认证的邮箱地址不一致

auth.user 需要与 from 中的邮箱一致
————————————————
版权声明：本文为CSDN博主「白小明80583600」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/QQ80583600/article/details/75647271