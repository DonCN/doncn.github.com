---
layout: post   
title: Don's HaikuOS Notes (2):系统架构、开发包... v1.0   
summary: 本篇详细介绍Haiku OS的系统架构的三个层级：内核层（kernel）、服务层（server）、软件开发包层（software kits）。三层之间为服务-客户端关系，底层为高层服务，高层调用底层功能；介绍了开发包的继承关系等。通过本篇内容，可以更详细的了解Haiku系统的一些细节技术，也为以后Haiku编程做知识准备。——Don Liu， Email：donliucn@gmail.com <p>
categories: [Haiku OS, HaikuOS notes]  
tags: [Haiku OS, HaikuOS notes]   
published: true  
---

# {{ page.title }} #

{{page.summary}}


## I 系统架构 ##

<p><div align="center">
<img src="/images/BeOS_Structure.png" alt="BeOS_Structure.png"><p>
应用程序和硬件之间的系统层次结构
</div>

《Don's HaikuOS Notes》系列的前一篇“简介”中介绍了Haiku操作系统的历史、特点、特性，介绍了系统架构分为三个层级：内核层（kernel）、服务层（server）、软件开发包层（software kits）。三层之间为服务-客户端关系：软件是服务的客户端，服务又是内核的客户端[2]，总之是，底层为高层服务，高层调用底层功能。各个层级简介如下：

1. __内核层 / kernel__<p>
    操作系统的最底层是内核，它直接工作在硬件之上，处理计算机的底层任务，提供了上层所需的操作系统的基本功能，包括多线程、多处理器、抢占式多任务处理、内存包含、虚拟内存、消息传递、线程调度、文件系统工具等。内核的线程调度初始就设计成支持多线程、多处理器，这一特性是Haiku的固有属性，是Haiku API的核心和灵魂所在[2]。

	上图是借用《Programming the Be Operating System》的一张图。实际上，Haiku的内核是混合内核(hybrid kernel)，并且是偏单一内核的混合内核[3]。首先，Haiku的硬件驱动运行于内核层，动态链接，图形驱动则分为两部分，分别位于内核和服务层。除去驱动的内核基本为模块化的单一内核。

2. __服务层 / server__<p>
    内核之上是服务层。服务层包含多个服务（servers），在后台处理程序请求的系统功能，各个服务运行在自己受保护的内存空间[2]，因而是独立的、可重启的[4]，因而某个服务崩溃不会影响到其他服务。作为程序员，不能直接操作服务层，需要通过上层的软件开发包提供的接口操作服务层。	
	

3. __软件开发包层 / software kits__<p>
    软件开发包是应用程序调用服务和内核的接口，是Haiku的各种应用编程接口（API）的集合，按照使用类别将API分成各种开发包（也就是用C++编写的面向对象的类库），以动态链接库的形式（扩展名为.so）存在和使用。   

    HaikuOS(BeOS)包含十几个软件开发包，一般的编程只需熟悉几个常用的开发包，比如显示一个窗口只用到应用开发包（Application Kit）和界面开发包（Interface Kit）。

服务层包含的服务（servers）大都在开发包层有对应的开发包，程序通过使用开发包的应用编程接口（API）来调用服务层和内核的操作系统功能，因而可以将二者结合起来阅读。主要服务和开发包列表如下：

**Table：**Haiku的开发包（Software Kits）与服务（Servers）对应说明 [1][5-7]

