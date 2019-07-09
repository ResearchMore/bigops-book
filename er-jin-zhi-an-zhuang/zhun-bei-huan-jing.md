# 操作系统

建议使用一台全新的服务器，理论上支持所有Linux操作系统，建议使用：

* CentOS 6 x86 64位
* CentOS 7 x86 64位

# 需要2个域名

1、sso.xxxx.com，用于同一认证

2、work.xxxx.com，用于主站

如果没有注册的域名，也可以设置hosts。

服务器和你的pc电脑的hosts都需要设置，切记！切记！切记！！！

要不然就会出现这个问题

![](/assets/bug1.png)

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

**MySQL，建议版本为5.7。**

> yum -y install mysql-community-server mysql-community-client mysql-community-devel

**Medusa，检查密码正确性工具。**

> yum -y install libssh2
>
> cd /opt/bigops/soft/
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

### Nginx**建议配置**

[https://github.com/yunweibang/bigops-LNMP-config/blob/master/nginx/nginx.conf](https://github.com/yunweibang/bigops-LNMP-config/blob/master/nginx/nginx.conf)

[https://github.com/yunweibang/bigops-LNMP-config/tree/master/nginx/conf.d](https://github.com/yunweibang/bigops-LNMP-config/tree/master/nginx/conf.d)

### MySQL**建议配置**

[https://github.com/yunweibang/bigops-LNMP-config/tree/master/mysql](https://github.com/yunweibang/bigops-LNMP-config/tree/master/mysql)

### PHP**建议配置**

[https://github.com/yunweibang/bigops-LNMP-config/tree/master/php](#)

