---
layout: post 
title: 2001：一个BeOS难民的故事(译文)(进行中...) 
summary: 本文译自[Tales of a BeOS Refugee](http://www.birdhouse.org/beos/refugee/) - Scot Hacker。原作者Scot Hacker是[BeOS Bible](http://www.amazon.com/BeOS-Bible-The-Scot-Hacker/dp/0201353776)的作者。这篇文章是他在2001年[BeOS](http://zh.wikipedia.org/zh-cn/BeOS)操作系统停止开发之后，无奈尝试转向其他操作系统，经历一番试用比较，最终转到MAC OS X。文中在多个方面比较了两种操作系统的异同，尤其是对BeOS的一些独特优势做了深入的介绍。虽然BeOS已经停止了开发，但是很多忠诚爱好者还是不愿放弃，其中一批人在2001年开始了旨在重现BeOS的Haiku OS([英文主页](http://haiku-os.org/))开源项目，目前Haiku处于Beta测试阶段，在重现BeOS的同时也做了大量的改进。自从两年前发现了Haiku，我也成了她的忠诚粉丝。这篇文章虽然成于2001年，但是现在读来依然有趣，也非常有助于对Haiku OS的了解，特地翻译出来，希望大家喜欢。   
categories: [Haiku OS]  
tags: [Haiku OS]  
published: true  
---

# {{ page.title }} #

{{page.summary}}


## 一个BeOS难民的故事 / Tales of a BeOS Refugee

—— 从BeOS到OS X (也试用过Windows、Linux) / From BeOS to OS X (by way of Windows and Linux)

<i>这个故事讲述了一个BeOS难民丧失了对计算机的未来的信仰，进而转向Windows，却发现它及其糟糕，linux也会让你拔光自己的头发，最后在Mac OS X那里才再次找到计算机的乐趣。</i>

<b>注: 这篇文章发表后收到500多封邮件回复. 因此，我写了一篇附文作为对这篇文章的补充，也作为这些邮件的回应，不再对每篇来信一一回复。附文请见 <a href="http://www.birdhouse.org/beos/refugee/redux.html">BeOS Refugee Redux</a> </b>

### 走出煎熬... / Out of the Frying Pan...

大部分用户都是渐进的转到Mac OS X上 - 他们已经用了多年的Mac计算机, 经历了Win32(即windows)和*nix用户抱怨Mac OS糟糕的内存管理、过时的协作式多任务处理(cooperative multitasking)和缓慢的文件系统。 更糟的是，反对者们向来喜欢指责Mac OS蹩脚的单键鼠标操作习惯和缺乏类似命令行的功能。

我知道所有这些对Mac OS的挖苦和嘲讽，因为我自己曾经就是一个Mac反对者。我承认，在一些聚会和论坛等公共场所，我公开说过我不喜欢Mac计算机和Mac OS的一切(尽管我很欣赏Mac光滑、细腻的图形界面)。

德语中有个形容这种放肆挖苦的词叫<i>Schadenfreude(幸灾乐祸)</i>，简单翻译过来就是：将自己的快乐建立在别人的痛苦之上。对许多 Windows和Linux用户来说，仅仅自己不使用Mac OS还不够，还要向别人宣扬自己对Mac的厌恶。

是的，我有时是对Mac世界的遭遇幸灾乐祸，也激怒了很多人。但我不是个坏人，我没为此骄傲。我只是对我的计算机要求很多，可Mac却只能满足我很少的苛求，却又有太多让我不满意。但是最近，我又看到了希望，我收回对Mac的挖苦，为我这个曾经的Mac反对者道歉。不止于此，我应该感谢OS X，我现在是一个真诚的Mac OS爱好者了。让过去的都随风而去吧。

需要指出的是，我从来不是爱好Windows或Linux的Mac反对者，我曾经是爱好BeOS的Mac反对者，我同样不喜欢Windows或Linux。

在90年代中期，我发现了BeOS，并喜欢上了它。我第一次发现了一个真正快速、高效的操作系统，为满足未来的个人计算而重新设计，采用了大量的现代科技和设计理念，同样拥有Unix那样的命令行。我发现了它同时具有Mac那样的优雅和Unix的强大(这超前Mac达到同等水平很多年)。 我开始了BeOS的专业写作，我创立了<a href="http://www.betips.net/" target="_blank">BeOS Tip Server</a>，创作了<a href="http://www.birdhouse.org/beos/bible/" target="_blank">The BeOS Bible</a>。
对我而言，BeOS是一个让我非常满意的操作系统，人们很快就会发现这一点。

<blockquote>
如果你不熟悉造就BeOS的全部科技，我会在下面一一介绍。这篇文章<a href="http://birdhouse.org/beos/byte/29-10000ft/" target="_blank">BeOS: The 10,000-Foot View</a>是一个简介。如果你对BeOS一点都不了解，你应该浏览下这篇文章。
</blockquote>

很显然，事情并没有完全按照Be的意愿发展，在90年代末，BeOS就不再向上发展。Be没能获得市场的成功，风险投资也渐渐枯竭。当Be宣布将转向网络应用的操作系统，大部分人意识到了不妙。应用程序开发者和用户开始离开这个平台，不再讨论半个世界都运行着BeOS会是怎样，转而讨论如何让这个平台继续活下去。 

在“焦点转移”之后，BeOS的场面就沉闷起来。BeOS用户并未奢求彻底的逆转，只是希望尽量将未完成的代码完成，私下交换着Be未完成的网络模块的代码，同时无奈的看着越来越多的Be不支持的硬件涌现。

我觉得是时候继续向前，重新进入BeOS之外的PC世界了。在5年的BeOS时光之后，我再次回归到Windows(Win2K)。开始还好，自从我上次(5年前)使用Windows以后，它有了长足的进步，有了海量的软件。我已经习惯了BeOS下有限的软件可供选择，忘记了计算机里有任何你想要的软件会是什么样子的。

但是这段快乐是如此短暂。不到一周，我就厌烦了。当然，Windows可以完成工作，海量的软件也值得探索，但是它的用户体验非常枯燥。只有功能，没有体验(All function and no 
form)。我感觉我就像工作在一个剪贴画工厂。我开始怀念使用BeOS的快乐。尽管Win2K比以前用的破烂Win95/98好太多，可Windows的使用方法多得让我难以忍受。对BeOS的深入研究让我对微软的商业行为有了深刻的认识。我无法摆脱和屈从于那深刻的厌烦之感。使用Windows让我感动虚伪和放荡。在糟糕的使用体验之间，我实在需要重新找到激情。

### ... 再获激情... / ... And Into the Fire...

那么我做了什么？我让事情变得更糟。我选择了转向Linux。我当时是怎么想的？我深入了解了Linux，我很欣赏开源软件的很多优点，但是开源同样有着深刻和棘手的问题，这些问题导致了可怕的用户体验。我了解到Mandrake被认为是最好用的Linux发行版，所以我选择了它。

经历了几次失败之后，我成功运行了Mandrake。与Linux的良好声望相反，它总是崩溃或死机。我错误的认为Linux已经发展的可以像Be那样完美的支持双处理器。错了！我把Mandrake移到单处理器PC上后，稳定问题才解决，才能正常使用这个系统。

虽然我不认同Richard Matthew Stallman的自由软件的理念：所有软件必须免费，但是投入开源国际社区还是令人深受鼓舞，也被那革命般的热情所感染。能下载和使用那么多我想要的软件的感觉不错。人们都喜欢免费。

尽管Linux用起来大部分还好，但是它的用户体验就让我发狂了。不管在命令行，还是Gnome / KDE桌面，我都没办法在程序间方便的剪切/复制/粘贴，那般痛苦让我只想撞墙。桌面上的任何体验都不完整，不舒服。软件包的安装也是无尽的依赖冲突(是的，apt-get包管理命令好多了，但是我的Debian体验比Mandrake还要糟糕)。有时，甚至软件开发者本人也不明白为什么我这里不能正常安装和使用他的软件。我折腾Linux桌面的时间比我用其工作的时间都长(一些Linux信徒认为“折腾”才是其中的目的和乐趣所在)。

别误会，我不介意使用命令行，我用起bash和tcsh来很舒适，也不喜欢使用没有Unix shell的操作系统。但我大部分时间不是在用命令行，我猜大部分用户也是如此。其他时间，我只想用成熟的程序，按我期待的方式，干净利索、快速、高效的完成我的工作。我希望所有的程序有着统一连贯的用户界面。但是，Linux程序不是一个统一的标准下开发的，它们的外观和行为缺乏统一设计。生物的多样性既是开源软件最多的优势，又是它的最大缺点，它使得Linux不管科技产业如何萧条也会继续发展(与Be相反)，同时Linux的用户体验也永远不会统一连贯。

尽管有抱怨，我还是尽力在我的Mandrake上建起了PHP/MySQL网络服务来运行betips.net网站 (我不得不关闭了之前的BeOS网络服务，因为BeOS不能全天的运行这个服务)。此外，我还在Linux机器上建立了Samba网络/打印服务。

那么我该去哪里？BeOS死了。我也不适应Windows的方式(发誓再也不用它)。我给了Linux四个月的机会来打动我，可惜失败了。不是因为它没有足够的软件，我也不介意编译软件源码。事实上，我喜欢自己动手编译软件。但是我不喜欢<i>被迫 </i>时不时的编译、修理这些软件，我只想装上软件就开始工作。

### 家的感觉 / Smells Like Home Cookin'

科技人员成天工作在操作系统提供的工作环境中，一段时间之后，这个工作环境应该给人家的感觉。但Linux从没给我这种感觉，从没让我感到家的舒适。Linux没有那种<i>风水 </i>，它的各个部分从没有统一起来、浑然一体的工作。我怀念这种在BeOS上体验，就像我和系统注定要在一起，它就是我理想的家园。在BeOS上，我几乎拥有我想要的Unix所有的功能，同时还能乐在其中。我的妻子都厌倦了我不断的抱怨Linux电脑。

半年前，我曾经给Byte网站写过一篇关于Mac OS X的文章，关于我之前对Mac OS X的良好印象。在文中，我的结论是OS X可能会达到BeOS所未达到的高度。BeOS和OS X的设计都是为了弥补Mac OS的缺陷。BeOS是由一组前苹果工程师设计和开发，Be的 执行总裁曾经领导苹果的产品研发多年。BeOS和OS X都具有Mac的优雅和Unix功能，都有很好的用户体验，并且都把多媒体的制作和播放作为一个重要目的。

在2001年的10月，我最后看了一眼Linux机器，然后去买了台Mac机器。现在，这台Linux机器仍然正常的运行着，是任务不重的没有图形界面的环境，从没出问题或者崩溃。在家有台Linux服务器也不错，它安静、可靠，不时地调整一下也很有趣。但是我估计很长时间都不会把Linux用作桌面操作系统了。

跟很多人一样，我之前也总是不愿在购买机器上花额外的钱，但这次我决定改变一下。我先买了一台PowerMac G4 867，它有60GB的硬盘、可读写的DVD驱动器和640MB的内存。正好MacWorld SF在我的机器到的前几天举办，所以之后我又及时的买到了OS X.1的升级CD。

当时不知道，在接下来的几个月里我将交织在兴奋与失望之中。我之前的一些期待将有结果，我将会发现Mac能做到的超出我的想象。我将遇到我期待的最好的个人桌面操作系统，甚至是服务器操作系统。但是同时，也会对其中的某些部分感到失望。

没有完美的操作系统，每种系统都有它的优点和不足。同样，每种系统都有好和不好的支持者。之所以称他们为不好的支持者，是因为他们只是他们宣扬的某个系统的<a href="http://www.adequacy.org/public/stories/2001.10.2.33542.4010.html" target="_blank">卫道士</a>。他们总是鼓吹他们喜欢的系统的优点，并为系统的缺点和糟糕的设计找各种理由，比如，这不是系统开发公司的错，这些错误马上就可以解决。

跟其他操作系统一样，OS X也是一个混合体。唯一能描述我从BeOS转到OS X的体验的方法也许就是我指出我对OS X的喜欢和失望之处。尽管有不足，但BeOS在某些方面树立了很高的标准，在这些方面OS X注定会令我失望了。我初始的，也许不一定正确的假设是OS X拥有BeOS所具有的所有现代操作系统的技术，并且拥有光明的前景。我认为苹果公司拥有Be公司曾经有过的那种机会：全新完美设计，没有历史负担，让用户不再背负以前的错误设计带来的历史遗留负担。这里，我忽略了苹果公司的一个重要因素：它并不是没有历史负担，他们得考虑向前兼容旧的Mac OS，并且满足数百万Mac用户的使用习惯和期望，以及过去二十多年Mac的高雅传统。

我可能会离题，这很容易。我可能正兴高采烈的讲述着OS X，转眼就开始哀叹抱怨。
 
# 很多喜欢 / A Lot To Like

### 第一印象 / First Impressions

从盒子中取出苹果PowerBook G4跟打开x86机器时可不一样。泡沫板的波浪曲线包裹着机器柔和的圆角, 即使印刷材料看起来都很诱人。你只要在USB键盘上按一个键就能打开光驱，还有按键可以控制内置的Harmon-Kardon扬声器(它的声音比起其他的内置扬声器好太多了)。按下音量控制键，桌面会有个精致的图标显示出来，然后就慢慢隐去。 手指划过苹果电脑显示器（Apple Cinema display）的小光点，屏幕上就会出现显示设置面板。显示器上的电源按钮不只是用来关掉显示器，还能通过挥手的手势让机器进入睡眠模式。

硬件之外，很难描述OS X系统界面在视觉上是如何的美。屏幕截图并不能完全表现出这点来。前面已经描述了很多OS X的动画效果--滑入位置的对话框，精灵般的窗口最小化效果，从Dock拖走图标时的幻影，等等。但更重要的是这些动画效果不只是为了吸引眼球，它们还是精心设计的操作反馈，系统通过这个反馈提示用户某物消失或下一步需要做什么。这些动画小提示足以表达含义，又不会干扰到高级用户。

在视觉上，OS X是惊人的。这并不只体现在它直接表现出来的不寻常的浅绿色界面（我对此并不介意，但我知道有人不喜欢这个），还体现在其他方面。由于显示引擎是基于矢量的，因而可以根据界面的大小调整图标大小，而不会引起图像失真。

我对系统的透明特性有着复杂的感觉。一方面，它新颖，有吸引力，有时的确有用。例如，能在另一个窗口下看到iTunes目前正在播放的歌曲就很好。感谢Tinker这个工具，使终端窗口部分透明，这样我就可以在使用命令行窗口的时候还能同时看到下面的Finder窗口的变化。

<div align="center">
<img src="/images/TalesBeOS-transparency.jpg" alt="transparency" height="212" width="633">
</div>
<i>透明效果在OS X系统中相当普遍，有时候很方便，有时候又会带来干扰，感觉很纠结呀。比如，在读到下层窗口的一个网络地址或一段数据时候会很有用。但总体来说，透明效果的目的只是为了摆酷，这对我来说还行。</i>

另一方面（这实际上是由一个苹果工程师指出的），在印刷行业人们花了很多钱研究让纸张不透明，这样相邻页的文字就不会透过纸张互相干扰，而OS X花费宝贵的CPU周期来达到相反的效果。透明度有时让事情看起来很杂乱，难以阅读。

可惜的是，OS X的界面目前是不可定制的。BeOS却能让你在BeOS, Windows, AmigaOS, and Mac OS9等不同窗口外观之间切换。提供这么多的窗口皮肤，多大的勇气啊！（What about the guts?）


### 网络的重生 / Networking Nirvana

网络和多用户功能关系相近，所以在这里一起讨论。

BeOS一个失败的可能原因就是他们没有实现多用户功能。Be的文件系统有支持多用户的能力，应用可以实现这些，但系统级别的执行权限的限制却很少，也没有任何用户界面来管理用户。BeOS符合POSIX标准，并包括一个bash shell，但她本质上并不是一个Unix。而OS X则是一个真正的Unix(尽管可能有人对什么是真正的Unix有异议)【译者注：OS X的内核来源于Unix-BSD】。 苹果系统内建了漂亮的界面来管理用户，进行用户权限控制。但是目前却没有与用户管理相对应的组管理。我可以很方便的为朋友或家人建立桌面账号和SSH登陆账号。

说到SSH和网络，我只需点击网络设置的一个按钮来运行一个安全壳守护进程，而不像BeOS那样不安全的telnet远程登录。远程管理我的OS X系统在开机后分分钟内就能实现。同样，每个OS X系统内都内置有Apache Web服务器，默认配置下<a href="http://oreillynet.com/pub/a/mac/2001/12/07/apache.html" target="_blank">[OS X的apache配置，英文]</a> 就能为公共root文件夹和<tt>~/Sites/</tt>文件夹下的页面服务. 

苹果正在或将很快成为世界上最大的UNIX系统供应商。创建一个用户友好的UNIX，几十年来一直作为最高目标，当然是很多Linux开发人员的目标。事实上，苹果（也包括Be公司）成功地给那些需要的人提供UNIX的强大功能，而不会让一般用户具有我之前说的那样的感受——开源的产品很难有好的用户体验。创造一个良好的用户体验，要求为项目工作的每个人都有一致的观点——而开源社区很难达到这点。在当年我为BeOS写作的时候，我就一遍又一遍地指出这一点，现在苹果的新经历再次证明了它的正确。Be和苹果用了很少的开发人员就提供了UNIX shell的强大功能，同时又拥有良好的用户体验，这比开源社区引入X11窗口管理器要早多年。

为一般的消费者提供UNIX的力量，就在一定程度上应该知道如何将用户体验与具体实现细节分开。例如，如果你希望使用Apache默认设置之外的高级配置，你应该知道如何找到并编辑<tt>/etc/httpd/httpd.conf</tt>。因为<tt>/etc</tt>在默认情况下对Finder是隐藏的，并且需要管理员密码权限来编辑,因而对普通用户是安全的。而这些普通用户可以从一个世界级的网络服务器上提交页面，而不用打开终端或输入一行命令。多棒！

更棒的是，PHP预装并配置好了，可以直接与Apache工作, 而MySQL按照简单明了的安装说明就能下载. 相反，BeOS的内核缺少<tt>mmap()</tt>意味着她仍然不能安装MySQL。苹果还包括一个内置的FTP服务器，可以工作在用户目录，还可以载入Samba，AFP和WebDAV共享。Be内置的FTP服务器只是单用户登录，并可以访问整个文件系统。在BeOS，SMB（Server Message Block，服务消息块，协议名）勉强能用。

OS X的网络已经比以前的Be更先进。虽然它的仍不完善，高级用户会遇到一些问题。Irfon-Kim Ahmad提供了这些笔记：

<blockquote>
 如果主要用（OS X）作Apache和SSH服务器，就很好。但是你若想用塔连接你工作室的VPN，还是用windows吧。尽管（OS X）有一些pptp工具，但是相应文档很少，我也从没成功运行过它们。 许多人都跟我谈到他们遇到过无线网络的密码不能一直保存，会定期的‘被遗忘’，我自从重装系统后还没遇到这样的问题。不过我发现OS X的一个主要减分项也是关于网络的：如果所有的DNS服务器断了之后，你可能会忘了它，而OS X则需要10多分钟才能开机，并且会出现各种怪状。这可能只是一个很容易纠正的小错误。
</blockquote>
 
总的来说，OS X中网络功能大体上式世界级水平的。它是安全、稳定的，跟UNIX一样…只是它还没有完成。如果我们把它与Linux网络相比较，Linux会赢。但是若与BeOS比较，OS X就成了赢家。然而，没有理由认为在未来OS X不能成为Linux和BSD那样世界级的服务器操作系统。现在，那些想在Mac上运行ISP（Internet service provider，网络服务提供商），则需要选择MAC OS X的服务器版本。

<h3>CD刻录与磁盘镜像 / CD Burning, Disk Images</h3>

仔细观察OS X系统的任何地方，你只会想到‘融合、统一’这个描述。以CD刻录为例，插入一张空白CD，OS X会问你是想让制作一个ISO，HFS +，还是音频CD。如果你选择ISO或HFS+，光盘会加载到桌面，只要把你想要刻录的东西拖到里面，然后将它拖到垃圾桶。一旦你开始拖，垃圾桶图标变成一个刻录图标（人们常抱怨将希望刻录的光盘拖到垃圾桶让人费解）。点击刻录，等等吧，剩下的工作由系统搞定，无需第三方软件。 


如果你刻录一个音频CD，iTunes会自动启动。将要刻录的音乐从你的音乐库拖动到一个播放列表，点击刻录，就行了。再次强调，无需第三方软件。没有歧义的，没有折磨，没有意外发生。虽然Be的cd刻录程序在刻录音乐的时候也有很多相同的易于使用的特点，刻录数据CD一直都不那么好用。而在Linux上，无论是用Mandrake发行版自带图形界面工具，还是命令行的<tt>cdrecord</tt>，我从来没有成功过，就像过山车一样，会有各种惊险发生。对于命令行，我在BeOS下就已经掌握了. 在OS X中, 这些事就是"小菜一碟" 。

在BeOS中, 我学会了用<tt>dd</tt>、<tt>mkisofs</tt>和<tt>mkfbs</tt>等命令<a href="http://betips.net/1997/09/09/burning-cds-with-beos/" target="_blank">刻录CD</a>，并加载到Tracker。这个过程一般情况都顺利，但也不是没有任何问题。而在OS X下， 苹果有自己的一套处理磁盘镜像的习惯。许多OS X下的软件下载下来是<tt>.dmg</tt>文件，打开它就能检查索引，并被加入Finder检索中。这对开发者来说是一种优雅方便的发布软件的方法，也便于用户创建磁盘和CD备份。隐藏了创建磁盘镜像以及加载、卸载的复杂性，苹果的DiskCopy工具就能完美的创建硬盘、数据CD、音乐CD的拷贝，而不用考虑文件系统。

<div align="center">
<img src="/images/TalesBeOS-diskimage.jpg" alt="diskimage" height="256" width="378">
</div>
<i>许多OS X软件都是可加载磁盘镜像格式发行的 - 双击它就能通过虚拟光驱加载到桌面和Finder检索，爱死这些大图标了... </i>

<br>

<div align="center">
<img src="/images/TalesBeOS-newimage.gif" alt="newimage" height="150" width="322">
</div>
<i>自带的DiskCopy工具使得从文件或光盘创建磁盘镜像极其简单。DiskCopy让Linux/BeOS的"dd"命令相形见绌</i>

一个不协调的缺点就是：刻录数据CD，需要将镜像拖到垃圾桶图标。而刻录音乐CD，就不需要。原因是iTunes不显示加载的镜像。而是直接在播放列表里刻录。一点小瑕疵。


<h3>到处都是PDF / PDF Everywhere</h3>


OS X的一个有趣的创新就是PDF技术在系统中得到了广泛的应用--石英显示引擎（Quartz display engine）建立在PDF的页面描述语言PostScript之上，这和NeXTStep上是一样的。这意味着任何程序都可以直接打印输出到PDF。选择打印，再点击预览（Preview），文本就转换为PDF，并显示在内置的预览程序中，另存就可以得到PDF文件了。不用再购买、安装Acrobat或者第三方软件。就这么简单，棒极了！

本文的<a href="http://www.birdhouse.org/beos/refugee/beos_osx.pdf" target="_blank">英文PDF版本</a>就是用这个方法得到的。


<h2>应用软件 / Applications</h2>

我曾经听到某些‘专家’说OS X仍然缺少应用软件。的确，Photoshop还没有从OS 9升级到OS X新界面，但是有许多软件在发行的第一年就会发布它的OS X版本。而BeOS则软件很少，我们这些BeOS用户已经习惯了请求软件发行者发布BeOS版本，任何小的软件都让我们感激。实际上还未升级到新界面的程序在OS 9经典模式*下都能很好运行。我没有老的Mac软件，所以不需要在经典模式下花费太多时间。偶尔使用，也很顺利（除了这些经典模式下的程序不能使用Samba共享，我的大量图像和文件都是采用的这个方式保存的）。

*我试用的经典模式下的程序有限。有人抱怨说各种音频软件和游戏在经典模式下兼容性不好。苹果刚刚发布了一个OS 9的更新来提高经典模式下的兼容性。

<blockquote>
下面的大部分软件都不是关于操作系统的，只是操作系统提供的一些软件，你可以跳过去看接下来的操作系统比较。但是我觉得这些程序是操作系统及操作体验的一部分，还是应该包含进来。
</blockquote>

<h3>音乐播放器 / iTunes</h3>

BeOS在某些方面还是要超过其他系统的，比如总体易用性，音频文件的创建、存储与播放。结合数据库式的文件系统——BFS（Be File System），Be操作系统处理多媒体文件及其高效，比如音频播放软件<a href="http://www.bebits.com/app/156" target="_blank">SoundPlay</a>与系统融合的很好，使用又非常灵活。作为对MP3音乐的爱好者，我马上就在OS X上寻找能达到Be系统里那样功能的MP3播放器。在BeOS中，任意的元数据（meta-data，属性标签）都可以与文件或某类型文件结合起来，并保存为属性（attributes）。这些属性可以在文件浏览器中进行筛选、排序和查询。因为属性是系统自动索引的，所以查询结果瞬间可得，不管查询的数据量有多大。在本质上，Be的文件系统就是一个数据库。

<blockquote>
注：微软还处于将所有的应用程序和操作系统本身置于一个基于SQL Server的共同的数据存储之上的早期阶段。如果他们能够成功，这将是微软历史上Windows产品线的一个重大变化。
</blockquote>

在一个虚拟数据库之上建立一个操作系统会对整个操作系统的功能产生影响，MP3的存储就是一个例子。BeOS的MP3编码工具存储元数据，不只是存储在ID3标签中，还保存于文件系统中。这就意味着我们能够创建自定义的播放列表，而不像Windows或Linux那样需要借助第三方工具。例如，在BeOS中创建一个播放列表，包括1978-1984年之间的所有乡村或朋克类型的歌曲，那就是小菜一碟。

<div align="center">
<img src="/images/TalesBeOS-id3attrs.gif" alt="id3attrs" height="274" width="682">
</div>
<i>文件浏览器Tracker中的MP3文件列表，包含了多种属性，而隐藏了实际文件名。注意浏览器同时显示了多少属性信息。尽管OS X的查询工具Finder也支持元数据，但是它也无法在视图内显示这么多的数据，除非缩小字体。既然Tinker工具可以改变Finder的字体，那么我们或许可以期待未来的OS X在这方面做出改进。</i>

我收藏的mp3音乐文件包含了详细的ID3标签，但是我在OS X中不得不顺从地接受事实，牺牲我那些自定义的播放列表。为了能显示更多的ID3列，我放大了iTunes窗口。我意识到可以用很多规则整理我的音乐文件。应用程序顶部的小的搜索窗口看起来不怎么样，可我很快意识到它能在任何ID3标签字段找到字符串。将搜索结果拖到一个新的播放列表，我就可以重现BFS的数据库功能，而无需属性功能。虽然在iTunes中，这些大量的，按任意规则的搜索不比直接在BFS文件系统下更快，但都是很快就能完成。在OS X下，因为一切都发生在iTunes这样单一的窗口内，反而会更好。

<div align="center">
<a href="http://www.birdhouse.org/beos/refugee/itunes.gif" target="_blank"><img src="/images/TalesBeOS-itunes.jpg" alt="itunes" border="0" height="304" width="500"></a>
</div>
<i>iTunes可以实现跟BeOS一样的元数据的存储和查询，只是BeOS限定在一个由操作系统供应商提供单一播放软件中。不幸的是，我无法在Finder中看到相同的元数据，而我在BeOS下就可以；我不能从Sherlock中查询，而BeOS下就可以。但我得承认，iTunes播放列表管理真的很好用，很有吸引力。此外，iTunes的皮肤更棒。</i>

iTunes给我的另一个惊喜是，有一天我用一个批处理工具批量修改mp3文件的名字。我以为修改后所有的文件名称都改变了，需要重新建立播放列表。但是，当操作完之后，我惊讶的发现，所有的播放列表仍然完好。这是符号链接的魔力，它在对象移动时还能保持链接。这样的功能在老的Mac用户看来是理所当然的，但对我传统的x86思维却是极大的震撼。

我对iTunes的一大抱怨就是缺少插件。目前，我见到的唯一的插件是可视化工具（visualizers）。用起来不错，但是谁在乎呢？我希望的是一些真正有用的插件，就像WinAmp或者BeOS的SoundPlay的那种插件。最近，我花了一晚上时间，尝试了能在<a href="http://www.versiontracker.com/" target="_blank">VersionTracker</a>找到的各种MP3播放器。我所需要的就是在某个指定端口广播前降低采样频率。可我还是空手而归。而用BeOS的SoundPlay实现同样的功能就很容易——启用LiveEncoder插件，指定使用的位率（比特率）、采样频率以及广播端口就好了。这样你在SoundPlay播放的音乐也会同时广播到网络。BeOS还有各种工具来控制你的MP3收藏，即使是远程的，比如搜索、随机播放，远程建立播放列表等等。我不知道iTunes的插件是否有这些功能，还是因为某些原因开发者没有实现，可插件目录却是开放的，很怪。

OS X的强项是它的iTunes有非常棒的播放列表管理，而BeOS则是任何关于MP3的创建、保存、远程控制、立体声接口等等。


<h3>视频播放 / iMovie, iDVD</h3>

既然苹果希望成为用户生活的数字中心，那么她的操作系统中就应该包含基本的视频制作程序。当我在<a href="http://www.adamation.com/" target="_blank">Adamation</a>工作时了解到编辑数字视频无论从程序员角度还是用户角度都是一个很复杂的过程。在Adamation我曾经花了几周时间尝试各种非线性编辑器。经过尝试，我发现没有一种非线性编辑器像iMovie这样容易学习和使用。苹果已经尽力去除了很多视频编辑的让人困惑的体验，让用户可以无故障、流畅播放的视频。

但不能说iMovie功能强大，它只有一个视频和两个音频层和及其有限的编辑功能，精明的用户会很快发现这些局限，并转而使用1000美元的Final Cut Pro来替代。adamation的29美元的personalstudio（曾经可以用在BeOS上，现在只有windows版），可以实时处理10层任何类型的多媒体，没有渲染，只要一个稍微有点陡峭的学习曲线，就能获得强大的编辑功能。与personalstudio相反，我发现iMovie中有不必要的限制。但我仍然对它的清晰，干净的工作流和演示印象深刻。它可以轻松击败Windows ME和XP上的非线性编辑器。

我只是开始尝试iDVD，但到目前为止，它的风格和表现似乎与iMovie一致，都不是非常强大，但很容易快速创建漂亮的成果。我第一次产生了为朋友和家人制作圣诞DVD小电影的念头。

至于平台对比，这正是BeOS的设计目标，以及为什么Adamation试图实时处理10个层次而不渲染。苹果需要从Adamation当初在BeOS上，以及目前在windows上的工作中学习很多。在实际应用中，MAC一直是DV编辑和视频制作的不错的平台。由于Adamation离开了BeOS平台，这个平台完全没有可用的非线性编辑器。另一方面，Final Cut Pro 3（FCP）已经宣布发行OS X版本。随着FCP迅速成为行业标准，风行于非线性编辑器领域，MAC仍然是DV编辑的一个好选项。

这次比较，OS X险胜。


<h3>Camera</h3>

在我得到我的MAC前一周，我花了一些时间将老爸的电脑从BeOS转移到了Windows 98。在那之前，他应该就是地球上最老的熟悉BeOS的用户了。他爱用BeOS。它也从没让人失望，100%防病毒（因为没有已知的BeOS病毒），并且像古老的Macintosh一样简单易用。但他厌倦了收到邮件，却打不开附件，访问网站，BeOS的垃圾浏览器却无法工作。

这次系统更换开始很顺利，直到他的数码相机串口连接电脑时。这在BeOS上用内置的摄像程序可以完美运行，用ImageGrinder批量修改照片大小也相当容易。而Windows的对应程序就很难看、难用，几乎不能完成。我花了半天时间寻找免费的、可用的替代品。最后的解决方案是，他得 切换到BeOS上处理照片，然后复制到windows分区，再重启回到windows，接着打印和发邮件。

开始遇到了这种让人头痛的问题，所以当我的相机接到MAC，有一个简单的，友好的应用窗口自动弹出，让我很吃惊。这个程序甚至提供用这些照片制作网页的选项。当我批量修改照片大小时，我发现OS X的软件强大到奢侈、功能过剩。这时，我记得我见到过苹果网站有很多集成在Finder的脚本。我找到了一个嵌入Finder工具栏的脚本，将一批照片拖到这个图标，输入一个百分数比例，所有的照片瞬间就可以改变大小。无需第三方软件。

我听说Windows XP能更好的支持相机，若windows具有类似的能力，我也不会惊讶。但是，如果我钱够的话，我会为爸爸买一台OS X电脑。

<h3>办公软件 / Office X</h3>

尽管我不认同微软的理念，但是事实上OS X上一些最复杂的软件来自微软。我使用办公软件并不多，但当需要时还是需要的。对于微软为Mac平台提供的Offic X，就像<a href="http://www.wired.com/news/technology/0,1282,48160,00.html" target="_blank">连线杂志评论文章“乔布斯喜欢盖茨的新办公软件”</a>里说的，将一堆旧的办公套件变成一件艺术品。增加了成千上万行代码，数百新部件和图标。这是一件和OS X本身一样华丽的软件。入驻微软的Mac移植团队不只是移植软件，他们为满足Mac用户的需求重写了大量代码。

<div align="center">
<a href="http://www.birdhouse.org/beos/refugee/office.jpg" target="_blank"><img src="/images/TalesBeOS-office.jpg" alt="office" border="0" height="236" width="350"></a>
</div>
<i>面对微软会有纠结。你最终离开了他们的操作系统，可是突然发现你喜欢上了他们在另一个平台上的软件。的确，面对Office和Internet Explorer你很难拒绝。</i>

值得讽刺的是，我对微软的主观反感是我离开Windows系统的一个原因，而现在我发现我喜欢上了Mac OS上的微软的Office软件。残酷的现实啊。

在BeOS上，人们使用Gobe Productive办公软件。这可能是BeOS上最复杂的软件了，它以一种独特的方法集成文字处理/表格/演示/位图编辑/矢量图形——一个应用程序，一种文件格式，却集成五个模式。我很喜欢它，希望它能移植到OS X*上。

可惜的是，因为微软没有公开它的Office文件格式，Word和Excel文件的兼容性与Gobe Productive并不完美。在大多数情况下，完全可用，但它不能处理一些更复杂的文件类型，如文档与数据透视表和修订跟踪。而Office X就一切正常，十分完美。不仅如此，但他们终于解决了所有的MAC和Windows Office DOC的兼容性问题，包括扩展字符集和向后兼容（Office X的文件可以在Windows的Word 97中完美的打开，而无需先保存为老的兼容格式）。

这轮比较OS X胜。

<i>*注：Gobe Productive 3 只发行了Windows版，他们声明计划在近期发布Linux版本。</i>


<h3>浏览器和邮件 / Browsers and E-Mail</h3>

BeOS用户抱怨最多的问题就是现有的Web浏览器很差。如果BeOS早出现几年，那么Netscape可能会为BeOS发行一个浏览器版本。可事实不是如此。多年来，BeOS上唯一的浏览器就是自带的netpositive，它是快速和高效的，事实上在大多时候用着还不错，但它不能处理Java、JavaScript、DHTML或CSS。无论BeOS多么现代或科幻，如果她上面没有相应现代的的软件，那她就名不副实。Opera 3.62可以用在BeOS上，但它仍然不完美。Mozilla的浏览器也可以用在BeOS，但它臃肿，经常崩溃。BeOS上没有好的浏览器呀。

而相反的，苹果是与魔鬼共骑。OS X将移植的IE 5.5作为它的默认浏览器。虽然与Windows上的版本不完全相同，但是很漂亮，所有的网站都能完美解析，打开也非常快。它对于我的最大不足就是不支持日益流行的PNG图像格式。

如果你不讨厌在Mac上运行MS的软件，还有一个更好的替代品。<a href="http://www.omnigroup.com/" target="_blank">OmniWeb</a>是一个稍慢，但是我见过的将网页显示的最漂亮的，只需启用OS X的脚本功能。iCab、Opera和Navigator 6都是现代的浏览器。OS X下浏览器的选择取决于个人的偏好，而不是像在BeOS上那样妥协和牺牲。 

浏览器的比较，OS X胜。

对于email客户端前台程序，Be的理念非常棒：提供一个单一的、标准的邮件格式，将邮件头的多属性元数据（如收件人、发件人、主题等），作为属性存储在统一的、共享的消息存储中。将每个消息（邮件）当作一个单独的文件存在用户的个人文件夹中。这种方法有两大优势：

<ol>
	<li>用户可以通过系统查询，用收件人、发件人、主题等任意字段找到邮件，而不用首先进入邮件夹或打开邮件。</li>

	<li>所有的电子邮件应用程序都可以使用同一个消息存储。BeOS上没有专有的电子邮件格式，用户可以自由的更换各种电子邮件客户端，而不必担心格式之间的转换。用户甚至可以使用Tracker文件浏览器本身作为电子邮件的组织程序，利用简洁的BeMail客户端读写邮件。</li>
</ol>

从体系结构上来说，这轮比较BeOS获胜。

<br><div align="center">
<a href="http://www.birdhouse.org/beos/refugee/bemail.jpg" target="_blank"><img src="/images/TalesBeOS-bemail.jpg" alt="bemail" border="0" height="146" width="400"></a>
</div>
<i>BeMail的每个消息都是一个单独的文件，存储于Tracker文件浏览器。可以按个人喜好排序，或通过定制系统查询来创建虚拟的邮件文件夹。可以通过BeMail客户端简单的阅读和书写邮件，而用其他的应用程序提供的更强大功能处理集中保存的邮件消息。</i>

可问题是，目前还没有很好的电子邮件软件来处理邮件消息。有几款不错的软件，如BeatWare的<a href="http://www.bebits.com/app/502" target="_blank">Mail-It</a>就是Eudora的一个很好的替代。但是BeatWare很早就放弃了BeOS平台的发展，所以这个Mail-It有不少缺陷和不足，无法得到修正。

另一方面，Qualcomm很早之前就移植了Beta测试版的Eudora到OS X平台，这个测试版达到了98%的完成度。我在BeOS上使用Eudora工作多年，于是在OS X上也使用它。但是，出于好奇，我尝试了几天苹果自带的邮件客户端，然后再也没有回到Eudora。这是超级整洁，可以处理多个帐户，有足够（但不是很棒）的规则/过滤器，有颜色标签代表的资料等级——与我一直非常喜欢的Mail-It上的特性相同，这也是为什么我遗憾的放弃了Eudora。 

<br><div align="center">
<img src="/images/TalesBeOS-mail.gif" alt="mail" border="0" height="575" width="552">
</div>
<i>苹果的邮件客户端不够强大，但用起来不错，看起来很好看。我非常喜欢它的彩色标签，使得同一个主题的邮件增多时更易于阅读。邮件也很好地处理引用的文本，所以同主题邮件多次引用时，锯齿状缩进引用的的文本，加上不同颜色标签，赏心悦目。</i>

如果这还不够的话，Office X中还包括Entourage，这是Windows下Outlook/Express的MAC版本。我还没试过，但听说不错。由于有这三款不错的选择，还有另外的多款其他电子邮件应用程序，所以这轮比较OS X获胜。如果有什么办法让这些厂商抛弃私有的邮件消息存储，而是以一个统一的格式存储，那就完美了。

<h3>文本编辑 / Power Editors</h3>

The most powerful text / scripting / HTML editor for BeOS is Maarten Hekkelman's <a href="http://www.birdhouse.org/www.hekkelman.com/" target="_blank">Pe</a>.
 I lived in Pe for years. I maintained three web sites, did all my shell
 scripting, and wrote two books and countless articles in Pe. Hekkelman 
has ported Pe to OS X under the name Pepper, so this transition could 
have been super easy for me. But for the sake of change, and because I 
wanted to see why <a href="http://www.barebones.com/" target="_blank">BBEdit</a>
 has the reputation it does, I adopted BBEdit for my power editing needs
 under OS X. That was a tough one for me, since I feel a certain loyalty
 to Maarten, and because it would be like a sentimental tie to my past. 
What finally swayed me was the fact that I wanted access to the huge 
community of BBEdit code wizards out there through the BareBones mailing
 lists.

Because BBEdit has been around longer, and because it comes from a team 
of programmers rather than an individual, BBEdit wins, 
feature-for-feature. But in practice, and for the kind of work I do, 
BBEdit hasn't offered any real-world advantages over Pe. They're equally
 elegant and powerful (roughly speaking), and the differences in the big
 picture are fairly minor. So this one is a draw.

Point: love-love.

<h3>X Compatibility</h3>

For those wanting to run *nix applications both BeOS and OS X have the 
ability to run an X server and client, and to run X applications. In OS 
X, X can run either "rooted" or "rootless." In rootless mode, the X 
system does not take over the entire desktop, so one can run *nix GUI 
apps side by side with Carbon/Cocoa apps. In BeOS, X runs in a large 
window, so the experience is fairly similar. However, the <a href="http://sourceforge.net/projects/xonx/" target="_blank">XonX</a>
 project has more developers and more momentum. Compatibility is 
greater, and we can expect to see the experience continue to improve 
with time. Whether or not BeOS' X implementation gets any better (it was
 fairly shaky last time I tried it) is anybody's guess.

