---
title: CentOS 安装 Python3 笔记
date: 2017-02-28 21:07:10
tags:
categories: 技术分享
---

最近有时间就学习了 python ，写一下笔记。

windows 下安装Python比较简单，这里我推荐一个 Python 的发行版—— [Anaconda](https://www.continuum.io/downloads)，这个发行版默认带了很多包。下面讲下怎样在 CentOS 上安装 python3。
一般安装好 CentOS 后都会自带 python ，这个版本是2.x，我们要安装 Python3。

### 安装

#### 安装基础依赖包
```
yum install -y ncurses-devel openssl openssl-devel zlib-devel gcc make glibc-devel libffi-devel glibc-static glibc-utils sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-deve
```

#### 下载源码
```
wget https://www.python.org/ftp/python/3.6.0/Python-3.6.0.tgz
```
由于国外下载比较慢，推荐使用国内源来进行下载，这里使用sohu的源
```
wget http://mirrors.sohu.com/python/3.6.0/Python-3.6.0.tgz
```
#### 解压
```
tar xvf Python-3.6.0.tgz
```
#### 编译安装
```
cd Python-3.6.0
./configure --prefix=/usr/local/python3
make all
make install
```
等待安装完成：
![](https://lhp9916.github.io/images/20170228/install-success.jpg)

### 使用
#### 添加软链接
```
ln -s /usr/local/python3/bin/python3.6 /usr/local/bin/python3
ln -s /usr/local/python3/bin/pip3.6 /usr/local/bin/pip3
```

#### 使用 python3 命令
![](https://lhp9916.github.io/images/20170228/python-version.jpg)
如上图所示，出现类似的内容，证明python安装成功。

#### pip 使用
pip 是Python的包管理工具，类似npm、composer。
![](https://lhp9916.github.io/images/20170228/pip-install.jpg)
