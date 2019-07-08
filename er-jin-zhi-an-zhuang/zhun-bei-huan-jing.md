# 操作系统

建议使用一台全新的服务器，理论上支持所有Linux操作系统，建议使用：

* CentOS 6 x86 64位
* CentOS 7 x86 64位

# 软件仓库

### epel仓库、remi仓库

**CentOS 6 x86 64位运行**

> wget -O /etc/yum.repos.d/CentOS-Base.repo [http://mirrors.aliyun.com/repo/Centos-6.repo](http://mirrors.aliyun.com/repo/Centos-6.repo)
>
> wget -O /etc/yum.repos.d/epel.repo [http://mirrors.aliyun.com/repo/epel-6.repo](http://mirrors.aliyun.com/repo/epel-6.repo)

**CentOS 7 x86 64位运行**

> wget -O /etc/yum.repos.d/CentOS-Base.repo [http://mirrors.aliyun.com/repo/Centos-7.repo](http://mirrors.aliyun.com/repo/Centos-7.repo)
>
> wget -O /etc/yum.repos.d/epel.repo [http://mirrors.aliyun.com/repo/epel-7.repo](http://mirrors.aliyun.com/repo/epel-7.repo)

### **remi仓库**

> remi包含最新版本 PHP 和 MySQL 包的 Linux 源，由 Remi 提供维护。请按照 [向导](https://rpms.remirepo.net/wizard/ "向导") 的指示安装配置。

# 相关软件

**Nginx**

> yum -y install nginx
>
> \#创建Nginx日志目录
>
> mkdir /opt/ngxlog/

**MySQL，建议版本为5.7或5.8，如果已安装就忽略。也可以安装其他MySQL发行版。**

> yum -y install mysql-community-server mysql-community-client mysql-community-devel

**Medusa，检查密码正确性工具。**

> yum -y install medusa libssh2
>
> 源码安装
>
> yum -y install libssh2
>
> wget -c [http://foofus.net/goons/jmk/tools/medusa-2.2.tar.gz](http://foofus.net/goons/jmk/tools/medusa-2.2.tar.gz)
>
> tar zxvf medusa-2.2.tar.gz
>
> ./configure --prefix=/usr
>
> make && make install

**Nmap，扫描工具，建议下载源代码安装最新版本。**

> yum -y install nmap

**jq，json格式处理工具，建议下载源代码安装最新版本。**

> yum -y install jq

**Ansibile，配置管理工具**

> yum -y install ansible
>
> cp /opt/bigops/config/ansible.cfg /root/.ansible.cfg

**PHP**

> 如果有运行zabbix，还需要安装php
>
> yum -y install zlib zlib-devel php php-mysql php-gd php-fpm php-mbstring mcrypt php-mcrypt openssl-devel pcre-devel php-bcmath php-xml php-xmlrpc php-ldap

### Nginx+MySQL+PHP**建议配置**

[参考](https://github.com/yunweibang/bigops-LNMP-config)

