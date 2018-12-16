---
layout: post
title: Haiku 操作系统的安装 
summary: 本篇简单介绍了Haiku操作系统的安装流程<p> ![安装界面Installer](/images/haiku-notes/Haiku_Installer.png) <p>
categories: [Haiku OS]  
tags: [Haiku OS]  
published: true  
---

# {{ page.title }} #

{{page.summary}}


很久没写关于Haiku的东西了。这两天因为重装Haiku，发现官网提供的将Haiku安装到U盘的方法实在是简单的令人发指，真正做到了傻瓜式安装，值得一书。

## 下载Haiku的最新测试版
Haiku 32-bit Hybrid (Compatible, Stable)，下载地址：https://download.haiku-os.org/nightly-images/x86_gcc2_hybrid/。
Haiku 64-bit (Modern, Fast)，下载地址：https://download.haiku-os.org/nightly-images/x86_64/。
选择最新的测试版，下载后解压得到Anyboot.ISO备用。

## 下载U盘写入工具Etcher
官网下载地址：https://etcher.io/，
百度网盘：https://pan.baidu.com/s/1ljTiTplH0A_4z1uFL1_Wsg。

## 制作U盘操作系统
制作步骤：
![Etcher](/images/haiku-notes/Etcher.gif)
（1）在Etcher界面最左侧"Select image"，选择Haiku安装镜像Anyboot.ISO。
（2）插入U盘，U盘会自动显示到Etcher的中间“Select drive”图标。
（3）检查中间“Select drive”图标下显示的是否是要安装的U盘，否则手动更改。
（4）鼠标点击Etcher界面最右侧"Flash"，将自动完成写入和校验。

完成上述几步，U盘Haiku操作系统就制作完成了，可以U盘启动，在U盘中运行Haiku操作系统。也可以运行Haiku系统后，在程序列表中找到Installer，用Installer将Haiku安装的物理硬盘。

官方的安装指南：[Installation Guide]https://www.haiku-os.org/get-haiku/installation-guide/）

也可以在虚拟机中安装Haiku试玩：[Virtualizing Haiku in VirtualBox](https://www.haiku-os.org/guides/virtualizing/virtualbox#part_iso)



首发地址：[Github pages《Don Liu's Blog》](http://doncn.github.io/blog)
Don Liu Copyright © 2013-2018， Email：donliucn@gmail.com


