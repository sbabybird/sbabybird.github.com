---
layout: single
title: 发现一款vim代码段补全的插件--snipMate
date: 2009-05-17
categories:
  - 博客日记
tags:
  - 心情随笔
---

作为一个工具狂人，我对vim的喜爱是天生的，喜欢vim的简单、高效、朴素、专业......&nbsp;。所以vim成了我的主编辑器，无论是在Linux下还是xp下都能帮我高效地完成工作。（当然，VisualStudio才是我混饭吃的主要工具，不过这不是今天要说的重点）对于使用vim的人来说，大部分的工作是用vim来编辑代码，这么一来代码的自动补全就很重要了，虽然使用super-tab、c-support等插件之后vim的代码补全功能有了很大提高，但是离vs下面的vsassistant还是有一定的距离的，比如对于代码块的补全就不是很方便，今天我发现的这个叫做snipMate的插件很好的弥补了这一点，这个插件再次证明了vim是无所不能的，也说明了聪明人要是懒起来真的可以很过分。snipMate的下载地址http&#58;//www.vim.org/scripts/script.php?script_id=2540下载解压到vimfiles目录即可，然后打开vim，试着编辑一个c文件，比如hello.c，输入main然后按tab键，你会发现代码变成了下面这样intmain(intargc,charconst*argv[])&#123;return0;&#125;先输入for再按tab键for(i=0;i&lt;count;i++)&#123;&#125;再按tab键，光标还会再count、i、code上自动跳跃，以方便编写自己的代码。snipMate同样也有if、while、define等常用的片段补全。当然了，snipMate是支持各种语言的补全的，比如python、html、java等等。最后，最重要的，就是snipMate支持自定义补全，语法也很简单，通过编辑配置文件可以很方便地定义自己的自动片段补全。再来一段演示视频，看完后就马上去下载安装吧！http&#58;//www.vimeo.com/3535418
