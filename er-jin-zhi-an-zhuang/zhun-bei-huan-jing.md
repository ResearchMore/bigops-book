### 操作系统

建议使用一台全新的服务器，理论上支持所有Linux操作系统，建议使用：

* CentOS 6 x86 64位
* CentOS 7 x86 64位

### 需要2个域名

1、sso.xxxx.com，用于统一认证

2、work.xxxx.com，用于主站

如果你没有注册域名，需要给服务器和你的笔记本系统都配置hosts。

Linux位置/etc/hosts，Windows位置C:\Windows\System32\drivers\etc\hosts

配置内容例如：

192.168.100.2 sso.bigops.com

192.168.100.2 work.bigops.com

切记设置！切记设置！切记设置！！！否则会报错

### ![](/assets/bug1.png) 关闭SElinux

> vi /etc/sysconfig/selinux
>
> SELINUX=disabled
>
> 需要重启系统



### 优化操作系统

> rm -f /etc/security/limits.d/\*
>
> sed -i '/^\[^\#\].\*/d' /etc/security/limits.conf
>
> echo -e "\*\t\tsoft\tnofile\t\t655360"&gt;&gt;/etc/security/limits.conf
>
> echo -e "\*\t\thard\tnofile\t\t655360"&gt;&gt;/etc/security/limits.conf
>
> echo -e "\*\t\tsoft\tmemlock\t\tunlimited"&gt;&gt;/etc/security/limits.conf
>
> echo -e "\*\t\thard\tmemlock \tunlimited"&gt;&gt;/etc/security/limits.conf
>
> echo -e "\*\t\tsoft\tnproc\t\t655360"&gt;/etc/security/limits.d/90-nproc.conf
>
> echo -e "\*\t\thard\tnproc\t\t655360"&gt;&gt;/etc/security/limits.d/90-nproc.conf



