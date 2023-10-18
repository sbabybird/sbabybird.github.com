---
layout: single
title: eeepc 使用技巧(4) 看电视
date: 2008-07-09
categories:
  - 日志
tags:
  - life
---

用小 e 在床头看电视在合适不过了，不过我没找到 Linux 下的网络电视软件。

找来找去，发现一些可以用 mplayer 播放的 mms 链接，试了一下效果还不错，几个著名的电视台都有对应的链接，比如：

凤凰卫视中文台 mms&#58;//58.22.96.10/litv01;

凤凰卫视资讯台 mms&#58;//58.22.96.10/litv03;

但是我的 mplayer 是基于命令行的，每次要看电视的时候还需把这些链接输入进去，感觉很不方便。

刚好这两天对 Python 这个脚本语言比较感兴趣，于是想用 Python 写一个脚本来帮我输入这些链接。

由于对 Python 还不熟，所以写的界面很丑，不过也够我用了。

具体思路是，将这些链接首先存入一个文本文件里保存为 channel.data，

内容如下：

```
凤凰卫视中文台|mms&#58;//58.22.96.10/litv01;
凤凰卫视资讯台|mms&#58;//58.22.96.10/litv03;
东风卫视|mms&#58;//58.22.96.10/litv07;
精品影院|mms&#58;//218.1.70.72&#58;
1755/JingPinYingYuan;
东方卫视|mms&#58;//live.smgbb.cn/dfws;
星空卫视|mms&#58;//58.22.96.10/litv06;
TVB8|mms&#58;//58.22.96.10/litv05;
```

然后写一个 python 脚本读取这些链接并将电视台的名称填入界面中的一个列表框里，到时候通过点击名称就可以播放了。

python 脚本内容如下：

```python
#!/usr/bin/env python
# -*- coding: UTF-8 -*-

from tkinter import *
import os
import string

class Application(Frame):
    clist = list({})

    def play_channel(self, channel_url):
        strcmd = 'mplayer ' + channel_url + ' -cache 1024'
        str_output = os.popen(strcmd).read()
        a = str_output.split("\\")

        for bin_a in a:
            print(bin_a)

        print(channel_url)

    def play_tv(self):
        print(self.clist[int(self.channellistbox.curselection()[0])])
        self.play_channel(self.clist[int(self.channellistbox.curselection()[0])])

    def init_channel_list(self, listbox):
        channel_file = open('tvchannel.dat', 'r')
        channel_info = channel_file.readlines()
        channel_file.close()

        for i in range(len(channel_info)):
            channel_list = channel_info[i].split(';')
            for j in range(len(channel_list)):
                channel = channel_list[j].split('|')
                channel_name = channel[0]
                channel_url = channel[1]
                listbox.insert(END, channel_name)
                self.clist.append(channel_url)

    def create_widgets(self):
        self.quit_button = Button(self)
        self.quit_button["text"] = "Quit"
        self.quit_button["command"] = self.quit
        self.quit_button["width"] = 30
        self.quit_button["height"] = 10
        self.quit_button.pack({"side": "left"})

        self.play_tv_button = Button(self)
        self.play_tv_button["text"] = "Play TV"
        self.play_tv_button["command"] = self.play_tv
        self.play_tv_button["width"] = 30
        self.play_tv_button["height"] = 10
        self.play_tv_button.pack({"side": "left"})

        self.channellistbox = Listbox(self)
        self.init_channel_list(self.channellistbox)
        self.channellistbox.selection_set(0)
        self.channellistbox.pack()

    def __init__(self, master=None):
        Frame.__init__(self, master)
        self.pack()
        self.create_widgets()

app = Application()
app.mainloop()
```

保存为 playtv.py，和刚才那个 channel.dat 放在一个目录，运行即可（python./playtv.py)。
