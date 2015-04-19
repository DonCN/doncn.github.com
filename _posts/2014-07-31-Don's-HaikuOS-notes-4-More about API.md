---
layout: post
title: Don's HaikuOS Notes 4:More About API — Kits、Classes、Functions v1.0  
summary: 本篇进一步介绍了Haiku的应用程序接口（API）——软件开发包Kits及其内部的类和函数。<p>
categories: [Haiku OS, HaikuOS notes]  
tags: [Haiku OS, HaikuOS notes]
published: true  
---

# {{ page.title }} #

{{page.summary}}


《Don's HaikuOS Notes》系列之前已有三篇：

[Don's HaikuOS Notes 1:Haiku操作系统简介... ](http://doncn.github.io/2013/12/28/Don%27s-HaikuOS-notes-1-introduce.html)

[Don's HaikuOS Notes 2:Haiku操作系统架构、开发包、消息机制...](http://doncn.github.io/2014/04/27/Don%27s-HaikuOS-notes-2-OS-Layers-DevKits.html)

[Don's HaikuOS Notes 3:Haiku编程简介——创建窗体程序及消息演示](http://doncn.github.io/2014/05/02/Don%27s-HaikuOS-notes-3-Programming-Introduce-Message.html)

前三篇介绍了Haiku操作系统的历史、特性；介绍了系统架构，以及它的三个层级：内核层（kernel）、服务层（server）、软件开发包层（software kits），以及开发包的继承关系，多线程的实现原理；以简单的图形界面程序为例介绍了Haiku的简单的程序开发及其消息机制。本篇结合代码实例，进一步介绍Haiku/BeOS的开发包Kits，主要是Application、Interface、Storage这三个开发包。开发包Kits就是用于编程的应用程序接口（API），不同开发包内部包含不同类别的类和成员函数（构造、析构、hook、普通）、成员变量，需要注意的是：

* 成员变量一般为私有private，主要用于成员函数间，而不直接被类的对象使用。
* hook function，hook函数是一种特殊的成员函数。与普通成员函数只能由类的对象激活，并被程序调用不同，hook函数可以被类激活，即可以被程序调用，又可以直接由系统调用。所以hook函数的名字需由系统指定，如：QuitRequested()。

窗体和应用示例代码MyHelloWindow.cpp和MyHelloWorld.cpp：

1. MyHelloWindow.cpp 定义了窗体内的函数

// -----------------------------------------------------------

	#ifndef _APPLICATION_H
	#include <Application.h>
	#endif
	#ifndef MY_HELLO_VIEW_H
	#include "MyHelloView.h"
    #endif
    #ifndef MY_HELLO_WINDOW_H
    #include "MyHelloWindow.h"
    #endif

    MyHelloWindow::MyHelloWindow(BRect frame)
    	: BWindow(frame, "My Hello", B_TITLED_WINDOW, B_NOT_RESIZABLE)
    {
    	MyHelloView *aView;
    	frame.OffsetTo(B_ORIGIN);
    	aView = new MyHelloView(frame, "MyHelloView");
    	AddChild(aView);
    	Show();
    }

    bool MyHelloWindow::QuitRequested()
    {
    	be_app->PostMessage(B_QUIT_REQUESTED);
    	return(true);
    }
// -----------------------------------------------------------

2. MyHelloWorld.cpp定义了主程序功能

// -----------------------------------------------------------

    #ifndef MY_HELLO_WINDOW_H
    #include "MyHelloWindow.h"
    #endif
    // removed inclusion of MyHelloView.h header file
    #ifndef MY_HELLO_WORLD_H
    #include "MyHelloWorld.h"
    #endif

    main()
    {
    	MyHelloApplication *myApplication;
    	myApplication = new MyHelloApplication();
    	myApplication->Run();
    	delete(myApplication);
    	return(0);
    }

    MyHelloApplication::MyHelloApplication()
    	: BApplication('myWD')
    {
    	MyHelloWindow *aWindow;
    	BRect aRect;
    	// moved to MyHelloWindow constructor: MyHelloView variable declaration
    	aRect.Set(20, 20, 250, 100);
    	aWindow = new MyHelloWindow(aRect);
    	// moved to MyHelloWindow constructor: the code to create view,
    	// attach it to window, and show window
    }
// -----------------------------------------------------------

MyHelloApplication()中创建了窗体对象，还可以将MyHelloApplication()在单独文件中定义。

## I. Application Kit / 应用开发包

正如上篇所说，Application开发包中的类与应用服务交互、或直接与内核交互。每个应用程序都开始于创建一个继承自该开发包的BApplication类的子类。这个子类的任务是：

1. 连接应用服务(Application Server)，负责程序显示和窗口交互。
2. 运行程序的主消息队列线程，让程序对各种事件进行响应。

BApplication类的一个重要成员函数是Run()。每个程序的main()函数都必须创建BApplication的子类的实例，并触发Run()。如：

	App *app = new App();//App为BApplication的子类
	app->Run();			//触发Run()
    delete app;			//程序结束，必须释放应用对象的内存

由于BApplication类继承自Application开发包的另外两个类—BLooper 和BHandler类，这两个类用于消息传递和处理。具体的，BLooper创建和控制消息队列，这个消息队列就是一个用于传递消息给对象的独立线程；BHandler用于处理从BLooper对象收到的消息。因而，BApplication的子类都有独立的消息线程，用于传递消息。

![应用程序开发包（Application Kit）的继承结构](/images/haiku-notes/2_ApplicationKit_hierarchy.png)

## II. Interface Kit / 界面开发包

Interface开发包是BeOS/Haiku最大的开发包，也是开发图形界面程序用的最多的开发包。Window，View，Menu，Control等相关的类都在这个开发包中。

![界面开发包（Interface Kit）的继承结构](/images/haiku-notes/4_InterfaceKit_hierarchy.png)

跟BApplication类一样，该开发包中的BWindow类也是继承自BLooper 和BHandler这两个类，因而窗体也有独立的消息线程，进行消息传递和处理。例如鼠标点击按钮，则系统收到这个事件，就通过应用服务将这个消息传递给窗体对象的消息队列线程，由窗体接收处理。

一个窗口通常包含一个或多个view——BView类的对象，一般有一个和窗体的内容区域一样大小的view，其他较小的view位于这个view之上，每个view都是独立操作的，可以用来展示各种界面元素。当窗体更新时，各个view的内容自动重绘，所以让界面元素位于它自己的view中是有道理的。有些界面开发包的控件就是BView的继承子类，如BCheckBox，
BRadioButton，BPictureButton。

下面简单介绍界面开发包中的主要类及其内部的主要函数：

### BWindow类

如前篇所述，在创建窗口对象前，首先要创建BApplication类的对象，因为Application服务器负责为窗口分配内存。

BWindow类有大量的Hook函数，即这些函数主要由系统来激活而不是由其他函数调用。如：BWindow（构建函数，用于创建窗体）、FrameMoved（感知窗体移动）、QuitRequested（窗体退出后的一些操作，如be_app->PostMessage(B_QUIT_REQUESTED);）等函数。在这些函数中定义了一些操作，等到条件满足，系统自动执行这些函数，比如BWindow在窗体对象建立后由系统自动运行，而FrameMoved在感知到窗体移动后由系统自动执行。

窗体类的构建函数，可以将窗体内的View等内容放入构建函数，而不是在Application构建函数中：

    MyHelloWindow::MyHelloWindow(BRect frame)
		: BWindow(frame, "My Hello", B_TITLED_WINDOW, B_NOT_RESIZABLE)
	{
		MyHelloView *aView;
		frame.OffsetTo(B_ORIGIN);
		aView = new MyHelloView(frame, "MyHelloView");
		AddChild(aView);
		Show();
	}

这样Application构建函数就比较简洁，只给窗体传递参数就可以：

	MyHelloApplication::MyHelloApplication()
		: BApplication('myWD')
	{
		MyHelloWindow *aWindow;
		BRect aRect;
		aRect.Set(20, 20, 250, 100);
		aWindow = new MyHelloWindow(aRect);
	}

主要函数的说明：

* 构建函数：BWindow(BRect frame, const char *title, window_type type, uint32 flags, uint32 workspace = B_CURRENT_WORKSPACE)

 	* 创建一个新窗口。window_type窗体类型有多种，现在需要记住的窗口类型是 B_TITLED_WINDOW 和 B_DOCUMENT_WINDOW。
	* BRect类定义了窗体、滑块、按钮等长方体的四角的坐标，即它有四个参数：(left, top, right, bottom)。该类用起来不像类，而更像一个int之类的类型，它不用new和delete。参数可以在定义对象时指定：BRect frame(left, top, right, bottom)，或者用set成员函数指定：frame.set(left, top, right, bottom)。
	
* void AddChild(BView *child)

	将一个 BView（或BView子类）附属到一个窗口。

* BView *FindView(const char *name)	

	返回一个指向名称为 name 的 BView 的指针，若不存在则为 NULL。将View加入窗体aWindow->AddChild(aView)。

* BRect Bounds(void)
	
	返回窗口的客户区域尺寸，例如窗口矩形框内部的白色区域。用于在窗体内添加控件时测量主窗体尺寸。如：

    	// 下面将定义菜单栏的高度。Bounds()返回窗口的尺寸。
    	BRect r(Bounds());
    	r.bottom = 20;    
    	// 在这里 r 唯一重要的部分是其高度。当我们添加项目到菜单栏时，
    	// 它将会在我们指定的高度根据窗口的宽度进行扩展。
    	BMenuBar *menuBar = new BMenuBar(r, "menubar");

* void Show(void)
	
	显示窗口。在使用Show命令前，创建的窗体是隐藏的。

### BView类

BView类用来在窗体内画图。

* BView(BRect frame, const char *name, int32 resizeMode, int32 flags)

	创建一个新的视图，查阅 BeBook 中有关 BView 章节中所有可用的自定义尺寸模式。无需担心 flags 参数，目前只需要记住 B_WILL_DRAW 即可。

* void SetViewColor(uint8 red, uint8 green, unit8 blue)
	
	设置视图的背景颜色。

* void Invalidate(void)

	强制 BView 重绘自己。

* void AddChild(BView *child)

	将一个 BView（或其子类）附属到视图。

### BControl

* ResizeToPreferred(void)

	子类调用它调整自己至合适尺寸以显示其标签和内容。

* SetLabel(const char *label)/const char * Label(void) 

	用于获取和设置子类的标签的方法。

* SetTarget(BHandler *handler, BLooper *looper)

	发送调用小弟到不同的目标，如 BView，BWindow，或者 BApplication。

* void SetEnabled(bool enabled)/bool IsEnabled(void)
 
	用于获取和设置控件启用/禁用状态的方法。

### BListView

* AddItem(BListItem *item)

	添加条目到列表。
	 
* int32 CountItems(void)
	 
	返回列表中条目的数量。
	
* BListItem *RemoveItem(int32 index)
	
	移除并返回指定索引的条目，如果不存在，则返回 NULL。
	
* void RemoveItem(BListItem *item)
	
	从列表中移除指定条目。如果列表中不存在，则不作任何动作。
	
* int32 CurrentSelection(int32 index = -1)
	
	返回当前选中项目的索引，如果不存在，则为 -1。index 参数用于获取支持多条目选择的列表中所有的选中项目。通常会有一个 while() 循环来获取所有的条目标记，并且当返回 -1 是，它将会退出。
	
* void Select(itn32 index, bool extend = false)
	
	从指定索引中选择条目。如果extend为false，在指定条目选定前，所有其他的条目将会取消选定。
	
* void Select(int32 start, int32 end, bool extend = false)
	
	选中 start 到 end 之间的所有条目。如果 extend 为 false，在指定条目选定前，其他的所有条目取消选定。
	
* void DeselectAll(void)
	
	取消选定列表中的所有条目。
	

## III. Storage Kit / 存储开发包

存储开发包提供了各种类进行文件、数据的读、写、存储、搜索等操作。

BNode类的对象用来表示磁盘上的数据。BFile类是BNode的继承子类，它的对象表示磁盘上的文件。创建BFile类的对象就打开一个文件，删除它的对象就关闭文件。

BDirectory类也是BNode的继承子类，它的对象表示一个文件夹，允许程序获取文件夹内容，在文件夹内创建文件。

文件属性包含了文件的额外信息，可以用作索引、查询。BQuery类用来执行查询操作。

## IV. Support Kit / 支持开发包

支持开发包就是用来支持其他开发包，它定义了一些数据类型、常量和一些类。

BArchivable类定义了基本接口用来将某个对象存入消息，或者将消息中的某个对象拷贝出来。

BLocker类用来限制程序的某些操作，因为Haiku/BeOS是多线程的，程序可能通过两个不同的线程同时操作数据。而两个线程同时写入同一个区块会产生不可预料的结果，为了避免这种情况，就需要Lock()和Unlock()函数来保护相应代码块。当然，这只是在某些特定情况下需要。

## V. Media Kit / 媒体开发包

媒体开发包提供了对音频、视频数据进行实时处理的类。这些操作依赖于节点(Node)，一个节点总是间接的继承自BMediaNode，有几种不同的节点类型，如producer、consumer节点，producer节点输出数据给媒体缓存，再有consumer节点接收。

## VI. Kernel Kit / 内核开发包

内核提供了对多线程的支持，包括产生和控制多线程、保护多线程的环境和共享内存等。



-----------------------------
__参考__：  本篇内容主要来自参考文献[1]

本篇就是这些内容，如有错漏之处，请不吝赐教。更多细节可参考后边的参考文献和扩展阅读。希望随着学习的深入，能有更多的内容与大家分享。

首发地址：[Github pages《Don Liu's Blog》](http://doncn.github.io/blog)
Don Liu Copyright © 2013-2014， Email：donliucn@gmail.com
  
**本篇创建于：**2014-07-31，**最后修改：**2014-12-13 v1.0

-----------------------------
###参考文献及扩展阅读：###
[1] [Programming the Be Operating System](http://www.haiku-os.org/legacy-docs/programming_the_be_operating_system.pdf)  
[2] [Learning to Program with Haiku, Lesson 17](http://darkwyrm.beemulated.net/downloads/pdf/Learning%20to%20Program%20With%20Haiku%20Lesson%2017.pdf)  
[3] [学习系列第十七课](https://github.com/pengphei/haiku-cn/wiki/%E5%AD%A6%E4%B9%A0%E7%B3%BB%E5%88%97%E7%AC%AC%E5%8D%81%E4%B8%83%E8%AF%BE)  
[4] [Haiku用户指南（中文）](http://www.haiku-os.org/docs/userguide/zh_CN/contents.html)  
[5] [Documents：包含用户使用及编程指南](http://www.haiku-os.org/documents)  
[6] [Articles：主要是历年来Haiku开发人员的写的一些关于Haiku开发相关文章](http://www.haiku-os.org/articles)  
[7] [Development：Haiku开发相关资源](https://www.haiku-os.org/development)  
