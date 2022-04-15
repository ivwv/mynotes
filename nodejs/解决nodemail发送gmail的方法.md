### 1.安装npm相关包

```shell
npm install nodemailer
npm install nodemailer-smtp-transport //必要，否者会出现发送错误
```



### 2.发送邮件的基本布局

```js
// Use at least Nodemailer v4.1.0
const nodemailer = require('nodemailer');
var smtpTransport = require('nodemailer-smtp-transport');
// Generate SMTP service account from ethereal.email
nodemailer.createTestAccount((err, account) => {


  console.log('Credentials obtained, sending message...');

  // Create a SMTP transporter object
  const transporter = nodemailer.createTransport(smtpTransport({
    // host: 'smtp.ethereal.email',
    service: 'Gmail',//
    // port: 587,
    port: 465, //SSL 端口
    secure: true,  // use TLS
    secureConnection: true, //use SSL ,smtp.gmail.com要求 SSL
    auth: {
      // user: 'upesj4hld2xxnwl7@ethereal.email',
      // pass: 'ZJHECtdP29r5N4845J'
      user: 'sy18959889840@gmail.com',
      pass: 'cjyjzieerjamempx'
    }
  }));
  // Message object
  let message = {
    from: 'sy18959889840@gmail.com',
    to: 'syyvvw@gmail.com',
    subject: 'Nodemailer is unicode friendly ✔',
    text: 'Hello to myself!',
    html: '<p><b>Hello</b> to myself!</p>'
  };

  transporter.sendMail(message, (err, info) => {
    if (err) {
      console.log('Error occurred. ' + err.message);
      return process.exit(1);
    }

    console.log('Message sent: %s', info.messageId);
    // Preview only available when sending through an Ethereal account
    console.log('Preview URL: %s', nodemailer.getTestMessageUrl(info));
  });
});
```

