---
layout: post
title: Don's HaikuOS Notes:3Haiku编程简介——创建窗体程序及消息演示 v1.1
summary: 本篇通过实例介绍Haiku的编程基础，实现一个简单的窗体程序，通过按钮改变窗体标题，这样就可以演示Haiku的消息机制，各程序、窗体之间如何利用消息通信。![click me window](/images/haiku-notes/3_click_me.png)<p>
categories: [Haiku OS, HaikuOS notes]  
tags: [Haiku OS, HaikuOS notes]
published: true  
---

# {{ page.title }} #

{{page.summary}}


《Don's HaikuOS Notes》系列的前两篇介绍了Haiku操作系统的历史、特性；介绍了系统架构，以及它的三个层级：内核层（kernel）、服务层（server）、软件开发包层（software kits），以及开发包的继承关系，多线程的实现原理；介绍了Haiku的消息机制。本篇结合实例介绍如何创建简单的Haiku窗体，以及窗体、程序、线程之间如何利用消息通信。

## I. 程序与窗体代码 / Source code of application and window

每个Haiku图形界面程序都需要至少创建BApplication和BWindow这两个类的对象，可能还会用到BMessage, BLooper, BView等类，前2个属于Application Kit, 后1个属于Interface Kit。

每个程序的开始都是创建一个BApplication类的对象，也就创建了程序的主线程，这个主线程用于程序和应用服务的交互。但是一般不直接使用BApplication类，而是创建它的子类，如App。如在app.h头文件中可以这样定义：

App.h

	#ifndef APP_H
	#define APP_H

	// 通过头文件引入 BApplication类
	#include <Application.h>

	//定义继承自BApplication的子类App
	class App : public BApplication
	{
	public:
		App(void); //构造函数
	};

	#endif

这个继承自BApplication的App类与应用程序服务（Application Server）通信，通过应用程序服务实现窗体管理等工作。这个App子类在程序启动时最先创建，程序退出时最后删除。具体实现在App.cpp的main函数中：

App.cpp

	#include "App.h"

	/* 引用头文件包含需要用到的类型或方法，因为要在程序构造中
	   创建窗体的对象并完成显示，所以要包含自己定义的主窗体的头文件
       MainWindow.h */
	#include "MainWindow.h"

	/* 定义应用程序时，要为每个程序起一个唯一的名字——签名，
       如双引号中所示，这是MIME字符串，格式就是“application/发行商名.程序名”  */
	App::App(void) : BApplication(“application/x-vnd.MyFirstApp”)
	{
	/* 创建自定义窗口类型对象，并通过调用Show() 函数来显示窗体，
       并创建它的消息队列线程 */
	MainWindow *mainwin = new MainWindow();
	mainwin->Show();
	}

	//主程序入口
	int main(void)
	{
	App *app = new App();

	/* 创建的程序对象必须调用它的运行函数Run()来创建它的消息队列线程
      （这个消息机制在上篇有详细介绍）。当Run()返回后，
       必须删除Application对象app来释放内存空间。或者在Window退出时通知Application退出*/
	app->Run();
	delete app;

	return 0;
	}

由App.cpp可以看到，程序子类App的构造函数完成程序启动操作，如创建窗体并显示。而程序App继承自BApplication类，该类的构建函数的功能主要有：

- 连接程序与应用服务
- 为程序指定独有签名（需要在App构造函数继承BApplication时指定）
- 将全局变量be_app指向程序对象

主程序入口main()的开始就是创建BApplication子类对象，并调用它的Run()函数来创建属于该程序的消息队列线程，并控制这个队列和线程直至程序退出。

那窗体是如何自定义的呢？如下：

MainWindow.h

	#ifndef MAINWINDOW_H
	#define MAINWINDOW_H

	#include <Window.h>

	/* 创建窗体一般总是创建 BWindow 的子类，通过与Application server
       会话来管理窗口元素，所以对窗体的操作都通过Application对象来
       传递消息,如上App程序中,通过调用Show() 函数来显示窗体，
       并创建它的消息队列线程。*/
	class MainWindow : public BWindow
	{
	public:
				MainWindow(void);

		// 为了演示按钮与窗体通信的消息机制，在窗体中定义消息接收函数，会覆盖掉BWindow本身的MessageReceived函数
		void	MessageReceived(BMessage *msg);

		//增加新的关闭功能
		virtual bool QuitRequested();

	private:
		// 定义按钮计数变量
		int32	fCount;
	};

	#endif

下边这个文件是主窗体类的实现：

