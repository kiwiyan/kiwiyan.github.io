---
title: windows下nvm管理nodejs版本
date: 2018-01-11 09:58:28
tags: nvm
categories: nodejs
comments: true
---
通过nvm工具可以很方便的进行nodejs版本管理，对于经常需要切换nodejs环境的朋友可以提升不少效率，下面介绍下下windows系统的工具的安装和使用。
<!-- more -->
## nvm的安装
安装nvm前需要先卸掉之前以普通方式安装的nodejs，点击下载[nvm安装包](https://github.com/coreybutler/nvm-windows/releases)
![](/images/2018/1/nvm.png)


## nvm 安装nodejs
```
nvm install 8.9.1
```

## nvm切换nodejs版本
```
nvm use 8.9.1
```

## nvm 展示nodejs安装列表
```
nvm list
```
![](/images/2018/1/nvm2.png)
## nvm命令
  命令                         | 解释
  ---                          | ---
  nvm arch                     |  展示node运行的操作系统是32位还是64位
  nvm install (version) [arch] | 安装node的命令，比如 nvm install 8.9.1。version可以是node的版本号或是单词"latest"(最新版),arch是操作系统位数，默认就是当前系统的系统位数。
  nvm list [available]         | nvm list 则列出当前已经安装的node版本号。nvm list available 则列出目前nodejs的可安装版本号以及LTS稳定版等信息
  nvm on                       | 启动nvm对node的版本管理
  nvm off                      | 关闭nvm对node的版本管理
  nvm proxy [url]              | 设置代理服务来下载，url为空则使用当前代理，url设置为"none"则移除代理。
  nvm node_mirror [url] | 设置node的安装镜像路径。默认镜像路径https://nodejs.org/dist/ ，不设置url则使用默认路径。
  nvm npm_mirror [url] | 设置npm的安装镜像路径。默认镜像路径是https://github.com/npm/npm/archive/，不设置url则使用默认路径。
  nvm uninstall (version)      | 卸载某个版本的nodejs
  nvm use [version] [arch]     | 切换node的版本号，如 nvm use 8.9.1 。arch为操作系统位数
  nvm root [path]              | 设置nvm保存不同版本的nodejs的路径
  nvm version                  | 展示nvm的版本号