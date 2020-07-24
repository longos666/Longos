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
