---
layout: single
title: 关机倒计时ahk脚本
date: 2009-04-22
categories:
  - 博客日记
tags:
  - 心情随笔
---

最近习惯在晚上听着音乐或相声、评书睡觉，但电脑总是忘记关，于是使用windows的shutdown-s-t命令来进行倒计时关机，但是我还嫌这样麻烦，因为要摁多次键，还要输入命令，于是就写了下面的ahk脚本，运行后只要按下windows键+s键即弹出一个输入框，输入3600即一个小时，到时候就自动关机啦。后来觉得有取消关机的可能，就加了一个判断，到时候点击取消的话，就放弃关机了。什么？你问ahk是什么？看这里&nbsp;;倒计时关机的ahk脚本#s&#58;&#58;InputBox,time,关机倒计时,请输入一个时间（单位是秒）if(time&gt;0)&#123;loop&#123;if(a_index&gt;time)&#123;break&#125;sleep,1000count&#58;=time-a_indexToolTip,剩余&#58;%count%秒关机&#125;ToolTipMsgBox,33,关机倒计时,定时关机的时间到了，确定要关闭计算机吗？`n`n此框6秒内自动确定,6IfMsgBoxCancelMsgBox取消了关机else&nbsp;Shutdown,9&#125;return
