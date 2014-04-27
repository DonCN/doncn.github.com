---
layout: post   
title: Don's HaikuOS Notes（1）：简介   
summary: Haiku OS是一个开源、免费的操作系统，主要面向个人计算机。它兼容、继承了BeOS的理念，是一个快速、简洁优雅、易学易用，而且非常强大的操作系统。它有着：<ul><li>- 统一的、简洁、优雅的全图形用户界面；</li><li>- 快速响应的内核；</li><li>- 对多处理器、多线程的完全支持和内存保护；</li><li>- 优雅的内置程序间通讯；</li><li>- 模块化设计和面向对象API便于快速开发；</li><li>- 先进的数据库式、全日志的64位文件系统；</li><li>- 基于属性的快速索引和查询；</li><li>- 拼贴和标签式堆叠的窗口管理。</li></ul>Haiku的众多特性和优点让我非常着迷，这篇文章是我的HaikuOS学习笔记，以及一些相关材料的整理。——Don Liu， Email：donliucn@gmail.com<p><center><a href="/images/HaikuOS-desktop.png" target="_blank"><img src="/images/HaikuOS-desktop.png" alt="HaikuOS-desktop" height="500" width="633"></a><p>Haiku OS 桌面</center><p>    
categories: [Haiku OS]  
tags: [Haiku OS, HaikuOS notes]   
published: true  
---

# {{ page.title }} #

{{page.summary}}


## 历史 ##

