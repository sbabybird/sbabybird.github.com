---
layout: single
title: 使用DockerToolbox在Windows下搭建Docker环境
date: 2016-07-02
categories:
  - 日志
tags:
  - 500
---

Docker 是一种比虚拟机更轻量级的应用程序执行容器，受云计算技术普及以及微服务架构的影响，Docker 这两年风声水起，成为用于管理应用部署的最佳利器，很多 DevOps 团队宣称使用该技术后能极大缩减开发、测试、生产环境切换的时间，提升整体效率。

考虑到目前很多开发人员仍是在 Mac 和 Windows 系统进行开发，为了方便环境的部署和管理，Docker 公司近期推出了 DockerToolbox 工具包，可以跨平台（Mac、Windows）使用，对于想在 Windows 环境下体验容器技术并开发产品的程序员来说真是福音。

安装过程很简单，直接去[官网下载](https://www.docker.com/products/docker-toolbox)对应的安装包到本地执行安装程序即可，安装后会自动在系统中打包安装 VirtualBox 虚拟机（因为 Docker 依赖 Linux 系统，必须模拟 Linux 环境）、Docker-engine、Docker-machine、Docker-compose 等组件，基本做到了即开即用。

然后主要就是进入命令行管理界面（安装包会创建快捷方式），执行各种 docker 命令进行工作了，我在使用过程中主要遇到了如下问题：

1、CPU 虚拟化的开启，现在的 CPU 一般都在硬件级别支持虚拟化技术，但是有的可能默认没有打开，需要到 BIOS 中手动开启，查看是否开启的方法是，在 windows 系统任务管理器的“性能”页，是否有虚拟化已开启的字样，当然目前也有一些比较老的低端 CPU 不支持，这个就建议更换设备吧。

2、与 Windows 系统自带的虚拟化技术 Hyper-V 冲突，专业版的 Windows 系统一般带有虚拟化技术组件，是微软自有的，名叫 Hyper-V（与 virtual box 等类似），但是与我们要安装的工具有冲突，需要关闭 Hyper-V 后才能正常使用，具体操作方法为到控制面板的“程序和功能”里面的“启用或关闭 windows 功能”将 Hyper-V 关掉。

3、VirtualBox 虚拟机网段 IP 分配冲突，这个是我遇到的特例，VirtualBox 会自动给用于模拟 Docker 环境的虚拟机分配内网 IP 地址，且默认为 10.0.2 网段，这个恰恰与我的工作环境存在冲突，而且界面中和配置文件里都没有可配置的地方，经过多天研究，终于找到通过命令行的方式将这个默认配置可以改掉 ，命令如下`
VBoxManage.exe modifyvm "default" --natnet1 "10.0.20.0/24"`（需要在 virtualbox 安装目录下执行，default 是虚拟机的名字。）

4、系统重启后环境丢失（偶然发生），这个可能是工具存在 bug，我在下载各种镜像进行测试后，将我的 Windows 重启后发现 default 虚拟机里的东西都丢了，这个可能是由于环境在运行的状态下我重启了系统导致。目前我的解决办法是在每次关机或重启的时候，先将 default 虚拟机停掉，方法是在命令行下执行如下指令`docker-machine stop default` 。

总的来说，这套工具包非常方便在 windows 下开发的人员，基本可以做到与容器环境的无缝对接，合理使用这一套工具包，对于我们的“持续集成”、“持续交付”等工作将有很大的促进作用。