In any case, I haven't found much reason to run XonX, as the only 
reasons I might want to are to compensate for missing application 
categories, and so far I haven't found an app category not filled either
 by Carbon/Cocoa apps or by Classic mode. I'm happy to let XonX remain 
the domain of people who keep one foot planted firmly in the *nix world.
 
Point goes to OS X.

<h3>Software Costs</h3>

One downside I didn't expect about OS X software is that it gets 
expensive fast. I don't come from the camp that believes software must 
be free, and I love to support developers who do good work. It makes me 
happy. But like anyone, I enjoy having access to free software as well, 
and there's very little in the way of freeware available for OS X. 
Freeware just isn't a part of the OS X culture, and shareware apps cost 
about 50% more on average than equivalent BeOS shareware apps. By the 
time you add up everything you pay to populate your machine with all the
 app launchers, text editors, image viewers, and other doo-dads you need
 to get through the day, it's easy to add a hefty sum to the initial 
price of purchase. Hey, it's a free market, and I respect it. But 
migrating users should be prepared.

Fortunately, the quality of the software I've  been digging up has been 
extremely high in general - independent Mac OS developers really seem to
 put a lot of care into their craft. In a way, software for Mac OS is 
kind of like Apple hardware - you pay more, but you  also get more.

<h2>Community</h2>

