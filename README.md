# MQTT客户端安装和配置
一开始，我不知道MQTT，MQTT服务器，Node-red 和node.js的关的关系。很模糊，无从下手。杨老师发的安装说明很模糊，看不懂,甚至不知道MQTT Broker就是MQTT客户端。

从这张图上能看出MQTT Broker是什么。
MQTT Broker 有很多种，Mosquitto的官网中是这样描述自己的

Eclipse Mosquitto is an open source (EPL/EDL licensed) message broker that implements the MQTT protocol versions 5.0, 3.1.1 and 3.1. Mosquitto is lightweight and is suitable for use on all devices from low power single board computers to full servers. 
"Eclipse Mosquitto 是实现MQTT协议的一个开源的message broker。
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
