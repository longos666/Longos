# MQTT客户端安装和配置
一开始，我不知道MQTT，MQTT服务器，Node-red 和node.js的关的关系。很模糊，无从下手。杨老师发的安装说明很模糊，看不懂,甚至不知道MQTT Broker就是MQTT客户端。

从这张图上能看出MQTT Broker是什么。
MQTT Broker 有很多种，Mosquitto的官网中是这样描述自己的

Eclipse Mosquitto is an open source (EPL/EDL licensed) message broker that implements the MQTT protocol versions 5.0, 3.1.1 and 3.1. Mosquitto is lightweight and is suitable for use on all devices from low power single board computers to full servers.   
Eclipse Mosquitto 是实现MQTT协议的一个开源的message broker。  
wiki上面写道MQTT 协议定义了两种网络实体：消息代理（message broker）与客户端（client），broker和server一个意思



**Client**(A topic) -- Post/Push--  **Server**---Post/Push----**Client**(Another topic/Which you want to Post to).


1.  在官网下载完mosquitto后执行安装文件。Mosquitto默认安装路径是在“C:\Program Files\mosquitto”，安装目录的完整路径中，不能出现空格，否则在命令行就无法通过，于是我改成了d:\mos”。按照发的视频里，先在配置文件mosquitto.conf中，加入下面文本  
设置不允许匿名登录  
allow_anonymous false  
设置账户密码文件位置为  
password_file /mos/pwfile.example  
安装的文件中有提供一个设置账密码的文件pwfile.example，所以没有参照视频里再重新新建一个text文本了。

2.  插入新用户名及密码，输入密码时不会显示。打开CMD并进入mosquitto根目录(安装目录)输入  
mosquitto_passwd -c /MosquittoTest/pwfile.example FirstUserName （使用-c 参数会导致清空密码文件，重新插入用户）  
mosquitto_passwd /MosquittoTest/pwfile.example SecondUserName （不使用-c 表示追加用户，不影响旧用户）  
这里的FirstUserName和SecondUserName是用户名 可以自己命名，创建成功后在pwfile.example会有显示。

3.  启动mosquitto 进行测试。    
首先启动第一个cmd窗口启动服务：mosquitto.exe -c mosquitto.conf  
然后启动第二个cmd窗口订阅'dissun/topic'主题：mosquitto_sub -u (设置的用户名) -P (对应的密码) -t 'dissun/topic' -v  
最后启动第三个cmd窗口发布订阅信息：mosquitto_pub -u  (设置的用户名)  -P (对应的密码) -t 'dissun/topic' -m '(要发送的信息)'  
发送后在第二个窗口回车就会显示第三个窗口发送的内容


## 可能出现的问题

1. 无法启动mosquitto，mosquitto broker在任务管理器services类中一直显示starting 状态   
 在processes中找到mosquitto.exe 结束任务 然后再在cmd 中重新启动
 
 # Node Red 安装及环境配置
 
 先在官网下载node.js http://nodejs.org  
 安装过程全部点next  
 
 安装完后打开power shell 输入 (一个输完回车再另一个)  
 node -v  
 npm  -v  
 版本号显示正常则node.js安装成功  
 NPM是随同NodeJS一起安装的包管理工具
 在power shell运行命令  
 npm install -g --unsafe-perm node-red
 
 我第一次安装出错，找了下重新安装的方法   
 在power shell运行命令  npm cache clean --force  
 再运行 npm install -g --unsafe-perm node-red
 
 然后安装成功
 再输入node-red 运行
 
 ## 可能出现的问题
 
无法加载文件 C:\Users\liuzidong\AppData\Local\Temp\chocolatey\chocInstall\tools\chocolateyInstall.ps1，因为在此系统上禁止运行脚本。有关详细信息，请参阅 https:/go.microsoft.com/fwlink/?LinkID=135170 中的 about_Execution_Policies。所在位置 行:242 字符: 3+ & $chocInstallPS1+   ~~~~~~~~~~~~~~~    + CategoryInfo          : SecurityError: (:) []，PSSecurityException    + FullyQualifiedErrorId : UnauthorizedAccess

出现以上报错，要以管理员运行power shell   
运行set-ExecutionPolicy RemoteSigned

因为首次在计算机上启动 Windows PowerShell 时，现用执行策略很可能是 Restricted（默认设置）。    
Restricted 策略不允许任何脚本运行。
然后输入Y 再进行之前的操作就能成功安装node-red
默认每次打开node red 界面时都要在power shell 中输入node-red 
