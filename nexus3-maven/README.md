---
title: nexus3-maven
tags: 
date: 2022-02-12 22:11:52
id: 1644675112080225900
---
# 摘要

# 私服搭建

## proxy

- jboss的maven中央仓库地址：http://repository.jboss.com/maven2/
- 阿里云的maven中央仓库地址：http://maven.aliyun.com/nexus/content/groups/public/
- apache的maven中央仓库地址：http://repo.maven.apache.org/maven2/

## group

# 使用

```xml
  <!--就是配置maven本地仓库的地址为自定义的地址-->
  <!--nexus服务器-->
  <servers>  
    <server>  
        <id>nexus</id>  
        <username>admin</username>  
        <password>admin123</password>  
    </server>   
  </servers>  
  <!--组资源库的url地址  id和name自定义，mirrorOf的值设置为central，写死的-->  
  <mirrors>     
    <mirror>  
        <id>nexus</id>  
        <name>maven-private-server</name>  
        <url>http://ps:7000/repository/maven-private-server/</url>  
        <mirrorOf>central</mirrorOf>  
    </mirror>     
  </mirrors>  
```



# 参考 

 [使用Nexus3搭建Maven私服_上传第三方jar包到本地maven仓库.html](assets\references\使用Nexus3搭建Maven私服_上传第三方jar包到本地maven仓库.html) 
