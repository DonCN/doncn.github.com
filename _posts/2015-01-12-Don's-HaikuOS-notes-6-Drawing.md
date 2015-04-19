---
layout: post
title: Don's HaikuOS Notes 6:Drawing v1.0  
summary: 本篇深入介绍了Haiku编程中的绘图（drawing），主要包括Colors颜色、Patterns图样、The Drawing Pen绘图笔、Shapes形状。<p>
categories: [Haiku OS, HaikuOS notes]  
tags: [Haiku OS, HaikuOS notes]  
published: true  
---

# {{ page.title }} #

{{page.summary}}


《Don's HaikuOS Notes》系列之前已有五篇：

 1. [Don's HaikuOS Notes 1:Haiku操作系统简介...](http://doncn.github.io/2013/12/28/Don%27s-HaikuOS-notes-1-introduce.html)
：介绍了Haiku操作系统的历史、特性。

 2. [Don's HaikuOS Notes 2:Haiku操作系统架构、开发包、消息机制...](http://doncn.github.io/2014/04/27/Don%27s-HaikuOS-notes-2-OS-Layers-DevKits.html)
：介绍了系统架构，以及它的三个层级：内核层（kernel）、服务层（server）、软件开发包层（software kits），以及开发包的继承关系，多线程的实现原理

 3. [Don's HaikuOS Notes 3:Haiku编程简介——创建窗体程序及消息演示](http://doncn.github.io/2014/05/02/Don%27s-HaikuOS-notes-3-Programming-Introduce-Message.html)
：以简单的图形界面程序为例介绍了Haiku的简单的程序开发及其消息机制。

 4. [Don's HaikuOS Notes 4:More About API — Kits、Classes、Functions](http://doncn.github.io/2014/07/31/Don%27s-HaikuOS-notes-4-More%20about%20API.html)
：结合代码实例，进一步介绍Haiku/BeOS的开发包Kits，主要是Application、Interface、Storage这三个开发包。

 5. [Don's HaikuOS Notes 5:Windows、Views and Messages](http://doncn.github.io/2014/12/14/Don%27s-HaikuOS-notes-5-Windows%20Views%20and%20Messages.html)
：深入介绍了Haiku的Windows、Views和Messages的使用。

本篇结合代码实例，深入介绍Haiku编程的绘图（drawing），主要包括Colors、Patterns、The Drawing Pen、Shapes。

Be或Haiku图形界面的绘图总是在视图Views中调用其子函数draw()完成。绘图的很多特性是在视图层级定义的，所以绘图可以直接使用视图的设定。下面分4部分介绍Haiku的绘图是如何实现的。

## I Colors

BeOS/Haiku利用多种颜色空间（color spaces）定义了颜色。每个颜色空间都对应一个常数，表征了用多少位二进制来表示一个像素的颜色，比如颜色空间B_COLOR_8_BIT表示用8位表示颜色，这样这个颜色空间就包含2的8次方种颜色。


* B_GRAY1：用1位表示灰色，则只有黑1和白0两种颜色。
* B_GRAY8：用8位表示灰色，包含从白到黑的256级灰色。
* B_CMAP8：用8位表示色图（color map），对应色图的256种颜色。各种程序用的色图的数值都是一致的。
* B_RGB15：用15位表示RBG颜色，各有5位分别表示R/G/B。
* B_RGB32：用32位表示RBG颜色，其中每8位分别表示R/G/B，剩余8位忽略。
* B_RGBA32：同上，每8位分别表示R/G/B，但是用最后8位表示透明度（alpha）。

### I-1 RGB Color System

RGB颜色系统是用的最多的一种，在BeOS/Haiku中是这样定义的：

	typedef struct {
		uint8 red;
		uint8 green;
		Uint8 blue;
		uint8 alpha;
	} rgb_color

可以在定义时候初始化：

	rgb_color redColor = {255, 0, 0, 255};

或者之后赋值;

	rgb_color blueColor;
	blueColor.red = 0;
	blueColor.green = 0;
	blueColor.blue = 255;
	blueColor.alpha = 255;

### I-2 High and Low Colors

视图的颜色是用高、低和高低混合颜色（B_SOLID_HIGH、B_SOLID_LOW、B_MIXED_COLORS）来填充的，默认的高颜色是黑色，默认的低颜色是白色。还可以通过如下两个函数指定高和低颜色（high and low colors）：

	SetHighColor(redColor);
	SetLowColor(blueColor);

指定了高/低颜色就可以将其填入视图区域中：

	rgb_color redColor = {255, 0, 0, 255};
	BRect aRect(10, 10, 110, 110);
	SetHighColor(redColor);
	FillRect(aRect, B_SOLID_HIGH);

视图中的颜色是首先填充一个8×8像素的小方块（称为pattern，将在下一节详细介绍）。然后将这个颜色小方块铺满指定区域。

还可以通过两个函数来获取当前视图的高低颜色：

	currentHighColor = HighColor();
	currentLowColor = LowColor();

要忽略最后的8位透明度，则可设置其为255。

### I-3 The View Color (Background)

上节的设置高低颜色不改变视图的背景颜色，一个视图默认的背景颜色是白色，可以通过SetViewColor()函数设置视图的背景颜色：

	rgb_color purpleColor = {255, 0, 255, 255};
	SetViewColor(purpleColor);

### I-4 Color Control View

BeOS/Haiku提供了BColorControl类，允许用户自己选择颜色。使用时首先要创建一个BColorControl类对象，并赋予参数：

	BColorControl *aColorControl;//创建对象
	BPoint leftTop(20.0, 50.0); //参数1，指定颜色面板在视图中的位置
	color_control_layout matrix = B_CELLS_16x16;//参数2，若用户显示器设置为8位每像素，则256色用矩阵形式显示，矩阵有以下多种：B_CELLS_4x64, B_CELLS_8x32, B_CELLS_16x16, B_CELLS_32x8, or B_CELLS_64x4.
	long cellSide = 16;//参数3，每个色块（cell）的大小
	aColorControl = new BColorControl(leftTop, matrix, cellSide, "ColorControl");//为对象赋参数
	AddChild(aColorControl);//将颜色控制面板加入视图。

创建了颜色控制面板，用户选择（8位选一个cell块，32位则选RBG三部分）后，如何得到用户选择的颜色呢？需要调用BColorControl类的成员函数ValueAsColor()：

	rgb_color userColorChoice;
	userColorChoice = aColorControl->ValueAsColor();

按照上述步骤在视图中定义了颜色控制面板，如何在视图中绘图和获取颜色呢？如下：

	void MyDrawView::Draw(BRect)
	{
		MovePenTo(BPoint(20.0, 20.0));//移动画笔到开始绘图点
		DrawString("Choose a color below, then move the cursor");//在视图输入一行文本。
		MovePenTo(BPoint(20.0, 35.0));//移动画笔到下一行
		DrawString("outside of the color control and click the mouse button");//在视图输入第二行文本。
	}

在鼠标点击响应函数中选取颜色并填充视图区域：

	void MyDrawView::MouseDown(BPoint point)
	{
		BRect aRect(20.0, 330.0, 350.0, 340.0);
		rgb_color userColorChoice;
		userColorChoice = fColorControl->ValueAsColor();
		SetHighColor(userColorChoice);
		FillRect(aRect, B_SOLID_HIGH);
	}

或者直接将鼠标响应函数中内容移入Draw函数，而在鼠标点击响应函数中：

	void MyDrawView::MouseDown(BPoint point)
	{
		Invalidate();
	}

这样，点击鼠标后，视图重绘，就刷新了视图中选定区域aRect的颜色。两种颜色控制面板如下图所示：
![视图中的两种颜色控制面板](/images/haiku-notes/6_ColorControlPanel.png)

上述例子中有个问题就是，选择的颜色改变了高颜色的值，这样在使用高颜色重绘整个视图时候，就不仅仅在选定的aRect区域使用选定颜色，而是整个视图都改变成了选择的颜色。因此，应该在选择填充颜色以后应还原高颜色：

	origHighColor = HighColor();//改变高颜色前保存原始高颜色
	userColorChoice = fColorControl->ValueAsColor();
	SetHighColor(userColorChoice);
	FillRect(aRect, B_SOLID_HIGH);//填充新选颜色
	SetHighColor(origHighColor);//还原高颜色

## II 图样 / Patterns

图样Pattern是一个颜色为目前的高或低颜色8×8像素的区域，用来填充不同大小、形状的区域。

### II-1 Be-Defined Patterns

我们已经遇到过3种操作系统定义的图样：

    B_SOLID_HIGH:高颜色
    B_SOLID_LOW:低颜色
    B_MIXED_COLORS：混合颜色将高、低颜色像国际象棋棋盘一样分布到像素块，再填入矩形区域，由于像素块很小，很密集，又由高低两种颜色组成，整体看起来，就是高低颜色混合成的颜色。例如：FillRect(aRect, B_MIXED_COLORS);

BView类包含多种画图或填充的成员函数，例如StrokeRect()、StrokePolygon()可以利用图样画出比单像素更粗的矩形或多边形，FillRect()、FillPolygon()可以利用图样填充矩形或多边形区域。但需注意的是，图样参数是可选的，省略时默认的图样是B_SOLID_HIGH，例如：

    FillRect(rect1, B_SOLID_HIGH);
    FillRect(rect2);//省略图样参数，和上边语句一样效果。

### II-2 Application-Defined Patterns

上节利用系统定义的图样，其实是说明利用当前的高或低颜色。此外，程序还可以自定义图样，能更好，更灵活的实现用户的需求。

(1) Bit definition of a pattern

8位二进制颜色可以用2个十六进制数字表示：11001100=0xcc。

(2) The pattern datatype

系统定义pattern为8个字节，共8×8=64位（一个字节为8位，用一组十六进制数字表示），如上的三个图样就是这样定义的：

    typedef struct {
        uchar data[8];//每个字节数字范围0x00-0xff
    } pattern

(3) Using a pattern variable

一旦定义了图样变量，就可以像系统定义的图样一样使用了。例如：

    void MyDrawView::Draw(BRect)
    {
        BRect aRect;
        pattern stripePattern = {0xcc, 0x66, 0x33, 0x99, 0xcc, 0x66, 0x33, 0x99};
        aRect.Set(10.0, 10.0, 110.0, 110.0);
        FillRect(aRect, stripePattern);
    }

上述代码得到的图像如下，经过Magnify放大工具放大显示图像细节。
![Application Defined Pattern](/images/haiku-notes/6_ApplicatioinDefinedPattern.png)

## III 画笔 / The Drawing Pen
使用画笔来描述视图的绘图环境，比如绘图位置、线条粗细等。

### III-1 画笔位置 / Pen Location
前边画矩形不用画笔，而是用Fillrect():
`BRect aRect(10.0, 10.0, 110.0, 110.0);
FillRect(aRect, B_SOLID_HIGH);`

使用画笔首先要将画笔移动到初始位置：MovePenTo()以视图左上角位置为原点，MovePenBy()以画笔当前位置为原点。
`MovePenTo(BPoint(30.0, 40.0));
MovePenTo(30.0, 40.0);
DrawString("A");`

### III-2 画笔大小 / Pen Size
函数StrokeRect(aRect)画出矩形的边框，边框的粗细受当前画笔大小的影响。

1）设定画笔大小：SetPenSize()
`SetPenSize(3.0); 
StrokeRect(aRect);`

2）获取画笔大小：PenSize()
`savedPenSize = PenSize();
SetPenSize(3.0);
StrokeRect(aRect);
SetPenSize(savedPenSize);`

## IV 形状 / Shapes

1)BPoint定义点：
`BPoint point1;
BPoint point2;
point1.Set(100.0, 200.0);
point2.x = 100.0;
point2.y = 200.0;`

2)划线：StrokeLine()
StrokeLine(point1, point2);
StrokeLine(point1, point2, B_SOLID_HIGH);
MovePenTo(start2);
StrokELine(end2, B_SOLID_LOW);

3)矩形
StrokeRect(outerRect,B_MIXED_COLORS);//画出矩形，第二个参数可省略
FillRect(innerRect,B_MIXED_COLORS);//填充矩形，第二个参数可省略

4)圆角矩形Round rectangles，后两个参数指出圆角大小
`StrokeRoundRect(aRect, 20.0, 20.0);
FillRoundRect(aRect, 30.0, 30.0);`

5)椭圆Ellipses：StrokeEllipse() or FillEllipse()
两种参数：
`StrokeEllipse(aRect);
FillEllipse(aRect);`
第二种：
`rgb_color blueColor = {0, 0, 255, 255};
BPoint center(100.0, 100.0);
float xRadius = 40.0;
float yRadius = 60.0;
SetLowColor(blueColor);
FillEllipse(center, xRadius, yRadius, B_MIXED_COLORS);
StrokeEllipse(center, xRadius, yRadius);`