<table border="1" width="100%">
    <tr align="center" bgcolor="gray">
        <th>Software Kits <p>Libraries</th>
        <th>Servers</th>
	<th>说明</th>
    </tr>
    <tr align="left">
        <th>应用程序开发包 Application kit <p>libbe.so</th>
        <th>应用程序服务 Application Server</th>
        <td>
		每个程序都要用到的一个服务，使用应用程序开发包调用该服务也是创建一个应用程序的开始，每个程序都是继承自该包中的BApplication类的一个实例。该类定义了程序、线程间通信的消息系统，用以传递用户界面交互、事件等。<p>
		Haiku具有多线性化的特性，她的每个窗口默认包含两个线程，第一个处理图形更新，第二个处理用户交互，第一个运行在应用程序服务中，第二个运行在程序中[2]。这使得图形更新与IO交互分开，解决了多任务处理时响应慢的问题，保证了Haiku系统响应快速。
		</td>
    </tr>
    <tr align="left">
        <th>界面开发包 Interface kit <p>libbe.so</th>
        <th> </th>
        <td>		
    	这是目前最大的一个软件开发包。提供了基于应用开发包的消息系统之上的图形用户界面，定义了窗口及其包含的各种元素，如滑动条、按钮、列表、文本框等。每个用到窗体的程序都要用到界面开发包。<p> 
    	此外haiku在界面开发包之外又增加了布局接口Layout API，使程序布局更灵活和简单。			
		</td>
    </tr>
    <tr align="left">
        <th>存储开发包 Storage Kit <p>libbe.so</th>
        <th> </th>
        <td>
		存储开发包Storage Ki包含了对文件系统操作的一些类，如在磁盘保存和更新数据等。			
		</td>
    </tr>
    <tr align="left">
        <th>支持开发包 Support Kit <p>libbe.so</th>
        <th> </th>
        <td>
		支持开发包为其他开发包提供支持，如数据类型、常数等的定义。还包含程序中使用的一些支持类，包括线程安全、IO、和序列化（serialization）用到的资源。			
		</td>
    </tr>
    <tr align="left">
        <th>媒体开发包 Media Kit <p>libmedia.so </th>
        <th>媒体服务 media server </th>
        <td>
		媒体服务用于实时处理数据，主要是多媒体数据流。媒体开发包通过调用媒体服务为媒体数据流和程序间通信提供了统一的接口。它通过缓存（buffer）的管道（popeline）将多媒体流分发给数据处理器（data  handler）。每个数据处理器都可以读写管道中的媒体数据流。而缓存作为共享存储，可以被多个程序访问，而不用复制。媒体服务还可以通过一个全局调度对象（global scheduling object）同步不同的媒体数据流。这对同时处理音频和视频非常重要。
		</td>
    </tr>
    <tr align="left">
        <th>打印开发包 Print Kit </th>
        <th>打印服务 Print Server  </th>
        <td>
		</td>
    </tr>
    <tr align="left">
        <th>音频设备数字接口开发包 <p>Midi Kit <p>libmidi.so libmidi2.so</th>
        <th>音频设备数字接口服务 Midi Server </th>
        <td>
		音频设备数字接口开发包MIDI(Musical Instrument Digital Interface) Kit 提供了处理MIDI格式音频数据的接口。Haiku在此基础上新加了MIDI2 Kit，扩展了部分功能。			
		</td>
    </tr>
    <tr align="left">
        <th>设备开发包 Device Kit <p>libdevice.so</th>
        <th> </th>
        <td>
		设备开发包Device Kit提供了硬件连接的接口，主要用于驱动开发。	
		</td>
    </tr>
    <tr align="left">
        <th>网络开发包 Network Kit <p>libnet.so </th>
        <th>网络服务 Network Server </th>
        <td>
		提供网络、WiFi相关的服务，如DHCP、WEP、ftp、telnet等。网络开发包调用网络服务处理网络相关的各种事物。			</td>
    	</tr>
    <tr align="left">
        <th>转换开发包 Translation Kit <p>libtranslation.so</th>
        <th> </th>
        <td>
		转换开发包Translation Kit不是传统意义上的语言翻译转换，而是媒体格式的转换，如jpg图片转换为png图片等。这是Haiku的一个特色，若想增加Haiku支持某种媒体格式，只需利用转换开发包将新媒体格式转换为Haiku支持的格式就可以用原来的媒体软件，而不用下载新软件。
		</td>
    </tr>
    <tr align="left">
        <th>邮件开发包 Mail Kit <p>libmail.so </th>
        <th>邮件服务 Mail Server </th>
        <td>
		邮件开发包Mail Kit提供了电子邮件的相关服务。			
		</td>
    </tr>
    <tr align="left">
        <th>游戏开发包 Game Kit <p>libgame.so </th>
        <th> </th>
        <td>
		游戏开发包Game Kit提供了处理游戏声音等全屏程序的一些类。
		</td>
    </tr>
    <tr align="left">
        <th> <p>libbe.so</th>
        <th>输入服务 Input Server </th>
        <td>
		处理键盘、鼠标、手柄等输入设备操作。			
		</td>
    </tr>
    <tr align="left">
        <th>包管理开发包 Package Kits <p>libpackage.so </th>
        <th>包管理服务 Package Server </th>
        <td>
		这是Haiku在测试版Alpha4.1之后新增加的功能，通过命令行或包管理的客户端程序HaikuDepot可以直接安装下载程序。		</td>
    	</tr>
    <tr align="left">
        <th>本地化开发包 Locale Kit <p>liblocale.so </th>
        <th> </th>
        <td>
		本地化开发包Locale Kit包含了本地化到各种语言、时区、数字格式等的类。这也是Haiku相对于BeOS增加的一个新特性。		</td>
    	</tr>
    <tr align="left">
        <th>Screen Saver <p>libscreensaver.so </th>
        <th> </th>
        <td>
		</td>
    </tr>
    <tr align="left">
        <th>桌面栏 Deskbar <p>libtracker.so </th>
        <th>桌面栏 DeskBar </th>
        <td>
		相当于Windows的任务栏			
		</td>
    </tr>
    <tr align="left">
        <th>文件浏览器 Tracker <p>libtracker.so</th>
        <th>文件浏览器 Tracker </th>
        <td>
		相当于Windows的Explorer文件浏览器，但是更好用^_^			
		</td>
    </tr>
    <tr align="left">
        <th>*内核开发包 Kernel Kit <p>libroot.so</th>
        <th></th>
        <td>
		内核开发包用于程序直接操作底层的内核，以及手动创建和维护线程。
		</td>
    </tr>
    <tr align="left">
        <th>*OpenGL Kit <p>libGL.so</th>
        <th></th>
        <td>
		为程序增加3D效果，以及处理三维对象			
		</td>
    </tr>
