---
title: vps安装配置
date: 2017-03-29 17:41:53
tags: [vps, linux]
category: 
- 折腾
toc: true
---
## 安装配置shadowsocks ##
### 1.安装pip ###
**ubuntu**:  
    sudo apt-get install python-pip  
**Centos**  
    yum install python-setuptools && easy_install pip  
之后运行  
    pip install shadowsocks  
### 2.配置Shadowsocks ###
安装完成后，在/etc/下新建一个叫shadowsocks.json的配置文件，内容如下：
```
{
	"server" : "::",
	"server_port" : 8388,
	"local_address" : "127.0.0.1",
	"local_port" : 1080,
	"password" : "PASSWORD",
	"timeout" : 300,
	"method" : "rc4-md5"
}
```
### 3.启动运行 ###
执行以下开启：  
    ssserver -c /etc/shadowsocks.json --fast-open -d start
关闭：  
    ssserver -d stop
### Google BBR 非openvz加速（非必须） ###
    wget --no-check-certificate https://github.com/52fancy/GooGle-BBR/raw/master/BBR.sh && sh BBR.sh
## 安装配置 Softether VPN ##
### 服务器端配置 ##
执行：  
```
wget http://www.softether-download.com/files/softether/v4.18-9570-rtm-2015.07.26-tree/Linux/SoftEther_VPN_Server/64bit_-_Intel_x64_or_AMD64/softether-vpnserver-v4.18-9570-rtm-2015.07.26-linux-x64-64bit.tar.gz
tar -xzvf softether-vpnserver-v4.18-9570-rtm-2015.07.26-linux-x64-64bit.tar.gz
cd vpnserver/
make
```
按提示输入三个1后：  
    ./vpnserver start
服务器端配置完毕
### 客户端 ###
[客户端点击下载](http://www.softether-download.com/files/softether/v4.18-9570-rtm-2015.07.26-tree/Windows/Admin_Tools/VPN_Server_Manager_and_Command-line_Utility_Package/softether-vpn_admin_tools-v4.18-9570-rtm-2015.07.26-win32.zip)

