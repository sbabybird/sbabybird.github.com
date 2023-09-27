---
layout: single
title: 关于windows7下无法安装Visual Studio2008的问题
date: 2009-12-30
categories:
  - 博客日记
tags:
  - 心情随笔
---

单位的机器，前一段时间，被我换成了windows7系统，没办法，咱就是爱折腾。

尝鲜总是要付出代价的，那就是不知怎地，过了一段时间就无法安装某些软件了，不能安装office这还能忍，可是连vs都不能装了那还用个屁啊。反复观察，原来是无法安装vc++的runtime了（也就是vc_redist_x86.exe），具体是为什么不太清楚，好像是一个系统的bug导致的。反复地google，去microsoft网站去查，折腾了好几天，总算有了解决办法。

步骤如下：

1、打开注册表编辑器regedit，找到这儿HKEY_LOCAL_MACHINE\\System\\CurrentControlSet\\Control，

下面有个叫RegistrySizeLimi的键，把它的值修改为0xffffffff

2、重新启动电脑，并使用administrator用户登录，如果该用户未启用则要首先到“计算机管理”里面把administrator帐号启用。

3、在cmd里运行“sfc/scannow”以上几步完成后，再次重启机器即可。
