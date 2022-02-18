---
title: nexus3-docker
tags: 
date: 2022-02-12 18:31:11
id: 1644661871858288100
---
# 摘要

# nexus3 配置

## docker (proxy)

1. Name：随意，我这里填 aliyuncs，你也可以填 docker-proxy-aliyuncs.com
2. 勾选 **Allow anonymous docker pull** 
3. 填写 Remote storage : https://6kx4zyno.mirror.aliyuncs.com

![image-20220218192615878](assets/images/image-20220218192615878.png)

如果你想代理更多，多加几个，都是一样的步骤：

| name                                           | Remote storage                            |
| ---------------------------------------------- | ----------------------------------------- |
| docker-proxy-gcr.io                            | https://gcr.io                            |
| docker-proxy-registry.aliyuncs.com             | https://registry.aliyuncs.com             |
| docker-proxy-registry.cn-hangzhou.aliyuncs.com | https://registry.cn-hangzhou.aliyuncs.com |

## docker (hosted)

1. Name：随意，我这里填 docker-hosted
2. HTTP : 暴露的端口，我这里填 7002
3. 勾选 **Allow anonymous docker pull** 

![image-20220218202152756](assets/images/image-20220218202152756.png)

## docker (group)

1. Name：随意，我这里填 docker-private-server
2. HTTP : 暴露的端口，我这里填 7001
3. 勾选 **Allow anonymous docker pull** 
4. Member repositories : 添加刚才创建的 aliyuncs、docker-hosted 

![image-20220218202323315](assets/images/image-20220218202323315.png)

## Docker Bearer Token Realm

![image-20220218194020243](assets/images/image-20220218194020243.png)

# 使用者配置

```sh
# 配置域名，方便与 IP 地址解耦
echo "192.168.0.10 ps" >> /etc/hosts

# 添加镜像、加入授信列表
tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["http://ps:7001"],
  "insecure-registries": ["ps:7002"]
}
EOF

# 重启
systemctl daemon-reload
systemctl restart docker
```

使用 `docker info` 可以检查是否成功配置：

```
 Insecure Registries:
  ps:7002
  127.0.0.0/8
 Registry Mirrors:
  http://ps:7001/
```

# 测试

## 代理测试

```sh
docker pull hello-world
```

拉取镜像后可见：

![image-20220218200015413](assets/images/image-20220218200015413.png)

## push 测试

```sh
# 登录 
docker login -u admin -p admin123 ps:7002
# push 测试
docker pull hello-world
docker tag hello-world:latest ps:7002/my-hello-world:1.0
docker push ps:7002/my-hello-world:1.0
# 删除本地镜像
docker image rm -f  ps:7002/my-hello-world:1.0
# pull 测试
docker pull ps:7002/my-hello-world:1.0
```

# 参考

 [利用nexus作为私库进行代理docker,进行上传和下载镜像操作.html](assets\references\利用nexus作为私库进行代理docker,进行上传和下载镜像操作.html) 

 [使用nexus3.x配置docker镜像仓库及仓库代理.html](assets\references\使用nexus3.x配置docker镜像仓库及仓库代理.html) 





# 本人常用 docker 镜像

```sh
# MySQL
docker pull mysql:5.7
docker pull mysql:5.7.30
# nacos
docker pull nacos:1.4.2
docker pull nacos:2.0.3
# gitlab
docker pull gitlab/gitlab-ce:12.4.2-ce.0
# redis
docker pull redis:5.0.8
# jdk
docker pull openjdk:8-jdk-alpine
docker pull openjdk:8u312-oraclelinux8
# nginx 
docker pull nginx:1.16.1
# tomcat
docker pull tomcat:8.5.73-jre8-openjdk-slim-bullseye
docker pull tomcat:9.0.56-jre8-openjdk-slim-bullseye
# jenkins
docker pull jenkins/jenkins:2.289.3-lts-centos7
# harbor
docker pull goharbor/prepare:v1.9.2
# elasticsearch
## springboot:2.3.2.RELEASE 的对应版本
docker pull elasticsearch:7.6.2


```





