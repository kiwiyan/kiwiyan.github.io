---
title: docker初探
date: 2018-01-16 10:22:17
tags: docker
categories: linux
comments: true
---

## yum 安装docker
```
yum install docker -y
```
<!-- more -->
## 启动
```
sercive docker start
```

## 安装镜像
```
docker run -i -t ubuntu /bin/bash
```
## 删除镜像
docker rmi
## docker中安装vim
apt-get update
apt-get install -y vim
创建文件：vi 文件名
创建文件夹： mkdir 文件夹
exit 从容器退出到宿主机 此时容器停止运行;重启容器： docker start container_name/id
进入容器：docker attach container_name

(卸载apt-get安装的软件 apt-get remove vim)
## 容器篇

### 创建容器
docker run --name test -idt -p 8080:8888 node /bin/bash

### 删除容器
（如果容器正在运行需要先关掉容器 docker stop/kill container_name）
docker rm container_id/container_name

## 安装git
ubuntu中 apt-get install git

## 下载
apt-get install/remove/update xxx 是ubuntu下的安装/卸载/更新软件方式
yum install/remove/update xxx是redhat centos下的安装/卸载/更新方式 