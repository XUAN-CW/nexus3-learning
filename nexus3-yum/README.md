---
title: nexus3-yum
tags: 
date: 2022-02-13 14:21:43
id: 1644733303678989500
---
# 摘要



# 实现步骤

## proxy

| name                          | Remote storage                            |
| ----------------------------- | ----------------------------------------- |
| yum-proxy-opsx.alibaba.com    | https://opsx.alibaba.com/centos/          |
| yum-proxy-download.docker.com | https://download.docker.com/linux/centos/ |
| yum-proxy-mirrors.aliyun.com  | http://mirrors.aliyun.com/                |

## 使用者配置

配置仓库：

```
# yum-proxy-opsx.alibaba.com
[private-os]
name=private-os
baseurl=http://ps:7000/repository/yum-proxy-opsx.alibaba.com/\$releasever/os/\$basearch/
enabled=1
gpgcheck=0

[private-updates]
name=private-updates
baseurl=http://ps:7000/repository/yum-proxy-opsx.alibaba.com/\$releasever/updates/\$basearch/
enabled=1
gpgcheck=0

[private-extras]
name=private-extras
baseurl=http://ps:7000/repository/yum-proxy-opsx.alibaba.com/\$releasever/extras/\$basearch/
enabled=1
gpgcheck=0

[private-centosplus]
name=private-centosplus
baseurl=http://ps:7000/repository/yum-proxy-opsx.alibaba.com/\$releasever/centosplus/\$basearch/
enabled=1
gpgcheck=0

[private-configmanagement]
name=private-configmanagement
baseurl=http://ps:7000/repository/yum-proxy-opsx.alibaba.com/\$releasever/configmanagement/\$basearch/ansible-29/
enabled=1
gpgcheck=0


# yum-proxy-download.docker.com
[private-docker-ce]
name=private-docker-cedocker-ce
baseurl=http://ps:7000/repository/yum-proxy-download.docker.com/$releasever/$basearch/stable/
enabled=1
gpgcheck=0

# yum-proxy-mirrors.aliyun.com
[private-epel]
name=private-epel
baseurl=http://ps:7000/repository/yum-proxy-mirrors.aliyun.com/epel/7/x86_64/
enabled=1
gpgcheck=0

[private-kubernetes]
name=kubernetes
baseurl=http://ps:7000/repository/yum-proxy-mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=0


```

**baseurl** 不要手写，要从页面上复制：

![image-20220213155241989](assets/images/image-20220213155241989.png)

# 测试

```sh
yum clean all && yum makecache fast    
# 如果 makecache 报错，请关注最后一条输出，确认是哪个url找不到，然后进行修改
```



```sh
# 清理缓存
yum clean all 
yum makecache
# 测试是否代理了 docker-ce
sudo yum install -y docker-ce-20.10.7 docker-ce-cli-20.10.7  containerd.io-1.4.6
# 测试是否代理了 kubernetes
sudo yum install -y kubelet-1.20.9 kubeadm-1.20.9 kubectl-1.20.9 --disableexcludes=kubernetes
```



```sh
 yum update --downloadonly --downloaddir=/tmp/ -y
```

# 有效参考

 [nexus3配置Yum源.html](assets\references\nexus3配置Yum源.html) 

 [nexus配置yum私有仓库.html](assets\references\nexus配置yum私有仓库.html) 

