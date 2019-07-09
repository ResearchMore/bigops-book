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

### 安装MySQL

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

优化MySQL

> cp -f /opt/bigops/install/lnmp\_conf/my-5.7.cnf /etc/my.cnf
>
> service mysqld start



### 运行安装文件

> sh /opt/bigops/install/newos\_install.sh



