---
title: 机器文摘 第 041 期
date: 2023-07-19
description: 机器文摘 第 041 期
tags:
    - 机器文摘
categories:
    - 机器文摘
---
# 机器文摘 第 041 期

## 长文
### C 也能一次编译到处运行了？
![](2023-07-19-09-28-30.png)
用 C 编写的程序，只编译一次，生成的可执行文件能同时在多个平台运行吗？

这在以往是 java 这类依赖虚拟机执行环境的语言宣称的事情。

然而我今天才听说还有这个神奇的库（好久没关注过c++领域的技术了）：[Cosmopolitan](https://github.com/jart/cosmopolitan)Libc 号称可以使 C 成为一种构建一次就能到处运行的语言，就像Java一样，除了它不需要解释器或虚拟机。相反，它重新配置了GCC和Clang，以输出POSIX批准的多语言格式，该格式在Linux + Mac + Windows + FreeBSD + OpenBSD + NetBSD + BIOS上本地运行，具有最佳的性能和最小的占用空间。

在使用的时候需要引入特殊的库和编译配置，具体执行效果我还没有测试。

然后，[这篇文章](https://ahgamut.github.io/2023/07/13/patching-gcc-cosmo/)的作者干脆来个更方便的操作，他给 GCC 打了大约 2000 行的补丁，使得 GCC 直接就嵌入了 Cosmopolitan 库，现在可以在不修改任何源代码（前提是得用纯 C 写）的情况下构建出到处都能运行可执行文件了（Windows也可以吗？我要测试）。

### 业余无线电入坑指南
![](2023-07-19-09-29-07.png)
业余无线电跟摄影、HiFi音响这一类的爱好在某种维度上非常相似，在“入坑”的境界上，甚至完全一样。

这里的坑，指需要投入大量精力和资金。

之所以这么说，是因为它们都有一个共同的特点。

即围绕这些爱好有大量的知识可以学习和探索。

比如拿业余无线电来说，上来就一堆“亚音”、“中继”、“频段”、“频差”、“杂散发射”等名词，对标摄影中的“构图”、“光圈”、“快门”、“ISO感光度”等名词。新手若想有所体会，单是这些概念就够琢磨几天的。更不用提后续还有逐渐步入玄学的一些操作流派，乃至一个不留神还会陷入无穷尽的装备升级竞赛。

这类知识对于好奇心强烈、喜欢求知的人来说有着巨大的吸引力。甚至直白的说，我们很可能不是爱好这项技能，而是单纯喜欢探索和求知的过程，喜欢那种获得感。

这篇[《业余无线电新手指南》](https://zhuanlan.zhihu.com/p/585518350)可以普及一些基本知识，愿意入坑的请阅读。

*我近期已考取了中国无线电协会的业余无线电操作能力 A 证* 算是合法的 [HAM 火腿](https://baike.baidu.com/item/%E6%97%A0%E7%BA%BF%E7%94%B5%E7%88%B1%E5%A5%BD%E8%80%85/6509242)了。

### 远程办公还能成为趋势吗？
![](2023-07-19-09-29-47.png)
疫情的时候，远程办公、异地协同等概念一度变得很火爆，当时很多人觉得这又是一个风口。

但随着当时极端环境的消失，各大公司又纷纷将员工从居家办公中召回。

那么？此类与远程协作相关的概念破灭了吗？

各种协同工具、平台相关的市场，还有没有继续扩大的可能，或者说还在等待一个巨大的技术革新来引爆？

这里有个项目，[积极收集远程办公相关的信息](https://github.com/LinuxSuRen/remote-jobs-in-china)，包括国内支持的公司清单、工具及使用资料等。

### 怎样做出伟大的成就？
![](2023-07-19-09-30-40.png)
昨日读了保罗格雷厄姆（《黑客与画家》的作者）新文章一篇----[《怎样做出伟大的成就》](http://paulgraham.com/greatwork.html)（实际上我觉得可以译为“怎样牛逼”）。

虽然标题看起来略有鸡汤味儿，但读起来还是比较实惠的。

文章从发现和选择要做的事情开始，谈论了一些具体的方法。然后展开讨论了在方法执行过程中可能会遇到的一些问题，以及如何克服。甚至介绍了一些心理暗示技巧。

文章比较长，我个人体会比较深的点如下：
  1. 一个人做什么才能牛逼？答：做自己天赋里有的东西，就是找一些你既有能力又非常感兴趣的事情。
  2. 要养成“自驱”的习惯。让“工作”来源于自己的认知，而不是别人告诉你、让你做的事情。主动，而不是等待。
  3. 拥有一个属于自己的“项目”是一个找到“自驱”的最佳方法。不断观察自己对什么有强烈的好奇心（甚至好奇到大多数人不能理解）可以找到这样的“项目”。
  4. 选定要做的“项目”还应遵循兴奋原则，即：做自己愿意用的产品，写自己想读的故事，而不是执着于满足想象中的不存在的复杂需求。
  5. 注重积累效应，日拱一卒、长期积累，每天写一篇文字，一年下来就是一本书。
  6. 周期性审视自己做的事情，确认它是否偏离了目标（在做自己最想做的事情），及时修正。
  7. 行动的重要性，很多人实际上可以更牛逼，但是因为“谦虚”和“恐惧”导致的拖延使得计划一再搁浅，浪费了时间。

## 资源
- [jabbr.ai](http://t.cn/A60wPLwI)是一个针对拳击比赛的打击判定进行训练的AI模型，可以在智能手机上运行，实时监测视频中拳击选手的打击得分情况，即时进行统计，多个智能手机多视角同时运行可以快速生成总结性视频。模型提供约50种监测参数（质量、步法、压力等）可用于运动员训练分析。
  ![](2023-07-19-09-31-11.png)
- 浏览器地址栏快捷操作，我今天才知道原来浏览器地址栏还有这些快捷操作（火狐浏览器支持的最多，我测试的Edge浏览器也支持部分操作）：
  1. 输入*星号，可以搜索你的收藏夹；
  2. 输入^，可以搜索历史浏览记录；
  3. 输入%，可以搜索当前打开的tab页；
  4. 输入？，可以显示所有搜索建议； ​​​
- [树莓磁带](https://video.weibo.com/show?fid=1034:4923133602234429) 一种用树莓派做的小硬件，为了支持在老式电脑中加载程序（之前用磁带存储的那种）。
  ![](2023-07-19-09-31-40.png)
- 两招教你“永久”关闭 Windows 自动更新（任选一个都可以）：
  1. 通过执行代码的方式：`reg add “HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings” /v FlightSettingsMaxPauseDays /t reg_dword /d 10000 /f` Win+R 打开「运行」对话框，输入 `cmd` 后按下 `Ctrl+Shift+Enter`，在弹出来的命令行窗口中输入上面的代码，并敲击回车。命令里的 10000 代表停止更新的天数。
  2. 手动把电脑时钟日期改成 2050 年（为了防止时间自动校准，可以暂时断开网络），然后在 Windows 更新设置界面里面点击“延迟更新”，完成设置后再把电脑时间调回来就行了。
- [pkg-size](https://pkg-size.dev/)，一个在线监测 npm 包大小的网站，可以实时查看一个 npm 包的真实依赖，网站利用了 web容器技术，直接在浏览器里执行 npm install 操作。
  ![](2023-07-19-09-32-07.png)
- [3e](https://marketplace.visualstudio.com/items?itemName=degreat.3e)，一个 VS Code 插件，可以让你在编辑器里直接浏览 3d 模型，基于 webgl 实现。
  ![](2023-07-19-09-32-58.png)

## 订阅
这里会隔三岔五分享我看到的有趣的内容（不一定是最新的，但是有意思），因为大部分都与机器有关，所以先叫它“机器文摘”吧。

喜欢的朋友可以订阅关注：

- 通过微信公众号“从容地狂奔”订阅。

![](../weixin.jpg)

- 通过[竹白](https://zhubai.love/)进行邮件、微信小程序订阅。

![](../zhubai.jpg)