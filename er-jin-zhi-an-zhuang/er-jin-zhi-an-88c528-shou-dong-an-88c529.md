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

### 安装MySQL，建议版本用5.7

[安装MySQL 5.7](/er-jin-zhi-an-zhuang/an-zhuang-mysql-5-7.md)    点我

### 进入MySQL，创建数据库

> mysql&gt;create database bigops;

### 导入数据

> cd /opt/bigops/install/mysql/
>
> mysql -u _user -p bigops &lt; bigops-1.0.0.sql_

### 安装Medusa，一个密码检查工具

> yum -y install libssh2 openssl openssl-libs openssl-devel
>
> cd /opt/bigops/install/soft/
>
> tar zxvf medusa-2.2.tar.gz
>
> cd medusa-2.2
>
> ./configure --prefix=/usr
>
> make && make install

### 安装Ansible，配置管理工具

> yum -y install ansible
>
> cp -f /opt/bigops/install/ansible.cfg /root/.ansible.cfg

修改文件/etc/ansible/ansible.cfg，编辑内容

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

修改ssh命令的配置文件 /etc/ssh/ssh\_config，将StrictHostKeyChecking设置为no

> StrictHostKeyChecking no

### 安装jq，json文件解析工具

> cp  /usr/bin/jq /usr/bin/jqbak
>
> cp -f /opt/bigops/install/soft/jq-linux64 /usr/bin/jq
>
> chmod 777 /usr/bin/jq

### 安装Nmap，扫描工具

> cd /opt/bigops/install/soft/
>
> tar zxvf nmap-7.70.tgz
>
> cd nmap-7.70
>
> ./configure --prefix=/usr
>
> make && make install

### 安装Nginx

> yum -y install nginx
>
> mkdir /opt/ngxlog
>
> cp -f /opt/bigops/install/lnmp\_conf/nginx.conf /etc/nginx/nginx.conf
>
> cp -f /opt/bigops/install/lnmp\_conf/conf.d/default.conf /etc/nginx/conf.d/default.conf
>
> cp -f /opt/bigops/install/lnmp\_conf/conf.d/sso.conf /etc/nginx/conf.d/sso.conf
>
> cp -f /opt/bigops/install/lnmp\_conf/conf.d/work.conf /etc/nginx/conf.d/work.conf
>
> cp -f /opt/bigops/install/lnmp\_conf/conf.d/zabbix.conf /etc/nginx/conf.d/zabbix.conf

修改sso.conf、work.conf、zabbix.conf里的域名为你网站的域名

### 配置hosts文件

如果你没有注册域名，需要给服务器和你的笔记本系统都配置hosts。

Linux位置/etc/hosts，Windows位置C:\Windows\System32\drivers\etc\hosts

配置内容如下，IP改成你自己服务器的

192.168.100.2 sso.bigops.com

192.168.100.2 work.bigops.com

切记设置！切记设置！切记设置！！！

### 设置配置文件

> vi /opt/bigops/config/bigops.properties

![](/assets/config.png)

### 检查数据库是否创建成功

用你填写的host、port、user、pass登录MySQL

mysql -h host -u user -p

mysql&gt; show databases;

查看是否有bigops

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

### 启动Nginx

> service nginx restart

### 登录系统

访问域名：[http://work.bigops.com](http://work.bigops.com)  \(就是你刚才设置的home url\)

默认账号：admin

默认密码：bigops

登陆后请尽快修改密码。

### 启动bigserver，bigserver服务用于执行一些内置任务

> sh /opt/bigops/sbin/bigserver.sh restart

bigserver配置文件在/opt/bigops/sbin/bigserver.properties

可以根据需要调整轮询时间

![](/assets/bigserversetting.png)

### 设置定时清理日志

> crontab -e
>
> 00 01 \* \* \* /bin/sh /opt/bigops/bin/clean\_log.sh



