---
title: nexus3-yum
tags: 
date: 2022-02-13 14:21:43
id: 1644733303678989500
---
# 摘要



# 对外暴露

```
http://ps:7000/repository/yum-private-service/
```

# 代理

- centos7-163 ： http://mirrors.163.com/centos/7/updates/x86_64/ 
- aliyun-kubernetes ：  http://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64 
- aliyun-docker-ce： http://mirrors.aliyun.com/docker-ce/linux/centos/7/x86_64/stable/ 

# 测试

```sh
# 清理缓存
yum clean all 
yum makecache
# 测试是否代理了 docker-ce
sudo yum install -y docker-ce-20.10.7 docker-ce-cli-20.10.7  containerd.io-1.4.6
# 测试是否代理了 kubernetes
sudo yum install -y kubelet-1.20.9 kubeadm-1.20.9 kubectl-1.20.9 --disableexcludes=kubernetes
```

