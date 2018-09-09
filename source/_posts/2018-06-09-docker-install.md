---
title: Docker 安装
date: 2018-06-09 11:32:15
tags:
---

## 安装 Docker

```
curl -sS https://get.docker.com/ | sh

# 国内用这个
curl -sSL https://get.daocloud.io/docker | sh

sudo usermod -aG docker your-user
```

## 安装 Docker Compose
```
curl -L https://get.daocloud.io/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```