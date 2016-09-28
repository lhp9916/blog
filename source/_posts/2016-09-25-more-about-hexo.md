---
title: Hexo换主题，域名绑定
date: 2016-09-25 22:09:54
tags:
---

### why Hexo ?
我写博客的萌芽阶段还是在学校学网页设计的时候，老师叫我们写一个个人网站作为节课作业，当时就用html/css/js写了几个页面交了上去，那时候还不知道有github的存在。后来无意间在慕课网上看到了有关 git和github的课程，认识了happypeter老师,他是用Jekyll+css写的博客托管到github上，Jekyll可以用markdown语法来写作，但是要自己写css装饰，对于我一个做后台的来说，不太擅长做页面美化的工作。后来也是机缘巧合在github上发现李笑来先生的博客，发现了Hexo。hexo是一个快速、简洁且高效的博客框架。支持 Markdown，并快速将markdown编译生成html静态页面，支持一键部署......还有，支持换主题，并提供了很多主题可供选择，对于不做会页面美化的人来说，简直是福音。所以，我开始全面拥抱Hexo。
<!-- more -->
### 换主题
Hexo 换主题非常容易，您只要在 themes 文件夹内，新增一个任意名称的文件夹，并修改 _config.yml 内的 theme 设定，即可切换主题。你可以去[https://hexo.io/themes/](https://hexo.io/themes/)选择自己喜欢的主题。

比如，我选择的NexT，接下来进入作者的github，找到该主题的项目仓库及[使用文档](http://theme-next.iissnan.com/getting-started.html)，当然这些你也可以通过搜索引擎完成。
首先下载主题，进入你的项目目录，
```
git clone https://github.com/iissnan/hexo-theme-next themes/next
```
启用主题,与所有 Hexo 主题启用的模式一样。当克隆/下载完成后打开站点配置文件，找到theme字段，并将其值更改为 next。
```
theme: next
```
验证主题，继续输入
```
hexo s
```
此时即可使用浏览器访问 http://localhost:4000，检查站点是否正确运行。
关于更多的主题设定，我这里就不多说，相信通过看文档就可以了，毕竟看文档也是程序员必备的能力。

### 绑定个人域名
你可以通过yourname.github.io来访问你的博客，还可以绑定你的域名。如果你没有可以先到[万网](https://wanwang.aliyun.com/)上注册一个，.top的域名最便宜，首年才2块钱。
我注册了一个域名liuhaipeng.top，接下来去控制台->域名->解析，添加这么一条记录。
![](/images/20160925/yuming.jpg)
然后在source目录下添加一个名为CNAME的文件，文件里面写入注册好的域名。
![](/images/20160925/cname.jpg)
最后，把项目部署到github上，那么你就可以通过你注册的域名来访问你的博客网站。

### hexo常用命令及简写
我写博客的流程通常是这样
```
    hexo new <title>    #新建文章，写作
    hexo server			#实时预览
    hexo generate       #生成静态页面至public目录             
    hexo deploy         #将.deploy目录部署到GitHub
```
当然，如果每次输入那么长命令，那么一定想到用简写：
```
    hexo n == hexo new
    hexo g == hexo generate
    hexo s == hexo server
    hexo d == hexo deploy
```