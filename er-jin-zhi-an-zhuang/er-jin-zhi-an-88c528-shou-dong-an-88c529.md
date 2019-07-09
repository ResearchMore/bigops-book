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

> cp -f /opt/bigops/install/yum.repos.d/\* /etc/yum.repos.d/
>
> yum -y install mysql-community-server mysql-community-client mysql-community-devel mysql-community-libs-compat

查看MySQL登录密码

> egrep 'temporary password' /var/log/mysqld.log

取消MySQL密码复杂度设置

> set global validate\_password\_policy=0;
>
> set global validate\_password\_mixed\_case\_count=0;
>
> set global validate\_password\_number\_count=3;
>
> set global validate\_password\_special\_char\_count=0;
>
> set global validate\_password\_length=3;
>
> ALTER USER 'root'@'localhost' PASSWORD EXPIRE NEVER;
>
> flush privileges;

修改root默认登录密码，your\_password为你的新密码

> ALTER USER 'root'@'localhost' IDENTIFIED BY 'your\_password';

优化MySQL

> cp -f /opt/bigops/install/lnmp\_conf/my-5.7.cnf /etc/my.cnf
>
> 修改datadir=/var/lib/mysql为你的数据存储目录
>
> 修改innodb\_buffer\_pool\_size=3G为你的内存的60%

最后重启MySQL

> service mysqld restart

### 进入MySQL，创建数据库

> mysql&gt;create database bigops;

### 导入数据

> cd /opt/bigops/install/mysql/
>
> mysql -u _user -p bigops &lt; bigops-1.0.0.sql_

### 安装Medusa，一个密码检查工具

> yum -y install libssh2
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

并修改文件/etc/ansible/ansible.cfg

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

StrictHostKeyChecking no

### 安装jq，json文件解析工具

> cp  /usr/bin/jq /usr/bin/jqbak
>
> cp -f /opt/bigops/install/soft/jq-linux64 /usr/bin/jq
>
> chmod 777 /usr/bin/jq

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

### 设置配置文件

> vi /opt/bigops/config/bigops.properties

![](/assets/config.png)

### 检查运行环境并启动网站服务

> \#检查环境
>
> sh /opt/bigops/bin/check\_env.sh
>
> \#启动网站服务
>
> sh /opt/bigops/bin/restart.sh

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

登陆后请尽快修改密码

### 启动bigserver，bigserver服务用于执行一些内置任务

> sh /opt/bigops/sbin/bigserver.sh restart

### 设置定时清理日志

> crontab -e
>
> 00 01 \* \* \* /bin/sh /opt/bigops/bin/clean\_log.sh



