---
title: 使用 supervisor 管理进程
date: 2017-08-20 11:31:32
tags:
categories: 笔记本
---
[Supervisor](http://supervisord.org/) 是一个用 Python 写的进程管理工具，可以很方便的用来启动、重启、关闭进程。比如当服务异常死掉时，Supervisor 可以帮我们自动重启。

## 安装
```shell
pip install supervisor
```
如果没有 pip ，请先安装，这里我使用的系统是 Ubuntu
```shell
apt-get install python-pip
```

## 配置

```
//生成配置文件
echo_supervisord_conf > /etc/supervisord.conf
//编辑
vim /etc/supervisord.conf
```
把 /etc/supervisord.conf 里 include 部分的的配置修改如下
```
[include]
files = /usr/supervisord.conf/*.ini
```
```
mkdir /usr/supervisord.conf
cd /usr/supervisord.conf
vim redis.ini
```
`redis.ini` 添加如下内容
```
[program:redis]
command=/usr/local/bin/redis-server
autostart=false
autorestart=true
```
启动 supervisord
```
supervisord -c /etc/supervisord.conf
```
## 使用 supervisorctl
Supervisorctl 是 supervisord 的一个命令行客户端工具。
```
supervisorctl status
supervisorctl start redis
//查看进程
ps aux | grep redis
```
如果 redis 服务异常退出，supervisor会重启它，由此可以保障服务的稳定性。

参考
[http://liyangliang.me/posts/2015/06/using-supervisor/](http://liyangliang.me/posts/2015/06/using-supervisor/)