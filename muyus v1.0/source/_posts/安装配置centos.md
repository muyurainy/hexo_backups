---
title: 安装配置centos
date: 2017-03-25 17:41:53
tags: [vps, linux]
category: 
- 折腾
toc: true
---
## 修改yum源为阿里云 ##  
阿里云Linux安装镜像源地址：http://mirrors.aliyun.com/

第一步：备份原镜像文件  

    mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak  

第二步：下载CentOS-Base.repo 到/etc/yum.repos.d/
```
CentOS 5

    wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-5.repo

CentOS 6

    wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo

CentOS 7

    wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```
第三步：运行yum makecache生成缓存

    yum clean all

    yum makecache

    rpm --import /etc/pki/rpm-gpg/
