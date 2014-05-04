---  
layout: post      
title: Don's HaikuOS Notes: (1) 简介 v1.01       
summary: Haiku OS是一个开源、免费的操作系统，主要面向个人计算机，它快速、简洁、易学易用，功能又非常强大。它有：<ul><li>- 拼贴和标签式的窗口；</li><li>- 快速响应的内核；</li><li>- 针对多核处理器设计；</li><li>- 深入的多线程化；</li><li>- 先进的全日志、数据库式64位文件系统；</li><li>- 基于属性的快速索引和查询；</li></ul>有人说，Haiku给人一种别样的美好感觉，它将让你重新认识个人计算机。的确，自从认识了Haiku，我就被她的别样风情和众多特性迷住了。这篇文章是我的HaikuOS学习笔记，以及一些相关材料的整理。希望能让大家认识、感受到一个别样美好的操作系统。<p> <center><a href="/images/HaikuOS-desktop.png" target="_blank"><img src="/images/HaikuOS-desktop.png" alt="HaikuOS-desktop" height="500" width="633"></a><p>Haiku OS 桌面</center><p>   
categories: [Haiku OS, HaikuOS notes]     
tags: [Haiku OS, HaikuOS notes]     
published: true    
---  

# {{ page.title }} #

{{page.summary}}


## I 历史 ##

