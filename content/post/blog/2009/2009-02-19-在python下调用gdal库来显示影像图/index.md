---
layout: single
title: 在python下调用gdal库来显示影像图
date: 2009-02-19
categories:
  - 博客日记
tags:
  - 心情随笔
---

很久没有更新了，懒是一方面原因，另一方面是因为最近忙的没有心思写博客了。其实按理说，每天抽出一点时间来唠叨两句还是能够办到的，只是一旦停下来，再开始就更费尽了。随便整理一些东西发上来吧，又是关于技术的。有一段时间我需要写程序来处理tif格式的影像图，在网上找来找去就发现了gdal这个好东西，可是在vc下调用它还是有些罗嗦，达不到快速调试的效果。于是前两天我又试着在python下调用gdal，把思路先用python实现一遍，调试通过了再用c++。下面是最简单的显示一幅tif影像图的python代码：importpygamefromosgeoimportgdalpygame.init()&nbsp;&nbsp;&nbsp;screen=pygame.display.set_mode(WINSIZE)&nbsp;&nbsp;&nbsp;pygame.display.set_caption(\'gdaltest\')&nbsp;&nbsp;&nbsp;pygame.time.set_timer(USEREVENT,50)dataset=gdal.Open(\"c&#58;\\\est.tif\")&nbsp;&nbsp;&nbsp;surface=pygame.Surface((WINWIDTH,WINHEIGHT))&nbsp;&nbsp;&nbsp;parr=dataset.ReadAsArray(1,1,WINWIDTH+1,WINHEIGHT+1)&nbsp;&nbsp;&nbsp;r=parr[0]&nbsp;&nbsp;&nbsp;g=parr[1]&nbsp;&nbsp;&nbsp;b=parr[2]&nbsp;&nbsp;&nbsp;img=pygame.PixelArray(surface)&nbsp;&nbsp;&nbsp;forxinxrange(WINWIDTH)&#58;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;foryinxrange(WINHEIGHT)&#58;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;img[x,y]=(r[y,x],g[y,x],b[y,x])&nbsp;&nbsp;&nbsp;show(img)注：用到了pygame库，因为用它显示图形或绘制图像比较方便。
