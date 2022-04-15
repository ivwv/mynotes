- **条件：**必须为此方法所需的Gmail邮箱启用POP / IMAP服务。

Gmail邮箱的POP服务默认是关闭，它需要手动打开。

## Gmail邮箱设置IMAP/POP3

**第 1 步：**点击Gmail设置

登录到你的Gmail，点击右上角的齿轮图标，然后选择“设置” ▼

![Gmail如何开启IMAP/POP3？设置Gmail邮箱服务器地址](https://img.chenweiliang.com/2018/04/gmail-setting.jpg)



**第 2 步：**启用 POP / IMAP

在转发和POP / IMAP页面，选择 “转发和POP / IMAP” 设置 ▼

![在转发和POP / IMAP页面，选择 “转发和POP / IMAP” 设置。 第3张](https://img.chenweiliang.com/2018/04/gmail-pop-imap-setting.jpg)

请选择“**对所有邮件启用POP**” 、“**启用 IMAP**”▲

- 如果未启用POP服务，则显示 “状态：POP已禁用”。
- “对所有邮件启用POP” 意味着Gmail邮箱中的所有邮件都将通过POP进行接收邮件。
- “仅对从现在起接收邮件启用POP” 意味着从现在开始只有新邮件将通过POP接收邮件。

**第 3 步：**点击 “保存更改”。

- 到此就能成功打开Gmail的POP服务。

**第 4 步：**请更改你的电子邮件客户端中的SMTP和其他设置。

有些[新媒体](https://www.chenweiliang.com/xin-mei-ti/)人想找 imap gmail ip 地址，其实根本不用设置什么IP地址。

你只需要使用以下表格的信息，更新你的电子邮件客户端即可 ▼

| 接收邮件 (IMAP) 服务器       | imap.gmail.com要求 SSL：是端口：993                          |
| ---------------------------- | ------------------------------------------------------------ |
| 发送邮件 (SMTP) 服务器       | smtp.gmail.com要求 SSL：是要求 TLS：是（如适用）使用身份验证：是SSL 端口：465TLS/STARTTLS 端口：587 |
| 完整名称或显示名称           | 你的姓名                                                     |
| 帐号名、用户名或电子邮件地址 | 你的完整电子邮件地址                                         |
| 密码                         | 你的 Gmail 密码                                              |