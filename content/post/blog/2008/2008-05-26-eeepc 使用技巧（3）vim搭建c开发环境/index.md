---
layout: single
title: eeepc 使用技巧（3）vim搭建c开发环境
date: 2008-05-26
categories:
  - 博客日记
tags:
  - 心情随笔
---

今天继续记录eeepc的使用经验，闲言碎语不要讲，说一说如何安装c、c++开发环境以及在vim下进行编程。安装开发环境很简单，不用单个安装gcc、make什么的，只需sudoapt-getinstallbuild-essential,这里面就什么都包含了（gcc、g++、gdb、make等）。然后就找个合适的编辑器吧，系统自带vim，vim太强大了，这里不能多说（我也是刚开始用它），但是只有最基本的编辑功能，要想比较方便地进行开发需要安装如下vim插件：ctags、Taglist、supertab、c.vimctags其实不算是插件，算是单独的程序，用来生成vim能识别的标签文件，这样在vim写代码时就可以进行函数、变量、枚举类型之间快速定位了。taglist可以在vim窗口的左侧生成一个tags列表，里面就是用ctags生成那些标签，方便随时定位到这些标签supertab是个增强版的代码补齐插件，写代码时按tab键可以弹出自动补齐列表供选择，如“p”可以自动补齐为“printf”c.vim是进行c、c++编程时的必备插件，能使vim变成一个为开发c语言定制的一个ide，拥有自动注释、F9编译，自动补全等强大功能。插件装好后，在vim的vimrc文件里需要加上syntaxon这样每次启动vim时，它的语法高亮功能就自动打开了。写一段代码试试看vimhelloworld.c#include&lt;stdio.h&amp;gt;intmain()&#123;printf(\"helloworld\");return0;&#125;&#58;wq退出编译：gcchelloworld.c-ohelloworld运行：./helloworld
