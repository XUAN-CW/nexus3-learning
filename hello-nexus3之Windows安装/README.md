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

解压后可见：

```
33719@DESKTOP-NBHJ5B7 MINGW64 /c/portable/nexus-3.16.2-01-win64
$ ls
nexus-3.16.2-01/  sonatype-work/
```

在 **nexus-3.16.2-01/bin** 目录下使用管理员身份打开 power shell：

简单启动一下，关了命令行就没了：

```
./nexus.exe /run
```

注册为服务，开关机之后还有：

```
./nexus.exe /install nexus3
```

# 访问

 http://localhost:8081/

# 配置

**nexus-3.14.0-04/etc/nexus-default.properties** 可进行配置，下面说两个常用配置：

1. application-host : Nexus服务监听的主机
2. application-port: Nexus服务监听的端口

# 迁移与备份

默认情况下，需要备份的资料在 sonatype-work 文件夹下



