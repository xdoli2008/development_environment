# 阿里云ECS服务器CentOS7配置java环境

>1.确保服务器系统处于最新状态

```powershell
[root@localhost ~]# yum -y update
```

>如果显示以下内容说明已经更新完成

`Replaced:
grub2.x86_64 1:2.02-0.64.el7.centos grub2-tools.x86_64 1:2.02-0.64.el7.centos
Complete!`

>2.重启服务器

```powershell
[root@localhost ~]# reboot
```

## JDK安装

1、查看yum库中都有哪些jdk版本

```powershell
[root@lyh:] # yum search java|grep jdk
```

2、选择指定的版本安装，注意最后的 * 以及yum源安装的是openjdk，注意openjdk的区别。

```powershell
[root@lyh:] # yum install java-1.8.0-openjdk*
```

3、安装完成后查看版本信息

```powershell
[root@lyh:] # java -version
```

## mysql安装

>下载MySql安装包

```powershell
[root@lyh:] # rpm -ivh http://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm
```

>安装MySql

```powershell
[root@localhost ~]# yum install -y mysql-server
```

>设置开机启动Mysql

```powershell
[root@localhost ~]# systemctl enable mysqld.service
```

>检查是否已经安装了开机自动启动

```powershell
[root@localhost ~]# systemctl list-unit-files | grep mysqld
```

**如果显示 `mysqld.service enabled` 说明已经完成自动启动安装**

> 设置开启服务

```powershell
[root@localhost ~]# systemctl start mysqld.service
```

> 查看MySql默认密码

```powershell
[root@localhost ~]# grep 'temporary password' /var/log/mysqld.log
```

> 登陆MySql，输入用户名和密码

```powershell
[root@localhost ~]# mysql -uroot -p
```

> 修改当前用户密码

```sql
mysql> SET PASSWORD = PASSWORD('Abc123!_');
```

> 开启远程登录，授权root远程登录

```sql
mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'a123456!' WITH GRANT OPTION;
```

> 命令立即执行生效

```sql
mysql> flush privileges;
```

**Mysql是为了安全考虑，初始的时候并没有开启Root用户的远程访问权限，Root只能本地localhost，127.0.0.1访问，但是我们操作起来实在是不方便，下面我们就使用Xshell连接Linux服务器操作Mysql给Root用户添加远程访问权限。
我们先试用Xshell链接我们的远程Linux服务器：**

> 登录mysql

```powershell
[root@localhost ~]# mysql -u root -p
```

> 切换数据库

```sql
mysql> use mysql
```

> 添加一个root用户，密码暂时为空，允许任意Ip访问'%

```sql
mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '你的密码不能太简单' WITH GRANT OPTION;
```

> 修改root用户的密码

```sql
mysql> update user set authentication_string=PASSWORD('123456') where user='root';
```

> 刷新mysql的权限

```sql
mysql> flush privileges;
```

### 开启定时任务

> 查找my.cnf 配置文件

```powershell
[root@localhost ~]#  whereis my.cnf
```

> 编辑my.cnf 配置文件、在文件最后添加

`event_scheduler = 1`

重启mysql `service mysqld restart`

> 查看是否开启定时任务

```sql
mysql> show variables like '%sche%';
```

`event_scheduler=ON` 表示开启成功

### 解决 Group by 查询时的ONLY_FULL_GROUP_BY错误

> 编辑my.cnf 配置文件、在文件最后添加

`sql_mode = STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUT`

重启mysql `service mysqld restart`