1990年，前苹果公司主管Jean-Louse Gassee创办了Be公司，历经4年艰苦，开发出了全新的BeOS操作系统([BeOS Wiki](http://en.wikipedia.org/wiki/BeOS)，[中文维基](http://zh.wikipedia.org/wiki/BeOS)，[百科](http://baike.baidu.com/link?url=RlMCN12Pq2RYX_9z1C_GsXaWVP7kK3e2SZF_PDZ6ptjrlRBS28YSQ-jUXIuAc4yx))。从设计之初，BeOS就针对多处理器、多线程和多媒体处理进行优化，性能异常优越，许多技术和理念遥遥领先于同期的操作系统。1996年，苹果公司放弃了自己开发新的操作系统，认为BeOS符合他对操作系统的要求，开价2亿美元收购Be公司，但遭到拒绝。转而以4.29亿美元的代价迎回了被踢出局的苹果创始人乔布斯和他的NeXTSTEP操作系统，乔布斯再次成了苹果掌门人，NeXTSTEP成了新的Mac OS X系统的基础。而Be公司，技术的先进并不能弥补市场开发的拙略，战略几经转变，均未获市场成功，在2001年，被Palm公司收购。BeOS这个领先于时代，却又命运多舛的多媒体操作系统也走到了尽头。

同年，一群忠实爱好者开始了OpenBeOS开源项目，目标是重建一个类似BeOS并与之兼容的自由操作系统。2003年，他们在美国纽约州成立了非营利的组织[Haiku,Inc](http://www.haiku-inc.org/) 以支持该项目。2004年，由于版权原因，项目名称改为Haiku(一种日本古典短诗-俳句的发音)。2009年9月，经过世界各地的十几个核心开发人员8年的努力，项目组终于发布了第一个测试版Haiku R1/Alpha1。目前，Haiku已经发布了4个Alpha版本，即将进入Beta发布阶段。

HaikuOS官方主页：<http://www.haiku-os.org/><p>
HaikuOS测试版本下载：<http://haiku-files.org/haiku/development/><p>

## II 设计理念和特点 ##

HaikuOS的设计理念继承于BeOS，专注于个人PC完全图形化的“多媒体操作系统”。设计目标是尽可能的减少内核延迟，从而实时处理大量多媒体数据，如音频和视频数据流。由于没有旧系统兼容的历史负担，它充分利用了现代硬件和技术的优点，如使用模块化I/O带宽的多处理器系统，深入的多线程，抢断式的多任务和被称为BFS的数据库式、全日志的64位文件系统等。因而，Haiku/Beos的性能异常优异，可以流畅地同时播放多个视频、音频；日志系统保证意外情况下的断点恢复，不会丢失数据；而数据库式文件系统又能快速、方便的存储、管理、查询多媒体文件的属性...

Haiku的内核基于开源内核[NewOS](http://www.newos.org)，由曾经的Be员工、参与文件系统和内核编写的[Travis Geiselbrecht](http://tkgeisel.com/)创建。同样继承了BeOS模块化、多处理器、多线程、内存保护等特点。

Haiku的GUI遵循清晰整洁的设计原则开发，简洁、优雅、人性化，容易上手。其API兼容于BeOS R5，由C++编写而成，非常容易编程。虽非源于Unix的操作系统，但实现了POSIX兼容，并实现了Bash shell命令行。

相比BeOS，Haiku在多方面进行了改进：内核中增加网络模块、文件缓存集成到虚拟内存中、矢量图标使得系统界面更现代、现代硬件支持：如USB、WiFi和显卡等。此外，软件包管理、CPU调度管理、基于Webkit的网络浏览器等更多新特性和改进也基本完成，正在最后测试调整，将在Beta版中呈现给众爱好者。

__参考__： [1] [2]

## III 诸多特性简介 ##

1. __统一、简洁、优雅的全图形用户界面 / unified，simple，decent graphic UI__<p>
    HaikuOS的图形化得到了内核级的深入支持，设计简洁、优雅、人性化，操作非常简单，几乎没有上手难度。

    Haiku的拼贴和标签式（Stack & Tile）窗口排列很有特点，可以将两个或多个窗口并排或竖排拼接或像标签一样堆叠起来作为一个整体，非常便于窗口的排列和管理。

	Haiku还提供一些钟表、计算器、音量控制等一些常用部件的桌面附件，称为Replicants，直接将Replicants面板拖到桌面，就可以嵌入桌面，与桌面壁纸融于一体，非常方便。

	扩展：[Haiku的图形用户界面、标签式窗口、桌面附件等的图示](http://www.haiku-os.org/docs/userguide/zh_CN/contents.html)

2. __数据库式64位文件系统 / Databese-like 64bit File System__<p>
    HaikuOS/BeOS的文件系统采用的是Unix模型，在字节级以上没有文件结构，支持文件属性，每个文件的每个属性都可以被索引和查询，整个文件系统就像一个数据库。Haiku/BeOS是我所知的唯一实现这种方法的操作系统，它对整个系统产生了根本的影响。想象一下：系统存储的音乐文件同时包含多个属性，如演唱者、专辑、码率、播放时间、评级等等（如上图Haiku桌面中的music文件夹），还有每封邮件同时包含发件人、收件人、标题、附件等属性，它们都按照统一格式存储，通过操作系统的搜索就可以快速查询、排序，无需第三方软件。这是一件多么美妙的事。

	此外，HaikuOS/BeOS的文件系统为全日志式，能保证意外情况下的断点恢复，不用担心丢失数据

	扩展：  
	[Haiku的文件系统布局](http://www.haiku-os.org/docs/userguide/zh_CN/filesystem-layout.html)   
	[Tracker文件浏览器](http://www.haiku-os.org/docs/userguide/zh_CN/tracker.html)   
	[文件类型](http://www.haiku-os.org/docs/userguide/zh_CN/filetypes.html)   
	[文件属性](http://www.haiku-os.org/docs/userguide/zh_CN/attributes.html)   
	[文件属性的索引](http://www.haiku-os.org/docs/userguide/zh_CN/index.html)   
	[文件属性的查询](http://www.haiku-os.org/docs/userguide/zh_CN/queries.html)    


3. __高度的多线程 / Highly Multithreaded__<p>
    HaikuOS（以及BeOS）是多线程化的操作系统。通过API，系统为每个程序和它的每个图形界面都分别创建一个新的线程[4]。每个线程都需要指定优先级，比如显示优先、多媒体优先、实时优先等[5]，而不像Linux那样所有线程都默认为相同的优先级。Haiku独特的消息共享传递机制，即保证了多个线程同步操作而不会死锁，又方便了编程工作[4]。这些也是为什么Haiku响应很快，可以同时播放几个多媒体文件，而不卡顿和失真。

    HaikuOS（BeOS）的“线程”实际上是Unix术语中的轻量级进程。线程间通信通过共享内存实现，快速而高效

4. __多处理器支持 / Multiprocessor Support__<p>
    HaikuOS采用对称多重处理（symmetric multiprocessing, or SMP）方式支持多处理器，自动根据各处理器的负荷情况为其分配不同的线程。高度的线程化使得Haiku能充分利用多处理器硬件优势，提高系统性能。

5. __抢占式多任务处理 / Preemptive Multitasking__<p>
    HaikuOS将根据任务优先级来分配任务。

6. __内存保护和虚拟内存 / Protected Memory and Virtual Memory__<p>
    系统为每个程序分配单独的内存，使其不受其他程序崩溃的影响。还提供了虚拟内存，保证多个程序并行运行的内存要求。


__参考__：  [2] [3]


## IV 系统架构 ##

Haiku操作系统架构分为三个层级：微内核层（microkernel）、服务层（server）、软件开发包层（software kits）。三层之间为服务-客户端关系：软件是服务的客户端，服务又是内核的客户端[6]。  
<p><div align="center">
<img src="/images/BeOS_Structure.png" alt="BeOS_Structure.png"><p>
应用程序和硬件之间的系统层次结构
</div>

1. __内核层 / kernel__<p>
    操作系统的最底层是内核，它直接工作在硬件之上，处理计算机的底层任务，如内存访问管理。内核还提供其他程序使用的一些基础功能，如线程调度、文件系统工具等。上图是借用《Programming the Be Operating System》的一张图。实际上，据Haiku的开发人员Adrien Destugues（pulkomandy）所说[5]，Haiku的内核是混合内核(hybrid kernel)，并且是偏单一内核的混合内核。首先，Haiku的硬件驱动运行于内核层，动态链接，图形驱动则分为两部分，分别位于内核和服务层。除去驱动的内核基本为模块化的单一内核。

2. __服务层 / server__<p>
    内核之上是服务层。服务（server）层包含多个服务（servers），在后台处理程序请求的系统功能，如输入服务（Input Server）处理键盘、鼠标等输入设备操作；应用程序服务（Application Server）处理图形显示、应用程序通信。各个服务都是独立的、可重启的[6]，因而某个服务崩溃不会影响到其他服务。

	作为程序员，不能直接操作服务层，需要通过上层的软件开发包提供的接口操作服务层。   

3. __软件开发包层 / software kits__<p>
    软件开发包层是应用程序调用服务和内核的接口。各种开发包用C++编写，包含各种编程需要的面向对象的类库，以动态链接库形式（DLL）存在和使用。主要有应用程序开发包、界面开发包、媒体开发包等，这些类库构成了操作系统的应用程序接口API（haikuOS兼容BeOS的API）。   

    HaikuOS(BeOS)包含十几个软件开发包，一般的编程只需熟悉几个常用的开发包，比如显示一个窗口只用到应用开发包（Application Kit）和界面开发包（Interface Kit）。  

__参考__：  [3]

下篇将继续详细介绍Haiku的架构和各种软件开发包API，以及Haiku的消息机制，线程，程序间的通信等。关于Haiku系统的更细节的内容大都在其[官方网站www.haiku-os.org](www.haiku-os.org)。为方便，列出主要资料链接：     

1. [Haiku用户指南（中文）](http://www.haiku-os.org/docs/userguide/zh_CN/contents.html)      
2. [Documents：包含用户使用及编程指南](http://www.haiku-os.org/documents)    
3. [Articles：主要是历年来Haiku开发人员的写的一些关于Haiku开发相关文章](http://www.haiku-os.org/articles)    
4. [Development：Haiku开发相关资源](https://www.haiku-os.org/development)    


此外，还可以阅读我后边列出的参考文献，或者关注我的更新，与我一起学习Haiku系统。

首发地址：[Github pages《Don Liu's Blog》](http://doncn.github.io/blog)，如有错漏之处请不吝赐教，Email：donliucn@gmail.com。   
Copyright © Don Liu

-----------------------------
###参考文献及扩展阅读：###
[1] [BeOS Wiki](http://en.wikipedia.org/wiki/Beos)  
[2] [The Art of Unix Programming](http://www.catb.org/esr/writings/taoup/html/ch03s02.html#beos)  
[3] [Programming the Be Operating System](http://www.haiku-os.org/legacy-docs/programming_the_be_operating_system.pdf)  
[4] [The Dawn of Haiku OS](http://spectrum.ieee.org/computing/software/the-dawn-of-haiku-os/0)  
[5] [http://www.freelists.org/post/haiku/A-Roadmap-Related-Question,23](http://www.freelists.org/post/haiku/A-Roadmap-Related-Question,23)   
[6] [Haiku Platform ](http://kernel-being.livejournal.com/3110.html)  
[7] [A Programmer's Introduction to the Haiku OS](http://www.osnews.com/story/24945/A_Programmer_s_Introduction_to_the_Haiku_OS)  
[8] [Tales of a BeOS Refugee](http://www.birdhouse.org/beos/refugee/)   [译文: 一个BeOS难民的故事(by Don)](http://doncn.github.io/2013/12/28/Tales-of-BeOS-Refugee.html)   