Hang out on some of the BeOS mailing lists for a while and you'll notice
 something interesting: There is a larger concentration of intelligent 
and friendly users in BeOS-land than in any computing community I've 
ever stumbled across. There's just something about the system that 
attracts sophisticated, articulate users with high standards (present 
writer excluded, of course). You almost never see the kind of rudeness 
and arrogance in BeOS-land that you see in Windows or Linux communities 
(Linux especially), and while there are always BeOS newbies, there are 
seldom computing newbies hanging out on BeOS lists. Over the years, I've
 hooked up with dozens of people whom I now count as genuine friends.

The Mac communities are much better than the Windows and Linux 
communities as far as signal/noise ratio goes, but suffer from a 
different kind of problem: Stubborn-ness. There seem to be endless 
armies of Mac users who feel that the old ways are the best. Who kick 
and moan and bitch about OS X and its cursed Unix underbelly and how 
evil the command line is and how Apple is off its rocker. These people 
would rather keep using a slow, crashy, OS with no remote administration
 and no appeal to command-line power users and no position in the server
 niche than be dragged kicking and screaming into the modern world. 

Granted, these voices seem to grow a little less loud and a little less 
prolific with every passing month. But they're still there, and the fact
 that they're clinging to OS9 for reasons mostly beyond my comprehension
 are bad for us all. App vendors who haven't yet ported point to a lack 
