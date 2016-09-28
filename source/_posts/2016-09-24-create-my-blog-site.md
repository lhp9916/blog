---
title: Hexo+Github Pages建立博客站点
date: 2016-09-24 21:34:59
tags:
---

### 开始之前
开始之前，我假定你已经注册了Github账号，并已经安装好了git,nodejs和一个文本编辑器。如果还没有，也可以先假装已经安装好了这些工具......听起来好像没道理，但你试试就知道了。

### 在 Github 上创建一个 Repo
在浏览器中登录 Github，创建一个 Repo，名称格式为 yourname.github.io。比如，我个人的 Github 账户用户名是 lhp9916，所以，我的这个 Repo 的名称就是 lhp9916.github.io。这里是Github官方的pages服务介绍 [pages.github.com](https://pages.github.com/)可以参考一下。
<!-- more -->
### 安装Hexo
首先确认本地已经安装好了git和npm。npm是nodejs的一个包管理工具，nodejs安装时会自动安装npm。
```
git --version
npm --version
```
在命令行中继续输入,即可安装Hexo
```
npm install hexo -g
npm install hexo-cli -g
```

### 初始化本地站点
```
hexo init <folder>    //初始化站点
cd <folder>  //进入项目目录
npm install     //安装hexo依赖包
hexo generate   //生成网站
hexo server     //启动一个本地服务器
```
这些完成之后，你就可以打开浏览器，在地址栏里输入： localhost:4000，在本地先看看网站是什么样子了。

### 配置
你可以在 _config.yml 中修改大部份的配置。具体的可以参考[hexo的官方文档](https://hexo.io/zh-cn/docs/)，里面有详细的介绍。修改配置必须结束hexo server服务，重新启动后才能生效。

### 写作
你可以执行下列命令来创建一篇新文章。
```
hexo new  <title>
```
执行后会在source/_posts目录下生成一个.md文件，打开就可以输入你想输入的内容。

### 部署到github上
去Github把你的Repo的git地址拷贝出来。地址是类似https://github.com/yourname/yourname.github.io.git 这种形式（其中，yourname是你github上的用户名）。选择 _config.yml 文件，找到deploy那一部分，改成：
```
deploy:
  type: git
  repo: https://github.com/yourname/yourname.github.io.git
```
注意，把 yourname 改成你的 Github 用户名。(对了，采用git方式部署，你必须事先在github上添加你的SSH key.)
当然你需要安装hexo-deployer-git这个部署工具。
```
npm install hexo-deployer-git --save
```
现在是最后一步了，在命令行里依次输入：
```
hexo deploy
```
部署成功后，在浏览器中输入yourname.github.io即可看到页面。

### 阶段性成果
到现在为止，你已经学会写作并发布了自己所写的文章，假定一切进行得很顺利。
不一定很简单 —— 对新手因为上面的过程中，每一个尽管相当简单的步骤，都可能出现各种莫名其妙的错误（比如，不小心使用了中文输入法的点字符“。”等等）…… 保持耐心，反复来过就好。遇到异常的地方，看下官方文档，google一下，你会解决90%的问题。当然你也可以发邮件给我（[lhp9916@gmail.com](mailto:lhp9916@gmail.com)），我很乐意和你一起解决问题。

### 继续折腾
没完事儿呢…… 这才刚刚开始，你现在有了个所有人都可以访问的站点，然后就要做起码两件事儿了：
>学会使用 Markdown 语法书写文章
>把站点装扮得更好看一些，也就是更换主题

好了，今天就到这了，下一篇再聊聊如何给博客换主题和绑定自己的域名。