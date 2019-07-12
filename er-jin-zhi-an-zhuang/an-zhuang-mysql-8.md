### \(推荐\)方法一：脚本安装MySQL 8

> wget [https://raw.githubusercontent.com/yunweibang/bigops-install/master/mysql8.sh](https://raw.githubusercontent.com/yunweibang/bigops-install/master/mysql8.sh)
>
> sh mysql8.sh

看到下面提示，输入root@127.0.0.1用户密码，保存好一会使用。另外root@localhost密码为空

> please input root@127.0.0.1 password, default bigops
>
> &gt;输入你的密码

### 方法二：手动安装MySQL 8

添加安装源

> wget -O /etc/yum.repos.d/CentOS-Base.repo [https://raw.githubusercontent.com/yunweibang/yum.repos.d/master/CentOS-Base.repo](https://raw.githubusercontent.com/yunweibang/yum.repos.d/master/CentOS-Base.repo)
>
> wget -O /etc/yum.repos.d/epel.repo [https://raw.githubusercontent.com/yunweibang/yum.repos.d/master/epel.repo](https://raw.githubusercontent.com/yunweibang/yum.repos.d/master/epel.repo)
>
> wget -O /etc/yum.repos.d/mysql8-community.repo [https://raw.githubusercontent.com/yunweibang/yum.repos.d/master/mysql8-community.repo](https://raw.githubusercontent.com/yunweibang/yum.repos.d/master/mysql-community.repo)
>
> wget -O /etc/yum.repos.d/nginx.repo [https://raw.githubusercontent.com/yunweibang/yum.repos.d/master/nginx.repo](https://raw.githubusercontent.com/yunweibang/yum.repos.d/master/nginx.repo)
>
> wget -O /etc/yum.repos.d/remi.repo [https://raw.githubusercontent.com/yunweibang/yum.repos.d/master/remi.repo](https://raw.githubusercontent.com/yunweibang/yum.repos.d/master/remi.repo)

安装MySQL

> yum -y install mysql-community-server mysql-community-client mysql-community-devel mysql-community-libs-compat

优化配置文件

> wget -O /etc/my.cnf https://raw.githubusercontent.com/yunweibang/bigops-config/master/mysql/my-8.cnf
>
> chown -R mysql:mysql /var/lib/mysql
>
> 修改参数innodb\_buffer\_pool\_size为你的内存的50%~60%，比如你有8G内存：
>
> innodb\_buffer\_pool\_size=4G

初始化目录，会丢失以前的数据，确认当前数据是否有用，再进行操作

> mysqld --user=mysql --lower-case-table-names=0 --initialize-insecure
>
> root默认口令为空。如果启动失败，有可能basedir有以前的残留文件，需要删除。

登录MySQL

> mysql -uroot -p

取消密码复杂度，有的小版本有，有的小版本没这些变量，没有就忽略

> set global validate\_password.policy=0;
>
> set global validate\_password.mixed\_case\_count=0;
>
> set global validate\_password.number\_count=0;
>
> set global validate\_password.special\_char\_count=0;
>
> set global validate\_password.length=6;

修改root@localhost密码，your\_password改成你的密码

> use mysql;
>
> ALTER USER 'root'@'localhost' IDENTIFIED BY 'your\_password' PASSWORD EXPIRE NEVER;
>
> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql\_native\_password BY 'your\_password';

添加用户root@127.0.0.1，给用户授权，重要！重要！重要！

> create user 'root'@'127.0.0.1' identified by 'your\_password';
>
> ALTER USER 'root'@'127.0.0.1' IDENTIFIED BY 'your\_password' PASSWORD EXPIRE NEVER;
>
> grant all privileges on \*.\* to 'root'@'127.0.0.1';
>
> flush privileges;

重启MySQL

> service mysqld restart



