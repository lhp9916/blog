---
title: Vagrant使用
date: 2016-10-02 00:38:20
tags:
---

### 初始化安装
做web开发的一定都用过虚拟机，以前安装一套新系统要去Ubuntu官网下载一个镜像文件，然后新建一个vitualbox虚拟机，然后需要有人值守的去完成整个系统安装过程，很是繁琐。但用了 Vagrant 以后这个过程变成无人值守的了，意思就是一个命令搞定一切。过程是这样：

首先，保证我的系统上有两个基础软件，一个是 vagrant 一个就是 virtualbox ，安装过程就是双击然后下一步下一步而已，没啥好说的。装好之后，到命令行中就有 vagrant 这个命令了。那么这个时候是不是就要去下载系统光盘了呢？ NO，有一个网站叫做https://vagrantcloud.com/ ，到上面搜一下 ubuntu，排名第一的这个 ubuntu / trusty64 就是 ubuntu 公司提供的 ubuntu 14.04 的64位系统镜像文件。<!-- more -->
新建一个目录，执行 
```
vagrant init
mkdir myproject
cd myproject
vagrant init ubuntu/trusty64
```
这样目录中就会多出一个文件叫 Vagrantfile 所有的机关也就都在这里了，继续执行
```
vagrant up
```
就会到 vagrant cloud 网站上下载 box 进行安装了。如果是第一次下载，可以需要等十来分钟，所以一般我是早上起来干这个活，网速比较快。但是，现在的情况是我之前以经在另外一个项目中执行过这个操作了，那么也就是这个box已经存在我本地机器上了。这时候，vagrant导入这个box进来，只需要几秒钟就可以在创建出一个新的virtualbox虚拟系统了，vagrant的基本思路是为每一个项目创建自己的一个虚拟机。而且这个系统和之前的系统是完全隔离的。如果我过一段时间不需要这台虚拟机了，执行 vagrant destroy 就都清理干净了，而且其他同样使用这个 box 虚拟机也不会受到影响。
打开 virtuabox的图形界面可以看到又多了一个虚拟机，也可以去修改配置，比如默认内存大小是 512，我一般用 2048 。Vigrant 有一个好处是所有一切都在命令行和配置文件中搞定，这样比图形界面用起来方便的多，所以一般是不需要启动 virtualbox 图形界面的。

### 基本配置

就拿修改内存为例子。打开 Vagrantfile 添加
config.vm.provider "virtualbox"do |v|
  v.memory = 2048
end
这样运行 vagrant reload 就修改成功了。

**创建新用户** 
vagrant ssh 登陆进来的用户名是 vagrant，这个用户挺好，执行 sudo 是不需要输入密码的，开发中实际使用挺好用的。不过如果我非要创建自己的用户也是可以的。
sudo adduser lhp --ingroup sudo
如何用这个用户的身份来登录呢？运行 vagrant up 的时候，可以看到有输出
==> default: Forwarding ports...
default: 22 => 2222 (adapter 1)
所以登录命令可以这样：
ssh lhp@127.0.0.1 -p 2222
输入密码就可以登录成功了。

**设置 IP**
添加config.vm.network "public_network", ip: "192.168.3.100"
以后可以浏览器中用 192.168.3.100 来访问里面的网站了。

**共享文件夹**
默认情况下，Vagrantfile 所在的这个文件夹，会自动对应虚拟机里面的 /vagrant 这个目录。这个意味着我不需要在虚拟机里面配置 sublimeText vim git 搜狗输入法 这些工具了，Mac/windows依旧是我写代码的环境。ubuntu 虚拟机是项目的安装运行环境。这个分工是太合理了！
通常的做法，项目源码就放在 myproject 目录下，把 Vagrantfile 和源码一起用 git 统一控制。然后再把apache/nginx的工作目录设置为/vagrant ,这样我们修改的文件就会实时同步到/vagrant 这个目录下，通过设置的IP来访问。

### vagant 常用命令
```
vagrant init #初始化box的操作
vagrant up	#启动虚拟机的操作
vagrant halt #关闭当前虚拟机
vagrant relaod #重新启动虚拟机，主要用于重新载入配置文件
vagrant destroy #停止当前正在运行的虚拟机并销毁所有创建的资源
```
vagrant box管理
```
vagrant box list
vagrant box add
vagrant box remove
vagrant box update
```