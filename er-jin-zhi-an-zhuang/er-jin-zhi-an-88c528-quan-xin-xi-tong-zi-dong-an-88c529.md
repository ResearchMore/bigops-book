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

### 安装MySQL 5.7或5.8，其他版本类似

添加安装源并安装

> cp -f /opt/bigops/install/yum.repos.d/\* /etc/yum.repos.d/
>
> yum -y install mysql-community-server mysql-community-client mysql-community-devel mysql-community-libs-compat

启动数据库

centos 6启动命令

> chown -R mysql:mysql /var/lib/mysql
>
> service mysqld start
>
> 如果启动失败，有可能/var/lib/mysql/有以前的残留文件，需要删除

centos 7启动命令

> systemctl start  mysqld.service

查找MySQL初始化的登录密码

> egrep 'temporary password' /var/log/mysqld.log

登录MySQL

> mysql -uroot -p

MySQL 5.7取消密码复杂度及更新密码

> set global validate\_password\_policy=0;
>
> set global validate\_password\_mixed\_case\_count=0;
>
> set global validate\_password\_number\_count=3;
>
> set global validate\_password\_special\_char\_count=0;
>
> set global validate\_password\_length=6;
>
> \#修改过期规则
>
> ALTER USER 'root'@'localhost' PASSWORD EXPIRE NEVER;
>
> \#更新密码
>
> ALTER USER 'root'@'localhost' IDENTIFIED BY 'your\_password';
>
> flush privileges;

MySQL 5.8取消密码复杂度及更新密码

> set global validate\_password.policy=0;
>
> set global validate\_password.mixed\_case\_count=0;
>
> set global validate\_password.number\_count=3;
>
> set global validate\_password.special\_char\_count=0;
>
> set global validate\_password.length=6
>
> \#修改过期规则
>
> ALTER USER 'root'@'localhost' IDENTIFIED BY 'your\_password' PASSWORD EXPIRE NEVER;
>
> \#更新密码
>
> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql\_native\_password BY 'your\_password';
>
> flush privileges;

优化MySQL 5.7

> cp -f /opt/bigops/install/lnmp\_conf/my-5.7.cnf /etc/my.cnf
>
> 修改datadir=/var/lib/mysql为你的数据存储目录
>
> 修改innodb\_buffer\_pool\_size=3G为你的内存的60%

优化MySQL 5.8

> cp -f /opt/bigops/install/lnmp\_conf/my-5.8.cnf /etc/my.cnf
>
> 修改datadir=/var/lib/mysql为你的数据存储目录
>
> 修改innodb\_buffer\_pool\_size=3G为你的内存的60%

最后重启MySQL

> service mysqld restart

注意：非MySQL 5.7版本请参考/opt/bigops/install/lnmp\_conf/my-5.7.cnf进行对应优化

### 配置Ansible

修改文件/etc/ansible/ansible.cfg

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

### 配置hosts文件

如果你没有注册域名，需要给服务器和你的笔记本系统都配置hosts。

Linux位置/etc/hosts，Windows位置C:\Windows\System32\drivers\etc\hosts

配置内容如下，IP改成你自己服务器的

192.168.100.2 sso.bigops.com

192.168.100.2 work.bigops.com

切记设置！切记设置！切记设置！！！

### 运行安装文件

> wget -O /opt/bigops/install/newos\_install.sh [https://raw.githubusercontent.com/yunweibang/bigops-install/master/newos\_install.sh](https://raw.githubusercontent.com/yunweibang/bigops-install/master/newos_install.sh)
>
> sh /opt/bigops/install/newos\_install.sh
>
> 根据提示填写相关信息，设置完后系统会自动启动。

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

运行下面命令，如果返回值包括「sso系统正常」，说明运行正常，如果没有返回值说明有问题，需要详细检查数据库配置，可以参考这个文件/opt/bigops/install/lnmp\_conf/my-5.7.cnf。

> curl 127.0.0.1:30001/signin/login

![](/assets/checkloginstatus.png)

### 登录系统

默认账号：admin

默认密码：bigops

登陆后请尽快修改密码。

### 启动bigserver，bigserver服务用于执行一些内置任务

> sh /opt/bigops/sbin/bigserver.sh restart

### 设置定时清理日志

> crontab -e
>
> 00 01 \* \* \* /bin/sh /opt/bigops/bin/clean\_log.sh



