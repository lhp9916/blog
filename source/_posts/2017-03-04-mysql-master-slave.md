---
title: MySQL 主从同步
date: 2017-03-04 23:50:56
tags:
categories: 技术分享
---
### MySQL 主从同步的机制
![](/images/20170304/Master-Slave.jpg)
MySQL 主从同步是在MySQL主从复制(Master-Slave Replication)基础上实现的，通过设置在Master MySQL上的binlog(使其处于打开状态)，Slave MySQL上通过一个I/O线程从Master MySQL上读取binlog，然后传输到Slave MySQL的中继日志中，然后Slave MySQL的SQL线程从中继日志中读取中继日志，然后应用到Slave MySQL的数据库中。这样实现了主从数据同步功能。

### MySQL主从同步的作用
- 可以作为一种备份机制，相当于热备份
- 可以用来做读写分离，均衡数据库负载

### 环境描述
OS：CentOS
主服务器master：192.168.3.222
从服务器slave：192.168.3.223

### mysql主服务器配置(master)
master服务器配置:
```
vim /etc/my.cnf
```

```
[mysqld]
server-id=1
log-bin=mysql-bin # 启用二进制日志
binlog-do-db=test_tongbu #指定数据库，如果不指定就是全部数据库
#binlog-ignore-db = mysql,information_schema #忽略写入binlog的库
```

重启服务器：
```
service mysqld  restart
```

在主服务器上建立帐户并授权slave_account：

```
#创建slave_account帐号，密码123456
mysql> grant replication slave on *.* to 'slave_account'@'%' identified by '123456';
#更新数据库权限
mysql>flush privileges;
```
查询master的状态：
```
mysql> show master status;
```
![](/images/20170304/master-status.jpg)
注：执行完这个步骤后不要再操作主数据库了，防止主数据库状态值变化。

### mysql从服务器配置(slave)
修改MySQL配置：
```
server-id =2  
```

执行同步命令，设置主数据库ip，同步帐号密码，同步位置
```
mysql>change master to master_host='192.168.3.222',master_user='slave_account',master_password='123456',master_log_file='mysql-bin.000014',master_log_pos=327;
```
开启同步功能
```
mysql>start slave;
```
检查从数据库状态：
```
mysql> SHOW SLAVE STATUS\G;
```
![](/images/20170304/slave-status.jpg)
注：Slave_IO_Running及Slave_SQL_Running进程必须正常运行，即YES状态，否则说明同步失败。

停止同步：
```
mysql>stop slave
```
到这里，主从数据库设置工作已经完成，自己可以新建数据库和表，插入和修改数据，测试一下是否成功。
