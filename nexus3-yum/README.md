---
title: nexus3-yum
tags: 
date: 2022-02-13 14:21:43
id: 1644733303678989500
---
# 摘要







# 代理

已验证，有用：

```
http://mirrors.163.com/centos/7/updates/x86_64/
```

```
 kubernetes的 Remote storage填写： http://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64
```





可用，

```
http://mirrors.aliyun.com/docker-ce/linux/centos/
```

但是配置时需要：

```
baseurl=http://your-nexus.com/repository/docker-ce-repo/$releasever/$basearch/stable
```

因此建议：

```
http://mirrors.aliyun.com/docker-ce/linux/centos/7/x86_64/stable/
```







# 清理缓存

```
yum clean all 
$ yum makecache
```