MainWindow.cpp

	#include "MainWindow.h"

	// Button.h包含按钮控件的一些类型和函数定义
	#include <Button.h>

	// BView类常用于在窗体内创建控件和绘图
	#include <View.h>

	// BString类用于处理字符串相关问题
	#include <String.h>

	/* 定义了按钮要发送的消息的代号常数，单引号内的字符会转换成整数
       赋值给代号常数作为唯一标识. */
	enum
	{
		M_BUTTON_CLICKED = 'btcl'
	};


	/* 定义窗体变量，并给定参数:指定窗口大小，括号中四个参数分别是
       左/上/右/下边框到屏幕左边和上边的像素数。然后是标题,
       B_TITLED_WINDOW指明要显示标题, B_QUIT_ON_WINDOW_CLOSE指明
       关闭窗口时通知程序退出)。fCount(0)为赋初值0 */
	MainWindow::MainWindow(void)
		:	BWindow(BRect(100,100,300,200),"ClickMe",B_TITLED_WINDOW, B_ASYNCHRONOUS_CONTROLS |
																		B_QUIT_ON_WINDOW_CLOSE),
			fCount(0)
	{
		/* BRect()作为按钮类的参数定义了按钮的大小，后边参数依次是
           控件名，控件上显示字符，按下后发送的消息 */
		BButton *button = new BButton(BRect(10,10,11,11),"button","Click Me!",
										new BMessage(M_BUTTON_CLICKED));

		// 让按钮自适应调节大小
		button->ResizeToPreferred();

		// 将按钮添加到窗体
		AddChild(button);
	}


	void
	MainWindow::MessageReceived(BMessage *msg)
	{
		// 消息包含在对象msg的内部变量'what'中.
		switch (msg->what)
		{
			// 若消息是按钮被按下
			case M_BUTTON_CLICKED:
			{
				fCount++;

				BString labelString("Clicks: ");

				// 将按键按下次数加到labelString之后
				labelString << fCount;

				// 设定窗体标题为按钮按下次数
				SetTitle(labelString.String());

				break;
			}
			default:
			{
				/* 若来的消息不符合我们自定义的消息，那肯定是系统消息，
                   所以调用我们窗体的父类BWindow的MessageReceived()
                   函数，它能处理这些系统消息。若想让你的窗体拥有系统
                   默认的窗体功能（如关闭/最大/最小化等）必须要有这个函数。*/
				BWindow::MessageReceived(msg);

				break;
			}
		}
	}

	
这就是这个演示程序的全部代码。主要分为两程序和窗体两部分，即App和 MainWindow两个.cpp文件及其对应.h头文件。MainWindow定义窗体，以及窗体上控件等的消息事件的响应——MainWindow::MessageReceived(BMessage *msg)。App创建窗体对象，并令其显示。主程序入口main用来创建App对象，并令其运行，运行完销毁内存。


## II. 代码中的几个重点 / Key points of the source code

#### 1. 消息的定义与发送 / Message and postmessage


消息用来在程序、窗口、线程之间通信，传递用户操作，访问剪切板。点击鼠标或按下键盘的消息是系统消息，是系统自己产生并自动发送的，本文的演示程序——按钮按下就属于这种，消息内容需要自己定义：

    enum
  	{
     	M_BUTTON_CLICKED = 'btcl'
  	};

每类系统消息都有一个命令常量与之对应，如"M\_BUTTON_CLICKED"。Application Kit中定义了两个类BLooper和BHandler来收发、处理消息。如下的BButton类就继承了这两个消息处理类。创建消息BMessage对象作为按钮对象的参数：

	BButton *button = new BButton(BRect(10,10,11,11),"button","Click Me!",
										new BMessage(M_BUTTON_CLICKED));

当按钮按下，就会自动发送这个M_BUTTON_CLICKED消息。还可以在程序中自己定义消息BMessage对象，来封装自定义的消息：

  	BMessage *msg = new BMessage(M_BUTTON_CLICKED);

BMessage也能在消息中包含额外数据，它提供了一些成员函数将各种数据打包进消息中，或将数据从消息中解包出来。

除了系统自动发送的消息，还可以在程序中人为发送消息，这就用到BLooper处理消息。每个BLooper都有一个线程作为事件轮询（event loop），也就是消息队列线程。如将消息传递给对象，只需调用SendMessage：

	SendMessage(M_BUTTON_CLICKED);

这个调用就将 M_BUTTON_CLICKED 消息推入程序或窗口的消息队列。由接收方在MessageReceived()中处理。

至于与其他程序通信，可以将其他程序的签名作为创建的BMessenger对象的参数，这样就可以将消息发送给拥有这个签名的程序。示例代码如下：

	BMessenger messenger("application/x-vnd.MyFirstApp");
	messenger.SendMessage(new BMessage(DO_SOMETHING));

若这个程序有几个实例，还需要区分将消息传给哪个实例，这要用到team_id：

	BMessenger(const char* signature, team_id team, status_t* error);


#### 2. 消息的接收 / Message receive