</table>

*\*这两个开发包在Haiku的源码库中找不到，等弄清楚了再补充。*
*上表中的库和开发包大都有对应关系，但是也有几个开发包编译为一个库。此外，libbe.so是所有库的母库，包含了应用框架的核心功能，包含了应用程序、图形接口、存储、支持等开发包的所有功能。[6]*

上述的各种软件开发包不是独立的，它们之间有类的继承关系。比如一个开发包的类可能派生自几个其他的开发包。将这些所有的类根据功能和概念分成多个开发包便于整理和应用。至于更细节的开发包之间如何继承，如何编程使用，请见下节。


## II 软件开发包的继承结构

上述的各种软件开发包不是独立的，它们之间有类的继承关系。比如一个开发包的类可能派生自几个其他的开发包。将这些所有的类根据功能和概念分成多个开发包便于整理和应用。下面介绍开发包的这种继承结构。由于会经常提到各种类的名称，首先介绍下开发包源码的命名规则：

### 1. 源码的命名规则

为了便于介绍开发包的类，首先简单介绍下源码的命名规则

__Table:__ Haiku OS Naming Conventions

<table border="1">
    <tr align="center" bgcolor="gray">
        <th>Category</th>
        <th>Prefix</th>
	<th>Spelling</th>
	<th>Example</th>
    </tr>
    <tr>
        <th>Class name </th>
        <td>B </td>
        <td>B+每个单词首字母大写 </td>
        <td>BTextView </td>
    </tr>
    <tr>
        <th>Member function </th>
        <td>none </td>
        <td>每个单词首字母大写 </td>
        <td>OffsetBy() </td>
    </tr>
    <tr>
        <th>Data member </th>
        <td>none </td>
        <td>第一个单词外的每个单词首字母大写 </td>
        <td>buttenDown </td>
    </tr>
    <tr>
        <th>Constant </th>
        <td>B_ </td>
        <td>B_+所有字母大写 </td>
        <td>B_LONG_TYPE </td>
    </tr>
    <tr>
        <th>Global variable </th>
        <td>be_ </td>
        <td>be_+全部小写 </td>
        <td>be_app, be_roster, be_clipboard </td>
    </tr>

</table>


### 2. 开发包的继承结构（以Interface Kit为例）

<p><div align="center">
<img src="/images/InterfaceKit_hierarchy.png" alt="InterfaceKit_hierarchy.png" width="633"><p>
接口开发包Interface Kit的继承结构
</div>

系统的开发包都是C++编写的，因此它的类都是面向对象的，自然的采用了继承结构。由上图可以看到接口开发包的类大都是继承自其它的类，如Support Kit、Application Kit。继承结构在Haiku API中发挥了重要作用，理解这个继承结构，有利于快速选择采用哪个类来实现既定功能。

如上图中，BView继承自BHandler，而BControl继承自BView。



首发地址：[Github pages《Don Liu's Blog》](http://doncn.github.io/blog)   
Copyright © Don Liu， Email：donliucn@gmail.com  

-----------------------------
###参考文献及扩展阅读：###
[1] [Programming the Be Operating System](http://www.haiku-os.org/legacy-docs/programming_the_be_operating_system.pdf)  
[2] [A Programmer's Introduction to the Haiku OS](http://www.osnews.com/story/24945/A_Programmer_s_Introduction_to_the_Haiku_OS)   
[3] [http://www.freelists.org/post/haiku/A-Roadmap-Related-Question,23](http://www.freelists.org/post/haiku/A-Roadmap-Related-Question,23)   
[4] [Haiku Platform ](http://kernel-being.livejournal.com/3110.html)  
[5] [The Haiku Book](https://api.haiku-os.org/)  
[6] [Division of Labor: Kits, Libraries, Servers, and Teams](https://www.haiku-os.org/documents/dev/division_of_labor_kits_libraries_servers_and_teams)    
[7] [Haiku Source Code](http://cgit.haiku-os.org/haiku/tree/src)   
[8] [Haiku用户指南（中文）](http://www.haiku-os.org/docs/userguide/zh_CN/contents.html)       
[9] [Documents：包含用户使用及编程指南](http://www.haiku-os.org/documents)      
[10] [Articles：主要是历年来Haiku开发人员的写的一些关于Haiku开发相关文章](http://www.haiku-os.org/articles)     
[11] [Development：Haiku开发相关资源](https://www.haiku-os.org/development)    