of wide-scale adoption of OS X. And whose fault is that? The very 
Macintosh userbase those app vendors are here to support! Note to the 
stubborn ones: You're a drag on us all. Get on board.

Aside from the highly vocal nay sayers, the Mac community has about the 
same level of friendliness, if not the same level of technical savvy as 
the BeOS community. 

Point: BeOS, by a narrow margin.

<blockquote>
 On the community note: As I began to pick up steam on OS X, I decided 
to create a site similar to betips.net, but for OS X users. But when I 
discovered that <a href="http://www.macosxhints.com/" target="_blank">MacOSXhints.com</a>
 already had a database of nearly 1,000 tips and tricks for OS X users, I
 gave up that idea. The site's founder Rob Griffiths and I started 
corresponding, and soon listed each other as "sister sites." I even 
helped Rob to edit his excellent <a href="http://homepage.mac.com/rgriff/osxguide2.html" target="_blank">OS X Power Guide</a>, which I highly recommed to anyone looking for ways to get more productive in OS X quickly.
</blockquote>

<h2>Happiness Quotient</h2>

So. I'm using this OS that provides a great experience. Everywhere I 
turn, things are integrated, smooth, composed, designed, fluid, 
beautiful to look at, a joy to use. I'm pretty much convinced that OS X 
is the best consumer OS on the market, with none of the compromises of 
BeOS (compromises that result not from bad design, but from lack of 
industry momentum  --  unfinished apps and an OS vendor that's been 
close to bankruptcy for years, not to mention the hassles of dealing 
with hardware and software vendors who won't give you the time of day 
until you can guarantee them a big userbase / chunk of change). I've got
 world-class stability, pretty good multitasking, true memory 