6)五角形Polygons：StrokePolygon(aPolygon),FillPolygon(aPolygon)
7)三角形StrokeTriangle(point1, point2, point3);FillTriangle().

8)区域region
定义区域对象和多个矩形：
BRect aRect;
BRegion *aRegion;
aRegion = new BRegion();
aRect.Set(20.0, 20.0, 70.0, 70.0);
aRegion->Include(aRect);
aRect.Set(50.0, 50.0, 150.0, 100.0);
aRegion->Include(aRect);
填充区域：
FillRegion(aRegion);

## VI 图片 / Pictures
图片BPicture类型对象可以包含多个不同形状，通过调用图片对象，可以一次绘出多种不同形状。

### III-1 创建图片 / Setting up a picture

图片对象通过new来申请内存，通过BView的成员函数BeginPicture()来创建，图片画完之后需要调用EndPicture()返回完整的图片对象：

	BPicture *aPicture;
	BeginPicture(new BPicture);
		BRect aRect;
		aRect.Set(10.0, 10.0, 30.0, 30.0);
		FillRect(aRect);
		MovePenTo(40.0, 10.0);
		StrokeLine(BPoint(60.0, 10.0));
	aPicture = EndPicture();
可以在上述代码之后给已有的图片aPicture添加图形:
	
	BeginPicture(aPicture);
		MovePEnTo(10.0, 40.0);
		StrokeLine(BPoint(10.0, 60.0));
	aPicture = EndPicture();

