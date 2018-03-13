---
title: 发布有全局命令行的npm包
date: 2018-02-26 19:50:41
tags: npm
categories: nodejs
comments: true
---

### npm 常用命令
npm是随着nodejs一起安装的包管理工具，可以安装，卸载，发布nodejs包。
```
npm init  工程初始化，生成package.json文件

npm i <name> 安装(i或者install都可以)
npm i <name@1.0.2> 制定版本安装
npm i <name> -S 安装以及将信息写入package.json的dependencies
npm i <name> -D 安装及将信息写入package.json的devDependencies里

npm root -g查看全局安装目录

npm list -g --depth 0  查看安装了哪些全局模块，深度为第一层

```
那么如何发布一个npm包呢？
本文主要介绍如何发布一个有全局命令的npm包。
<!-- more -->
### 发布全局命令行npm包
在这里我们做一个命令行工具，运行全局命令$ viewcom，可以查看电脑基本信息，包括cpu，ipv4，ipv6，mac地址等，并且发布到npm仓库可为大家下载使用。
#### 1. 创建根文件夹viewcom 
运行 $ npm init，产生package.json，填写相关信息。
为了规范化，package.json里我们尽量写上name，description，keywords，git地址等信息，方便他人搜索和使用，万一哪天我们的项目对别人产生价值也说不定呢。
#### 2. 根路径下创建index.js 
index.js里边是工程的核心代码。
根路径下，运行node index.js也可以打印出电脑信息。代码比较简单，就是通过node的os模块获取电脑信息并整合在一起。
index.js文件内容：
```js
const os = require('os');

let cpu = os.cpus()[0].model;
let memory = Math.round(os.totalmem() / 1024 / 1024 / 1024) + 'G';
let memoryUseRatio = Math.round(os.freemem() / os.totalmem() * 100) + '%';

let localnet = os.networkInterfaces()['本地连接']; // todo 有些电脑获取不到，待解决
let macAddress = localnet ? localnet[0].mac : '';
let ipv6 = localnet ? localnet[0].address : '';
let ipv4 = localnet ? localnet[1].address : '';

let platform = os.platform();
let arch = os.arch();
let hostname = os.hostname();
let username = os.userInfo().username;

console.log('\x1B[33m%s\x1b[0m', 'Computer Info:', {
  cpu,
  memory,
  memoryUseRatio,
  macAddress,
  ipv6,
  ipv4,
  platform,
  arch,
  hostname,
  username
});

```
#### 3. 添加bin/viewcom文件内容
直接node index.js也可以打印出电脑的基本信心，但我们想通过命令行的方式来打印，在这里编辑bin/viewcom, 写入如下代码。
第一行代码是linux/unix的写法，意思是告诉系统用node来执行下面的代码。
第二行代码表示引入根路径的index.js并执行。
bin/viewcom文件中的内容：
```
#!/usr/bin/env node
require('../index.js');

```
#### 4. 修改package.json的内容

在文件尾部添加
```
  "bin": {
    "viewcom": "bin/viewcom"
  }
```

#### 5. 测试运行
根目录下运行如下命令，将此模块添加进全局。
```
npm i . -g
```
然后随意找个目录，运行
```
viewcom
```
这时你会发现，电脑信息打印出来了，这个模块开发就完成了。
注意这一步骤不是必需的，这里只是用来测试，这也是一种全局安装方式，测试完成后，可以先卸掉这个全局模块,发布成功后再拉去线上模块来使用。
卸载安装的全局模块
```
npm uninstall viewcom -g
```

#### 6. 上传到npm仓库
首先你需要有一个npm账号，没有的话官网注册很简单。接着，在项目跟路径下运行 npm login 登录npm。
最后运行npm publish，出现 '+viewcom@1.0.0'的话表示发布成功了。

#### 7. 使用
发布成功后就可以像安装其他模块那样来使用了。
安装：
```
npm i viewcom -g
```
使用：
```
viewcom
```

#### 8. 发布注意下项
如果只是发布npm包，不需要全局命令行的话，那么也不需要bin文件以及package.json中的bin配置项，发布到npm的方式是一样的。
注意name项是必填的，而且不能同名，命名前可以搜下是否有这个命名的模块。更新发布的话，修改下version信息，重新publish就可以