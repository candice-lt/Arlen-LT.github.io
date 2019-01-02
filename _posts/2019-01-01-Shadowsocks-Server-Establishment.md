---
layout: base
title:  "Shadowsocks Server Establishment"
author: "Arlen"
date:   2019-01-01
tags:   "VPN"
---

# Establish ssserver
[root@shadowsocks-server src]# yum install lsof -y

[root@shadowsocks-server src]# cd /usr/local/src/

[root@shadowsocks-server src]# wget --no-check-certificate https://pypi.python.org/packages/source/s/setuptools/setuptools-19.6.tar.gz#md5=c607dd118eae682c44ed146367a17e26

[root@shadowsocks-server src]# tar -zvxf setuptools-19.6.tar.gz

[root@shadowsocks-server src]# yum -y install epel-release

[root@shadowsocks-server src]# yum -y install pip python-pip

[root@shadowsocks-server src]# pip install –-upgrade pip

[root@shadowsocks-server src]# pip install shadowsocks

[root@shadowsocks-server src]# pip install M2Crypto

[root@shadowsocks-server src]# vi /etc/shadowsocks.json

{

"server": "0.0.0.0",

"port_password": {

"***port1***": "***passwd1***",

"***port2***": "***passwd2***",

"***port3***": "***passwd3***"

},

"timeout":300,

"method":"aes-256-cfb",

"fast_open": false

}

---
[root@shadowsocks-server src]# vim /etc/systemd/system/ssserver.service

[Unit]

Description=ssserver

[Service]

TimeoutStartSec=0

ExecStart=/usr/bin/ssserver -c /etc/shadowsocks.json

[Install]

WantedBy=multi-user.target



---

[root@shadowsocks-server src]# systemctl enable ssserver

[root@shadowsocks-server src]# systemctl start ssserver

[root@shadowsocks-server src]# systemctl status ssserver -l

[root@shadowsocks-server src]# lsof -i:***port***



# Install boost

[root@shadowsocks-server src]# uname -r

[root@shadowsocks-server src]# wget --no-check-certificate https://blog.asuhu.com/sh/ruisu.sh

[root@shadowsocks-server src]# bash ruisu.sh

[root@shadowsocks-server src]# wget --no-check-certificate -O appex.sh https://raw.githubusercontent.com/0oVicero0/serverSpeeder_Install/master/appex.sh && chmod +x appex.sh && bash appex.sh install

[root@shadowsocks-server src]# uname -r

[root@shadowsocks-server src]# wget -N --no-check-certificate https://raw.githubusercontent.com/91yun/serverspeeder/master/serverspeeder-all.sh && bash serverspeeder-all.sh

[root@shadowsocks-server src]# service serverSpeeder start



# Firewall

[root@shadowsocks-server src]# firewall-cmd --add-port=***port***/tcp --permanent

[root@shadowsocks-server src]# firewall-cmd --remove-port=***port***/tcp --permanent
