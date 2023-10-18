---
layout: single
title: 不好意思，小折腾了一把
date: 2009-01-07
categories:
  - 日志
tags:
  - life
---

前一段时间我在 eeepc 上装了 ubuntu，这个 linux 的发行版确实比 asus 自带的那个强大得多得多得多（继续），但是有个缺点------慢。

为此我忍了很久了。

今天回到家，想装上一个最新的播放器软件，发现没有合适的安装包，于是就想，反正有源码，那就自己编译吧，于是，卷起袖子就开始了。

下载代码后，configure 发现我的 gtk 太老，apt-get 又不给我装 gtk（说我已经有了最新版），于是我又要先把 gtk 的最新版编译好，但是问题又来了，gtk 的编译依赖 glib，于是我又要先把 glib 编译好，但是问题又来了，glib 的编译又依赖另外的包，于是我耐着性子一个一个把这些包都编译完，make，makeinstall，手都酸了，然后再编译 gtk，又告诉我没有 atk、freetype、cairo、pango、pixman 等等一大堆依赖包，

好吧，非编译出来不可！

全部下载这些东东的代码，一个一个 make 再 makeinstall，终于可以编译 gtk 了，终于把 gtk 编译完了。发现我的 Firefox 却运行不起来了，Fuck！
