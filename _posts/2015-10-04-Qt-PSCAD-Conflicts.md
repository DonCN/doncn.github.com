---
layout: post
title: Qt MinGW编译错误，与PSCAD fortran编译器冲突 
summary: 在Windows7下安装Qt + MinGW，安装完成后的编译示例出错，显示“mingw32-make[1] *** [debug/main.o] Error 1 ”。最后终于在windows的变量设置时发现了问题所在，原来是跟电力系统仿真软件PSCAD的EGCS Fortran编译器的环境变量冲突了。 
categories: [技术, 电力]  
tags: [技术, 电力]  
published: true  
---

# {{ page.title }} #

{{page.summary}}

## 问题及解决简述
几年来，我在Windows7下安装Qt + MinGW的次数加起来几十上百次，每次都是安装完成后的编译示例出错，错误信息在中英文网络中搜遍了，各种方法都试过还是不行。今天，在试了五六遍以后终于在windows的变量设置时发现了问题所在，原来是跟电力系统仿真软件PSCAD的EGCS Fortran编译器的环境变量冲突了，删除其环境变量（GCC_EXEC_PREFIX = c:\progra~2\egcs\lib\gcc-lib\）就可以编译通过。

## 安装过程及错误处理过程详述：
1. 下载
下载MinGW版本的QT（qt-opensource-windows-x86- mingw492-5.5.0.exe）。

2. 安装
按照提示安装，在选择组件时，注意要在Qt - Tools中选择MinGW，这样就不用再另外下载安装它了。其他按照默认选择即可。

3. 配置
安装完毕后，在Qt Creator的工具 - 选项 - 构建和运行 - 构建套件(Kits)标签页中检查，此时的自动检测中应该有“Desktop Qt 5.5.0 MinGW 32bit (默认)”。这说明软件自动检测到了Qt Versions、编译器、Debugger，否则需要自己手动设置，具体方法网上有，这里不详述。

4. 创建新工程
创建新的工程 Application - Qt Widgets Application空窗体程序，作为示例验证安装正确。创建完成，编译运行看编译结果，若成果则出现一个空白窗体。

5. 缺少环境变量，编译出错
编译出错，在提示的“问题”中显示“CreateProcess: No such file or directory”，在“编译输出”中有详细的提示，说明是g++出错。

6. 补充环境变量
解决这个错误需要设置环境变量：桌面的计算机图标右键 属性 - 高级系统设置 - 系统属性 - 高级 - 环境变量 - 系统变量 - Path 中增加Qt和MinGW的路径：C:\Qt\Qt5.5.0\5.5\mingw492_32\bin;C:\Qt\Qt5.5.0\Tools\mingw492_32\bin;C:\Qt\Qt5.5.0\Tools\mingw492_32\libexec\gcc\i686-w64-mingw32\4.9.2; 上述这三个路径需要根据实际安装路径修改，尤其需要注意的是上述第三个libexec路径一定要设置，否则还会报错。若是一般的win7下安装，到这里就完成设置，一般就不会编译报错了。

7. 与PSCAD编译器的环境变量冲突导致编译出错
但是，我这里还是出现了错误，在“编译输出”中错误信息包含：“mingw32-make[1]: *** [debug/main.o] Error 1 ”。

8. 解决与PSCAD编译器的环境变量冲突问题
再次打开系统变量，发现其中有个变量名为“GCC_EXEC_PREFIX”，它的值是“c:\progra~2\egcs\lib\gcc-lib\”，这个变量是我的专业仿真软件PSCAD用的fortran编译器的路径，和6.中的第三个路径冲突，只有将这个变量删除Qt才能编译运行。但是删除这个变量后，PSCAD又不能运行，我的解决办法是，用Qt时在环境变量中删除“GCC_EXEC_PREFIX”变量和它的值，用PSCAD时，再将这个变量和值加上。



首发地址：[Github pages《Don Liu's Blog》](http://doncn.github.io/blog)
Don Liu Copyright © 2013-2018， Email：donliucn@gmail.com


