---
layout: single
title: 怎样使用VC6的远程调试
date: 2008-07-03
categories:
  - 博客日记
tags:
  - 心情随笔
---

今天遇到一个问题，我们的程序在本地执行一切正常，但在售后的一台笔记本电脑中却无法启动且爆出runtimeerror。

无奈只有通过调试来查找问题所在，由于该笔记本并未安装开发环境，于是想到了VC6的远程调试。上网翻看资料，写的都不太详细，摸索半天终于成功，并通过远程调试搞定了程序的问题。

现将远程调试的详细操作记录下来以备忘。


1、需机器两台：一台为调试机（装有VC6开发环境），一台为客户机（运行程序）

2、假定客户机的ip地址为192.168.0.168

3、假定需要运行调试的程序放在客户机的C\emote_bin\emote_test.exe

4、共享客户机C&#58;\emote_bin文件夹，并开放所有权限（读、写），共享名为remote_bin;

5、在调试机上映射客户机remote_bin共享目录为\"Z\"盘(可在cmd中执行\"netusez&#58;\\\\192.168.0.168\emote_bin\")&nbsp;

6、拷贝调试机上VC6安装目录下的Bin目录中的全部内容到客户机任意位置（该目录在调试机的路径一般为\"C&#58;\\ProgramFiles\\MicrosoftVisualStudio\\COMMON\\MSDev98\\Bin\"），在此假定拷贝在客户机的\"C&#58;\\Debugger\"&nbsp;

7、在客户机运行\"C&#58;\\Debugger\\MSVCMON.exe\"，启动后再对话框上直接点击\"Connect\"按钮（不用点\"Setting\"按钮），期间如有防火墙告警提示，需允许该程序。&nbsp;

8、回到调试机，打开VC6并打开要调试的工程文件（再此为remote_test)，在VC6的\"Build\"菜单下点击\"DebuggerRemoteConnection\"，在弹出的对话框左侧选择\"NetWork(TCP/IP)\"，点击右侧\"Setting\"按钮，填入客户机ip地址(192.168.0.168)点击\"ok\"&nbsp;

9、点击VC6的\"Project\"菜单下\"Setting\"，切换到Link页面，在Outputfile中填入\"Z&#58;\emote_test.exe\"，切换到Debug页，在Executablefordebugsession中填入\"Z&#58;\emote_test.exe\"，在Remoteexecutablepathandfilename中填入\"C&#58;\emote_bin\emote_test.exe\"（注意：此行甚为重要，需填写程序在客户机的完整路径）&nbsp;

10、大功告成，按F7编译可执行文件，按F5开始远程调试吧！
