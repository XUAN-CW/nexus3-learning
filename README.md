---
title: nexus3-learning
tags: 
date: 2022-02-18 19:16:15
id: 1645182975702940300
---
# 摘要

# 运行

```sh
docker container rm -f nexus3
rm -rf /docker-v/nexus3/
mkdir -p /docker-v/nexus3/nexus-data
chmod 777 -R /docker-v/nexus3/
docker run -itd  -p 7000:8081 -p 7001-7100:7001-7100 -v /docker-v/nexus3/nexus-data:/nexus-data --privileged=true --restart=always --name=nexus3 sonatype/nexus3:3.16.2
watch docker logs nexus3
```

# 访问

- 路径： http://nexus3-ip:7000/
- 账号：admin
- 密码：admin123