protection, all kinds of open source networking software, and a Unix 
command line. 

I know I'm not alone in finding OS X a happy campground for the despairing BeOS refugee. This LiveJournal <a href="http://www.livejournal.com/talkread.bml?itemid=13186510&amp;view=16922846#t16922846" target="_blank">comment</a> from Balatro mirrors my own experiences pretty accurately:

<blockquote>
I suffered with OS9 for a while, it was usable but crash prone. Then OS X
 came out (Which I had been waiting for months). It was a dream come 
true (though slow as hell on the iBooks 66Mhz bus). Finally I bought the
 bullet and bought a Titanium 400.

OS X 10.1 is the only OS other than BeOS that I truly ENJOY working 
with. Windows is just "there." It offers me no joy -- only 
compatibility. Linux/Unix is like pulling teeth, and has a horrible 
appearance no matter how hard you try to dress it up. OS X is a 
beautiful marriage of elegance and power.
</blockquote>


<h1>The Bad and The Ugly</h1>

Overall, I'm happier than a pig in shit. What could I possibly find to complain about? 

Whereas BeOS is renowned as one of the fastest and most efficient 
operating systems ever designed, OS X may well be one of the slowest. 
Problems with performance and efficiency in OS X have been discussed ad 
nauseam all over the net, but the BeOS user feels this contrast more 
acutely than most, because the BeOS user has been so completely spoiled 
by the amazing speed of BeOS. 

According to some reports, the PowerMac 867 is functionally equivalent 
to a 2Ghz Pentium, CPU-wise. Loaded up with 640Mbs of memory, this 
machine should absolutely fly through just about anything I could care 
to throw at it. But that's not the case. With this much horsepower, 
performance is merely acceptable. OS X on a lesser machine is an 
exercise in pain. OS X apologists have a myriad of excuses for OS X's 
high resource requirements  --  it's the Finder's fault, it's Quartz' 
fault, it's the window buffers that give you all those cool transparency
 effects, etc. etc.


I'll allow for one thing: Optimization is the very last thing developers
 do with a code base, and Apple has steadily increased performance with 
every point upgrade to the OS to date. There's no reason to think that 
future updates won't raise the performance bar as well. In fact, <a href="http://forums.macnn.com/cgi-bin/ultimatebb.cgi?ubb=get_topic&amp;f=46&amp;t=000100" target="_blank">this discussion</a>
 implies that the next release may offer significant efficiency gains in
 the window buffering department. In reality, I don't think the problem 
can be localized to any one OS element  --  there are probably 
improvements to be made in nearly every aspect of the OS. 

Still, BeOS never had this problem. While BeOS did get faster as years 
went by, the OS was a speed demon from day one  --  radical efficiency 
was one of its hallmarks from the start, and one of its great drawing 
cards. The fact of the matter is, BeOS on a Pentium 233 with 64 Mbs of 
memory is faster than OS X is on this so-called supercomputer. The Mac's
 CPU is roughly 8x faster and the machine is stocked with 10x more 
memory, but the BeOS machine out-performs the Mac. BeOS boots faster, 
applications launch faster, windows resize more smoothly, you can play 
more simultaneous audio and video clips without affecting system 
performance.

This wide delta is partly explained by the fact that BeOS was designed 
from the ground up and didn't carry any baggage, partly explained by the
 fact that OS X's windowing system is so advanced and does so much, and 
partly explained by OS X's youth. But I can't help but think that Apple 
is being somewhat lazy here. Fast CPUs and memory are very cheap these 
days, and Apple seems to be using that fact as an excuse for inefficient
 OS design. If Moore's law weren't in effect, the market would not be 
stocked with so many fast machines, and OS X would be dead in the water 
without radical improvements to general efficiency.

Try this: open a Terminal window (instantaneous on BeOS, a few seconds 
on OS X) and run "top." Then resize its window. The resize operation is 
clunky and blocky. Now try the same on a far lesser BeOS machine  --  
the resize operation is silky smooth, even if several CPU-intensive 
processes are going on. I even tried this on a dual 800 at MacWorld 
Expo, and found the same chunky resizing behavior.

Now launch four QuickTime movies and get them all playing at once. Move 
them around on screen, and resize them while playing. Try the same on a 
far lesser BeOS machine. The difference is night and day. 

I do a lot of MP3 encoding, so it's a drag to discover that other tasks 
in the OS are noticeably affected (not hugely, but noticeably) when 
encoding is in process. Not so in BeOS. Neither OS creates glitched MP3s
 when encoding under load though.

There is not a single operation I can find that involves multithreading 
and multitasking that is not leagues faster on a lesser BeOS machine 
than it is on a hot-rod OS X box. If the performance hit is a tough pill
 for OS 9 users to swallow, imagine how much harder it is for the BeOS 
user. We could go into a long discussion about priorities, kernel 
scheduling, and effective multithreading techniques, but the bottom line
 is that it's all about the user experience. Be nailed this one a decade
 ago, while Apple still hasn't gotten it right. 

I should, however, take a moment to say that most of the time, and for 
most of what I do, OS X on this machine is fast enough. I'm not typing 
ahead of the cursor, I'm not sitting on my thumbs waiting for 
hourglasses, and I'm not in any real-world way stymied by OS X on my 
current hardware. It's just that I have lived with a very high standard 
of performance for long enough that it started to feel normal to me. 
Be's performance bar is going to be a tough hurdle for Apple. 
Unfortunately, the vast, vast majority of the Mac-using population has 
never tried BeOS, and doesn't know what they're missing. 

<h2>File System Shoot-Out</h2>

Speaking of not know what you're missing, we now come to the single 
largest usability difference between BeOS and OS X  --  the file system 
and the practices and policies used to work in it. I've written at great
 length about Be's file system, as it remains the one functional aspect 
of the operating system which truly sets BeOS apart from anything else 
on the market (not that BeOS is really "in the market" anymore).

