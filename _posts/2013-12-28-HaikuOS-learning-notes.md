---
layout: post
title: HaikuOS学习笔记(进行中...)
summary: Haiku OS是一个开源、免费的操作系统，主要面向个人计算机。它兼容、继承了BeOS的理念，是一个快速、简洁优雅、易学易用，而且非常强大的操作系统。它有着<ul><li>- 统一的、简洁优雅的全图形用户界面；</li><li>- 定制的快速响应的内核；</li><li>- 对多处理器、多线程的完全支持和内存保护；</li><li>- 优雅的内置程序间通讯；</li><li>- 模块化设计和面向对象API便于快速开发；</li><li>- 先进的数据库式、全日志的64位文件系统；</li><li>- 基于属性的快速索引和查询。</li></ul>它的众多特性和优点让我非常着迷，这篇文章是我的HaikuOS学习笔记和一些相关资源链接。<p><center><a href="/images/HaikuOS-desktop.png" target="_blank"><img src="/images/HaikuOS-desktop.png" alt="HaikuOS-desktop" height="500" width="633"></a><p>Haiku OS 桌面</center><p>
categories: [Haiku OS]
tags: [Haiku OS]
published: true
---

# {{ page.title }} #

{{page.summary}}

## 历史 ##
2001年，前Apple公司主管Jean-Louse Gassee创办的Be公司被Palm公司收购，BeOS([BeOS Wiki](http://en.wikipedia.org/wiki/BeOS)，[中文维基](http://zh.wikipedia.org/wiki/BeOS)，[百科](http://baike.baidu.com/link?url=RlMCN12Pq2RYX_9z1C_GsXaWVP7kK3e2SZF_PDZ6ptjrlRBS28YSQ-jUXIuAc4yx))这个领先于时代，却又命运多舛的多媒体操作系统也走到了尽头。一群忠实爱好者开始了OpenBeOS开源项目，目标是创立一个与BeOS兼容的自由操作系统。2003年，在纽约州成立了一个非营利的组织 [Haiku,Inc](http://www.haiku-inc.org/) 以支持该项目。2004年，由于版权原因，项目名称改为Haiku(一种日本古典短诗-俳句的发音)。2009年9月，经过世界各地的十几个核心开发人员8年的努力，项目组终于发布了第一个测试版Haiku R1/Alpha1。目前，已经发布了4个Alpha版本，即将进入Beta发布阶段。

HaikuOS官方主页：<http://www.haiku-os.org/><p>
HaikuOS中文社区：<http://haiku-cn.org/><p>
HaikuOS测试版本下载：<http://haiku-files.org/haiku/development/><p>
HaikuOS源码编译指南：<http://www.haiku-os.org/guides/building><p>


## 设计理念 ##
HaikuOS的设计理念继承于BeOS，采用先进的64位BeFS文件系统，支持多处理器，其多媒体性能异常优越。Haiku能够充分利用多处理器系统通过模块化的I/O带宽，多线程，抢断式的多任务和被称为BFS的定制64位日志文件系统。Haiku的GUI遵循清晰整洁的设计原理而开发。其API是用C++编写而成，非常容易编程。虽非源于Unix的操作系统，但其实现了POSIX兼容，并通过Bash shell 命令行界面来访问。

## 特性详情 ##

1. __多线程 Multithreaded__<p>
    HaikuOS（以及BeOS）是多线程化的操作系统。每创建一个窗口，系统都会自动为这个窗口创建一个新的线程。所有的线程都由系统处理、维护。

2. __多处理器支持 Multiprocessor Support__<p>
    HaikuOS采用对称多重处理（symmetric multiprocessing, or SMP）方式支持多处理器，自动根据各处理器的负荷情况为其分配不同的线程，提高系统性能。

3. __抢占式多任务处理 Preemptive Multitasking__<p>
    HaikuOS将根据任务优先级来分配任务。

4. __内存保护 Protected Memory__<p>
    系统为每个程序分配单独的内存，并不受其他程序崩溃的影响。

5. __虚拟内存 Virtual Memory__<p>
    系统提供了虚拟内存，保证多个程序并行运行的内存要求。

6. __没有历史兼容负担 Less Hindered by Backward Compatibility__<p>
   HaikuOS（以及BeOS）作为全新设计的个人电脑操作系统，充分利用了现代硬件和现代计算机技术，没有旧系统和程序兼容的负担。


## 系统架构 ##

<div align="center">
<img src="/images/BeOS_Structure.png" alt="BeOS_Structure.png" height="212" width="633"><p>
应用程序和硬件之间的系统层次结构
</div>
1. __微内核层microkernel__<p>
    操作系统的最底层是微内核，它直接工作在硬件及其驱动之上，处理计算机的底层任务，如内存访问管理。内核还提供其他程序使用的一些基础功能，如线程调度、文件系统工具等。

2. __服务层server__<p>
    微内核之上是服务层。服务server层包含多个服务servers，在后台处理程序请求的系统功能，如输入服务Input Server处理键盘、鼠标等输入设备操作；应用服务Application Server处理图形显示、应用程序通信。作为程序员，不能直接操作服务层，需要通过下面的软件开发包提供的接口操作服务层。

3. __软件开发包层software kits__<p>
    软件开发包包含各种编程需要的面向对象的类库（用C++编写），这些类库构成了操作系统的应用程序接口API（haikuOS兼容BeOS的API）。一般应用程序通过调用软件开发包software kits里的类与对应的服务server通信来完成指定的任务；也有些软件开发包software kits直接与服务层通信，而不需要经过开发包。

    HaikuOS(BeOS)包含十几个软件开发包，一般的编程只需熟悉几个常用的开发包，比如显示一个窗口只用到应用开发包Application Kit 和 接口开发包Interface Kit。

    全部开发包的功能简介：
    *Application Kit
        The Application Kit is the starting point for developing applications and includes classes for messaging and for interacting with the rest of the system.

    *Interface Kit
        The Interface Kit is used to create responsive and attractive graphical user interfaces building on the messaging facilities provided by the Application Kit.

        The Layout API is a new addition to the Interface Kit in Haiku which provides resources to layout your application flexibly and easily.

    *Storage Kit
        The Storage Kit is a collection of classes that deal with storing and retrieving information from disk.

    *Support Kit
        The Support Kit contains support classes to use in your application including resources for thread safety, IO, and serialization.

    *Media Kit
        The Media Kit provides a unified and consistent interface for media streams and applications to intercommunicate.

    *Midi Kit
        The MIDI 2 Kit describes an interface to generating, processing, and playing music in MIDI format. For reference documentation on the The old Midi Kit (libmidi.so) is also included.
    
    *Device Kit


    *Network Kit
        The Network Kit handles everything network related, from interface IP address settings to HTTP connections.

    *Translation Kit
        The Translation Kit provides a framework for converting data streams between media formats.

    *Mail Kit


    *Game Kit
        The Game Kit provides classes for producing game sounds and working with full screen apps.
    *Locale Kit 
        The Locale Kit includes classes to localize your application to different languages, timezones, number formatting conventions and much more.

    *Kernel Kit和OpenGL Kit *

参考：[Programming the Be Operating System](http://www.haiku-os.org/legacy-docs/programming_the_be_operating_system.pdf)

