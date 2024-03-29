---
layout: single
title: 注册atl组件返回错误0x80040154的原因及解决办法
date: 2008-05-28
categories:
  - 日志
tags:
  - life
---

今天用 VC6 做了一个 com 组件，使用 ATL 模板创建，结果在使用 regsvr32.exe 注册时死活注册不上，返回 0x80040154，使用 ErrorLookup 查看错误号结果是“没有注册类别”，百思不得其解，即使以前可以注册的组件现在也无法注册了，怀疑是操作系统的问题。

上网搜索了半天，最终还是在微软的官方网站上找到了一点儿蛛丝马迹：

“WhenyouregisteranATLserver,youmightgeterror0x80040154(Classnotregistered).ForDLLs,REGSVR32.exereturnsthiserror.ForEXEs,thecallto_Module&#58;&#58;

RegisterServer(CComModule&#58;&#58;RegisterServer)in_tWinMain()returnsthiserror.”，

接着往下看“InstallATL70.dll(orATL.dllforearlierversionsofVisualStudio)intheWindows\\SystemorWinnt\\System32directory.YoudonothavetoregisterATL70.dll,however,youmustregisterATL.dllbyusingRegsvr32.exe.ThereareUNICODEandANSIversionsofATL70.dllandATL.dll.Installtheappropriateversiononthetargetoperatingsystem(thatis,UNICODEforMicrosoftWindowsNT,andANSIforMicrosoftWindows95orMicrosoftWindows98).”

哦，原来是 system32 下面的 atl.dll 没有注册，打开 C&#58;\\windows\\system32\\找到 atl.dll 后使用 regsvr32 注册，然后再注册我的组件，成功！

结论：怀疑在安装、卸载软件或使用优化软件进行系统清理的时候不小心反注册了 atl.dll，导致使用 atl 模板创建的 com 组件均无法注册。

ps：两年前就遇到过此问题，当时无法搞定，只得重装系统，今天总算找到问题的原因了
