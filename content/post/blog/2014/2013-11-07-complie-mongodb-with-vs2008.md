---
title : 使用vs2008编译mongodb
date: 2013-11-07
categories : 
  - 技术研究
tags : 
  - mongodb
  - vs2008
---

## 背景问题
mongodb在windwos下的官方编译包是使用vs2010编译的，从官网上下载的源代码在vs2008环境下不能直接编译通过，因为mongodb提供的相关配置文件是针对vs2010的，可能是因为mongodb最新的代码使用了部分C++11的特性，而vs2008没有提供对C++11支持的原因。可是我们在一个具体的项目上需要在vs2008环境下使用mongodb，只好通过手工修改部分配置和代码的办法完成编译。

## 环境准备
mongodb是使用scons进行编译控制的，所以在进行以下编译之前需要安装并配置好如下环境：

### python2.7
官方建议是安装python2.7版本，而且要在环境变量PATH中加入python的安装路径和python/scripts的路径，以便在命令行中执行python脚本。
*不过我在编译的时候使用的是python2.6版本，也没有发现问题*

### scons
 - 直接去网上下载最新版本进行安装即可。

### vs2008
 - 需要安装vc++的全部组件（主要是默认安装不带amd64的编译支持），如果只需要编译32位版本的话则可以忽略此条。
 - 需要安装sp1补丁，否则会在编译时报错。

### boost库
 - 最好使用boost1.4.9版本，去官网上下载对应的源码包然后自己在vs2008的命令行环境下编译
 - 编译boost的命令如下（只编译了所需库）：
    
        bjam stage variant=debug  --with-filesystem --with-thread --with-date_time --with-program_options --layout=versioned threading=multi toolset=msvc-10.0 --build-type=complete

 *如果需要编译release版本，就把`variant`的选项改为`release`，如果需要编译64位的版本，就在以上命令中加入`address-model=64`*

## 配置及代码修改

### SConstruct文件修改

SConstruct文件用于存放scons的关键配置信息，我们为了在vs2008下编译mongodb首先要做的就是修改mongodb源码下根目录的SConstruct文件。

 - 修改env配置，找到 evn = Environment

        env = Environment( BUILD_DIR=variantDir,
                   CLIENT_ARCHIVE='${CLIENT_DIST_BASENAME}${DIST_ARCHIVE_SUFFIX}',
                   CLIENT_DIST_BASENAME=get_option('client-dist-basename'),
                   CLIENT_LICENSE='#distsrc/client/LICENSE.txt',
                   CLIENT_SCONSTRUCT='#distsrc/client/SConstruct',
                   DIST_ARCHIVE_SUFFIX='.tgz',
                   EXTRAPATH=get_option("extrapath"),
                   MODULE_BANNERS=[],
                   MODULETEST_ALIAS='moduletests',
                   MODULETEST_LIST='#build/moduletests.txt',
                   MSVS_ARCH=msarch ,
                   PYTHON=utils.find_python(),
                   SERVER_ARCHIVE='${SERVER_DIST_BASENAME}${DIST_ARCHIVE_SUFFIX}',
                   TARGET_ARCH=msarch ,
                   tools=["default", "gch", "jsheader", "mergelib", "unittest"],
                   UNITTEST_ALIAS='unittests',
                   UNITTEST_LIST='#build/unittests.txt',
                   PYSYSPLATFORM=os.sys.platform,

                   PCRE_VERSION='8.30',
                   CONFIGUREDIR = '#' + scons_data_dir + '/sconf_temp',
                   CONFIGURELOG = '#' + scons_data_dir + '/config.log'
                   )

