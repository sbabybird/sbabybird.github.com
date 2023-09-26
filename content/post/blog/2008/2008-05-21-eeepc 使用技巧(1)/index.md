---
layout: single
title: eeepc 使用技巧(1)
date: 2008-05-21
categories:
  - 博客日记
tags:
  - 心情随笔
---

买了eeepc900一段时间了，翻遍很多论坛，也慢慢摸索一些基本使用技巧，不敢独享，一直想写出来，只是最近工作很忙，加上地震带来的全国性灾难，导致最近几天也没心思去写。

现在，让我整理一下思路，慢慢把经验写下来，也防止我以后会忘记。

eeepc可以安装xp操作系统，但是我喜欢linux，买了eeepc有一半是为了使用linux，所以我不会把他自带的系统干掉然后安装xp系统，windows操作系统我实在是用腻了。

因为只有装了linux系统的机器才能让我感到完全是“自己的”。

eeepc900自带有定制的linux操作系统，而且是基于debian的发行版，哇，有了debian一切都好办了。

debian有强大的apt－get软件包管理系统，但是eeepc的说明书上吓唬我说“用户不能自行安装其他软件”，咳，管他呢，我查了一下，原来是在apt的source.list里没有相应的源而已，而且eeepc里也自带了“新立得软件管理器”只是没放出来而已。

好了，先从“控制台”开始，刚拿到手的时候，我费了老半天的劲儿才找到控制台窗口打开的办法，看来asus实在太担心用户的智商了。答案是按“Ctrl+Alt+T“就能调出控制台，要知道在Lxiux下有了”控制台“才算有了系统的操纵权啊！

由于默认是英文版的，让我先把系统从英文调整到中文吧在控制台输入/opt/xandros/bin/locale_dialog然后在弹出的对话框中选择简体中文，重启机器，就变成中文系统了。

随机带的软件太少了，而且大部分还是给小孩子用的，根本不够我用，本地化之后就我就开始想办法安装软件控制台输入`vim/etc/apt/sources.list`发现该文件就两行
```
debhttp&#58;//update.eeepc.asus.com/p900p900maindebhttp&#58;//update.eeepc.asus.com/p900/enp900main增加如下内容：debhttp&#58;//debian.cn99.com/debianstablemaincontribnon-free
```
然后：wq存盘退出sudoapt-getupdate这样就有了debian的基本源，现在开始使用apt-getinstall疯狂安装想要的软件吧！

由于我这个版本默认的输入法管理器是gcin的，虽然也有拼音输入，但是不符合大陆人的输入习惯，所以我首先要安装scim，在控制台输入sudoapt-getinstallscimscim-chinese，要想使用scim还需要一个软件sudoapt-getinstallim-swich，然后把gcin卸载sudoapt-getinstallgcin-好了，切换到scim吧，输入sudoim-switch-sscim然后重启机器，输入法管理器就变成scim啦！

唉，eeepc的键盘实在是太小了，在上面打字实在是太累，先写这么多，估计也就有十分之一吧，剩下的以后再慢慢写。
