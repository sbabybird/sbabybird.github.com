---
layout: single
title: eeepc 使用技巧（3）vim搭建c开发环境
date: 2008-05-26
categories:
  - 日志
tags:
  - life
---

今天继续记录 eeepc 的使用经验，闲言碎语不要讲，说一说如何安装 c、c++开发环境以及在 vim 下进行编程。

安装开发环境很简单，不用单个安装 gcc、make 什么的，只需 sudoapt-getinstallbuild-essential,这里面就什么都包含了（gcc、g++、gdb、make 等）。

然后就找个合适的编辑器吧，系统自带 vim，vim 太强大了，这里不能多说（我也是刚开始用它），但是只有最基本的编辑功能，要想比较方便地进行开发需要安装如下 vim 插件：ctags、Taglist、supertab、c.vimctags 其实不算是插件，算是单独的程序，用来生成 vim 能识别的标签文件，这样在 vim 写代码时就可以进行函数、变量、枚举类型之间快速定位了。

taglist 可以在 vim 窗口的左侧生成一个 tags 列表，里面就是用 ctags 生成那些标签，方便随时定位到这些标签 supertab 是个增强版的代码补齐插件，写代码时按 tab 键可以弹出自动补齐列表供选择，如“p”可以自动补齐为“printf”c.vim 是进行 c、c++编程时的必备插件，能使 vim 变成一个为开发 c 语言定制的一个 ide，拥有自动注释、F9 编译，自动补全等强大功能。

插件装好后，在 vim 的 vimrc 文件里需要加上 syntaxon 这样每次启动 vim 时，它的语法高亮功能就自动打开了。

写一段代码试试看 vimhelloworld.c#include&lt;stdio.h&amp;gt;intmain()&#123;printf(\"helloworld\");return0;&#125;&#58;wq 退出编译：gcchelloworld.c-ohelloworld

运行：./helloworld
