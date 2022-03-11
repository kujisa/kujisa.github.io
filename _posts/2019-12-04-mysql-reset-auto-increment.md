---
layout: post
title: MySQL重置当前自动增量值
author: Kujisa
categories: Database
tags: MySQL Database MSSQL
---


**mysql的语法与sql server的语法不同**

## 1. sql server
sql server的语法`dbcc checkident('tablename',reseed,5)`

## 2. mysql
mysql的语法是`ALTER TABLE tablename AUTO_INCREMENT = 5;`

其中tablename是表名，5是重置之后的自动增量值大小（不能小于等于当前的自动增量值）

注意：不能将计数器重置为小于或等于当前使用的值。对于InnoDB和MyISAM，如果该值小于或等于AUTO_INCREMENT列中当前的最大值，则该值将重置为当前的最大AUTO_INCREMENT列值加1。

> 参考文档：<https://dev.mysql.com/doc/refman/8.0/en/alter-table.html>