---
title: Minecraft个人私服搭建指南（下）
tab: Minecraft个人私服搭建指南
catalog: true
date: 2017-06-17 19:26:21
subtitle: 如果某些服务器操作指令代码在执行时发生奇奇怪怪的问题，建议先使用搜索引擎查找相关词条。
header-img: img/Demo.jpg
tags:
- Minecraft
categories:
- Minecraft
- 服务器
comments: true
---

&emsp;&emsp;接着上一篇教程[Minecraft个人私服搭建指南（上）](http://oxygenmode.me/articles/2017/06/17/minecraft-server-1/)，在准备好服务器和控制端之后，通过Xshell软件来远程访问控制云端服务器，然后我们需要给这个空空的服务器搭建好环境。

&emsp;&emsp;前排提示：教程从此处开始出现linux操作指令代码，如有疑问和搞不明白的地方，强烈建议打开浏览器使用搜索引擎查找相关词条。另外，注意空格。

---

## 服务器系统更新

&emsp;&emsp;不管你在申请服务器时选了什么版本的服务器系统，请在配置服务器之前更新一下系统组件，以免遇到不必要的问题。首先是按照上一篇的教程结尾示范，使用Xshell登录到远程服务器。

![Xshell登录](img/img1.png)

&emsp;&emsp;更新CentOS服务器系统组件，使用一下指令进行：
```
yum -y update
```

&emsp;&emsp;最后显示 “Complete!” ，结束之后再输入一下内容：
```
yum -y upgrade
```

&emsp;&emsp;等待结束后系统更新完事。

![更新系统](img/img2.png)

---

## Java环境和Screen工具

### 配置Java环境

&emsp;&emsp;Minecraft这款沙盒游戏的运行，必须有Java环境支持，在服务器上要运行Minecraft服务端，也需要先配置Java环境。本教程推荐直接yum命令装配Java环境，更加方便。

&emsp;&emsp;上一流程结束后，在远程界面中输入一下内容来在yum库里查找java安装包：
```
yum -y list java*
```
&emsp;&emsp;之后你会看见这样的查找结果：

![Java安装](img/img3.png)

&emsp;&emsp;选择一个较为新的版本，比如我们选用“java-1.8.0-openjdk”系列的安装包，输入一下安装命令：
```
yum -y install java-1.8.0-openjdk*
```

&emsp;&emsp;等待最后出现 “Complete!” 这样就将“java-1.8.0-openjdk”所有先关的程序安装完成。完成之后输入以下内容验证Java环境已经成功配置：
```
java -version
```

&emsp;&emsp;结果如下图所示的话，就意味着Java环境配置成功。

![Java安装](img/img4.png)

<br>

### 安装Screen工具

&emsp;&emsp;然后我们还需要一个神奇的工具——screen。全称GUN Screen，[就是这个东西](https://link.jianshu.com/?t=http://baike.baidu.com/item/screen/2287462)。简单来说的话，就像是用来虚拟出屏幕（其实叫终端窗口），来跑某个程序，比如我们即将要用的Minecraft服务端，来保证即使我们断开服务器再次连接也可以继续执行对于服务端的命令操作。

&emsp;&emsp;你只需要在Xshell远程界面中输入一下命令来安装Screen：
```
yum -y install screen
```

![Screen安装](img/img5.png)

&emsp;&emsp;同样，等待最后出现 “Complete!” 表示完成安装。

&emsp;&emsp;至此，我们的云服务器基本已经完成配置，准备运行Minecraft服务端。接下来我们将要用Xftp上传服务端文件，配置并运行服务端。

---

## 搞到手一个服务端文件

&emsp;&emsp;就像你玩网游之前要在电脑上安装客户端一样，要搭建Minecraft服务器你要在你的服务器上安装配置好一个Minecraft服务端。Minecraft的服务端可在网上自找资源，有好多版本以及第三方mod可供选择。本教程使用官方原版服务端（不含第三方mod）,[点击这里](https://link.jianshu.com/?t=http://pan.baidu.com/s/1pLnmv6F)下载服务端。

&emsp;&emsp;**注意：你的服务端版本号必须要与客户端版本号一致才能正常连接使用，请安装配置前再三确认。**

&emsp;&emsp;当然，你也可以自己选择喜欢的版本和第三方mod进行配置，大致方法没差。

---

## 把文件上传到云服务器上

&emsp;&emsp;拿到手你的服务端之后，我们要做的是吧这个服务端文件上传到我们配置好的云服务器上。

&emsp;&emsp;打开上一篇教程中在电脑上安装的**Xftp**（如果不记得有这个东西的话往上一篇翻看一下）软件，然后点击“新建”。

![Xftp新建](img/img6.png)

&emsp;&emsp;与上篇教程中新建连接大致一样，在【新建会话属性】里，【名称】看心情随意填，【主机】一样填入服务器公网ip地址，注意【协议】要选择【**SFTP**】，【说明】随意填写。登录中填写上篇教程中申请服务器时设置的用户名（root）与密码，确定。

![Xftp设置](img/img7.png)

&emsp;&emsp;之后点击【连接】，就可以接入我们的云服务器。连接进去之后，软件界面左边是你电脑本机的资源管理器，右边是你云服务器的资源管理器。接下来就可以向服务器传文件了。

![Xftp连接](img/img8.png)

&emsp;&emsp;在右边云服务器资源管理器，按照下图，在上方路径框里输入 `/home` ,回车，在界面里右键【新建】，【新建文件夹】，字母命名（可加下划线）如“mc_server”，双击点进。

![新建文件夹](img/img9.png)

&emsp;&emsp;在左边电脑本机资源管理器中找到你下载好的服务端文件，右键点击“传输”。

![文件传输](img/img10.png)

&emsp;&emsp;上传完成之后，断开连接退出即可。

---

## 远程配置运行服务端文件

&emsp;&emsp;进入最后一个步骤，一切就绪之后就我们就可以配置运行服务端文件。

&emsp;&emsp;通过Xshell远程登录到你的云端服务器，然后我们先创建一个Screen进程，命名为mc，用来启动和运行我们的服务端，在远程操作界面输入：
```
screen -S mc
```

![创建Screen进程](img/img11.png)


&emsp;&emsp;在mc这个Screen进程中，首先切换到我们服务端的上传目录：
```
cd /home/mc_server
```
&emsp;&emsp;然后建立服务端启动脚本：
```
nano start.sh
```
![创建Screen进程](img/img12.png)

&emsp;&emsp;回车弹出新建的start.sh文件编辑器窗口，输入一下内容：
```
#!/bin/sh java -Xmx768M -Xms512M -jar /home/mc_server/minecraft_server.1.11.2.jar
```
&emsp;&emsp;其格式可理解为：#!/bin/sh java 【最大内存占用】 【最小内存占用】 -jar 【文件路径】 【服务端全称】

&emsp;&emsp;**注意：空格不要漏掉**

![编辑start.sh](img/img13.png)

&emsp;&emsp;输入完成之后按 Ctrl+X，然后输入Y，最后回车完成编辑。

&emsp;&emsp;完成start.sh脚本编辑之后，输入一下内容查看当前目录下文件：
```
ls -al
```
&emsp;&emsp;再输入以下内容，赋予脚本执行权限：
```
chmod 777 start.sh
```

![设置start.sh](img/img14.png)

&emsp;&emsp;然后，我们需要修改一下EULA文件来让start.sh脚本顺利运行，输入：
```
nano eula.txt
```

&emsp;&emsp;进入编辑器，将 “eula=false” 改为 “eula=true”。

&emsp;&emsp;同样完成之后按 Ctrl+X，然后输入Y，最后回车完成编辑。

![修改eula.txt](img/img15.png)

&emsp;&emsp;以上操作完成之后，输入以下命令启动服务端：
```
sh ./start.sh
```

![启动start.sh](img/img16.png)

&emsp;&emsp;启动完成之后，就会看到以上的界面，这个界面就意味着服务端成功运行，Minecraft服务器就成功上线啦。

---

## 还有一些后续设置工作

&emsp;&emsp;现在我们的Minecraft服务端已经算是成功上线，接下来还需要一些后续设置工作。

&emsp;&emsp;首先，我们先暂时关掉我们的服务端，按下 “Ctrl+C”，输入：
```
nano server.properties
```

&emsp;&emsp;在编辑器里修改要修改的一些选项来设置Minecraft服务器，比如相对必要的设置：去掉正版验证，将其中 “online-mode=true”改为“online-mode=false”。

&emsp;&emsp;关于服务端properties详细参数设置，还请大家自行搜索，参数名称都是是英文，相信大家的水平完全可以看懂都是哪些参数，当然也可以发挥一下英语词典的用处。

&emsp;&emsp;重新设置之后再次输入 “sh ./start.sh” 启动服务端就可以啦。

&emsp;&emsp;启动完成之后可以直接关掉Xshell软件结束远程控制，下次再次启动连接之后，输入：
```
screen -r mc
```
&emsp;&emsp;这样就可以回到我们命名为mc的Screen进程中。

---

&emsp;&emsp;至此，我们的Minecraft私服已经完整上线开放了，在本地启动我们的Minecraft客户端，选择“多人模式”，人后选择“添加服务器”，看心情命名服务器名称，服务器地址就是整个教程远程连接一直用的那个公网ip地址。之后就可以加入服务器玩耍啦。

&emsp;&emsp;别的小伙伴同样可以通过添加服务器的方式连进去。接下来，一起在Minecraft私服里玩耍吧！