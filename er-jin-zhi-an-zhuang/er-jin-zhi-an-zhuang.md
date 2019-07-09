### **下载文件到/opt目录**

[http://www.bigops.com/dl.html](http://www.bigops.com/dl.html)

### **解压文件**

> 请把下载的文件放在/opt目录
>
> tar zxvf bigops-1.0.0.tar.gz
>
> mv bigops-1.0.0 bigops

### 检查运行环境

> sh /opt/bigops/bin/check\_env.sh

### 关闭SElinux

> vi  /etc/sysconfig/selinux
>
> SELINUX=disabled
>
> 需要重启系统

### 启动「安装向导」

> sh /opt/bigops/bin/start.sh

向导启动会比较慢，因为第一次连接不上数据库，需要等一个连接MySQL的超时时间，大概1-2分钟可以启动好。

### **检查BigOps Tomcat服务是否启动**

> \# netstat -nptl\|egrep 3000
>
> tcp        0      0 127.0.0.1:30000             0.0.0.0:\*                   LISTEN      32346/java
>
> tcp        0      0 127.0.0.1:30001             0.0.0.0:\*                   LISTEN      32346/java
>
> tcp        0      0 127.0.0.1:30002             0.0.0.0:\*                   LISTEN      26830/java
>
> tcp        0      0 127.0.0.1:30003             0.0.0.0:\*                   LISTEN      26830/java

### 需要2个域名

sso.xxxx.com和work.xxxx.com

如果没有注册的域名，也可以设置hosts，最好服务器和你的pc电脑都设置一下

### 确认Nginx、MySQL安装正确，**访问安装向导，根据提示进行操作**

[http://work.bigops.com/wizard/](http://work.bigops.com/wizard/)

![](/assets/Xnip2019-05-20_16-05-02.jpg)

# 登录系统

默认账号：admin

默认密码：bigops

# 定时清理日志

> crontab -e
>
> 00 01 \* \* \* /bin/sh /opt/bigops/bin/clean\_log.sh



