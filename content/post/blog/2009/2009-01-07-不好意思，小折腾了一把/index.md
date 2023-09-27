---
layout: single
title: 不好意思，小折腾了一把
date: 2009-01-07
categories:
  - 博客日记
tags:
  - 心情随笔
---

前一段时间我在eeepc上装了ubuntu，这个linux的发行版确实比asus自带的那个强大得多得多得多（继续），但是有个缺点------慢。

为此我忍了很久了。

今天回到家，想装上一个最新的播放器软件，发现没有合适的安装包，于是就想，反正有源码，那就自己编译吧，于是，卷起袖子就开始了。

下载代码后，configure发现我的gtk太老，apt-get又不给我装gtk（说我已经有了最新版），于是我又要先把gtk的最新版编译好，但是问题又来了，gtk的编译依赖glib，于是我又要先把glib编译好，但是问题又来了，glib的编译又依赖另外的包，于是我耐着性子一个一个把这些包都编译完，make，makeinstall，手都酸了，然后再编译gtk，又告诉我没有atk、freetype、cairo、pango、pixman等等一大堆依赖包，

好吧，非编译出来不可！

全部下载这些东东的代码，一个一个make再makeinstall，终于可以编译gtk了，终于把gtk编译完了。发现我的Firefox却运行不起来了，Fuck！
