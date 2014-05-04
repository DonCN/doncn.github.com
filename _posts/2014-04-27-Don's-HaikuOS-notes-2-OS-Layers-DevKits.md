---
layout: post   
title: Don's HaikuOS Notes:(2)系统架构、开发包、消息机制... v1.0   
summary: 本篇详细介绍Haiku OS的系统架构的三个层级：内核层（kernel）、服务层（server）、软件开发包层（software kits）。三层之间为服务-客户端关系，底层为高层服务，高层调用底层功能；介绍了API开发包的继承关系；Haiku的消息机制，程序、进程间的通信等。通过本篇内容，可以更详细的了解Haiku系统的一些细节技术，也为以后Haiku编程做知识准备。 <p>   
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

**Table 2-1：**Haiku的开发包（Software Kits）与服务（Servers）对应说明 [1][5-7]

<table border="1" width="100%">
    <tr align="center" bgcolor="gray">
        <th>Software Kits </th>
		<th>Library</th>
        <th>Servers</th>
		<th>说明</th>
    </tr>
	<tr align="left">
        <th>Application kit </th>
		<th>libbe.so </th>
        <th>Application Server</th>
        <td>
		应用程序服务是每个程序都要用到的一个服务，使用应用程序开发包调用该服务也是创建一个应用程序的开始，每个程序都是继承自该包中的BApplication类的一个实例。该类定义了程序、线程间通信的消息系统，用以传递用户界面交互、事件等。<p>
		Haiku具有多线性化的特性，她的每个窗口默认包含两个线程，第一个处理图形更新，第二个处理用户交互，第一个运行在应用程序服务中，第二个运行在程序中[2]。这使得图形更新与IO交互分开，解决了多任务处理时响应慢的问题，保证了Haiku系统响应快速。
		</td>
    </tr>
    <tr align="left">
        <th>Interface kit </th>
		<th>libbe.so </th>
		<th> </th>
        <td>		
    	界面开发包是目前最大的一个软件开发包。提供了基于应用开发包的消息系统之上的图形用户界面，定义了窗口及其包含的各种元素，如滑动条、按钮、列表、文本框等。每个用到窗体的程序都要用到界面开发包。<p> 
    	此外haiku在界面开发包之外又增加了布局接口Layout API，使程序布局更灵活和简单。			
		</td>
	</tr>
    <tr align="left">
        <th>Storage Kit </th>
		<th>libbe.so </th>
		<th> </th>
        <td>
		存储开发包Storage Ki包含了对文件系统操作的一些类，如在磁盘保存和更新数据等。		
		</td>
    </tr>
    <tr align="left">
        <th>Support Kit </th>
		<th>libbe.so </th>
		<th> </th>
        <td>
		支持开发包为其他开发包提供支持，如数据类型、常数等的定义。还包含程序中使用的一些支持类，包括线程安全、IO、和序列化（serialization）用到的资源。			
		</td>
    </tr>
    <tr align="left">
        <th>Media Kit </th>
		<th>libmedia.so </th>
		<th>media server </th>
        <td>
		媒体服务用于实时处理数据，主要是多媒体数据流。媒体开发包通过调用媒体服务为媒体数据流和程序间通信提供了统一的接口。它通过缓存（buffer）的管道（popeline）将多媒体流分发给数据处理器（data  handler）。每个数据处理器都可以读写管道中的媒体数据流。而缓存作为共享存储，可以被多个程序访问，而不用复制。媒体服务还可以通过一个全局调度对象（global scheduling object）同步不同的媒体数据流。这对同时处理音频和视频非常重要。
		</td>
    </tr>
    <tr align="left">
        <th>Print Kit </th>
		<th> </th>
		<th>Print Server  </th>
        <td>打印有关服务
		</td>
    </tr>
    <tr align="left">
        <th>Midi Kit </th>
		<th>libmidi.so libmidi2.so </th>
		<th>Midi Server </th>
        <td>
		音频设备数字接口开发包MIDI(Musical Instrument Digital Interface) Kit 提供了处理MIDI格式音频数据的接口。Haiku在此基础上新加了MIDI2 Kit，扩展了部分功能。			
		</td>
    </tr>
    <tr align="left">
        <th>Device Kit </th>
		<th>libdevice.so </th>
		<th> </th>
        <td>
		设备开发包Device Kit提供了硬件连接的接口，主要用于驱动开发。	
		</td>
    </tr>
    <tr align="left">
        <th>Network Kit </th>
		<th>libnet.so </th>
		<th>Network Server </th>
        <td>
		网络服务提供网络、WiFi相关的服务，如DHCP、WEP、ftp、telnet等。网络开发包调用网络服务处理网络相关的各种事物。			
		</td>
    	</tr>
    <tr align="left">
        <th>Translation Kit </th>
		<th>libtranslation.so </th>
		<th> </th>
        <td>
		转换开发包Translation Kit不是传统意义上的语言翻译转换，而是媒体格式的转换，如jpg图片转换为png图片等。这是Haiku的一个特色，若想增加Haiku支持某种媒体格式，只需利用转换开发包将新媒体格式转换为Haiku支持的格式就可以用原来的媒体软件，而不用下载新软件。
		</td>
    </tr>
    <tr align="left">
        <th>Mail Kit  </th>
		<th>libmail.so </th>
		<th>Mail Server </th>
        <td>
		邮件开发包Mail Kit提供了电子邮件的相关服务。			
		</td>
    </tr>
    <tr align="left">
        <th>Game Kit </th>
		<th>libgame.so </th>
		<th> </th>
        <td>
		游戏开发包Game Kit提供了处理游戏声音等全屏程序的一些类。
		</td>
    </tr>
    <tr align="left">
        <th> </th>
		<th>libbe.so </th>
		<th>Input Server </th>
        <td>
		输入服务处理键盘、鼠标、手柄等输入设备操作。			
		</td>
    </tr>
    <tr align="left">
        <th>Package Kits </th>
		<th>libpackage.so </th>
		<th>Package Server </th>
        <td>
		包管理开发包是Haiku在测试版Alpha4.1之后新增加的功能，通过命令行或包管理的客户端程序HaikuDepot可以直接安装下载程序。		
		</td>
    </tr>
	<tr align="left">
        <th>Locale Kit </th>
		<th>liblocale.so </th>
		<th> </th>
        <td>
		本地化开发包Locale Kit包含了本地化到各种语言、时区、数字格式等的类。这也是Haiku相对于BeOS增加的一个新特性。		
		</td>
    	</tr>
    <tr align="left">
        <th>Screen Saver </th>
		<th>libscreensaver.so </th>
		<th> </th>
        <td>
		</td>
    </tr>
    <tr align="left">
        <th>Deskbar  </th>
		<th>libtracker.so </th>
		<th>DeskBar </th>
        <td>
		桌面栏Deskbar相当于Windows的任务栏			
		</td>
    </tr>
    <tr align="left">
	</tr>
    <tr align="left">
        <th>Tracker </th>
		<th>libtracker.so </th>
		<th>Tracker </th>
        <td>
		文件浏览器 Tracker相当于Windows的Explorer文件浏览器，但是更好用^_^			
		</td>
    </tr>
	</tr>
    <tr align="left">
        <th>*Kernel Kit </th>
		<th>libroot.so </th>
		<th></th>
        <td>
		内核开发包用于程序直接操作底层的内核，以及手动创建和维护线程。
		</td>
    </tr>
    <tr align="left">
        <th>*OpenGL Kit </th>
		<th>libGL.so </th>
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

