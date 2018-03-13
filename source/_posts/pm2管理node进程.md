---
title: pm2管理node进程
date: 2018-01-25 11:15:08
tags: nodejs管理工具
categories: nodejs
comments: true
---
pm2.5, 不好意思，pm2是一个nodejs应用管理工具，可以很方便得进行以前比较繁琐的管理工作，比如自动重启，性能监控，负载均衡等。

以前启动一个node server，一般是运行npm start，其实是运行node app.js,如果想修改server代码的话，就得ctrl + c关掉服务，再运行npm start，这样的工作进行多次着实繁琐。使用pm2 的话，运行pm2 start appId --watch,会监听你的进程，每次修改后服务会自动重启。而且pm2还能同时管理多个node进程，只开一个命令行窗口就可以。
<!-- more -->
## 安装pm2
```
npm install pm2 -g
```

## 常用pm2 命令
```
$ pm2 start app.js # 启动app.js应用程序
$ pm2 start app.js -i 4 # cluster mode 模式启动4个app.js的应用实例
# 4个应用程序会自动进行负载均衡
$ pm2 start app.js --name="api" # 启动应用程序并命名为 "api"
$ pm2 start app.js --watch # 当文件变化时自动重启应用
$ pm2 start script.sh # 启动 bash 脚本

$ pm2 list # 列表 PM2 启动的所有的应用程序
$ pm2 monit # 显示每个应用程序的CPU和内存占用情况
$ pm2 show [app-name] # 显示应用程序的所有信息

$ pm2 logs # 显示所有应用程序的日志
$ pm2 logs [app-name] # 显示指定应用程序的日志

$ pm2 stop all # 停止所有的应用程序
$ pm2 stop 0 # 停止 id为 0的指定应用程序
$ pm2 restart all # 重启所有应用
$ pm2 reload all # 重启 cluster mode下的所有应用
$ pm2 gracefulReload all # Graceful reload all apps in cluster mode
$ pm2 delete all # 关闭并删除所有应用
$ pm2 delete 0 # 删除指定应用 id 0
$ pm2 scale api 10 # 把名字叫api的应用扩展到10个实例
$ pm2 reset [app-name] # 重置重启数量

$ pm2 startup # 创建开机自启动命令
$ pm2 save # 保存当前应用列表
$ pm2 resurrect # 重新加载保存的应用列表
$ pm2 update # Save processes, kill PM2 and restore processes
$ pm2 generate # Generate a sample json configuration file
pm2 start app.js --node-args="--max-old-space-size=1024"

```