### III-2 绘制图片 / Drawing a picture

图片创建后需要调用BView的成员函数DrawPicture()绘制图片：

	MovePenTo(100.0, 20.0);
	DrawPicture(aPicture);

或：

	DrawPicture(aPicture, BPoint(100.0, 250.0);


-----------------------------
__注__：  本篇内容主要来自参考文献[1]，可能与Haiku有部分出入，若发现请不吝指出。

本篇就是这些内容，如有错漏之处，请不吝赐教。更多细节可参考后边的参考文献和扩展阅读。希望随着学习的深入，能有更多的内容与大家分享。

首发地址：[Github pages《Don Liu's Blog》](http://doncn.github.io/blog)
Don Liu Copyright © 2013-2015， Email：donliucn@gmail.com
  
**本篇创建于：**2015-01-11，**最后修改：**2015-04-19 v1.0

-----------------------------
###参考文献及扩展阅读：###
[1] [Programming the Be Operating System](http://www.haiku-os.org/legacy-docs/programming_the_be_operating_system.pdf)  
[2] [Learning to Program with Haiku, Lesson 15](http://darkwyrm.beemulated.net/downloads/pdf/Learning%20to%20Program%20With%20Haiku%20Lesson%2015.pdf)
[3] [Haiku用户指南（中文）](http://www.haiku-os.org/docs/userguide/zh_CN/contents.html)
[4] [Documents：包含用户使用及编程指南](http://www.haiku-os.org/documents)
[5] [Articles：主要是历年来Haiku开发人员的写的一些关于Haiku开发相关文章](http://www.haiku-os.org/articles)
[6] [Development：Haiku开发相关资源](https://www.haiku-os.org/development)
