---
title: 基于 OpenWrt 搭建 KMS 服务
date: 2019-10-11 10:38:57
tags:
---

## 准备工作
首先需要一台安装了 OpenWrt 系统的路由，然后在路由系统中安装 vlmcsd 插件，这是一个开源的 KMS服务器。我使用的是 KoolShare LEDE 固件，LEDE自带软件中心，安装插件很方便。

## 激活
#### Windows 激活
以管理员身份运行 cmd 或 powershell
```
# 卸载WINDOWS自带密钥
slmgr /upk

# 新密钥
slmgr /ipk W269N-WFGWX-YVC9B-4J6C9-T83GX

# 指定 Windows KMS服务器到你的路由器
slmgr /skms 192.168.1.1

# 激活
slmgr /ato
```
**注意事项**
1. 保证你的WINDOWS系统和OFFICE是VOL版的，这样才可以激活
1. WINDOWS系统除了旗舰版和家庭版都能激活（我使用WIN10 专业版）
1. 激活期限为 180 天
1. 常用Windows VL版KMS激活密钥列表：
Win10专业版KMS： W269N-WFGWX-YVC9B-4J6C9-T83GX
Win10企业版KMS： NPPR9-FWDCX-D2C8J-H872K-2YT43
Win10LTSB版KMS： DCPHK-NFMTC-H88MJ-PFHPY-QJ4BJ
Win10家庭版KMS： TX9XD-98N7V-6WMQ6-BX7FG-H8Q99
Win10教育版KMS： NW6C2-QMPVW-D7KKK-3GKT6-VCFB2
Win7专业版KMS： FJ82H-XT6CR-J8D7P-XQJJ2-GPDD4
Win7企业版KMS： 33PXH-7Y6KF-2VJC9-XBBR8-HVTHH

#### OFFICE 激活
找到你的OFFICE目录，我的是OFFICE 2016 32位版，目录为：
`C:\Program Files (x86)\Microsoft Office\Office16`
进去这个目录，可以看见有个`OSPP.VBS`文件
如果是OFFICE 2016 64位版，目录应为：
`C:\Program Files\Microsoft Office\Office16`
```
cd “C:\Program Files (x86)\Microsoft Office\Office16” # （双引号中对应你的实际目录）

cscript ospp.vbs /sethst:192.168.1.1 #你的路由IP

cscript ospp.vbs /act
```
**注意事项**
OFFICE 2016在 MSDN 只有专业增强版，下载进来并安装，可以使用 [office-C2R-to-VOL](https://github.com/kkkgo/office-C2R-to-VOL) 这个工具能将 OFFICE 转为 VOL 版，然后再激活。

使用系统自身批处理命令激活，因此会有后门，也不用担心病毒和信息窃取之类的。如果失败，请检查 Windows 和 OFFICE 具体版本信息。
