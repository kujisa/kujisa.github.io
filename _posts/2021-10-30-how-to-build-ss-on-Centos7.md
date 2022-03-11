---
layout: post
title: centos7如何搭建酸酸
author: Kujisa
categories: Linux
tags: Linux Proxy
---

## 1. 系统配置
Centos 7 x64

## 2. 依赖安装
执行以下代码
{% highlight bash linenos %}
yum install -y pcre pcre-devel git gettext gcc autoconf libtool automake make asciidoc xmlto c-ares-devel libev-devel


wget https://download.libsodium.org/libsodium/releases/libsodium-1.0.18.tar.gz && tar xf libsodium-1.0.18.tar.gz && cd libsodium-1.0.18 && ./configure && make -j2 && make install && cd /
echo /usr/local/lib > /etc/ld.so.conf.d/usr_local_lib.conf
ldconfig

export MBEDTLS_VER=2.6.0
wget https://tls.mbed.org/download/mbedtls-$MBEDTLS_VER-gpl.tgz
tar xvf mbedtls-$MBEDTLS_VER-gpl.tgz
pushd mbedtls-$MBEDTLS_VER
make SHARED=1 CFLAGS=-fPIC
make DESTDIR=/usr install
popd
ldconfig

# clean directory
rm -rf /tmp/shadowsocks-libev

# compile and install
cd /tmp
git clone https://github.com/shadowsocks/shadowsocks-libev.git
cd shadowsocks-libev
git submodule update --init --recursive
./autogen.sh
./configure
make
make install
cd ..
rm -rf /tmp/shadowsocks-libev

mkdir /etc/shadowsocks-libev
touch /etc/shadowsocks-libev/config.json
{% endhighlight %}

## 3. 配置文件
配置文件在/etc/shadowsocks-libev/config.json
将下列代码添加进文件中
```json
{
    "server_host": "你的服务器ip或域名",
    "server_port": 8111,
    "password":"密码",
    "timeout":300,
    "method":"rc4-md5",
    "fast_open": false
}
```

## 4.设置后台运行
新建文件/etc/default/shadowsocks-libev
将下列代码添加进文件中
{% highlight properties linenos %}
# Defaults for shadowsocks initscript
# sourced by /etc/init.d/shadowsocks-libev
# installed at /etc/default/shadowsocks-libev by the maintainer scripts

#
# This is a POSIX shell fragment
#
# Note: `START', `GROUP' and `MAXFD' options are not recognized by systemd.
# Please change those settings in the corresponding systemd unit file.

# Enable during startup?
START=yes

# Configuration file
CONFFILE="/etc/shadowsocks-libev/config.json"

# Extra command line arguments
DAEMON_ARGS="-u"

# User and group to run the server as
USER=nobody
GROUP=nobody

# Number of maximum file descriptors
MAXFD=32768
{% endhighlight %}

## 5. 添加服务脚本
新建文件/lib/systemd/system/shadowsocks-libev.service
将下列代码添加进文件中
{% highlight properties linenos %}
#  This file is part of shadowsocks-libev.
#
#  Shadowsocks-libev is free software; you can redistribute it and/or modify
#  it under the terms of the GNU General Public License as published by
#  the Free Software Foundation; either version 3 of the License, or
#  (at your option) any later version.
#
#  This file is default for Debian packaging. See also
#  /etc/default/shadowsocks-libev for environment variables.

[Unit]
Description=Shadowsocks-libev Default Server Service
Documentation=man:shadowsocks-libev(8)
After=network.target

[Service]
Type=simple
EnvironmentFile=/etc/default/shadowsocks-libev
User=nobody
Group=nobody
LimitNOFILE=32768
ExecStart=/usr/local/bin/ss-server -c $CONFFILE $DAEMON_ARGS

[Install]
WantedBy=multi-user.target
{% endhighlight %}

## 6. 命令

启动： `systemctl start shadowsocks-libev`

停止： `systemctl stop shadowsocks-libev`

重启： `systemctl restart shadowsocks-libev`

查看状态： `systemctl status shadowsocks-libev -f`

开机启动： `systemctl enable shadowsocks-libev`

取消开机启动： `systemctl disable shadowsocks-libev`