---
title: 切换国内“源”
date: 2017-03-08 22:03:27
tags:
categories: 笔记本
---

### 切换 Node 源

由于 Node 的官方模块仓库网速太慢，模块仓库需要切换到阿里的源。
```
 npm config set registry https://registry.npm.taobao.org/
```
执行下面的命令，确认是否切换成功。
```
 npm config get registry
 ```
### 切换 Composer 源
设置中国的镜像：
```
composer config -g repo.packagist composer https://packagist.phpcomposer.com
```

通过 Composer 安装 Laravel 安装器：
```
composer global require "laravel/installer"
```

确保 $HOME/.composer/vendor/bin 在系统路径中，否则不能在任意路径调用 laravel 命令。

安装完成后，通过简单的 laravel new 命令即可在当前目录下创建一个新的 Laravel 应用，例如，laravel new blog 将会创建一个名为 blog 的新应用，且包含所有 Laravel 依赖。该安装方法比通过 Composer 安装要快很多：
```
laravel new blog
```
