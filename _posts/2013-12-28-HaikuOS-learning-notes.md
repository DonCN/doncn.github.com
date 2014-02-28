---
layout: post
title: HaikuOS学习笔记(简介、编程基础...进行中)
summary: Haiku OS是一个开源、免费的操作系统，主要面向个人计算机。它兼容、继承了BeOS的理念，是一个快速、简洁优雅、易学易用，而且非常强大的操作系统。它有着<ul><li>- 统一的、简洁优雅的全图形用户界面；</li><li>- 定制的快速响应的内核；</li><li>- 对多处理器、多线程的完全支持和内存保护；</li><li>- 优雅的内置程序间通讯；</li><li>- 模块化设计和面向对象API便于快速开发；</li><li>- 先进的数据库式、全日志的64位文件系统；</li><li>- 基于属性的快速索引和查询。</li></ul>它的众多特性和优点让我非常着迷，这篇文章是我的HaikuOS学习笔记和一些相关资源链接。<p><center><a href="/images/HaikuOS-desktop.png" target="_blank"><img src="/images/HaikuOS-desktop.png" alt="HaikuOS-desktop" height="500" width="633"></a><p>Haiku OS 桌面</center><p>
categories: [Haiku OS]
tags: [Haiku OS] 
      [Haiku OS learning notes]  
published: true
---

# {{ page.title }} #

{{page.summary}}