BFS (the Be File System) is fully journaled, which means that data 
integrity is guaranteed even in the event of a loss of power. Pull the 
plug on a BeOS box and it boots back up in 15 seconds with no loss of 
data. File system operations that were in process at the time of the 
outage are simply replayed from the journal. No ScanDisk, no fschk, no 
rebuilding the desktop. OS X does not have a journaled file system 
(although, to be fair, I have lost power on this machine and found that 
it booted back up in a normal time span without appearing to do anything
 special). 

BFS is also fully multithreaded for optimum performance, and in keeping 
with the rest of BeOS, which is multithreaded from the lowest levels to 
the highest. I do not know whether HFS+ is multithreaded (I've heard 
that  it's not), but it sure doesn't feel as fast as BFS. However, I do 
not have equivalent hardware on which to run comparative disk access 
benchmarks under various conditions.

The address space in BFS is 64-bit, meaning that the theoretical maximum
 file size on a BFS volume is 18,000 petabytes (the practical maximum is
 much smaller for various reasons, but is still in the tens of thousands
 of gigabytes range). The 32-bit HFS+, like all 32-bit file systems, has
 a maximum file size of around four gigabytes. Larger files are possible
 via behind-the-scenes magic which transparently stitches files 
together, but it seems like this is an issue Apple would have addressed 
as long as they were creating a new operating system and had the chance 
to get it right.

For the everyday user, though, BFS has much more tangible advantages. 
Any file or file type on a BFS volume can have arrays of metadata 
associated with it, in the form of "attributes." There is no limit to 
the amount, size, or type of attributes, and attributes can be displayed
 and edited, sifted, sorted, and queried for directly in the Tracker 
(Be's equivalent of the Finder). Because most attributes are indexed, 
search results are nearly instantaneous, regardless the size of the 
volume or the number of files being searched through. By default, BeOS 
ships with reasonable sets of attributes for common file types, but 
users are allowed to extend and customize these, and to create entirely 
new file types with entirely new arrays of attributes. In other words, 
the Be File System doubles as a database. 

<div align="center">
<a href="http://www.birdhouse.org/beos/refugee/trackerbase.gif"><img src="/images/TalesBeOS-trackerbase.gif" alt="trackerbase" border="0" height="169" width="405"></a>
</div>
<i>Be's filesystem doubles as a database. Users can use built-in 
filetypes with existing attributes, or create entirely new filetypes 
with custom collections of attributes. These files were used to deliver a
 dynamic web site out of the BFS database without using 3rd-party 
database software. Click for larger image.</i>

It is difficult to describe to users of other operating systems just how
 advantageous an operating system built on top of a virtual database can
 be. Only other BeOS users really seem to understand the power and 
flexibility of the database-like file system, and it is the single 
feature I miss the most from BeOS. 

Some examples of Be's database-like file system in action:


<ul>
	<li>Copy your MP3 files' ID3 tags to Artist, Title, Year, Genre 
attributes. Sift and sort through your collection in the Tracker in 
almost anyway imaginable, or build playlists from MP3 attribute queries 
with far more flexibility than you get in other OSes. </li>

	<li>BeMail messages store Subject, From, To, CC:, Date, etc. in 
attributes. Create virtual mailboxes based on live, instantaneous query 
results. This lets you obtain views of your email store that are 
irrespective of the actual folder locations of BeMail messages on disk.</li>

	<li>Years ago, I created a custom file type based on text, with 
attributes for author, title, email, URL, etc. Then I wrote a CGI script
 in perl to extract and dish up these attributes over the web. In other 
words, I was serving up a database-backed web site without having to 
install or learn any database software whatsoever. That site now runs on
 <a href="http://www.onlamp.com/" target="_blank">LAMP</a>, but you can see how the site was created <a href="http://www.betips.net/TrackerBase/" target="_blank">here</a>.</li>

</ul>

OS X's closest approximation is the pathetic <a href="http://www.Mac%20OS%20Xhints.com/article.php?story=2001103013060434" target="_blank">comments field</a>,
 which is a pain to use (hell, you can't even enter Comments directly 
into the Finder), and which offers next to nothing in comparison to BFS 
attributes.


The great usability of BFS and the Tracker don't end with plain-sight 
attributes. Additional attributes describe each file's type via the 
Internet-standard MIME system, which provides a great deal of 
compatibility with the world at large (download a file from the internet
 and its type can be gleaned from the HTTP header, without use of 
extensions), and BeOS web servers don't need to maintain separate MIME 
tables - each file's type is taken directly from the file system. 

Attributes are used by StyledEdit to allow for rich formatting in plain 
text documents, which are still viewable as plain text on other 
platforms. Attributes are used to retain cursor position in documents 
even after they're closed and re-opened, and are used to store 
equalization and cross-fade settings for MP3 files. The possibilities 
are endless.


<h3>Application-Binding Policies</h3>

Neither BeOS nor Mac  OS 9 require users to add extensions to their  
filenames. Without extensions, some other means of identifying a file's 
type and associated application is necessary. All versions of Mac OS 
assume that the application that created a document is also the best 
application to launch it in, resulting in situations where files of the 
same type launch in different applications when double-clicked. For some
 reason, a lot of Mac users don't seem to see this creator-based 
launching schema as a problem, but I do. It results in not-infrequent 
unexpected and undesired behavior on the part of the OS, and seems like a
 major usability disadvantage. Just recently an OS 8 user in our 
department sent me a bunch of JPEG images as an attachment. When I 
double-clicked them, the Classic environment started to launch. Turns 
out they had a Creator code for the Classic version of QuickTime.  
Excuse me? When did I ever tell the OS that I'd rather not view JPEGs in
 my viewer of choice? What  does QuickTime have to do with these images,
 other than the fact that she created them in it on her system? I've 
experienced similar events half a dozen times in the few months I've 
been using OS X, and have heard  similar  stories from others. Why Mac 
users are so complacent about Creator-based launching is beyond me. 

In an attempt  to become more compatible with the Windows world, OS X 
requires extensions for file type identification. Meanwhile, it 
continues to respect the Creator code for application binding. In other 
words, rather than moving forward by dropping the Creator code and 
moving to a complete FileTypes preferences panel, OS X adopted a bad 
habit from Windows (extensions) and retained its own bad habits (using 
the Creator code for application binding). While the rest of the OS was 
moving forward, filetyping left  one foot in the mud and stepped 
backwards with the other foot. This is utterly baffling to me. 
Filetyping under OS X is now doubly problematic, rather than better than
 it was.

Recently, a <a href="http://www.macslash.com/article.pl?sid=01%2F12%2F05%2F1624227" target="_blank">discussion</a>
 explored this issue in the context of metadata in OS X in general. In 
the course of that discussion, it was pointed out to me that it is not 
the Creator code per se' that I don't like, but rather the application 
binding policy of the OS / Finder. What's needed to provide maximum 
flexibility to the user, IMO, is to allow for storage of any type of 
metadata. And one of those pieces of metadata needs to be a 
"preferred_app" attribute. The operating system's application-binding 
policy should look first to see if the user has established a preferred 
application for handling the current file. If not, it should look to see
 if there's a globally preferred application for handling this file's 
type. If not, it can try and use the Creator code if necessary. 
Respecting the Creator code should only be a last resort, since it's so 
often responsible for unexpected and undesirable behavior. But as seen 
in the screenshot below from <a href="http://www.brockerhoff.net/xray/" target="_blank">X-Ray</a>,
 the Creator code is looked at first, the file's extension second, and 
the file type third - the exact opposite of what logic and usability 
would dictate.

<div align="center">
<img src="/images/TalesBeOS-binding_prio.gif" alt="xray" height="343" width="468">
</div>
<i>OS X prioritizes Creator code over file type in the application 
binding process. Since the document's creator is logically irrelevant to
 the determination of the best app to launch the document in, and 
because it often results in unexpected and undesirable document 
launching behavior, and because more flexible and powerful application 
binding can be accomplished through file type-based binding, I find this
 100% backwards.</i>


If Apple is ultimately to provide a central FileTypes preferences panel,
 and simultaneously wants to satsify users who for some reason feel 
strongly about the Creator code, there's another possible option here. 
Rather than simply elevating the importance of  the file type and 
deprecating the importance of the creator, Apple could let the user 
select the order of the binding rules. For example, users who want 
maximum control over binding preferences could opt to have the file's 
preferred app checked first, the preferred  app for that file's type 
checked second, and the creator third. Died-in-the wool traditionalists 
could have the Creator checked first, and other options checked second 
and third. In other words, Apple could not only match Be's level of 
flexibility, but could surpass it.


The other part of the problem is that OS X offers no central file types 
preferences panel. It needs one, badly. Without it, OS X will never be 
able to depart from the cursed practice of respecting the Creator code, 
and will never be able to approach Be's level of flexibility. BeOS ships
 with reasonable defaults for file type-to-application bindings, and 
these are configurable by the user on a system-wide basis, at the 
individual file level, and on batches of files at once via a built-in 
Tracker Add-On. The BeOS user does not need to put extensions on his/her
 files, BeOS never makes the rotten assumption that the creating app is 
also the best launching app, and the BeOS user has control over 
application binding from the micro to the macro level.

The BeOS filetyping and application binding system has more  
flexibility, more usability, and is more logical than OS X's. After the 
performance issues, OS X's backwards filetyping schema is my single 
largest disappointment with OS X.  


After several weeks of using OS X, it was pointed out to me that OS X 
does offer some semblance of control here. Get Info on a file, select 
"Open With Application", and navigate to the new app. You can then 
re-set the binding for that document, or choose to make the change 
globally. It's great that it's possible to do so, but there's a logic 
problem here:

The Get Info panel relates to info on a selected file or files. But 
here, it is being used to make a system-wide change -- in other words, a
 System Preference. It is not intuitive to look in a single file's Info 
panel for a system preference, which is why I never found the option 
when looking around, and why a friend had to point out to me that it was
 even possible to do so.

A central FileTypes panel would be more intuitive, more powerful, and 
would give the user much more control over every aspect of file types 
and bindings.

<div align="center">
<img src="/images/TalesBeOS-filetypes.jpg" alt="be_filetypes" border="0" height="406" width="570">
</div>
<i>The BeOS FileTypes preferences panel gives the user total control 
over MIME types, icons, associations between applications and filetypes 
(application binding), optional filename extensions, and attributes. 
This is the global (system-wide) preferences panel. A separate FileType 
panel for individual files or groups of files lets you override the 
global settings on a local level.</i>

On this note, an additional BeOS advantage is that the MIME typing 
system allows the OS to easily keep track of which apps can handle which
 file types, and thus to suggest candidate applications. For example, if
 I create a custom filetype with the MIME type <tt>text/x-shacker</tt> 
and send it to a user who hasn't registered that filetype on his system,
 BeOS will still be able to tell that it's a text file. Since every BeOS
 app registers itself to handle certain MIME types, BeOS can instantly 
provide a list of all text-handling apps on the user's system. This 
capability also comes into play when displaying the "Open With..." 
context menu when right-clicking a file in the Tracker. 

<blockquote>
For a detailed discussion on the entire filetyping / binding / identification / customization schema in BeOS, buy a copy of <a href="http://www.birdhouse.org/beos/bible/" target="_blank">The BeOS Bible</a>. To read an excerpt from the chapter on filetyping, <a href="http://www.beosbible.com/exc_filetype.html" target="_blank">click here</a>.
</blockquote>


<h3>Alien Filesystems</h3>

In BeOS, file systems (even the native BFS) are handled via plug-ins 
called add-ons. Download a file system add-on, drop it into place, and 
you have the immediate capability to read (and often write to) alien 
file systems. Out of the box, every BeOS machine, whether x86 or 
PowerPC, can read and write BFS, HFS, HFS+, FAT16, and FAT32 volumes. It
 can also read (but not write to) ext2fs and NTFS. More obscure file 
system add-ons can be written by developers and posted for others to 
use. OS X did a great job of reading a FAT32 volume I stuck in my G4 for
 a while, but as far as I know, does not handle other file systems as 
elegantly.


<h3>Finder</h3>
 
Overall, my experience with the OS X Finder has been a wash -- it's both
 better and worse than the BeOS Tracker. On one hand, I love and use 
constantly the horizontal scrolling column view. And dynamic resizing of
 icons is a nice touch. On the other hand, the current Finder does not 
offer spring-loaded folders, as OS 9 and BeOS do. Be's right-click 
scroll | navigate mechanism provides the fastest means of navigating, 
copying, and moving files around in a file system of any I've 
encountered.

<div align="center">
<a href="http://www.birdhouse.org/beos/refugee/horiz_scroll.gif" target="_blank"><img src="/images/TalesBeOS-horiz_scroll_thumb.jpg" alt="horiz" border="0" height="161" width="400"></a>
</div>
<i>The Finder's horizontal scrolling view is easy to work in and quite 
elegant, but I still miss spring-loaded folders. Click for larger  
version.</i>

But my real complaint with the Finder is that it does a poor job of 
displaying large quantities of information at once. The default Finder 
font is too large, and is not user-configurable. However, the 3rd-party 
Tinker Tool will allow you to change the Finder font. Since Tinker Tool 
only exposes existing but hidden preferences in the OS, it seems 
probable that Apple will open this up in the future.

Which leads to yet another complaint: Compared to BeOS, OS X is 
downright hostile to long filenames. Sure, OS X now supports filenames 
up to 255 characters just like BeOS, but displaying long filenames is a 
pain because of that huge Finder font. Worse, something about the LFN 
API (I'm not a programmer) makes it very difficult to add LFN support to
 applications. When it came time to move my MP3 collection from BeOS to 
OS X via FTP, I found that both Interarchy and Fetch, both of which are 
Carbonized, truncated the filenames on transfer (I finally solved that 
one by putting via FTP from the BeOS machine to the OS X box, rather 
than the other way around). Another day, I was trying to export movies 
from iMovie with filenames long enough to describe all the video and 
audio codecs and settings I was using, for the purposes of comparison. 
The filenames were truncated with garbage characters when viewed in the 
Finder. 

And neither of the two most popular MP3 encoding tools for OS X -- 
iTunes and Audion -- give you any control whatsoever over file naming 
convention. Every MP3 encoder I've tried on any platform offers a dialog
 giving the user full control over how the MP3 filenames should be 
constructed. But both of these tools simply spit out <tt>songname.mp3</tt>.
 Sure, they're nested in artist and album parent folders, as is also the
 case on other platforms, but the filenames are next to useless without 
the parent folders or ID3 tags. Fine for personal use, but rotten for 
(god forbid) Internet use. Since Apple wants to be the digital hub of my
 entertainment life, they'll need to recognize that MP3 storage is one 
of the most common / popular situations where people use very long 
filenames. OS X apps need to learn to start creating them, and the 
Finder needs to become more adept at displaying them.


<div align="center">
<img src="/images/TalesBeOS-shortnames.gif" alt="shortnames" height="330" width="535">
</div>
<i>Short filenames like these are no way to treat your MP3 collection, 
but neither iTunes nor Audion will generate anything but. Then again, 
this Finder view is terrible at displaying long filenames. But on the 
other other hand, being able to preview MP3s and movies directly in the 
Finder is pretty cool...</i>


The BeOS Tracker uses a technology called "node monitoring" which lets 
the Tracker give instant feedback to the user and to other apps. For 
example, you can see the size of a file increase in the Tracker's info 
panel in real time as it's being downloaded from the Internet. Fancy 
node monitoring need not be a priority for Apple, but there's one area 
where something similar should be considered important: Finder views 
don't seem to reflect changes in the filesystem until forced to. Try 
this: Open a Terminal session and a Finder window on the same folder. 
Type <tt>touch foo</tt> and watch the Finder. In BeOS, "foo" appears in 
the Tracker instantaneously. In Windows, the change is reflected 
quickly. In OS X, the file doesn't show up until I click in that Finder 
view. This becomes a problem on occasssion when unpacking a tar.gz 
archive, and the contents don't appear on the desktop until I basically 
force them to.



<h3>Sherlock Shmerlock</h3>

The OS X Find panel is still known as Sherlock, and basically gets the 
job done, but is a bit too cutesy for my tastes. Cosmetics aside, search
 capabilities under OS X are not as flexible as they are BeOS, with its 
virtual database. Attributes aside, Sherlock won't even let me limit my 
search to specific file types (though the Custom search panel does offer
 a few generic type categories).  




More problematic, though, is the difference in the way the two systems 
create indexes. Indexed file systems provide lightning-fast search 
results. BeOS indexes most attributes and keeps its index up to date 
automatically, every time a file or attribute is added, modified, or 
removed. But before you can perform fast searches with Sherlock, you 
have to let it index your file system, an excruciatingly slow process. 
One volume on my machine, with around 8,000 MP3s, took almost four hours
 to index. I'm not kidding.
Another cool advantage to BeOS queries is that they can be saved for 
later execution. Drag a query onto the desktop and have instant access 
to all emails from a certain person, or all MP3s downloaded in the past 
five days, or all bookmarks related to Mac OS (BeOS bookmark files have 
keyword attributes), or whatever you like. Queries are always live and 
real-time, so you always get the freshest data, immediately. You can 
even "navigate" a query with the right-click | scroll technique 
mentioned earlier, so you don't even to have to "launch" a query to get 
at any one of the items in its found set. Sherlock offers nothing 
similar.

Sherlock's one advantage* over BeOS queries is that it allows searching 
on actual file contents, rather than just filename and attributes. BeOS 
users wanting to search through file contents have to resort either to 
bash tools or to the 3rd-party Tracker add-on <a href="http://www.bebits.com/app/1306" target="_blank">Tracker Grep</a>.
 Speaking of which, I know that Mac OS 9 had context menus for the 
Finder which allowed functionality similar to that provided by BeOS 
Tracker add-ons. Having the functionality of the file manager be 
essentially infinitely expandable is a powerful feature, and I'm looking
 forward to seeing that functionality restored in OS X.

<i>* Sherlock has other advantages if you want to use it to search the 
Internet, but I'm happy with the mighty Google, and get the impression 
from talking to other people that Sherlock is used for file finding the 
vast majority of the time.</i>

<h2>Miscellaneous Moans and Groans</h2>


So, those are my biggest complaints about OS X. But there are other, smaller differences I have to get off my chest.


<h3>Scripting</h3>

OS X embraces and enhances the time-honored AppleScript system for 
automating tasks. AppleScript is a pretty cool language, with one big 
disadvantage -- you have to learn it,  even if you already consider 
yourself a master in another scripting language.

BeOS takes a different approach to application scripting. Applications 
provide whatever array of scriptable "hooks" they deem appropriate, and 
expose / document them as they see fit. These hooks are addressable by 
the BeOS interapplication messaging model, the BMessage. BMessages can 
be sent from within compiled applications, or from scripts. From what 
kind of scripts? Any kind of scripts! Bash, perl, Python, PHP, REBOL, 
whatever you like and know. All that's required for any scripting 
language to talk to any application is a command-line utility called 
"hey," which is conceptually very similar to the Mac OS "tell" command 
found in AppleScript.

As long as your scripting language of choice can invoke "hey," or can 
otherwise send BMesssages, it can be used to script the behavior of 
applications running on the system. 

But while the BeOS scripting system is more flexible than Apple's 
system, the reality is that Apple is much larger, there are more 
scriptable Mac OS applications out there, and there are far, far more 
AppleScripts than hey scripts available to make your daily computing 
life easier and more productive.

I don't mind AppleScript. I wish the system were open to other languages, but AppleScript does a fine job, and is very powerful.


<h3>Keyboardability</h3>

Mac OS has never stood up to other operating systems in the 
keyboardability department. OS X is a little better than OS 9 in this 
regard, but still has some puzzling omissions. For example, it is not 
possible to tab around or arrow-key amongst the buttons in dialog boxes,
 which means reaching for the mouse. MS Windows dialogs also have a 
shortcut key for each possible field and button, which makes many tasks 
much faster. For example, if I'm doing a search and replace in a Windows
 app, Alt+A is going to activate the Replace All button rather than the 
default Replace. In OS X, I have to stop and reach for the mouse, which 
interrupts the workflow and the train of thought.

<div align="center">
<img src="/images/TalesBeOS-dialog.png" alt="dialog" height="258" width="187">
</div>
<i>I have two problems with OS X dialogs. 1) You can tab through fields 
with the Tab key, but you can't use the arrow or tab keys to move 
between buttons. 2) Buttons don't have associated trigger keys, which 
means you can't activate any but the default button from the keyboard. 
If I want to Replace All from this BBEdit dialog, I'll have to reach for
 the mouse. </i> 


For the record, I was never completely happy with BeOS' keyboardability 
either, and found Linux inconsistent here (Gnome and KDE dialogs behave 
differently, for example). I've never used an OS that was as 
keyboardable as Windows, and have never understood why it's so hard for 
other OSes to catch up with Windows here.

As with BeOS, Cmd-Tab cycles between open apps rather than toggling 
between the current and the last-used app (yes, there are third-party 
solutions for this). The Windows and Linux Alt+Tab method is far more 
efficient. It just is.

There is an "Enable full keyboard access" panel in the System Prefs, but
 it doesn't get you very far. E.g. you can use a hotkey to activate an 
app's toolbar, but then have to arrow around to get to things. Windows 
gives us a trigger for each menu and each menu item. Thus, getting a 
word count in Word for Windows is a quick Alt+T, W. Getting the same in 
Word for OS X is yet another reach, move, navigate, click -- a 
mouse-driven workflow interruption that takes a good four to five times 
longer to accomplish. 

There are other old Mac OS keyboard habits which are retained in OS X, 
such as Home and End keys moving to the top and bottom of the document 
rather than start or end of the current line. As a result, the Home and 
End keys sit unused on the keyboard, because the need to move to the top
 or bottom of a document is extremely rare. To get to the start or end 
of the current line in Mac OS, you use the Cmd+right/left arrow 
shortcuts. These aren't as easy to learn, as intuitive, or as easy to 
reach. 


The same argument applies to launching files and folders from the Finder
 with the Enter key. In Mac OS, Enter puts you into rename mode. How 
often do you want to rename something compared to how often you want to 
launch it? In Mac OS, you need to hit Cmd-O to "open" a file or folder. 
Why not have the most-used action be the default for the Enter key, and 
the less-used action (renaming) be a hotkey? (In BeOS, rename is Alt+E).


Yes, I know that muscle memory is worth a lot, but user testing should 
make it easy to see which tasks are performed most often. Common sense 
dictates mapping the easiest / most plainly marked keys to those tasks. 
Or am I missing something?


<h3>Workspaces</h3>

I'm pretty surprised to see some equivalent of workspaces missing from 
OS X. In BeOS, you get up to 32 virtual desktops to spread your apps and
 windows amongst. Each desktop can have a different resolution and color
 depth, and a different background color or bitmap. Users can toggle 
through desktops 1-12 with the Alt+Fx keys, and can move windows from 
one workspace to another by clicking and holding the window's title tab 
while switching workspaces. BeOS also includes a Workspaces panel that 
lets you drag apps between workspaces visually, if you prefer. Linux has
 similar tools, though none I've seen are quite as elegant as those in 
BeOS.

After you get used to working in workspaces, it's hard to go back to a 
single desktop. They're a major usability advantage, have been around in
 various forms for 15 years, and just make good sense. The only 
3rd-party utility I've seen for OS X to replicate this behavior is <a href="http://www.Mac%20OS%20Xapps.com/article.php?story=20010207042546723" target="_blank">Space</a>.
 Space will indeed clear your desktop so you can launch other apps in a 
clean environment, but that's about it. This should be an OS-level 
service, and one I hope more OS X users will begin to demand it from 
Apple.



<h3>Dotfiles</h3>

I love the Samba connectivity in OS X, but am frustrated that the Finder
 creates .dotfiles in every directory it touches on the remote SMB host.
 This, unfortunately, puts OS X users in the uncomfortable position of 
not being able to use their Macs on work and school networks without 
littering the directory listings for others on the same network. And 
I've seen posts from more than one user complaining that their sysadmins
 wouldn't allow them to continue using OS X's SMB tools if they couldn't
 get this fixed. So far, I haven't seen a fix posted anywhere. Let's 
hope one is forthcoming.



<h3>Window Positions</h3>

This is fairly minor, but it seems that some apps remember their window 
positions when closed and some do not. Mail.app and Internet Explorer do
 remember their exact size and position between runs, but Terminal and 
many others do not. This is another good candidate for consistency in 
the user experience.



<h3>Cropping Images</h3>

Another fairly minor point: In BeOS, the concept of snippets / clippings
 is extended to images. Launch an image in the built-in ShowImage app, 
drag out a region of it, and drag it to the desktop -- you get a new 
image file containing just that selection. I've never seen an easier way
 to crop images and screenshots in any app, any platform.

OS X offers something good enough and similar to nearly make up for it 
though -- Cmd-Shift-4 activates screenshot mode, but gives you a set of 
cross-hairs. Drag out a selection and that region is saved to the 
desktop as a new image file. Very nice, but limited to screenshots, 
rather than all images, as you get with BeOS (of course, one can always 
take a regional screenshot of a screenshot...)


<h3>Case (In)sensitivity</h3>

Open a Terminal and type:

<pre>touch foo
touch Foo
</pre>

The shell returns no errors, so you conclude that OS X is properly case 
sensitive. But get a directory listing, and you'll find that you've got a
 "foo," but no "Foo." As it turns out, the problem is in the filesystem,
 not in the OS -- HFS+ is case-respecting, but case-insensitive. Maybe 
that's old-hat for old-timers, but to me it seems just  plain weird. As 
if Apple got started on case-sensitivity but never got around to 
finishing it. Those  who want true case sensitivity need to install OS X
 with UFS, rather than HFS+. I'm sure someone somewhere can provide a 
whole host  of reasons why  HFS+ was constructed this way, but I still 
hope  to see true  case sensitivity in HFS+ in the future. BeOS (or, 
rather, BFS) got this one right.





<h2>All Told, Life Is Good</h2>

I was once fond of referring to BeOS as "the promised land" of operating
 systems. Well, I wasn't wrong -- it really was, in many ways. 
Unfortunately, BeOS never attracted enough visitors to turn the promised
 land into a thriving metropolis. But the best OS in the world ain't 
worth jack without millions of users, billions of dollars, and 
kajillions of programmer hours flowing through it. 

While OS X can't boast about jaw-dropping performance like BeOS could 
(although the new Core Audio services offer audio latencies nearly as 
low as Be's, and in some cases (MIDI and jitter) even better than Be's),
 and while its file system is mesozoic in comparison to Be's, the 
"traction" problem that always plagued BeOS is not a problem for OS X. 
There are users. The world is paying attention. Multi-million dollar 
companies are releasing polished, mature applications for it. The press 
is taking notice. The same sort of excitement that filled the BeOS 
community with eagerness for the future is taking hold in the OS X 
community. 


Do I think Apple should have bought Be when they had the chance? Yes and
 no. On one hand, Apple would have gotten a fantastic architecture on 
which they could build their modern OS. And OS X would have a 
state-of-the-art filesystem and superior multithreading / multitasking 
today. OS X might have gotten out the door sooner, and it would be a 
faster, more efficient operating system. 



Those observations are in no way meant to disparage Darwin or the many 
NeXTStep technologies that live on in OS X. Together, they form a 
rock-solid OS core with a mostly great user experience. Rather, I mean 
that Be had achieved "the grace of the Mac, the power of Unix" nearly a 
decade before Apple got OS X out the door, and that many of the 
complaints I list above would not be issues for OS X today.

But. Apple would not have gotten Steve Jobs back if they had purchased 
Be. They would have gotten Jean-Louis Gass閑 and Steve Sakoman instead. 
JLG is a brilliant man, a rare literate intellectual in a sea of stuffed
 shirts. Despite the ultimate failure of Be, I think he's got his head 
screwed on straight, and is a man of true vision -- a fine CEO. But 
Steve Jobs is Steve Jobs, and Steve Jobs makes things happen. He has 
pulled Apple out of a long downward spiral, has succeeded in finally 
dragging Mac users kicking and screaming into the 21st century, and is 
doing it with tremendous style. While I've said just the opposite in the
 past, I now believe Apple ultimately made the right decision by going 
with NeXT and Jobs rather than Be and Gass閑.

In software development you don't often get a chance to break all the 
rules and start over. Being able to start from scratch was Be's greatest
 trump card. Apple <i>sort of</i> had that opportunity. OS X is a brand 
new operating system, yes, but it is also a mutt bred from Unix and 
NeXTStep -- two truly excellent, but also historically laden operating 
systems. Apple also got dealt the backwards compatibility card, both 
technologically (so that old Mac apps would continue to run) and 
psychologically (there had to be enough similarities between pre-X Mac 
OS and OS X that the existing userbase would not become alienated. 

All of that is a long way of saying that I truly love what Apple has 
created in OS X and am happy to have made the switch. But I also lament 
that OS X falls so short of BeOS in a few important categories. Now that
 OS X is out there in the field and developers are busily coding for 
Carbon and Cocoa, it's going to be much harder for them to change the 
application binding policy (for example) than it would have been if they
 had gotten it right prior to release. Not impossible, but much harder.


The trouble with BeOS is that gets under your skin and stays there. BeOS
 showed the world how much power is really locked away in their 
computers, and how much efficiency is wasted by bloated operating 
systems. It showed the world what can be done when a company sits back, 
examines all the problems in the market's OS offerings, and decides to 
build something that doesn't have those problems. 

At the height of the BeOS revolution that never really happened, it 
seemed that the world couldn't possibly do anything but see the light 
and switch to BeOS. In retrospect, BeOS seems like little more than a 
tremendously expensive proof-of-concept. But that's a pessimistic view 
of things. I agree with Urban Lindeskog, who recently posted on a Be 
mailing list:

<blockquote>
... in that sense BeOS has not been a waste of time, on the contrary. It
 has added to the collective knowledge, and showed us some interesting 
views of the art of computing.
</blockquote>

In any case, anyone who has spent time with BeOS is forever spoiled, their expectations for OS technology permanently affected. 




As a migrating user, I'm torn between admiration for and frustration 
with OS X. But I know that, deep down, Jobs and Gass閑 have similar 
ideas about creating the ultimate user experience, and about bringing 
together the ultimate in ease of use with the ultimate in power and 
flexibility. Gass閑 never got to finish painting in the details of his 
vision. Jobs has just gotten started on his.
 
<b>Note: The publication of this article  generated more than 500 email 
responses. Rather than respond to everyone individually, I've written an
 addendum to this document  summarizing reactions and my responses to 
them, as well as errors in this piece. Please read <a href="http://www.birdhouse.org/beos/refugee/redux.html">BeOS Refugee Redux</a> before responding to this  article.</b>

<blockquote>
<i>Many thanks to Irfon Kim-Ahmad, Kurt von Finck, Balatro, Allen 
Brunson, and Jim Rippie for their comments on and contributions to this 
piece.</i>
</blockquote>

_【译文结束】_

[译者Don Liu注：由于译者本人并没有苹果电脑的使用经历且英文水平有限，其中难免有疏漏之处，请不吝指出。Email: dongliucn@gmail.com]

(<a href="http://www.birdhouse.org/beos/refugee/beos_osx.pdf" target="_blank">本文英文版PDF下载</a>)