__Table 2-2:__ Haiku OS Naming Conventions

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

![应用程序开发包（Application Kit）的继承结构](/images/ApplicationKit_hierarchy.png)

系统的开发包都是C++编写的，因此它的类都是面向对象的，自然的采用了类的继承结构，有包之间的类的继承，也有本包内的类的继承。继承结构在Haiku API中发挥了重要作用，理解这个继承结构，有利于快速选择采用哪个类来实现既定功能。

由上图可以看到应用程序开发包（Application Kit）的BHandler、BMessage等类继承自Support Kit的BObject类，而BLooper又继承自的BHandler，BApplication和Interface Kit的BWindow都继承自BLooper。那么这几个类都有什么功能，他们又是如何通过继承来“借用”别的类的功能，再增加自己的功能呢？首先将这几个类的功能列一个表简要说明：

__Table 2-3:__ Haiku API类的继承举例 [5]

<table border="1">
    <tr align="center" bgcolor="gray">
        <th>类</th>
        <th>功 能</th>
		<th>说 明</th>	
    </tr>
    <tr>
        <th>BHandler</th>
        <td><li>处理消息</li> 
		</td>
		<td>消息由BLooper传过来。
		</td>
    </tr>
    <tr>
        <th>BLooper</th>
        <td><li>处理消息</li>
 			<li>接收消息到队列</li>
		</td>
    	<td>创建一个BLooper对象会自动产生一个新线程，在其中接收和处理消息。即BLooper的函数用来接收消息，再传给继承自BHandler的函数处理消息。
		</td>
    </tr>
    <tr>
        <th>BApplication</th>
        <td><li>处理消息</li>
 			<li>接收消息到队列</li>
			<li>根据消息类型实现程序功能</li>
		</td>
		<td>通过继承自BLooper、BHandler的函数接收、处理消息，然后根据消息类型调用应用程序服务功能或其他功能。
		</td>
    </tr>
    <tr>
        <th>BWindow</th>
        <td><li>处理消息</li>
 			<li>接收消息到队列</li>
			<li>实现窗体管理相关功能</li>
		</td>
		<td>通过继承自BLooper、BHandler的函数接收、处理消息，然后根据消息类型管理窗体显示。
		</td>
    </tr>
