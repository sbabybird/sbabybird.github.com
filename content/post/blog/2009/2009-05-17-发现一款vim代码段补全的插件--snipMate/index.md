---
layout: single
title: 发现一款vim代码段补全的插件--snipMate
date: 2009-05-17
categories:
  - 日志
tags:
  - life
---

作为一个工具狂人，我对 Vim 的喜爱是天生的。喜欢 Vim 的简单、高效、朴素、专业...。所以 Vim 成了我的主编辑器，无论是在 Linux 下还是 XP 下都能帮我高效地完成工作。（当然，Visual Studio 才是我混饭吃的主要工具，不过这不是今天要说的重点）

对于使用 Vim 的人来说，大部分的工作是用 Vim 来编辑代码，这么一来代码的自动补全就很重要了。虽然使用 SuperTab、C-Support 等插件之后 Vim 的代码补全功能有了很大提高，但是离 VS 下面的 VSAssistant 还是有一定的距离的，比如对于代码块的补全就不是很方便。

今天我发现的这个叫做 snipMate 的插件很好的弥补了这一点。这个插件再次证明了 Vim 是无所不能的，也说明了聪明人要是懒起来真的可以很过分。

snipMate 的下载地址：[http://www.vim.org/scripts/script.php?script_id=2540](http://www.vim.org/scripts/script.php?script_id=2540)

下载解压到`vimfiles`目录即可，然后打开 Vim，试着编辑一个 C 文件，比如`hello.c`，输入`main`然后按 Tab 键，你会发现代码变成了下面这样：

```c
int main(int argc, char const *argv[])
{
    return 0;
}
```

先输入 for 再按 Tab 键：

```c
for (i = 0; i < count; i++)
{
}
```

再按 Tab 键，光标还会自动跳跃到 count、i、code 上，以方便编写自己的代码。snipMate 同样也有 if、while、define 等常用的片段补全。

当然了，snipMate 是支持各种语言的补全的，比如 Python、HTML、Java 等等。

最后，最重要的，就是 snipMate 支持自定义补全，语法也很简单，通过编辑配置文件可以很方便地定义自己的自动片段补全。

再来一段演示视频，看完后就马上去下载安装吧！[演示视频链接](http://www.vimeo.com/3535418)
