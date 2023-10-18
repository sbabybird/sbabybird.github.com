---
layout: single
title: 写了个脚本整理我的照片
date: 2010-05-01
categories:
  - 日志
tags:
  - life
---

上次整理硬盘的时候把我的照片一股脑儿的放在了一个目录下，这次又有闲功夫了，写了个 python 脚本来处理我的照片。基本思路是使用 PIL 库读取照片的 exif 信息，取出拍摄的日期时间，根据日期建立新的文件夹，然后照片文件以日期时间格式命名。批量处理，比较简单。

```python
#!/usr/bin/env python
# -*- coding: gbk -*-

"""
复制指定目录的照片到目标目录，并且根据照片的拍摄时间进行重命名
比如某张照片拍摄于2008年3月15日12:00:00，则目标目录为2008\\03\\15\\120000.jpg
"""

from PIL import Image
import os
import sys

def get_dist_path(str, dist_dir):
    date = str.split(' ')[0].split(':')
    dirs = dist_dir + os.sep + os.sep.join(date)

    if not os.path.exists(dirs):
        os.makedirs(dirs)

    dirs = dirs + os.sep + ''.join(str.split(' ')[1].split(':')) + '.jpg'
    return dirs

def copy_image(src_dir, dist_dir):
    for path in [src_dir + os.sep + i for i in os.listdir(src_dir)]:
        if os.path.isdir(path):
            copy_image(path, dist_dir)
        else:
            write_log(path)
            try:
                image = Image.open(path)
            except:
                log_str = 'file open error: ' + path
                write_log(log_str)
            try:
                dist_path = get_dist_path(image._getexif()[306], dist_dir)
                log_str = 'dist path: ' + dist_path
                write_log(log_str)
            except:
                log_str = 'get exif error: ' + path
                write_log(log_str)
            try:
                if not os.path.exists(dist_path):
                    image.save(dist_path)
            except:
                log_str = 'file copy error: ' + path
                write_log(log_str)

def write_log(str):
    global log_file
    log_file.write(str + '\n')
    print(str)

def main():
    if len(sys.argv) == 3:
        global log_file
        log_file = open('cilog.txt', 'w')
        copy_image(sys.argv[1], sys.argv[2])
        log_file.close()
    else:
        print('需要给出两个参数，第一个是照片目录，第二个是目标目录')
        print('例如：', sys.argv[0], 'e:\\photo f:\\goodphoto')

if __name__ == '__main__':
    main()
```
