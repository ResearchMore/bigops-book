# 操作系统

理论上支持所有Linux操作系统，建议使用：

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



### percona备份命令xtrabackup

参考地址：[https://www.percona.com/downloads/Percona-XtraBackup-LATEST/](https://www.percona.com/downloads/Percona-XtraBackup-LATEST/)

**安装依赖**

> yum -y install perl perl-devel libaio libaio-devel perl-Time-HiRes perl-DBD-MySQL libev

**CentOS 6 x86 64位运行**

> wget https://www.percona.com/downloads/Percona-XtraBackup-LATEST/Percona-XtraBackup-8.0-6/binary/redhat/6/x86\_64/percona-xtrabackup-80-8.0.6-1.el6.x86\_64.rpm
>
> rpm -ivh percona-xtrabackup-80-8.0.6-1.el6.x86\_64.rpm



**CentOS 7 x86 64位运行**

> wget https://www.percona.com/downloads/Percona-XtraBackup-LATEST/Percona-XtraBackup-8.0-6/binary/redhat/7/x86\_64/percona-xtrabackup-80-8.0.6-1.el7.x86\_64.rpm
>
> rpm -ivh percona-xtrabackup-80-8.0.6-1.el7.x86\_64.rpm



# 相关软件（Nginx+MySQL+PHP+Medusa）

Nginx、Medusa

> yum -y install nginx openssl openssl-devel medusa
>
> \#创建Nginx日志目录
>
> mkdir /opt/ngxlog/

MySQL，建议版本为5.7或5.8，如果已安装就忽略。也可以安装其他MySQL发行版。

> yum -y install mysql-community-server mysql-community-client mysql-community-devel

### Linux+Nginx+MySQL+PHP**建议配置**

[参考](https://github.com/yunweibang/bigops-LNMP-config)

