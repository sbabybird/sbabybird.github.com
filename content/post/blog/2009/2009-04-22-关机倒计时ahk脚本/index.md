---
layout: single
title: 关机倒计时ahk脚本
date: 2009-04-22
categories:
  - 日志
tags:
  - life
---

最近习惯在晚上听着音乐或相声、评书睡觉，但电脑总是忘记关，于是使用 Windows 的`shutdown -s -t`命令来进行倒计时关机，但是我还嫌这样麻烦，因为要按多次键，还要输入命令，于是就写了下面的 AHK 脚本，运行后只要按下 Windows 键 + S 键即弹出一个输入框，输入 3600 即一个小时，到时候就自动关机啦。后来觉得有取消关机的可能，就加了一个判断，到时候点击取消的话，就放弃关机了。

```autohotkey
#s::
InputBox, time, 关机倒计时, 请输入一个时间（单位是秒）
if (time > 0) {
    loop {
        if (A_Index > time) {
            break
        }
        sleep, 1000
        count := time - A_Index
        ToolTip, 剩余：%count%秒关机
    }
    ToolTip
    MsgBox, 33, 关机倒计时, 定时关机的时间到了，确定要关闭计算机吗？
    `n`n此框6秒内自动确定, 6
    IfMsgBoxCancel
    {
        MsgBox 取消了关机
    }
    else
    {
        Shutdown, 9
    }
}
return
```
