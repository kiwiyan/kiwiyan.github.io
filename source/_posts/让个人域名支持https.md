---
title: 让个人域名支持https
date: 2018-03-10 15:53:45
tags: https
categories: linux服务器
comments: true
---
通过Github pages可以搭建免费的个人站点，默认域名为yourGithubName.github.io，在github上可以设置开启https访问模式。但是如果我们想使用自己注册的域名的话，一般就只能使用http协议打开网站了。

那么如何使个人域名也支持https呢？
<!-- more -->

通过Cloudflare可以免费让你的域名支持https，操作方式如下：
## 注册[Cloudflare](https://www.cloudflare.com/)。
注册成功后，添加你的域名，然后点击下一步，选择免费项。
![](/images/2018/3/https1.png)

## 配置NameServer。
如下图所示，添加两条解析记录，对于类型为A的记录，域名的ip地址值可以通过在系统控制台 ping [你的域名]获得。完成后点击提交。
![](/images/2018/3/https2.png)
![](/images/2018/3/https3.png)

## 设置SSL为Flexible。
在Crypto项中设置解析为Flexible
![](/images/2018/3/https4.png)

## 设置Page Rules路由匹配规则。
在Page Rules项中点击Create Page Rule，然后add a Setting创建两条规则，规则内容为http://域名/*与http://域名/。并且设置属性为ALways Use Https，然后点击Save and Deploy发布就OK了。这样的话，在浏览器就算输入http域名，也会跳转到https域名。
![](/images/2018/3/https5.png)
![](/images/2018/3/https6.png)

## 注意项。
一般设置完24小时内会起效(我的设置十几分钟就可以访问了)。https起效后，访问链接的https可能是灰色的，可能是你的页面引入了http方式的资源，不够安全，所以浏览器给了警告。

![](/images/2018/3/https7.png)去掉那些引入的http的资源就正常了。

![](/images/2018/3/https8.png)

