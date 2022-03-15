---
layout: post
title: How to Customize the Right-Click Menu in Windows 11
author: Kujisa
categories: Windows
tags: Windows
---

**其他人说的一半是对的，修改权限那有点问题而已**

## 1. 打开注册表
运行`regedit`
找到目录
`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Discardable\PostSetup\ShellNew`

## 2. 修改权限
`ShellNew`文件夹上右键`权限`--`高级`--`禁用继承`--把两个完全控制修改为只读（留下Administrator那个）--`确定`

修改`Classes`里的顺序

把剩下的Administrator的完全控制修改为只读