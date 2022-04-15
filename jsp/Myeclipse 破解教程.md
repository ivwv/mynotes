Myeclipse 2014 破解补丁，首先需要先下载 Myeclipse 2014 官方安装文件，下载地址

 

https://www.jb51.net/softs/150886.html

,然后下载此补丁。

本文以MyEclipse Professional 10.6 为例来介绍如何破解MyEclipse 10.x。

本文使用的破解补丁对MyEclipse Standard/ Professional/ Blue/ Spring的10.x版本均有效(例如：MyEclipse 10.0、MyEclipse 10.1、MyEclipse 10.5、MyEclipse 10.6、MyEclipse 10.7.1等)。

操作环境说明：

操作系统： Windows 7 SP1 旗舰版 64位
MyEclipse： MyEclipse Professional 10.6

1、运行破解补丁

下图即为破解补丁压缩文件解压后的文件列表。如图中所示，主文件*cracker.jar*用于运行并破解MyEclipse。为了跨平台兼容，该破解程序采用Java开发，因此我们需要先确保计算机中已经正确安装了Java运行环境。

![MyEclipse 10.x 破解补丁文件列表](https://img.jbzj.com/file_images/article/201404/2014040701333027.png)

进入系统命令界面键入命令：`java -jar cracker.jar`(如果是Windows操作系统，也可直接双击运行*run.bat*批处理文件)，我们即可看到破解程序的图形界面。

2、生成注册码相关信息

如下图所示，我们先输入Usercode(可任意输入)，然后选择当前安装的MyEclipse版本，然后依次点击【SystemId】和【Active】。

![生成MyEclipse注册码相关信息](https://img.jbzj.com/file_images/article/201404/2014040701333028.png)

3、重新生成密钥文件

如下图所示，当我们在上个步骤点击【Active】后，破解程序就为我们生成了License Key、Activation Code、Activation Key等信息。

接着，我们点击菜单栏的【Tools】->【RebuildKey】来重新生成密钥文件。

![重新生成密钥文件](https://img.jbzj.com/file_images/article/201404/2014040701333029.png)

4、替换MyEclipse相关JAR文件

接着，我们点击菜单栏【Tools】->【ReplaceJarFile】。

请确保此时的MyEclipse处于未运行状态，否则替换无法成功。

![替换相关Jar文件](https://img.jbzj.com/file_images/article/201404/2014040701333030.png)

在弹出的目录选择对话框中，选中MyEclipse的插件目录，然后单击【打开】。

在10.x及之前版本的MyEclipse中，插件目录为：`MyEclipse安装目录\Common\plugins`。

在2013及之后版本的MyEclipse中，插件目录为：`MyEclipse安装目录\plugins`。

![MyEclipse安装路径下的plugins目录](https://img.jbzj.com/file_images/article/201404/2014040701333031.png)

5、保存MyEclipse用户配置文件

最后，点击菜单栏的【Tools】->【SaveProperties】。

![保存MyEclipse配置文件](https://img.jbzj.com/file_images/article/201404/2014040701333032.png)

到这里，我们的MyEclipse就已经破解成功了。你现在可以打开MyEclipse，然后点击菜单栏的【MyEclipse】->【Subscription Information】，我们就可以看到MyEclipse已经破解激活成功了。

![MyEclipse已经破解成功](https://img.jbzj.com/file_images/article/201404/2014040701333033.png)

破解一次的有效期为3年，到期后可以按照上述步骤再次破解。





   