—— _内容主要来自[Programming the Be Operating System](http://www.haiku-os.org/legacy-docs/programming_the_be_operating_system.pdf) ，根据HaikuOS及其他资料做了适当修改。_ 

## 历史 ##
1990年，前苹果公司主管Jean-Louse Gassee创办了Be公司，历经4年艰苦，开发了全新的BeOS操作系统([BeOS Wiki](http://en.wikipedia.org/wiki/BeOS)，[中文维基](http://zh.wikipedia.org/wiki/BeOS)，[百科](http://baike.baidu.com/link?url=RlMCN12Pq2RYX_9z1C_GsXaWVP7kK3e2SZF_PDZ6ptjrlRBS28YSQ-jUXIuAc4yx))，从设计之初就针对多处理器和多线程的应用程序，多媒体性能异常优越，许多技术和理念遥遥领先于同期的操作系统。但是，技术的先进并不能弥补市场开发的拙略，在错过苹果公司的收购之后，2001年Be公司被Palm公司收购，BeOS这个领先于时代，却又命运多舛的多媒体操作系统也走到了尽头。

同年，一群忠实爱好者开始了OpenBeOS开源项目，目标是创立一个与BeOS兼容的自由操作系统。2003年，在纽约州成立了一个非营利的组织[Haiku,Inc](http://www.haiku-inc.org/) 以支持该项目。2004年，由于版权原因，项目名称改为Haiku(一种日本古典短诗-俳句的发音)。2009年9月，经过世界各地的十几个核心开发人员8年的努力，项目组终于发布了第一个测试版Haiku R1/Alpha1。目前，已经发布了4个Alpha版本，即将进入Beta发布阶段。

HaikuOS官方主页：<http://www.haiku-os.org/><p>
HaikuOS中文社区：<http://haiku-cn.org/><p>
HaikuOS测试版本下载：<http://haiku-files.org/haiku/development/><p>
HaikuOS源码编译指南：<http://www.haiku-os.org/guides/building><p>


## 设计理念和特点 ##
HaikuOS的设计理念继承于BeOS，专门用于多媒体处理的完全图形化的“多媒体操作系统”。设计目标是尽可能的减少内核延迟，从而实时处理大量多媒体数据，如音频和视频流。它充分利用了现代硬件和技术的优点，如使用模块化I/O带宽的多处理器系统，深入的多线程，抢断式的多任务和被称为BFS的定制64位日志文件系统。

Haiku的内核基于开源内核[NewOS](http://www.newos.org)，由曾经的Be雇员、参与文件系统和内核编写的[Travis Geiselbrecht](http://tkgeisel.com/)创建。同样继承了BeOS多处理器、多线程、内存保护等特点。

Haiku的GUI遵循清晰整洁的设计原则开发。其API是用C++编写而成，非常容易编程。虽非源于Unix的操作系统，但其实现了POSIX兼容，并通过Bash shell 命令行界面来访问。

__参考__：  
[1] [BeOS Wiki](http://en.wikipedia.org/wiki/Beos)  
[2] [The Art of Unix Programming](http://www.catb.org/esr/writings/taoup/html/ch03s02.html#beos)  

## 特性详情 ##

* __数据库式64位文件系统 Databese-like 64bit File System__<p>
    HaikuOS（以及BeOS）采用的是Unix模型，在字节级以上没有文件结构，支持和使用文件属性，整个文件系统就像一个数据库，可以按任意属性索引。

* __多线程 Multithreaded__<p>
    HaikuOS（以及BeOS）是多线程化的操作系统。每创建一个窗口，系统都会自动为这个窗口创建一个新的线程。所有的线程都由系统处理、维护。

    HaikuOS（BeOS）的“线程”实际上是Unix术语中的轻量级进程。线程间通信通过共享内存实现，快速而高效

* __多处理器支持 Multiprocessor Support__<p>
    HaikuOS采用对称多重处理（symmetric multiprocessing, or SMP）方式支持多处理器，自动根据各处理器的负荷情况为其分配不同的线程，提高系统性能。

* __抢占式多任务处理 Preemptive Multitasking__<p>
    HaikuOS将根据任务优先级来分配任务。

* __内存保护 Protected Memory__<p>
    系统为每个程序分配单独的内存，并不受其他程序崩溃的影响。

* __虚拟内存 Virtual Memory__<p>
    系统提供了虚拟内存，保证多个程序并行运行的内存要求。

* __没有历史兼容负担 Less Hindered by Backward Compatibility__<p>
   HaikuOS（以及BeOS）作为全新设计的个人电脑操作系统，充分利用了现代硬件和现代计算机技术，没有旧系统和程序兼容的负担。

__参考__：  
[1] [Programming the Be Operating System](http://www.haiku-os.org/legacy-docs/programming_the_be_operating_system.pdf)  
[2] [The Art of Unix Programming](http://www.catb.org/esr/writings/taoup/html/ch03s02.html#beos)  

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

    * __应用开发包 Application kit__   
        应用开发包（Application Kit）是开发应用程序的开始，每个应用程序都是基于一个继承自该包中的BApplication的类开发的。定义了消息系统、程序间通信等。

    * __接口开发包 Interface kit__   
        这是目前最大的一个软件开发包。提供了基于应用开发包的消息系统之上的图形用户接口，定义了窗口及其包含的各种元素。

        此外haiku在接口开发包之外又增加了布局接口Layout API，使程序布局更灵活和简单。

    * __存储开发包 Storage Kit__   
        存储开发包Storage Ki包含了在磁盘保存和更新数据的一些类。

    * __支持开发包 Support Kit__  
        支持开发包Support Kit包含程序中使用的一些支持类，包括线程安全、IO、和序列化（serialization）用到的资源，如数据类型、常数等的定义。 

    * __媒体开发包 Media Kit__  
        媒体开发包 Media Kit为媒体数据流和程序间通信提供了统一的接口。

    * __音频设备数字接口开发包 Midi Kit__      
        音频设备数字接口开发包MIDI(Musical Instrument Digital Interface) Kit 提供了处理MIDI格式音频数据的接口。Haiku在此基础上新加了MIDI2 Kit，扩展了部分功能。
 
    * __设备开发包 Device Kit__    
        设备开发包Device Kit提供了硬件连接的接口，主要用于驱动开发。

    * __网络开发包 Network Kit__   
        网络开发包Network Kit处理网络相关的各种事物，从IP地址设置接口到HTTP连接。

    * __转换开发包 Translation Kit__   
        转换开发包Translation Kit不是传统意义上的语言翻译转换，而是媒体格式的转换，如jpg图片转换为png图片等。

    * __邮件开发包 Mail Kit__     
        邮件开发包Mail Kit提供了电子邮件的相关服务。

    * __游戏开发包 Game Kit__  
        游戏开发包Game Kit提供了处理游戏声音等全屏程序的一些类。

    * __本地化开发包 Locale Kit__   
        本地化开发包Locale Kit包含了本地化程序到各种语言、时区、数字格式等的类。

    *Kernel Kit（在底层直接操作内核）和OpenGL Kit（为程序增加3D效果，以及处理三维对象） *


###扩展阅读：
[1] [Tales of a BeOS Refugee](http://www.birdhouse.org/beos/refugee/)   [译文: 一个BeOS难民的故事(by Don)](http://doncn.github.io/2013/12/28/Tales-of-BeOS-Refugee.html)  
[2] [Programming the Be Operating System](http://www.haiku-os.org/legacy-docs/programming_the_be_operating_system.pdf)  
[3] [The Art of Unix Programming](http://www.catb.org/esr/writings/taoup/html/ch03s02.html#beos)   
