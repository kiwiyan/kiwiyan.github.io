---
title: 连接mongodb
date: 2018-01-08 15:25:47
tags: 数据库
categories: mongodb
comments: true
---
## 下载mongodb
如w3c菜鸟所示

## mongodb数据库概念

SQL术语/概念	|MongoDB术语/概念	|解释/说明
---|---|---
database	    |database	        |数据库
table	        |collection	        |数据库表/集合
row	            |document	        |数据记录行/文档
column	        |field	            |数据字段/域
index	        |index	            |索引
table joins	 	|                    |表连接,MongoDB不支持
primary key	    |primary key	         |主键,MongoDB自动将_id字段设置为主键
<!-- more -->
## 连接数据库
在安装路径下设置数据库集合的位置
D:\setUp\mongodb\bin>mongodb.exe -dbpath d:\data\db

## mongodb原生模块 vs moogose
## mongodb 原生模块

## moogose
支持原生promise用法：
mongoose.Promise = global.Promise;