在Environment里追加一条 `MSVC_VERSION='9.0'`，这是因为如果机器上有其他的编译环境，比如vs2010或vs2012，scons会自动使用他们的编译器进行编译，即使你是在vs2008的命令行环境下，我最初因为此问题困扰了很久，后来才只得强制指定编译器的版本，修改完成后如下：

    env = Environment( BUILD_DIR=variantDir,
                   CLIENT_ARCHIVE='${CLIENT_DIST_BASENAME}${DIST_ARCHIVE_SUFFIX}',
                   CLIENT_DIST_BASENAME=get_option('client-dist-basename'),
                   CLIENT_LICENSE='#distsrc/client/LICENSE.txt',
                   CLIENT_SCONSTRUCT='#distsrc/client/SConstruct',
                   DIST_ARCHIVE_SUFFIX='.tgz',
                   EXTRAPATH=get_option("extrapath"),
                   MODULE_BANNERS=[],
                   MODULETEST_ALIAS='moduletests',
                   MODULETEST_LIST='#build/moduletests.txt',
                   MSVS_ARCH=msarch ,
                   PYTHON=utils.find_python(),
                   SERVER_ARCHIVE='${SERVER_DIST_BASENAME}${DIST_ARCHIVE_SUFFIX}',
                   TARGET_ARCH=msarch ,
                   tools=["default", "gch", "jsheader", "mergelib", "unittest"],
                   UNITTEST_ALIAS='unittests',
                   UNITTEST_LIST='#build/unittests.txt',
                   PYSYSPLATFORM=os.sys.platform,

                   PCRE_VERSION='8.30',
                   CONFIGUREDIR = '#' + scons_data_dir + '/sconf_temp',
                   CONFIGURELOG = '#' + scons_data_dir + '/config.log',
									 MSVC_VERSION = '9.0'
                   )

 - 给编译器搜索路径增加你自己本地的boost库路径
因为在编译时需要用到boost库，所以需要把你在本地的boost所在目录加入scons的环境，否则会报找不到boost头文件或链接库的错误，打开Sconstruct文件直接在最后加入如下代码

    env.Append(CPPPATH=["d:/thirdlib/boost_1_49_0", "d:/thirdlib/boost_1_49_0/boost/tr1"], LIBPATH=["d:/thridlib/boost_1_49_0/stage/lib"])

		*你在编译时需要将路径替换成你自己的*

### 准备stdint.h

 - 去这个地址<https://msinttypes.googlecode.com/files/msinttypes-r26.zip>下载msinttypes，将压缩包里的stdint.h解压并复制到 `C:\Program Files\Microsoft Visual Studio 9.0\VC\include` 目录
 - 修改mongodb源码目录下platform下的cstdint.h，将`#include<cstdint>`修改为`#include<stdint.h>`，将`#define _MONGO_STDINT_NAMESPACE std`这一行里的std注释掉，变成`#define _MONGO_STDINT_NAMESPACE /*std*/ `
 - 修改mongodb源码目录下util下的time_support.h，在文件开头加入`#include<stdint.h>`，否则在编译这个文件时会无法识别int64_t类型

### 修改windows_basic.h

 - 修改mongodb源码目录下platform下的windows_basic.h，
 - 在` #if !defined(NTDDI_WINXPSP3) || (NTDDI_VERSION < NTDDI_WINXPSP3)` 之前加入 `#define NTDDI_WINXPSP3 0x05010300`  在`#if !defined(NTDDI_WS03SP2) || (NTDDI_VERSION < NTDDI_WS03SP2)`之前加入`#define NTDDI_WS03SP2 0x05020200`  否则会报 "32 bit mongo does not support Windows versions older than XP Service Pack 3" 和"64 bit mongo does not support Windows versions older than Windows Server 2003 SP 2" 错误

### 修改listen.cpp和sock.cpp

 - 修改util下net下listen.cpp，在#include段之后加入如下代码

        #ifdef _WIN32
        #define EADDRINUSE WSAEADDRINUSE
        #define ECONNABORTED WSAECONNABORTED
        #define EBADF           9
        #define ENFILE          23
        #define EMFILE          24
        #endif

 - 修改util下net下sock.cpp，在#include段之后加入如下代码
 
        #ifdef _WIN32
        #define EAGAIN          11
        #endif

## 开始编译

环境准备好之后，编译就比较简单了，打开vs2008命令行窗口，执行如下代码即可完成编译
    `scons --dd --32 mongoclient.lib`

如果是编译release版本，就把--dd换成--release，如果是编译64位版本，就把--32换成--64


