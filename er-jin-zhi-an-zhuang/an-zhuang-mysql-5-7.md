### 安装MySQL 5.7

添加安装源

> cp -f /opt/bigops/install/yum.repos.d/\* /etc/yum.repos.d/

设置安装源，打开对应版本的源

vi /etc/yum.repos.d/mysql-community.repo

> \[mysql57-community\]
>
> name=MySQL 5.7 Community Server
>
> baseurl=[http://repo.mysql.com/yum/mysql-5.7-community/el/$releasever/$basearch/](http://repo.mysql.com/yum/mysql-5.7-community/el/$releasever/$basearch/)
>
> enabled=1  \#这里设置为1，把其他版本设置为0
>
> gpgcheck=0
>
> gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql

安装MySQL

> yum -y install mysql-community-server mysql-community-client mysql-community-devel mysql-community-libs-compat

复制优化的配置文件

> cp -f /opt/bigops/install/lnmp\_conf/my-5.7.cnf /etc/my.cnf
>
> 修改datadir=/var/lib/mysql为你的数据存储目录，这个目录需要给mysql用户属主权限chown -R mysql:mysql xxxxxxxxxx。
>
> 修改innodb\_buffer\_pool\_size=3G为你的内存的60%

初始化目录，会丢失以前的数据，确认没有有用数据再操作

> mysqld --user=mysql --lower-case-table-names=0 --initialize-insecure
>
> root默认口令为空。如果启动失败，有可能basedir有以前的残留文件，需要删除。

centos 6启动命令

> chown -R mysql:mysql /var/lib/mysql
>
> service mysqld start

centos 7启动命令

> systemctl start  mysqld.service

查找MySQL初始化的登录密码

> egrep 'temporary password' /var/log/mysqld.log

登录MySQL

> mysql -uroot -p

取消密码复杂度，有的小版本有，有的小版本没这些变量，没有就忽略

> set global validate\_password\_policy=0;
>
> set global validate\_password\_mixed\_case\_count=0;
>
> set global validate\_password\_number\_count=0;
>
> set global validate\_password\_special\_char\_count=0;
>
> set global validate\_password\_length=6;

修改root@localhost密码，your\_password改成你的密码

> use mysql;
>
> ALTER USER 'root'@'localhost' IDENTIFIED BY 'your\_password' PASSWORD EXPIRE NEVER;
>
> grant all privileges on \*.\* to "root"@"localhost" identified with mysql\_native\_password by "your\_password";

添加root@127.0.0.1用户，your\_password改成你的密码。重要！重要！重要！

> grant all privileges on \*.\* to "root"@"127.0.0.1" identified with mysql\_native\_password by "your\_password";
>
> flush privileges;

重启MySQL

> service mysqld restart