首先，要根据按钮按下次数修改需要窗体标题，这样窗体就要接收消息。BWindow类同样继承了BLooper、BHandler这两个类，因此，窗体对象可以接收、处理消息。在MainWindow.h中创建窗体自己的MessageReceived 函数，可以覆盖原有的MessageReceived函数，增加新功能：

	class MainWindow : public BWindow
	{
	public:
				MainWindow(void);

		// 为了演示按钮与窗体通信的消息机制，在窗体中定义消息接收函数
		void	MessageReceived(BMessage *msg);

		//增加新的关闭功能
		virtual bool QuitRequested();

	private:
		// 定义按钮计数变量
		int32	fCount;
	};

窗体接收到消息后，通过MessageReceived(BMessage *msg)处理消息：

	void
	MainWindow::MessageReceived(BMessage *msg)
	{
		// 消息包含在对象msg的内部变量'what'中.
		switch (msg->what)
		{
			// 若消息是按钮被按下
			case M_BUTTON_CLICKED:
			{
				fCount++;

				BString labelString("Clicks: ");

				// 将按键按下次数加到labelString之后
				labelString << fCount;

				// 设定窗体标题为按钮按下次数
				SetTitle(labelString.String());

				break;
			}
			default:
			{
				/* 若来的消息不符合我们自定义的消息，那肯定是系统消息，
                   所以调用我们窗体的父类BWindow的MessageReceived()
                   函数，它能处理这些系统消息。若想让你的窗体拥有系统
                   默认的窗体功能（如关闭/最大/最小化等）必须要有这个函数。*/
				BWindow::MessageReceived(msg);

				break;
			}
		}
	}

#### 3. 程序的退出 / Quit of Application

程序退出释放内存空间有两种方式：

1. 当Run()返回后，删除Application对象app来释放内存空间：

    app->Run();
    delete app;

2. 在Window退出时通知Application退出

	//为窗体的QuitRequested函数增加新功能
	bool MainWindow::QuitRequested()
	{
		//通知Application退出
		be_app->PostMessage(B_QUIT_REQUESTED);
		return(true);
	}
这段代码为窗体的QuitRequested函数增加新功能：发消息通知Application退出。

若没有上述两种方法退出程序，那么点击窗体关闭按钮关闭窗体后，只是窗体退出，而其后台的程序Application并未退出。因为窗体和程序运行着不同的BLooper线程，因而就有两个由BLooper定义的QuitRequested。关闭窗体，只是窗体的BLoopers的QuitRequested函数收到关闭系统消息，去关闭窗体。而程序Application的BLooper定义的QuitRequested并没有收到消息。因此，若想退出Application，还需要给它的BLooper发送消息。be_app正是指向Application的全局指针，由它发送的消息就由Application的BLooper接收，由对应的QuitRequested处理。

本文是一个简单的Haiku消息传递的例子，演示了Haiku的消息传递机制，显示出使用Haiku API编程的简便。你也去尝试下吧...

[原文所用源代码下载](http://darkwyrm.beemulated.net/downloads/pdf/15ClickMe.zip)  
源代码在[haiku-nightly测试版本hrev47169-x86gcc2hybrid-vmware](http://www.haiku-files.org/haiku/development/)中用Paladin IDE编译。


__参考__：  本篇程序代码来自参考文献[2]


本篇就是这些内容，如有错漏之处，请不吝赐教。更多细节可参考后边的参考文献和扩展阅读。

截止目前（2014-05-02），包括本篇，已经有了三篇Haiku操作系统的介绍文章，前两篇如下：

[Don's HaikuOS Notes:(1)简介... ](http://doncn.github.io/2013/12/28/Don%27s-HaikuOS-notes-1-introduce.html)

[Don's HaikuOS Notes:(2)系统架构、开发包、消息机制...](http://doncn.github.io/2014/04/27/Don%27s-HaikuOS-notes-2-OS-Layers-DevKits.html)

前两篇主要是对Haiku操作系统的概括介绍，本篇对Haiku编程作了简单演示。以我目前水平，暂时也就能写出这些东西了。希望随着学习的深入，能有更多的内容与大家分享。

首发地址：[Github pages《Don Liu's Blog》](http://doncn.github.io/blog)
Don Liu Copyright © 2013-2014， Email：donliucn@gmail.com  
**创建于：**2014-05-02，**最后修改：**2014-07-31-v1.1

-----------------------------
###参考文献及扩展阅读：###
[1] [Programming the Be Operating System](http://www.haiku-os.org/legacy-docs/programming_the_be_operating_system.pdf)  
[2] [Learning to Program with Haiku, Lesson 15](http://darkwyrm.beemulated.net/downloads/pdf/Learning%20to%20Program%20With%20Haiku%20Lesson%2015.pdf)
[3] [Haiku用户指南（中文）](http://www.haiku-os.org/docs/userguide/zh_CN/contents.html)
[4] [Documents：包含用户使用及编程指南](http://www.haiku-os.org/documents)
[5] [Articles：主要是历年来Haiku开发人员的写的一些关于Haiku开发相关文章](http://www.haiku-os.org/articles)
[6] [Development：Haiku开发相关资源](https://www.haiku-os.org/development)
