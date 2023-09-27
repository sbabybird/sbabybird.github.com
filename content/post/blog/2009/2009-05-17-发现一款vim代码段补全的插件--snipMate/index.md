---
layout: single
title: 发现一款vim代码段补全的插件--snipMate
date: 2009-05-17
categories:
  - 博客日记
tags:
  - 心情随笔
---

作为一个工具狂人，我对Vim的喜爱是天生的。喜欢Vim的简单、高效、朴素、专业...。所以Vim成了我的主编辑器，无论是在Linux下还是XP下都能帮我高效地完成工作。（当然，Visual Studio才是我混饭吃的主要工具，不过这不是今天要说的重点）

对于使用Vim的人来说，大部分的工作是用Vim来编辑代码，这么一来代码的自动补全就很重要了。虽然使用SuperTab、C-Support等插件之后Vim的代码补全功能有了很大提高，但是离VS下面的VSAssistant还是有一定的距离的，比如对于代码块的补全就不是很方便。

今天我发现的这个叫做snipMate的插件很好的弥补了这一点。这个插件再次证明了Vim是无所不能的，也说明了聪明人要是懒起来真的可以很过分。

snipMate的下载地址：[http://www.vim.org/scripts/script.php?script_id=2540](http://www.vim.org/scripts/script.php?script_id=2540)

下载解压到`vimfiles`目录即可，然后打开Vim，试着编辑一个C文件，比如`hello.c`，输入`main`然后按Tab键，你会发现代码变成了下面这样：

```c
int main(int argc, char const *argv[])
{
    return 0;
}
```
先输入for再按Tab键：
```c
for (i = 0; i < count; i++)
{
}
```
再按Tab键，光标还会自动跳跃到count、i、code上，以方便编写自己的代码。snipMate同样也有if、while、define等常用的片段补全。

当然了，snipMate是支持各种语言的补全的，比如Python、HTML、Java等等。

最后，最重要的，就是snipMate支持自定义补全，语法也很简单，通过编辑配置文件可以很方便地定义自己的自动片段补全。

再来一段演示视频，看完后就马上去下载安装吧！[演示视频链接](http://www.vimeo.com/3535418)
