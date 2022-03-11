---
layout: post
title: windows 10 激活方法
author: Kujisa
categories: Windows
tags: Windows
---

## 1. 以管理员身份运行cmd
## 2. 安装证书并激活
### 2.1 安装产品密钥
输入`slmgr /ipk W269N-WFGWX-YVC9B-4J6C9-T83GX`，回车运行
### 2.2 配置KMS服务器
输入`slmgr /skms zh.us.to`，回车运行
### 2.3 激活
输入`slmgr /ato`，回车运行
### 2.4 查询激活状态
输入`slmgr.vbs -dlv`，回车运行
### 2.5 如果激活失败
请尝试将步骤2.2中的`zh.us.to`替换为以下任意一个，并执行步骤2.2，2.3，2.4
```bash
zh.us.to
kms.03k.org  #这个在2020/9/10测试可用
kms.chinancce.com
kms.shuax.com
kms.dwhd.org
kms.luody.info
kms.digiboy.ir
kms.lotro.cc
www.zgbs.cc
cy2617.jios.org
```

## 3. 注意事项
180天后重新照此方法激活