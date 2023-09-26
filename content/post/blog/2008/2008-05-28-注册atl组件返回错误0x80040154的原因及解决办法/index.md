---
layout: single
title: 注册atl组件返回错误0x80040154的原因及解决办法
date: 2008-05-28
categories:
  - 博客日记
tags:
  - 心情随笔
---

今天用VC6做了一个com组件，使用ATL模板创建，结果在使用regsvr32.exe注册时死活注册不上，返回0x80040154，使用ErrorLookup查看错误号结果是“没有注册类别”，百思不得其解，即使以前可以注册的组件现在也无法注册了，怀疑是操作系统的问题。

上网搜索了半天，最终还是在微软的官方网站上找到了一点儿蛛丝马迹：

“WhenyouregisteranATLserver,youmightgeterror0x80040154(Classnotregistered).ForDLLs,REGSVR32.exereturnsthiserror.ForEXEs,thecallto_Module&#58;&#58;

RegisterServer(CComModule&#58;&#58;RegisterServer)in_tWinMain()returnsthiserror.”，

接着往下看“InstallATL70.dll(orATL.dllforearlierversionsofVisualStudio)intheWindows\\SystemorWinnt\\System32directory.YoudonothavetoregisterATL70.dll,however,youmustregisterATL.dllbyusingRegsvr32.exe.ThereareUNICODEandANSIversionsofATL70.dllandATL.dll.Installtheappropriateversiononthetargetoperatingsystem(thatis,UNICODEforMicrosoftWindowsNT,andANSIforMicrosoftWindows95orMicrosoftWindows98).”

哦，原来是system32下面的atl.dll没有注册，打开C&#58;\\windows\\system32\\找到atl.dll后使用regsvr32注册，然后再注册我的组件，成功！

结论：怀疑在安装、卸载软件或使用优化软件进行系统清理的时候不小心反注册了atl.dll，导致使用atl模板创建的com组件均无法注册。

ps：两年前就遇到过此问题，当时无法搞定，只得重装系统，今天总算找到问题的原因了
