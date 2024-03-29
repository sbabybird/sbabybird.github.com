---
layout: single
title: 如何给项目写一篇合适的readme
date: 2016-08-07
categories:
  - 日志
tags:
  - 500
---

![](http://www.readmeonline.com.au/images/readme_head.jpg)
很多人忽视这个说明文档，往往给自己的项目工程建立一个空 readme 文件或者在里面随便写几行不清不楚的文字，这样非常不利于代码工程的后期管理，尤其是对于有团队协作的项目，即使是个人项目，考虑到后期可能要给别人用，写一份合适的说明也十分必要。

现在我们的项目工程已经全部迁移到 gitlab 中了，大家使用 git 工具管理 自己的代码版本已经比较得心应手，但是仅仅使用 git 管理代码并没有发挥出 gitlab 的全部功能，我上次也提到了更好的使用 gitlab 的几个技巧，这次详细说一下如何给自己的项目写一篇 readme。

1. 在自己的项目代码的根目录中建立一个 readme.md 文件，注意扩展名为 md，这样 gitlab 就可以自动识别并在这个项目主页上自动渲染（将源码翻译成 html）这个文件了。

2. 学会使用[Markdown](http://www.jianshu.com/p/q81RER)语法，充分利用文档的“插入图片”、“嵌入代码”、“标题分级”、“超链接”等功能，将内容“富”起来，尤其是图片和超链接，可以弥补文本文件表达的不足。

3. 开头的简介很关键，readme 文档的主要意义在于向读者描述你这个项目做了什么，运行在什么环境，如何使用，所以在文档的开头首先要简要介绍这个项目的存在意义，为什么要做这个，主要解决什么问题，运行在什么环境，如果需要与别的项目配合，那么你的项目处于什么样的位置。

4. 必备信息，由于是开发工程，所以很多信息是必须要在文档中说明的，主要有：

   > - 开发编译和系统运行的必要参数

   - 项目中的文件和目录结构信息
   - 编译或安装步骤说明
   - 使用示例

5. 扩展信息，以上是传统的 readme 文档的套路，对于我们的软件开发工程（私有的非开源项目），我个人认为可以将 readme 稍作扩展，使得参与这个项目的人员能够在协作上更加顺畅，主要有：
   > - 项目的业务范围，可以理解为项目需求的简化索引，具体的需求可以链接到其他的 Markdown 文档

- 项目的流程图和架构图，可以理解为设计文档的索引，具体内容也可以链接到其他 Markdown 文档
- 版本信息，如果有发布版本，则持续更新版本的发布记录，说明每次发布的重要更新项

总之，文档的重要性不亚于项目代码，简洁有效的文档是一个成功项目的必要条件，在这个到处需要团队协作（或本地或远程）的时代，程序员想要让自己的项目得到更多的支持，发挥更好的作用，必须养成给编写技术文档的习惯。那么，先从一份能拿得出手的 readme 开始吧！
