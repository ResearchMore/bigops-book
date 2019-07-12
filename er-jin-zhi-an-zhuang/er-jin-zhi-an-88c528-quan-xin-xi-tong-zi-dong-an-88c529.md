进QQ群获取安装软件

* QQ一群：1027031676

* QQ二群：建设中

入群暗号：BigOps

### **解压文件**

> 请把下载的文件放在/opt目录
>
> tar zxvf bigops-1.0.0.tar.gz
>
> mv bigops-1.0.0 bigops

### 安装MySQL 8或5.7，参考

[安装MySQL 8](/er-jin-zhi-an-zhuang/an-zhuang-mysql-8.md)   点我

[安装MySQL 5.7](/er-jin-zhi-an-zhuang/an-zhuang-mysql-5-7.md)   点我

### 配置hosts文件

如果你没有注册域名，需要给服务器和你的笔记本系统都配置hosts。

Linux位置/etc/hosts，Windows位置C:\Windows\System32\drivers\etc\hosts

配置内容如下

你的服务器IP sso.bigops.com

你的服务器IP work.bigops.com

切记设置！切记设置！切记设置！！！

### 下载并运行安装脚本

> wget -O /opt/bigops/install/newos\_install.sh [https://raw.githubusercontent.com/yunweibang/bigops-install/master/newos\_install.sh](https://raw.githubusercontent.com/yunweibang/bigops-install/master/newos_install.sh)
>
> sh /opt/bigops/install/newos\_install.sh
>
> 根据提示填写相关信息，设置完后服务会自动启动。
>
> dbhost不要填localhost，填127.0.0.1或对应IP

![](/assets/Xnip2019-07-11_21-15-29.jpg)

### **检查服务端口是否启动**

> \# netstat -nptl\|egrep 3000
>
> tcp        0      0 127.0.0.1:30000             0.0.0.0:\*                   LISTEN      32346/java
>
> tcp        0      0 127.0.0.1:30001             0.0.0.0:\*                   LISTEN      32346/java
>
> tcp        0      0 127.0.0.1:30002             0.0.0.0:\*                   LISTEN      26830/java
>
> tcp        0      0 127.0.0.1:30003             0.0.0.0:\*                   LISTEN      26830/java

### 验证sso服务是否正常

> curl 127.0.0.1:30001/signin/login

![](/assets/checkloginstatus.png)

如果返回值包括「sso系统正常」，说明运行正常，如果没有返回值说明有问题，需要详细检查数据库配置，可以参考这个文件/opt/bigops/install/lnmp\_conf/my-5.7.cnf。

### 验证work服务是否正常

> curl 127.0.0.1:30003/api/common/ssourl/

### ![](/assets/checkwork.png)

如果返回message为ok就是正常

### 启动Nginx，检查状态

> service nginx restart
>
> ps aux\|grep nginx.conf

![](/assets/nginx.png)

### 登录系统

访问域名：[http://work.bigops.com](http://work.bigops.com)  \(就是你刚才设置的home url\)

默认账号：admin

默认密码：bigops

登陆后请尽快修改密码。

### 配置Ansible

如果ansible已安装成功，这个文件/etc/ansible/ansible.cfg会存在，请修改

> \[defaults\]
>
> inventory = /etc/ansible/hosts
>
> stdout =json
>
> host\_key\_checking= False
>
> deprecation\_warnings=False
>
> \[ssh\_connection\]
>
> scp\_if\_ssh=True
>
> ssh\_args = -o LogLevel=quiet -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null

### 启动bigserver，bigserver服务用于执行一些内置任务

> sh /opt/bigops/sbin/bigserver.sh restart

bigserver配置文件在/opt/bigops/sbin/bigserver.properties

可以根据需要调整轮询时间

![](/assets/bigserversetting.png)

### 设置定时清理日志

> crontab -e
>
> 00 01 \* \* \* /bin/sh /opt/bigops/bin/clean\_log.sh



