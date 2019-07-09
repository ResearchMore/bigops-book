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

### 启动「安装向导」

> sh /opt/bigops/bin/start.sh

### **检查BigOps Tomcat服务是否启动**

> \# netstat -nptl\|egrep '30002\|30003'
>
> tcp6       0      0 127.0.0.1:30002         :::\*                    LISTEN      2710/java
>
> tcp6       0      0 127.0.0.1:30003         :::\*                    LISTEN      2710/java

### 确认Nginx、MySQL安装正确，**访问安装向导，根据提示进行操作**

[http://work.bigops.com/wizard/](http://work.bigops.com/wizard/)

wizard启动会比较慢，因为第一次连接不上数据库，需要等一个连接MySQL的超时时间，大概1-2分钟可以启动好。

![](/assets/Xnip2019-05-20_16-05-02.jpg)

# 登录系统

默认账号：admin

默认密码：bigops

# 定时清理日志

> crontab -e
>
> 00 01 \* \* \* /bin/sh /opt/bigops/bin/clean\_log.sh



