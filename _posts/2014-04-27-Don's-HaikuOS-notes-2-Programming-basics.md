---
layout: post   
title: Don's HaikuOS Notes（2）：编程基础（进行中...)   
summary: 本篇介绍Haiku OS的开发包继承结构、消息通信机制等编程基础。——Don Liu， Email：donliucn@gmail.com <p>
categories: [Haiku OS]  
tags: [Haiku OS, HaikuOS notes]   
published: true  
---

# {{ page.title }} #

{{page.summary}}

 
<p><div align="center">
<img src="/images/BeOS_Structure.png" alt="BeOS_Structure.png"><p>
应用程序和硬件之间的系统层次结构
</div>

上篇简要介绍了Haiku操作系统的一些基本情况，介绍了其系统架构分为如上图所示的三个层级：微内核层（microkernel）、服务层（server）、软件开发包层（software kits）。

系统架构最高层中的软件开发包层包含了十几个软件开发包，主要有：

* __应用开发包 / Application kit__<p>
    应用开发包（Application Kit）是开发应用程序的开始，每个应用程序都是基于一个继承自该包中的BApplication的类开发的。定义了消息系统、程序间通信等。

* __接口开发包 / Interface kit__<p>
    这是目前最大的一个软件开发包。提供了基于应用开发包的消息系统之上的图形用户接口，定义了窗口及其包含的各种元素。

    此外haiku在接口开发包之外又增加了布局接口Layout API，使程序布局更灵活和简单。

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


### 软件开发包的继承结构###

上述的各种软件开发包不是独立的，它们之间有类的继承关系。比如一个开发包的类可能派生自几个其他的开发包。将这些所有的类根据功能和概念分成多个开发包便于整理和应用。下面介绍开发包的这种继承结构。由于会经常提到各种类的名称，首先介绍下开发包源码的命名规则：

#### 源码的命名规则####

为了便于介绍开发包的类，首先简单介绍下源码的命名规则

__Table__ Haiku OS Naming Conventions

| Category       | Prefix | Spelling                          |  Example    | 
| :------------- | :----- | :-------------------------------- | :---------- | 
| Class name     | B      | Begin words with uppercase letter | BTextView   | 
| Member function| none   | Begin words with uppercase letter | OffsetBy()  | 
| Data member    | none   | Begin words (excepting the first) with uppercase letter |  bottom    | 
| Constant       | B_     | All uppercase                     | B_LONG_TYPE | 
| Global variable| be_    | All lowercase                     | e_clipboard | 


#### 开发包的继承结构（以Interface Kit为例） ####

<p><div align="center">
<img src="/images/InterfaceKit_hierarchy.png" alt="InterfaceKit_hierarchy.png" width="633"><p>
接口开发包Interface Kit的继承结构
</div>

系统的开发包都是C++编写的，因此它的类都是面向对象的，自然的采用了继承结构。由上图可以看到接口开发包的类大都是继承自其它的类，如Support Kit、Application Kit。理解这个继承结构，有利于快速选择采用哪个类来实现既定功能。

## Haiku OS 编程基础 ##

### 消息、线程、程序通信 ###

前面提到“深入的多线程”造就了Haiku的快速响应和高性能，这是如何实现的呢？

* **消息 Message**

一个Haiku OS程序的开始，是创建一个继承自应用开发包中的BApplication类的新派生类的对象，如下图所示为一个应用开发包的继承结构。

<p><div align="center">
<img src="/images/ApplicationKit_hierarchy.png" alt="ApplicationKit_hierarchy.png" width="633"><p>
应用开发包Interface Kit的继承结构
</div>

创建一个应用对象就建立了程序的主线程，用来与应用服务Application Server联络（这就是前述系统三层结构中的开发包层与服务层的联络，服务层的Server通过开发包为程序提供服务）。应用服务管理着许多程序的基础任务，如向应用程序报告用户事件（点击鼠标或按下键盘），这个报告的是以消息（Message）的形式传递的，被程序的主线程接受。消息（Message）本身是一个对象，即包含了事件细节的数据包。由系统（应用服务）确定用户事件，然后用独立的线程传递消息细节给程序的主线程，这让编程工作变得简单。

点击鼠标或按下键盘的消息是系统消息，是系统自己产生的；还可以在程序中自己定义消息BMessage对象。

* **消息循环和处理(Message loops and message handling)**



-----------------------------
###扩展阅读：###
[1] [Programming the Be Operating System](http://www.haiku-os.org/legacy-docs/programming_the_be_operating_system.pdf)  
