### 进QQ群获取安装软件

* QQ一群：1027031676

* QQ二群：建设中

入群暗号：BigOps

### **解压文件**

> 请把下载的文件放在/opt目录
>
> tar zxvf bigops-1.0.0.tar.gz
>
> mv bigops-1.0.0 bigops

### 检查运行环境

> sh /opt/bigops/bin/check\_env.sh

### 进入MySQL，创建数据库，建议MySQL版本为5.7

> mysql&gt;create database bigops;
>
> mysql&gt;exit

### 导入数据

> cd /opt/bigops/install/mysql/
>
> mysql -u _user -p bigops &lt; bigops-1.0.0.sql_

### 修改配置文件

> vi /opt/bigops/config/bigops.properties

![](/assets/config.png)

### 检查运行环境并启动服务

> \#检查环境
>
> sh /opt/bigops/bin/check\_env.sh
>
> \#启动主站web
>
> sh /opt/bigops/bin/restart.sh
>
> \#启动bigserver
>
> sh /opt/bigops/sbin/bigserver.sh restart

### **检查服务是否启动**

> \# netstat -nptl\|egrep 3000
>
> tcp        0      0 127.0.0.1:30000             0.0.0.0:\*                   LISTEN      32346/java
>
> tcp        0      0 127.0.0.1:30001             0.0.0.0:\*                   LISTEN      32346/java
>
> tcp        0      0 127.0.0.1:30002             0.0.0.0:\*                   LISTEN      26830/java
>
> tcp        0      0 127.0.0.1:30003             0.0.0.0:\*                   LISTEN      26830/java

### 登录系统

默认账号：admin

默认密码：bigops

### 设置定时清理日志

> crontab -e
>
> 00 01 \* \* \* /bin/sh /opt/bigops/bin/clean\_log.sh



