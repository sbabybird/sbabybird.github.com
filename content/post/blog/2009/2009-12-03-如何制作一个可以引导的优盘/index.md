---
layout: single
title: 如何制作一个可以引导的优盘
date: 2009-12-03
categories:
  - 日志
tags:
  - life
---

这两天小笔记本出故障害我卷起袖子修了两个晚上，由于没有光驱，所以没少用到我的优盘，可是网上可下载系统盘一般都是 iso 文件，即光盘镜像刻录成光盘才可以引导机器启动，不过现在是 21 世纪了，几乎所有的主板都支持 usb 启动，所以没有光驱也无所谓了，只要手中有可引导光盘的 iso 文件就可以制作出一个可引导的优盘出来。

正所谓授之以鱼不如授之以渔，下面介绍一下制作可引导优盘的步骤，并非所有的引导盘都必须这么做，这仅是其中的一种方法，也最省事。

1、必备条件：运行 Windowsxp 系统的计算机一台，优盘一只。

2、去网上搜索并下载名叫“UltraISO\"的软件，试用版亦可。（该软件同时具有光盘刻录、iso 制作、虚拟光驱的功能，真是居家旅行........）

3、可引导的光盘镜像文件（扩展名一般为 iso）一只，比如 ubuntu9.10-i386-livecd.iso，具体要什么 iso 取决于你要干的事情，如果这一句你弄不明白，那就别往下进行了。

4、把那只倒霉的优盘插入电脑。（记清楚他的盘符，如果你插入了多个优盘的话）。

4、启动 UltraISO，在菜单里选择“文件”==》“打开”选中你的 iso 文件。确定。

5、在菜单里找到“启动”下面的“写入硬盘映像”并猛烈点击之。

6、现在弹出了一个新对话框，在名叫“选择硬盘驱动器”的那个下拉框中选择你刚才插入的那个优盘（如果就插入了一个，就不用于选了）。

7、在“写入方式”那个下拉框里选择“USB-HDD+”，除了这个选项还有“USB-ZIP”等选项，但是你选择 USB-HDD+就可以了，因为这个格式的兼容性最好，实在不行再换其他的。

8、点击“写入按钮”并耐心等待。注意：优盘的内容会被清空。

9、等写完了就拔掉优盘尽情的去得瑟吧。
