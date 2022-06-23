---
title: hello-nexus3之Windows安装
tags: 
date: 2022-06-23 14:20:42
id: 1655965242887928400
---
# 摘要

参考  [windows系统nexus3安装和配置.html](assets\references\windows系统nexus3安装和配置.html) ，在Windows下安装nexus3

# 版本选择

[Nexus Repository Manager 3.16.2-01](https://help.sonatype.com/repomanager3/product-information/download/download-archives---repository-manager-3#DownloadArchivesRepositoryManager3-NexusRepositoryManager3.16.2-01) 

# 启动

解压后在 bin 目录下使用管理员身份打开 power shell：

简单启动一下：

```
./nexus.exe /run 
```

注册为服务：

```
./nexus.exe /install nexus3
```

# 访问

 http://localhost:8081/