</table>

由上表可见，子类可以通过继承很方便的“继承”父类的功能，并扩展出自己的新功能。上表几个类的除了说明了Haiku API的继承关系，还隐含了Haiku的两个重要机制：

- **消息机制：** 上表几个类继承的功能（BLooper、BHandler）就是关于消息的接收、处理，也就是消息机制的，它在Haiku中发挥着重要作用。
- **深入的多线程化：** 我们前面说到，Haiku能快速响应的功劳要归于深入的多线性化。上述几个类就能说明这个机制：由于创建一个BLooper对象会自动产生一个新线程，而BApplication、BWindow又继承自BLooper，所以每创建一个新程序（新窗体）都会产生自身主线程及属于它的消息队列线程这两个线程。所以一个包含窗体的程序至少有4个线程，每个主线程都有它单独的消息线程，所以Haiku程序响应快，很少会延迟、卡顿。

那么什么是消息呢？消息是用来在程序、窗口、线程之间通信，传递系统事件、用户操作等。由上述开发包的继承例子可以看到，消息机制对Haiku非常重要。下节介绍具体的Haiku的消息机制，你会发现Haiku的消息系统使得程序、线程之间的通信简单、可靠。

## III. 消息、线程，程序间通信 / Messages, Threads, and Application Communication

与消息机制相关的几个重要的类[12]：

#### 1. BMessage类

BMessage类就是用来封装消息内容的，包括消息类型和消息数据，以及添加消息内容的函数。

#### 2. BLooper类

BLooper类用来接收、处理消息队列，它的每个对象都运行在自己单独的线程内。它不停的检查队列中进入的消息，再利用继承的Bhandler类的函数处理消息。

消息是通过PostMessage()函数传给消息队列BMessageQueue类的对象。

#### 3. BHandler类

BHandler类用来处理消息，一般都是与消息队列BLooper类关联的，创建BHandler类的对象后应该将它传给想要处理的消息队列的BLooper::AddHandler()函数，来获取消息。消息处理是在MessageReceived()中完成的，可以重写这个函数来定义自己消息处理操作。

#### 4. BMessenger类

BMessenger类的对象可以将消息传给本程序和其他程序。

- 通过调用BMessenger::SendMessage()传递消息相对于BLooper::PostMessage()的优势：允许同步回复，这样保证处理了消息回复给发送者。
- 可以作为其他程序签名的参数，这样就可以很方便的实现程序间通信。

本篇就是这些内容，下篇将介绍如何利用Haiku API的Application Kit和Interface Kit中的BApplication, BMessage, BLooper, BWindow, BView等类创建简单的程序和窗体，以及窗体与程序的消息传递。


首发地址：[Github pages《Don Liu's Blog》](http://doncn.github.io/blog)   
Don Liu Copyright © 2013-2014， Email：donliucn@gmail.com  

-----------------------------
###参考文献及扩展阅读：
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
[12] [Haiku Messaging Foundations](https://api.haiku-os.org/app_messaging.html)     
