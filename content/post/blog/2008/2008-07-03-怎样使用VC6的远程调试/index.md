---
layout: single
title: 怎样使用VC6的远程调试
date: 2008-07-03
categories:
  - 日志
tags:
  - life
---

今天遇到一个问题，我们的程序在本地执行一切正常，但在售后的一台笔记本电脑中却无法启动且爆出 runtimeerror。

无奈只有通过调试来查找问题所在，由于该笔记本并未安装开发环境，于是想到了 VC6 的远程调试。上网翻看资料，写的都不太详细，摸索半天终于成功，并通过远程调试搞定了程序的问题。

现将远程调试的详细操作记录下来以备忘。

1、需机器两台：一台为调试机（装有 VC6 开发环境），一台为客户机（运行程序）

2、假定客户机的 ip 地址为 192.168.0.168

3、假定需要运行调试的程序放在客户机的 C\emote_bin\emote_test.exe

4、共享客户机 C&#58;\emote_bin 文件夹，并开放所有权限（读、写），共享名为 remote_bin;

5、在调试机上映射客户机 remote_bin 共享目录为\"Z\"盘(可在 cmd 中执行\"netusez&#58;\\\\192.168.0.168\emote_bin\")&nbsp;

6、拷贝调试机上 VC6 安装目录下的 Bin 目录中的全部内容到客户机任意位置（该目录在调试机的路径一般为\"C&#58;\\ProgramFiles\\MicrosoftVisualStudio\\COMMON\\MSDev98\\Bin\"），在此假定拷贝在客户机的\"C&#58;\\Debugger\"&nbsp;

7、在客户机运行\"C&#58;\\Debugger\\MSVCMON.exe\"，启动后再对话框上直接点击\"Connect\"按钮（不用点\"Setting\"按钮），期间如有防火墙告警提示，需允许该程序。&nbsp;

8、回到调试机，打开 VC6 并打开要调试的工程文件（再此为 remote_test)，在 VC6 的\"Build\"菜单下点击\"DebuggerRemoteConnection\"，在弹出的对话框左侧选择\"NetWork(TCP/IP)\"，点击右侧\"Setting\"按钮，填入客户机 ip 地址(192.168.0.168)点击\"ok\"&nbsp;

9、点击 VC6 的\"Project\"菜单下\"Setting\"，切换到 Link 页面，在 Outputfile 中填入\"Z&#58;\emote_test.exe\"，切换到 Debug 页，在 Executablefordebugsession 中填入\"Z&#58;\emote_test.exe\"，在 Remoteexecutablepathandfilename 中填入\"C&#58;\emote_bin\emote_test.exe\"（注意：此行甚为重要，需填写程序在客户机的完整路径）&nbsp;

10、大功告成，按 F7 编译可执行文件，按 F5 开始远程调试吧！
