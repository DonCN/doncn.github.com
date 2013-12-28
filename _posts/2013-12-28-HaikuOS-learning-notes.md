---
layout: post
title: HaikuOS学习笔记
summary: Haiku OS是一个开源、免费的操作系统，主要面向个人计算机。它兼容、继承了BeOS的理念，是一个快速、简洁优雅、易学易用，而且非常强大的操作系统。它有着
- 统一的、简洁优雅的全图形用户界面；
- 定制的快速响应的内核；
- 对多处理器、多线程的完全支持和内存保护；
- 优雅的内置程序间通讯；
- 模块化设计和面向对象API便于快速开发；
- 先进的数据库式、全日志的64位文件系统；
- 基于属性的快速索引和查询。
它的众多独特优点和特性让我非常着迷，这篇文章是我的HaikuOS学习笔记和相关资源链接。<p><center><a href="/images/HaikuOS-desktop.png" target="_blank"><img src="/images/HaikuOS-desktop.png" alt="HaikuOS-desktop" height="500" width="633"></a></center></p>
categories: [Haiku OS]
tags: [Haiku OS]
published: true
---

# {{ page.title }} #

{{page.summary}}

## 历史 ##
2001年，前Apple公司主管Jean-Louse Gassee创办的Be公司被Palm公司收购，BeOS([BeOS Wiki](http://en.wikipedia.org/wiki/BeOS)，[中文维基](http://zh.wikipedia.org/wiki/BeOS)，[百科](http://baike.baidu.com/link?url=RlMCN12Pq2RYX_9z1C_GsXaWVP7kK3e2SZF_PDZ6ptjrlRBS28YSQ-jUXIuAc4yx))这个领先于时代，却又命运多舛的多媒体操作系统也走到了尽头。一群忠实爱好者开始了OpenBeOS开源项目，目标是创立一个与BeOS兼容的自由操作系统。2003年，在纽约州成立了一个非营利的组织 [Haiku,Inc](http://www.haiku-inc.org/) 以支持该项目。2004年，由于版权原因，项目名称改为Haiku(一种日本古典短诗-俳句的发音)。2009年9月，经过世界各地的十几个核心开发人员8年的努力，项目组终于发布了第一个测试版Haiku R1/Alpha1。目前，已经发布了4个Alpha版本，即将进入Beta发布阶段。

HaikuOS官方主页：<http://www.haiku-os.org/><p>
HaikuOS中文社区：<http://haiku-cn.org/><p>
HaikuOS测试版本下载：<http://haiku-files.org/haiku/development/>


## 设计理念 ##
HaikuOS的设计理念继承于BeOS，采用先进的64位BeFS文件系统，支持多处理器，其多媒体性能异常优越。Haiku能够充分利用多处理器系统通过模块化的I/O带宽，多线程，抢断式的多任务和被称为BFS的定制64位日志文件系统。Haiku的GUI遵循清晰整洁的设计原理而开发。其API是用C++编写而成，非常容易编程。虽非源于Unix的操作系统，但其实现了POSIX兼容，并通过Bash shell 命令行界面来访问。

## 优缺点 ##
### 优点 ###
- 优秀的性能
- 易于安装配置
- 清晰的GUI, 强大的命令行
- 均衡的多处理技术
- 面向对象
- 32 个工作空间（桌面）64位
- 全日志的文件系统
- 类似数据库的文件系统
- 内存保护
- 无毒
- 遵循POSIX标准
- 支持各种不同的文件系统
- 整洁的编程API
- 优雅的内置通讯系统 
### 缺点 ###
- 有限的硬件支持
- 有限的可选应用程序
- 有限的办公文档兼容性
- 勉强的系统维护
- 非标准的web浏览器