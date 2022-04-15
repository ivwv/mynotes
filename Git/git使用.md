### 1.下载 git 寻找到自己电脑适合的版本，一直点击下一步

### 2.配置用户名和邮箱

```bash
git config --global user.name "sy"
git config --global user.email "sy18959889840@gmail.com"
#查看git config帮助
git config -h
#查看当前用户名和邮箱
git config user.name
git config user.email
```

### 3.初始化代码仓库

##### (1)

```bash
$ git init  			#在当前目录创建一个.git 的隐藏文件夹
$ git status  			#查看当前文件夹是否提交到git仓库 查看是否被跟踪
```

##### (2)

```bash
#以精简的方式显示文件状态
$ git status -s
$ git status --short
  #注意:修改过的，执行查看状态命令，没有放入暂存区的文件前面有'M'标记
```

##### (3)跟踪新文件

```bash
$ git add index.html  	#只跟踪index.html
$ git add .				#向暂存区中一次性添加多个文件
```

##### (4)提交更新

```bash
#git commit -m "提交信息"
$ git commit -m "新建了index.html文件"
```

##### (5)取消暂存的文件

```bash
#如果需要从暂存区中移除对应的文件，可以使用如下的命令:
$ git reset HEAD 要移除的文件名称
```

##### (6)**跳过使用暂存区域**

```bash
#Git 标准的工作流程是工作区 → 暂存区 → Git 仓库，但有时候这么做略显繁琐，此时可以跳过暂存区，直接将工作区中的修改提交到 Git 仓库，这时候 Git 工作的流程简化为了工作区 → Git 仓库。

#Git 提供了一个跳过使用暂存区域的方式， 只要在提交的时候，给 git commit 加上 -a 选项，Git 就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 git add 步骤：
$ git commit -a -m "描述信息"
```

##### (7)移除文件

```bash
#从Git仓库和工作区中同时移除index.js
$ git rm -f index.js
#只从Git仓库中移除index.css ，但保留工作区中的index.css文件
$ git rm --cached index.css
```

##### (8)**忽略文件**

```bash
#一般我们总会有些文件无需纳入 Git 的管理，也不希望它们总出现在未跟踪文件列表。 在这种情况下，我们可以创建一个名为 .gitignore 的配置文件，列出要忽略的文件的匹配模式。
#文件 .gitignore 的格式规范如下：
#1.以 # 开头的是注释
#2.以 / 结尾的是目录
#3.以 / 开头防止递归
#4.以 ! 开头表示取反
#5.可以使用 glob 模式进行文件和文件夹的匹配（glob 指简化了的正则表达式）

```

##### (9)**glob** **模式**

```bash
#所谓的 glob 模式是指简化了的正则表达式：
 #1.星号 * 匹配零个或多个任意字符
 #2.[abc] 匹配任何一个列在方括号中的字符 （此案例匹配一个 a 或匹配一个 b 或匹配一个 c）
 #3.问号 ? 只匹配一个任意字符
 #4.在方括号中使用短划线分隔两个字符， 表示所有在这两个字符范围内的都可以匹配（比如 [0-9] 表示匹配所有 0 到 9 的数字）
 #5.两个星号 ** 表示匹配任意中间目录（比如 a/**/z 可以匹配 a/z 、 a/b/z 或 a/b/c/z 等）

```

##### (10)**.gitignore** **文件的例子**

![1645261176477](../mdBeforeImg\1645261176477.png)

##### (11)**.** **查看提交历史**

```bash
#如果希望回顾项目的提交历史，可以使用 git log 这个简单且有效的命令。
```

![1645261251203](../mdBeforeImg\1645261251203.png)

##### (12)**回退到指定的版本**

![1645261270617](../mdBeforeImg\1645261270617.png)

### 4. 小结

##### 1.① 初始化 Git 仓库的命令

```bash
$ git init
```

##### 2.查看文件状态的命令

```bash
$ git status 或 git status -s
```

##### 3.一次性将文件加入暂存区的命令

```bash
$ git add .
```

##### 4.将暂存区的文件提交到 Git 仓库的命令

```bash
$ git commit -m "提交消息"
```

### 5.github 远程仓库使用

Github 上的远程仓库，有两种访问方式，分别是 HTTPS 和 SSH。它们的区别是：

 ①HTTPS：零配置；但是每次访问仓库时，需要重复输入 Github 的账号和密码才能访问成功

 ②SSH：需要进行额外的配置；但是配置成功后，每次访问仓库时，不需重复输入 Github 的账号和密码

注意：在实际开发中，推荐使用 SSH 的方式访问远程仓库。

1.**基于** **HTTPS** **将本地仓库上传到** **Github**

![1645261534352](../mdBeforeImg\1645261534352.png)

#### 2.**SSH key**

SSH key 的**作用**：实现本地仓库和 Github 之间免登录的加密数据传输。

SSH key 的**好处**：免登录身份认证、数据加密传输。

SSH key 由**两部分组成**，分别是：

①id_rsa（私钥文件，存放于客户端的电脑中即可）

②id_rsa.pub（公钥文件，需要配置到 Github 中）

**3.生成** **SSH key**

```bash
①打开 Git Bash

②粘贴如下的命令，并将 your_email@example.com 替换为注册 Github 账号时填写的邮箱：

$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

③连续敲击 3 次回车，即可在 C:\Users\用户名文件夹\.ssh 目录中生成 id_rsa 和 id_rsa.pub 两个文件
```

#### 4.**配置** **SSH key**

```bash'
使用记事本打开 id_rsa.pub 文件，复制里面的文本内容
在浏览器中登录 Github，点击头像 -> Settings -> SSH and GPG Keys -> New SSH key
将 id_rsa.pub 文件中的内容，粘贴到 Key 对应的文本框中
在 Title 文本框中任意填写一个名称，来标识这个 Key 从何而来
```

#### 5.**检测** **Github** **的** **SSH key** **是否配置成功**

 1.打开 GitBash，输入如下的命令并回车执行：

    ssh -T git@github.com

 2.上述的命令执行成功后，可能会看到如下的提示消息：

![1645265209514](../mdBeforeImg\1645265209514.png)

3.输入 yes 之后，如果能看到类似于下面的提示消息，证明 SSH key 已经配置成功了：

![1645265252493](../mdBeforeImg\1645265252493.png)

# 创建 git 仓库后的提交方式

…or create a new repository on the command line

#或者在命令行上创建一个新的存储库

\*\*注意 ：repositoryName 自行替换为自己的仓库名

```bash
echo "# repositoryName >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/ivwv/repositoryName.git
git push -u origin main
```

…or push an existing repository from the command line

... 或者从命令行推送现有存储库

```bash
git remote add origin https://github.com/ivwv/repositoryName.git
git branch -M main
git push -u origin main
```

# 拉去指定分支

```bash
$ git clone -b 分支名 https://github.com/ivwv/MisakaLinuxToolbox.git
```

## 使用 https 传输

使用 https 传输每次提交都要输入账号和密码,但是使用密码登录 github 官方有在 2021 年 8 月 13 日禁止了

可以使用令牌的方法,但是一个令牌只能出现一次，默认令牌存在时间 30 天，可自行修改，最少 7 天。刷新后就不会再显示了,所以要妥善保管好，在 Linux 上使用令牌密码可以直接登录提交

#### 教程

```bash
点击 :头像 -> Settings -> Developer settings -> Personal access tokens -> Generate new token ->(输入note 名称 ->选择生效天数 ->勾选使用权限 ->保存token密钥 (密钥很重要))
```
