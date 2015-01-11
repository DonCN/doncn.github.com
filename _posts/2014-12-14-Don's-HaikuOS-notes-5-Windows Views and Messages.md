---
layout: post
title: Don's HaikuOS Notes 5:Windows、Views and Messages v1.0  
summary: 本篇深入介绍了Haiku编程中Windows、Views和Messages的使用。Windows窗体是图形界面程序与用户交流的接口，Views视图用于窗体显示图形和文字，Messages消息是各种服务、程序间通讯的媒介。<p>
categories: [Haiku OS, HaikuOS notes]  
tags: [Haiku OS, HaikuOS notes]  
published: true  
---

# {{ page.title }} #

{{page.summary}}


《Don's HaikuOS Notes》系列之前已有四篇：

 1. [Don's HaikuOS Notes 1:Haiku操作系统简介... ](http://doncn.github.io/2013/12/28/Don%27s-HaikuOS-notes-1-introduce.html)
：介绍了Haiku操作系统的历史、特性。

 2. [Don's HaikuOS Notes 2:Haiku操作系统架构、开发包、消息机制...](http://doncn.github.io/2014/04/27/Don%27s-HaikuOS-notes-2-OS-Layers-DevKits.html)
：介绍了系统架构，以及它的三个层级：内核层（kernel）、服务层（server）、软件开发包层（software kits），以及开发包的继承关系，多线程的实现原理

 3. [Don's HaikuOS Notes 3:Haiku编程简介——创建窗体程序及消息演示](http://doncn.github.io/2014/05/02/Don%27s-HaikuOS-notes-3-Programming-Introduce-Message.html)
：以简单的图形界面程序为例介绍了Haiku的简单的程序开发及其消息机制。

 4. [Don's HaikuOS Notes 4:More About API — Kits、Classes、Functions](http://doncn.github.io/2014/07/31/Don%27s-HaikuOS-notes-4-More%20about%20API.html)
：结合代码实例，进一步介绍Haiku/BeOS的开发包Kits，主要是Application、Interface、Storage这三个开发包。

本篇结合代码实例，深入介绍Haiku编程中Windows、Views和Messages的使用。Windows窗体是界面程序与用户交流的接口，Views视图用于窗体显示图形和文字，Messages消息是各种服务、程序间通讯的媒介。

## I Windows

你创建的程序的窗体一定是继承自BWindow类或其子类。由于BWindow类又是BLooper的子类，所以每个窗体都有其独立的线程和消息队列线程。窗体的消息队列用于接收和响应来自应用服务（Application Server）的消息。

### I-1 窗体类的特性 / Windows Characteristics

窗体类的特性——大小、位置、按钮等元素都在自建窗体类的构建（constructor）函数中定义。自建窗体的构建函数将窗体的特性传递给BWindow的构建函数，由BWindow的构建函数来创建窗体。

#### BWindow constructor

    MyHelloWindow::MyHelloWindow(BRect frame)//frame为窗体大小位置形参
    	:BWindow(frame, "My Hello", B_TITLED_WINDOW, B_NOT_RESIZABLE)
    {
    	//窗体内部视图、按钮等元素
    }

可以看到这个构建函数的参数就是一个位置变量frame。它是如何传递的呢？在application的构建函数中创建窗体类的对象后，用new为对象申请内存（激活构建函数）时给定参数，参数就传递给窗体的构建函数了。如下所示：

	MyHelloWindow 	*aWindow;
	BRect 			aRect(20, 30, 250, 100);
	aWindow = new MyHelloWindow(aRect);

构建函数中声明继承BWindow时给定了窗体的特性BWindow(frame, "My Hello", B_TITLED_WINDOW, B_NOT_RESIZABLE)，分别是大小位置，标题，是否有标题栏，是否可变大小。BWindow构建函数的原型可以有更多参数（5个），如下：

	BWindow(BRect 		frame,  //窗体的大小位置
			const char 	*title,	//窗口标题
			window_type type,	//窗体类型
			ulong 		flags,	//控制类型
			ulong 		workspaces = B_CURRENT_WORKSPACE)	//指定工作区

分别介绍如下：

(1) frame：窗体的大小位置由窗体的四个边分别距离屏幕的左边和上边的距离决定，顺序是（左，上，右，下）。注意不包括标题栏的大小。
	
如果希望窗体的大小取决于屏幕分辨率，那么需要利用BScreen类。
    
	BScreen mainScreen(B_MAIN_SCREEN_ID);
	BRect 	screenRect;
	int32 	screenWidth;
	screenRect = mainScreen->Frame();
	screenWidth = screenRect.right - screenRect.left;

(2) Window Title：没有标题栏的窗体可以为NULL或""。

(3) Window type：窗体类型主要有这几种
	
		B_DOCUMENT_WINDOW：有标题栏的非情态窗体。右下两侧边框较窄。	
	    B_TITLED_WINDOW：带标题栏窗体。	
		B_MODAL_WINDOW：情态窗口，没有标题栏。用于告警、提示等。	
		B_BORDERED_WINDOW：没有标题栏的非情态窗体。	
		B_FLOATING_WINDOW：悬浮窗体。

(4) Window behavior and elements：控制类型标识
	
		B_NOT_MOVABLE：创建的窗体不能移动。
		B_NOT_H_RESIZABLE：创建的窗体不能在水平方向改变大小。
		B_NOT_V_RESIZABLE：创建的窗体不能在竖直方向改变大小。
		B_NOT_RESIZABLE：创建的窗体不能改变大小。
		B_NOT_CLOSABLE：创建的窗体没有关闭按钮。
		B_NOT_ZOOMABLE：创建的窗体没有放大缩小按钮。
		B_NOT_MINIMIZABLE：创建的窗体没有最小化按钮。

(5) Workspace：工作区		

工作区，也就是虚拟桌面。窗体构建器的第5个参数用于指定新建窗体出现在哪个工作区。可选用系统指定的常量：

    B_CURRENT_WORKSPACE：新建窗体显示在当前桌面。
    B_ALL_WORKSPACES：新建窗体显示在所有桌面。

### I-2 Accessing Windows

应用服务维护着程序的窗体列表，列表从0开始，逐渐增加，但是并不能直接索引到指定的窗体，而有两种办法：一是需要使用API函数——BApplication的成员函数WindowAt()来找到窗体；二是用数据成员变量保存窗体指针。

(1) 使用API函数WindowAt()找到窗体

调用WindowAt()，则返回指定窗体对象，例如下述代码让theWindow指向当前应用的每一个窗体：

    BWindow *theWindow;
    BWindow *frontWindow = NULL;
    int32 i = 0;
    while (theWindow = be_app->WindowAt(i++)) {
    	if (theWindow->IsFront())
   			frontWindow = theWindow;
    }

上述代码中，be_app总是指向当前活动应用。若WindowAt()参数超出范围则返回NULL。若窗体在最前，则IsFront()返回布尔值TRUE。

MoveBy()移动窗体
BWindow成员函数MoveBy()用来移动选中窗体。例如将最前的窗体向下和向右移动100像素：

    frontWindow->MoveBy(100, 100);

(2) 使用数据成员变量保存窗体指针

从多个窗体中找到指定窗体可以使用API函数WindowAt()，另一个方法是在应用（application）对象中定义数据成员保存窗体的指针。

在上述例子中，在application的构建函数中定义了局部窗体变量aWindow来调用窗体的构建函数：

    MyHelloWindow *aWindow;
    ...
    aWindow = new MyHelloWindow(aRect);

这里可以在应用类定义时，定义其私有数据成员，而不是在构建函数中定义，这样就可以在该程序类的所有成员函数中直接使用：

    class MyHelloApplication : public BApplication {
    public:
                        MyHelloApplication();
    private:
        MyHelloWindow   *fMyWindow;
    };
    
 ### I-3 窗体类要点  
 
 * BWindow(BRect frame, const char *title, window_type type, uint32 flags, uint32 workspace = B_CURRENT_WORKSPACE) — 创建一个新窗口。现在需要记住的窗口类型是 B_TITLED_WINDOW 和 B_DOCUMENT_WINDOW。
 * void AddChild(BView *child) — 将一个BView（或BView子类）附加到一个窗口。
 * BView *FindView(const char *name) — 返回一个指向名称为 name 的 BView 的指针，若不存在则为 NULL。
 * BRect Bounds(void) — 返回窗体的客户区域（窗口矩形框内部的白色区域）尺寸，。
 - void Show(void) — 显示窗口。

## II Views / 视图

一个窗体一般包含多个视图，每个视图都可以单独进行绘图，滑块、按钮、文本等元素都包含在单个视图中。下面讲视图的创建、使用以及对消息的响应。

### II-1 Accessing Views

找到一个窗体有两种方法：一是在应用Application类中定义数据成员变量保存窗体的指针；二是利用API函数——Application的成员函数WindowAt()。View也是如此。

(1) 使用数据成员函数

存窗体指针是Application类的数据成员变量，而View的指针则保存在window类的数据成员函数中。


    class MyHelloWindow : public BWindow {
    	public:
    				MyHelloWindow(BRect frame);
    		virtual bool QuitRequested();
    	private:
    		MyHelloView *fMyView; //view指针
    };

定义了view指针，就可以在窗体构建函数中使用了。

    fMyView = new MyHelloView(frame, "MyHelloView");
    AddChild(fMyView);

(2) 使用API函数——FindView()

view的定义：

    MyHelloView::MyHelloView(BRect rect, char *name)
    	: BView(rect, name, B_FOLLOW_ALL, B_WILL_DRAW)
    {
    }

由view的定义可以看到，传递给view构建函数的变量有两个：大小位置、名称。若每个view都有不同的名称，则可以使用BWindow的成员函数FindView()来找到制定的view。

    MyHelloView *theView;
    theView = (MyHelloView *)fMainWindow->FindView("MyHelloView");

### II-2 View Hierarchy / 视图的层级

一个窗体可以包含多个视图，这样这些视图就有了层级。不管是否手动创建并利用AddChild()添加视图，窗体创建之后都会自动创建一个视图——最高层级视图（top view），它占满了窗体整个内容区域，跟随窗体大小变化，作为其他视图的容器和管理器。

手动添加视图通过调用BWindow的成员函数AddChild()。添加的视图与最高等级视图形成层级结构：

            Top View        
             ___|___        
            |       |
          View1   View2
                     
添加的视图可以在同一个层级，也可以互相嵌套。将一个视图放入另一个视图同样利用AddChild()：

    view1->AddChild(view2);

### II-3 Coordinate System / 坐标系

协调系统用来协调窗体及其内部的view位置的协调。

(1) 全局坐标系

系统定义了每个像素的坐标对（x，y），x指该点到屏幕左边的像素数，y指该点到屏幕顶部的像素数。

(2) 窗体和视图坐标系

窗体的坐标位置是相对屏幕左上角的全局坐标系。但视图的坐标位置则是相对于其容器（窗体或母视图）左上角，而不是屏幕。
![Coordinate systems](/images/haiku-notes/5_CoordinateSystems.png)

示例：

    void MyHelloView::Draw(BRect)
    {
        BRect frame = Bounds();
        StrokeRect(frame);
        MovePenTo(BPoint(10.0, 30.0));
        DrawString("Hello, My World!");
    }
    
    * Bounds()：返回View相对于自身的矩形坐标，左、上均为0，右、下分别是View的宽、高。要获得view相对于容器的坐标需要调用Frame()。

### II-4 视图View类要点

 * BView(BRect frame, const char *name, int32 resizeMode, int32 flags) — 创建一个新的视图。 
 * void SetViewColor(uint8 red, uint8 green, unit8 blue)
   — 设置视图的背景颜色。 
 * void Invalidate(void) — 强制 BView 重绘自己。 
 * void AddChild(BView *child) — 将一个BView（或其子类）附加到视图。

## III Messages

应用服务（Application Server）通过向应用程序传递系统消息（system Messages），让其感知用户操作。

### III-1 系统消息 / System Messages

具体的，系统消息是从应用服务传递给消息队列BLooper的对象，由应用服务决定消息传给哪个对象。BApplication和BWindow类都继承自BLooper，所以它们的对象都可以接收消息，分别称为应用消息（Application Messages）和界面消息（Interface Messages）。

(1) 系统消息分发 / System message dispatching

looper对象收到系统消息以后，通过调用虚钩子函数（virtual hook function）处理或分发消息。虚函数便于用户自己定义的函数覆盖。例如
：B_ABOUT_REQUESTED, B_KEY_DOWN, and B_MOUSE_DOWN等系统消息对应的AboutRequested(), KeyDown(), and MouseDown()等虚函数，可以定义为用户自己的操作。

(2) 钩子函数的种类 / Types of hook functions

* 对某些系统消息，系统定义的钩子函数处理消息指定的所有工作，如B_ZOOM消息对应的窗体类子函数Zoom()。可以自定义完全覆盖掉这些钩子函数。
* 对另一些系统消息，钩子函数处理消息指定的大部分工作，自定义的钩子函数完成增加的功能，还可以调用原版的钩子函数，完成原有的功能。如，B_SCREEN_CHANGED对应的钩子函数ScreenChanged()。
* 还有一些系统消息，将钩子函数的实现完全交给用户自定义，如B_KEY_DOWN、B_MOUSE_DOWN对应的KeyDown()、MouseDown()完全需要用户完成。

(3) 界面消息 / Interface messages

* B_KEY_DOWN：
用户按下字符按键，该消息发送给活动窗体。接收窗体调用/激活相应BView类的钩子函数KeyDown()，用户在其中定义相应操作。
* B_KEY_UP：
用户释放字符按键，该消息发送给活动窗体。接收窗体调用/激活相应BView类的钩子函数KeyUp()，用户在其中定义相应操作。一般来说程序只响应按下消息，而忽略接下来的释放消息。
* B_MOUSE_DOWN：
用户按下鼠标按键，该消息发送给鼠标所在窗体。接收窗体调用/激活相应BView类的钩子函数MouseDown()，用户在其中定义相应操作。
* B_MOUSE_UP：
用户释放鼠标按键，该消息发送给鼠标按下影响的窗体。接收窗体调用/激活相应BView类的钩子函数MouseUp()，用户在其中定义相应操作。一般来说程序只响应按下消息，而忽略接下来的释放消息。
* B_MOUSE_MOVED：
用户移动鼠标，该消息发送给鼠标光标所在的窗体。若用户拖动鼠标，则应用服务重复发出B_MOUSE_MOVED消息。若鼠标从一个窗体移动到另一个窗体，则消息发给新窗体。若鼠标在桌面移动，则消息发给Tracker的桌面窗体。

### III-2 鼠标点击和视图 / Mouse Clicks and Views

应用服务将鼠标按下消息传给鼠标光标所在窗体的相应视图，该视图的MouseDown()钩子函数被激活。该子函数是空的，若用户不用自定义函数覆盖掉它，那么就没有任何反应。
用户自定义钩子函数，首先在希望响应的视图类中，声明钩子虚函数：

    class MyHelloView : public BView {
        public:
                        MyHelloView(BRect frame, char *name);
            virtual void AttachedToWindow();
            virtual void Draw(BRect updateRect);
            virtual void MouseDown(BPoint point);
    };

BPoint point变量保存了应用服务传过来的鼠标按下时光标位置，(point.x、point.y)为位置坐标。

在视图实现中，定义钩子函数的功能实现：

	void MyHelloView::MouseDown(BPoint point)
	{
    	//功能实现
	}

### III-3 按键和视图 / Key Presses and Views

上节中判断鼠标按下对应的视图很简单，就是光标所在视图。但是判断键盘按下对应的视图就不太容易，需要使用focus view。

(1) 焦点视图 / Focus view

程序可以调用某个视图的MakeFocus()函数，来将该视图设为焦点视图。如，鼠标按下后将对应视图设为焦点视图：

    void MyHelloView::MouseDown(BPoint point)
    {
        MakeFocus();
    }

-----------------------------
__注__：  本篇内容主要来自参考文献[1]

本篇就是这些内容，如有错漏之处，请不吝赐教。更多细节可参考后边的参考文献和扩展阅读。希望随着学习的深入，能有更多的内容与大家分享。

首发地址：[Github pages《Don Liu's Blog》](http://doncn.github.io/blog)
Don Liu Copyright © 2013-2015， Email：donliucn@gmail.com
  
**本篇创建于：**2014-12-14，**最后修改：**2015-01-11 v1.0

-----------------------------
###参考文献及扩展阅读：###
[1] [Programming the Be Operating System](http://www.haiku-os.org/legacy-docs/programming_the_be_operating_system.pdf)  
[2] [Learning to Program with Haiku, Lesson 15](http://darkwyrm.beemulated.net/downloads/pdf/Learning%20to%20Program%20With%20Haiku%20Lesson%2015.pdf)  
[3] [Haiku用户指南（中文）](http://www.haiku-os.org/docs/userguide/zh_CN/contents.html)  
[4] [Documents：包含用户使用及编程指南](http://www.haiku-os.org/documents)  
[5] [Articles：主要是历年来Haiku开发人员的写的一些关于Haiku开发相关文章](http://www.haiku-os.org/articles)  
[6] [Development：Haiku开发相关资源](https://www.haiku-os.org/development)  