1990年，前苹果公司主管Jean-Louse Gassee创办了Be公司，历经4年艰苦，开发出了全新的BeOS操作系统([BeOS Wiki](http://en.wikipedia.org/wiki/BeOS)，[中文维基](http://zh.wikipedia.org/wiki/BeOS)，[百科](http://baike.baidu.com/link?url=RlMCN12Pq2RYX_9z1C_GsXaWVP7kK3e2SZF_PDZ6ptjrlRBS28YSQ-jUXIuAc4yx))。从设计之初，BeOS就针对多处理器、多线程和多媒体处理进行优化，性能异常优越，许多技术和理念遥遥领先于同期的操作系统。1996年，苹果公司放弃了自己开发新的操作系统，认为BeOS符合他对操作系统的要求，开价2亿美元收购Be公司，但遭到拒绝。转而以4.29亿美元的代价迎回了被踢出局的苹果创始人乔布斯和他的NeXTSTEP操作系统，乔布斯再次成了苹果掌门人，NeXTSTEP成了新的Mac OS X系统的基础。而Be公司，技术的先进并不能弥补市场开发的拙略，战略几经转变，均未获市场成功，在2001年，被Palm公司收购。BeOS这个领先于时代，却又命运多舛的多媒体操作系统也走到了尽头。

同年，一群忠实爱好者开始了OpenBeOS开源项目，目标是重建一个类似BeOS并与之兼容的自由操作系统。2003年，他们在美国纽约州成立了非营利的组织[Haiku,Inc](http://www.haiku-inc.org/) 以支持该项目。2004年，由于版权原因，项目名称改为Haiku(一种日本古典短诗-俳句的发音)。2009年9月，经过世界各地的十几个核心开发人员8年的努力，项目组终于发布了第一个测试版Haiku R1/Alpha1。目前，Haiku已经发布了4个Alpha版本，即将进入Beta发布阶段。

HaikuOS官方主页：<http://www.haiku-os.org/><p>
HaikuOS测试版本下载：<http://haiku-files.org/haiku/development/><p>

## 设计理念和特点 ##

HaikuOS的设计理念继承于BeOS，专注于个人PC完全图形化的“多媒体操作系统”。设计目标是尽可能的减少内核延迟，从而实时处理大量多媒体数据，如音频和视频数据流。由于没有旧系统兼容的历史负担，它充分利用了现代硬件和技术的优点，如使用模块化I/O带宽的多处理器系统，深入的多线程，抢断式的多任务和被称为BFS的数据库式、全日志的64位文件系统等。因而，Haiku/Beos的性能异常优异，可以流畅地同时播放多个视频、音频；日志系统保证意外情况下的断点恢复，不会丢失数据；而数据库式文件系统又能快速、方便的存储、管理、查询多媒体文件的属性...

Haiku的内核基于开源内核[NewOS](http://www.newos.org)，由曾经的Be员工、参与文件系统和内核编写的[Travis Geiselbrecht](http://tkgeisel.com/)创建。同样继承了BeOS模块化、多处理器、多线程、内存保护等特点。

Haiku的GUI遵循清晰整洁的设计原则开发，简洁、优雅、人性化，容易上手。其API兼容于BeOS R5，由C++编写而成，非常容易编程。虽非源于Unix的操作系统，但实现了POSIX兼容，并实现了Bash shell命令行。

相比BeOS，Haiku在多方面进行了改进：内核中增加网络模块、文件缓存集成到虚拟内存中、矢量图标使得系统界面更现代、现代硬件支持：如USB、WiFi和显卡等。此外，软件包管理、CPU调度管理、基于Webkit的网络浏览器等更多新特性和改进也基本完成，正在最后测试调整，将在Beta版中呈现给众爱好者。

__参考__：  
[1] [BeOS Wiki](http://en.wikipedia.org/wiki/Beos)  
[2] [The Art of Unix Programming](http://www.catb.org/esr/writings/taoup/html/ch03s02.html#beos)  

## 特性详情 ##

* __统一的、简洁、优雅的全图形用户界面 / unified，simple，decent graphic UI__<p>
    HaikuOS的图形化得到了内核级的深入支持，设计简洁、优雅、人性化，操作非常简单，几乎没有上手难度。

* __数据库式64位文件系统 / Databese-like 64bit File System__<p>
    HaikuOS（以及BeOS）采用的是Unix模型，在字节级以上没有文件结构，支持文件属性，整个文件系统就像一个数据库，可以按任意属性索引。比如歌曲的歌手、专辑、码率、播放时间、评级等（如本文Haiku桌面图中的music文件夹，显示了音乐文件的众多属性），再如邮件的联系人、标题、地址等，在整个操作系统就可以查询，无需第三方软件。

* __深入的多线程 / indepth Multithreaded__<p>
    HaikuOS（以及BeOS）是多线程化的操作系统。每创建一个窗口，系统都会自动为这个窗口创建一个新的线程。所有的线程都由系统处理、维护。

    HaikuOS（BeOS）的“线程”实际上是Unix术语中的轻量级进程。线程间通信通过共享内存实现，快速而高效

* __多处理器支持 / Multiprocessor Support__<p>
    HaikuOS采用对称多重处理（symmetric multiprocessing, or SMP）方式支持多处理器，自动根据各处理器的负荷情况为其分配不同的线程，提高系统性能。

* __抢占式多任务处理 / Preemptive Multitasking__<p>
    HaikuOS将根据任务优先级来分配任务。

* __内存保护和虚拟内存 / Protected Memory and Virtual Memory__<p>
    系统为每个程序分配单独的内存，使其不受其他程序崩溃的影响。还提供了虚拟内存，保证多个程序并行运行的内存要求。

* __拼贴和标签式堆叠的窗口管理 / Stack & Tile window__<p>
    Haiku的窗口排列很有特点，可以将两个或多个窗口拼在一起或像标签一样堆叠起来作为一个整体移动，非常便于窗口的排列和管理。


__参考__：  
[1] [Programming the Be Operating System](http://www.haiku-os.org/legacy-docs/programming_the_be_operating_system.pdf)  
[2] [The Art of Unix Programming](http://www.catb.org/esr/writings/taoup/html/ch03s02.html#beos)  

## 系统架构 ##

Haiku操作系统架构分为以下三个层级：
<p><div align="center">
<img src="/images/BeOS_Structure.png" alt="BeOS_Structure.png"><p>
应用程序和硬件之间的系统层次结构
</div>

1. __微内核层 / microkernel__<p>
    操作系统的最底层是微内核，它直接工作在硬件及其驱动之上，处理计算机的底层任务，如内存访问管理。内核还提供其他程序使用的一些基础功能，如线程调度、文件系统工具等。   

2. __服务层 / server__<p>
    微内核之上是服务层。服务（server）层包含多个服务（servers），在后台处理程序请求的系统功能，如输入服务（Input Server）处理键盘、鼠标等输入设备操作；应用服务（Application Server）处理图形显示、应用程序通信。作为程序员，不能直接操作服务层，需要通过上层的软件开发包提供的接口操作服务层。   

3. __软件开发包层 / software kits__<p>
    软件开发包包含各种编程需要的面向对象的类库（用C++编写），比如应用程序开发包、界面开发包、媒体开发包等，这些类库构成了操作系统的应用程序接口API（haikuOS兼容BeOS的API）。一般应用程序通过调用软件开发包里的类，来和对应的服务（server）通信来完成指定的任务；也有些软件开发包直接与服务层通信，而不需要经过开发包。   

    HaikuOS(BeOS)包含十几个软件开发包，一般的编程只需熟悉几个常用的开发包，比如显示一个窗口只用到应用开发包（Application Kit）和界面开发包（Interface Kit），所有开发包介绍见下节：**软件开发包 / software kits**。


## 软件开发包 / software kits##

上节系统架构的三层中的软件开发包层包含了十几个软件开发包，简介如下：

* __应用开发包 / Application kit__<p>
    应用开发包（Application Kit）是开发应用程序的开始，每个应用程序都是基于一个继承自该包中的BApplication的类开发的。定义了消息系统、程序间通信等。

* __界面开发包 / Interface kit__<p>
    这是目前最大的一个软件开发包。提供了基于应用开发包的消息系统之上的图形用户界面，定义了窗口及其包含的各种元素。

    此外haiku在界面开发包之外又增加了布局接口Layout API，使程序布局更灵活和简单。

* __存储开发包 / Storage Kit__<p>
    存储开发包Storage Ki包含了在磁盘保存和更新数据的一些类。

* __支持开发包 / Support Kit__<p>
    支持开发包Support Kit包含程序中使用的一些支持类，包括线程安全、IO、和序列化（serialization）用到的资源，如数据类型、常数等的定义。 

* __媒体开发包 / Media Kit__<p>
    媒体开发包 Media Kit为媒体数据流和程序间通信提供了统一的接口。

* __音频设备数字接口开发包 / Midi Kit__<p>
    音频设备数字接口开发包MIDI(Musical Instrument Digital Interface) Kit 提供了处理MIDI格式音频数据的接口。Haiku在此基础上新加了MIDI2 Kit，扩展了部分功能。
 
* __设备开发包 / Device Kit__<p>
    设备开发包Device Kit提供了硬件连接的接口，主要用于驱动开发。

* __网络开发包 / Network Kit__<p>
    网络开发包Network Kit处理网络相关的各种事物，从IP地址设置接口到HTTP连接。

* __转换开发包 / Translation Kit__<p>
    转换开发包Translation Kit不是传统意义上的语言翻译转换，而是媒体格式的转换，如jpg图片转换为png图片等。

* __邮件开发包 / Mail Kit__<p>
    邮件开发包Mail Kit提供了电子邮件的相关服务。

* __游戏开发包 / Game Kit__<p>
    游戏开发包Game Kit提供了处理游戏声音等全屏程序的一些类。

* __本地化开发包 / Locale Kit__<p>
    本地化开发包Locale Kit包含了本地化程序到各种语言、时区、数字格式等的类。

*Kernel Kit（在底层直接操作内核）和OpenGL Kit（为程序增加3D效果，以及处理三维对象）这两个BeOS中的开发包在Haiku的源码库中找不到，等弄清楚了Haiku的修改后再补充。*


上述的各种软件开发包不是独立的，它们之间有类的继承关系。比如一个开发包的类可能派生自几个其他的开发包。将这些所有的类根据功能和概念分成多个开发包便于整理和应用。至于更细节的开发包之间如何继承，如何编程使用，请见下篇《Don's HaikuOS Notes（2）：编程基础》


-----------------------------
###扩展阅读：###
[1] [Tales of a BeOS Refugee](http://www.birdhouse.org/beos/refugee/)   [译文: 一个BeOS难民的故事(by Don)](http://doncn.github.io/2013/12/28/Tales-of-BeOS-Refugee.html)  
[2] [Programming the Be Operating System](http://www.haiku-os.org/legacy-docs/programming_the_be_operating_system.pdf)  
[3] [The Art of Unix Programming](http://www.catb.org/esr/writings/taoup/html/ch03s02.html#beos)   
