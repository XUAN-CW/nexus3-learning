---
title: hello-nexus3之docker安装
tags: 
date: 2022-06-23 14:16:21
id: 1655964981189445000
---
# 摘要



# 版本选择

[Nexus Repository Manager 3.16.2-01](https://help.sonatype.com/repomanager3/product-information/download/download-archives---repository-manager-3#DownloadArchivesRepositoryManager3-NexusRepositoryManager3.16.2-01) 



# 运行

```sh
docker container rm -f nexus3
rm -rf /docker-v/nexus3/
mkdir -p /docker-v/nexus3/nexus-data
chmod 777 -R /docker-v/nexus3/
docker run -itd  \
  -p 7000:8081 \
  -p 7001-7100:7001-7100 \
  -v /docker-v/nexus3/nexus-data:/nexus-data \
  --privileged=true \
  --restart=always \
  --name=nexus3 \
  sonatype/nexus3:3.16.2
```

# 访问

- 路径： http://nexus3-ip:7000/
- 账号：admin
- 密码：admin123



# 迁移与备份





直接备份整个/nexus-data目录即可，建议将此卷挂载出来，作为备份对象，详情见 [Nexus数据的备份与恢复.html](assets\references\Nexus数据的备份与恢复.html) 
