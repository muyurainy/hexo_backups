---
title: 搭建hexo博客
date: 2017-03-29 17:41:53
tags: [vps, linux, hexo]
category: 
- 折腾
toc: true
---

# 客户端安装 #
## node.js 安装 ##
直接去[官网下载](https://nodejs.org/en/)
进入源码所在文件夹，并执行：
```
sudo ./configure
sudo make
sudo make install
```
或者使用[hexo官网](https://hexo.io/docs/)提供的方法
## git 安装 ##
Linux (Ubuntu, Debian):  

    sudo apt-get install git-core
Linux (Fedora, Red Hat, CentOS): 

    sudo yum install git-core
# hexo 安装配置 #
## hexo 安装 ##
Once all the requirements are installed, you can install Hexo with npm.

    npm install -g hexo-cli
## hexo 配置 ##
### 1. setup ###
Once Hexo is installed, run the following commands to initialise Hexo in the target <folder>.
```
$ hexo init <folder>
$ cd <folder>
$ npm install
```
Once initialised, here’s what your project folder will look like:
```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```
具体内容参见[官网](http:\\hexo.io)
# 服务器端安装配置 #
以下分为两节，分别是将hexo配置到github上和配置到vps上
## 搭建github博客 ##
这一节是将hexo搭建到github上，下一节是将hexo搭建到vps上，请根据需求选择
### 1. 修改网站相关信息 ###
打开_config.yml
```
title: inerdstack
subtitle: the stack of it nerds
description: start from zero
author: inerdstack
language: zh-CN
timezone: Asia/Shanghai
```
language和timezone都是有输入规范的，详细可参考[语言规范](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)和[时区规范](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)。

注意：每一项的填写，其:后面都要保留一个空格，下同。

### 2. 配置统一资源定位符（个人域名） ###

    url: http://inerdstack.com

对于root（根目录）、permalink（永久链接）、permalink_defaults（默认永久链接）等其他信息保持默认。
### 3. 配置部署 ###
```
deploy:
  type: git
  repo: https://github.com/yourname/yourname.github.io.git
  branch: master
```
### 4. 运行 ###
    hexo server
然后打开浏览器测试
### 5. 发布到github ###
执行  
```
$ hexo generate
$ npm install hexo-deployer-git --save
$ hexo deploy
```
完毕！
## 在vps上部署hexo ##
### 0. 创建hexo用户 ###
使用root权限添加用户，修改密码。
```
# adduser hexo
# passwd hexo
```
生成公钥并复制到用户hexo下

    ssh-keygen -t rsa
    mkdir /home/hexo/.ssh
    cp /root/.ssh/id_rsa.pub /home/hexo/.ssh/authorized_keys
    
***注：此步骤也可以不做，直接用原来的用户***
### 3.1 安装nginx ###
Linux (Ubuntu, Debian):  

    sudo apt-get install nginx
Linux (Fedora, Red Hat, CentOS): 

    sudo yum install nginx
### 3.2 nginx 配置 ###

以下内容添加到/etc/nginx/conf.d/hexo.conf中
```
server {
        listen 80;
        server_name 118.89.243.187;
        location / {
                root /home/ubuntu/www;
                index index.html index.htm;
}
}

```

启动nginx服务

    sudo nginx -t
    sudo nginx -s reload
如果输出和上面的一致就说明配置文件没有问题，接下来就启动nginx服务，并设置为开机启动。
```
$ sudo systemctl start nginx
$ sudo systemctl enable nginx  
```
### 3.3 配置git ###
安装完成后，初始化git仓库
```
$ mkdir hexo
$ cd hexo/
$ git init --bare
```
将以下内容添加到hexo/hooks/post-receive中，并将post-receive文件权限改为755。
```
#!/bin/bash
GIT_REPO=/home/ubuntu/hexo
TMP_GIT_CLONE=/tmp/HexoBlog
PUBLIC_WWW=/home/ubuntu/www
rm -rf ${TMP_GIT_CLONE}
git clone $GIT_REPO $TMP_GIT_CLONE
rm -rf ${PUBLIC_WWW}/*
cp -rf ${TMP_GIT_CLONE}/* ${PUBLIC_WWW}	
```

    $ chmod 755 hexo/hooks/post-receive

以上就将服务器配置完毕，下面就需要配置客户端。
### 3.4 客户端 ###
在hexo根目录_config.yml中添加部署配置  
```
deploy:
- type: git
  repo: ssh://hexo@VPS的IP:ssh的端口/home/ubuntu/hexo
  branch: master
```
# hexo使用 #
见[官网](https://hexo.io/zh-cn/docs/writing.html)