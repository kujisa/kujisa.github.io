---
layout: post
title: 反编译apk
author: Kujisa
categories: Android
tags: Android Decomplie
---

## Step 1 反编译apk

使用apktool.jar

`java -jar apktool.jar d -f demo.apk -o outDir`

会生成outDir文件夹

## Step 2 修改内容

在jadx中查看源代码，找到需要改的，在outDir中修改对应的smali代码文件

## Step 3 重新打包

使用apktool.jar

`java -jar apktool.jar b -o demo_no_signalign.apk outDir`

会生成未签名和对齐的apk文件

## Step 4 对齐

检查APK是否对齐

`zipalign -c -v 4 demo_no_signalign.apk`

 4字节对齐优化

`zipalign -v 4 demo_no_signalign.apk demo_align.apk`

## Step 5 生成签名文件

**生成签名**

`keytool -genkey -keystore kujisa.keystore  -alias kujsia -keyalg RSA -validity 10000`

kujisa.keystore：想要生成的签名文件

kujisa：生成的别名

10000：10000天，单位天

修改别名

keytool -changealias -keystore kujsia.keystore -alias kujisa -destalias kujisanew

修改别名密码

keytool -keypasswd -keystore kujsia.keystore -alias kujisanew

修改密钥库密码

keytool -storepasswd -keystore kujsia.keystore  -alias kujisanew

## Step 6 签名

**jarsigner给apk签名,只支持V1签名**

`jarsigner -verbose -keystore 签名文件.keystore -signedjar (签名后的apk路径及名称) (要给谁签名.apk路径 ) 签名文件的别名`

示例:

`jarsigner -verbose -keystore kujisa.keystore -signedjar demo_signedV1.apk demo_align.apk kujisa`

**apksigner给apk签名,默认同时使用V1和V2签名**

`apksigner sign --ks 密钥库名 --ks-key-alias 密钥别名 --out 生成的签名文件路径及名称 给哪个apk文件签名`

示例：

`apksigner sign --ks kujisa --ks-key-alias kujisa --out demo_signedV2.apk demo_align.apk`