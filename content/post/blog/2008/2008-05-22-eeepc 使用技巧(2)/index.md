---
layout: single
title: eeepc 使用技巧(2)
date: 2008-05-22
categories:
  - 日志
tags:
  - life
---

接着昨天的继续，系统修改为中文了，软件源设好了，输入法也装好了，接下来就想看看小 e（姑且把我的 eeepc 叫做小 e）的多媒体性能咋样儿了（其实就是看看能不能看片儿）。

小 e 自带有 mplayer 以及前端的 SMPlayer，播放一般视频（mpeg、wmv）效果挺不错，遗憾的是还不能播放 rmvb，上网查了一下原来是缺少相应的解码包，

于是乎，就找到了这个 win32codecs 下载后将这个压缩包解压后的内容放到/usr/lib/codecs 下即可，系统默认并没有 codecs 这个文件夹，需要手动创建 sudomkdir/usr/lib/codecs，然后复制 cp/home/user/win32codecs/\*/usr/lib/coecs。

好了，在命令行输入 mplayer/home/user/\*.rmvb-f-z 很流畅的画面就出现了，此时的-f 和-z 参数分别代表全屏和自动缩放画面到窗口大小。然后我又尝试播放了一下 720p 的高清视频（wmv 格式），小 e 也能轻松胜任，画面很清晰，也很流畅，看来 mplayer 这个软件写的很棒，虽然是命令行格式的，但是我喜欢。
