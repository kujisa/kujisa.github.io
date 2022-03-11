---
layout: post
title: Eclipse 没有Server选项，没有Dynamic Web Project的解决办法
author: Kujisa
categories: Other
tags: Eclipse
---

## 1. 查看当前Eclipse版本
在`Help`--`About Eclipse IDE` 中查看当前Eclipse的版本，记住它。

## 2. 安装扩展包
选择`Help`--`Install New Sofewares`，点击`Work with` 后面的输入框的小箭头，选择前缀是你当前版本的那一项，然后等待下方出现一堆的选项，**勾选Web, XML, Java EE and OSGi Enterprise Development**，**取消勾选底下的Contact all update sites during install to find required software**，否则加载非常慢，接着点击Next，选择I accpet 协议，选择Finish 。

## 3. 结束
等待下载进度条走完重启 Eclipse 即可，注意会卡在49%特别久，但是是正常现象，它在下文件，后台运行即可。偶尔会弹出是否信任证书的东西，同意即可。