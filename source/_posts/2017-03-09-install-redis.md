---
title: redis 安装
date: 2017-03-09 22:05:31
tags:
categories: 笔记本
---

### 开始之前
系统环境：CentOS release 6.8 (Final)
安装 gcc 和 tcl 依赖：
```
 yum install -y gcc tcl
```

### 编译安装

```
wget http://download.redis.io/releases/redis-3.2.8.tar.gz

tar -xf redis redis-3.2.8.tar.gz

make

make install
```
redis 安装到 /usr/local/bin 目录下。

### 配置
拷贝配置文件：
```
cp redis.conf   /root/config/
```
修改配置文件
```
vim   /root/config/redis.conf
```
将 daemonize 改为 yes ，即后台启动 redis 服务器

### 启动 redis 服务器
```
redis-server   /root/config/redis.conf
```

### 登录redis
```
redis-cli
```
