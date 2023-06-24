---
tip: translate by openai@2023-06-23 19:41:39
...
---
description: Contributors (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Contributors (Debugging with GDB)
lang: en
resource-type: document
title: Contributors (Debugging with GDB)
---
::: header
Previous: [Free Documentation](Free-Documentation.html#Free-Documentation)]
:::

---

### Contributors to [GDB]


Richard Stallman was the original author of [GDB] distribution approximates a blow-by-blow account.

> 李察·斯托曼是[GDB]发行版的原始作者，近乎一步一步地记录了它。

Changes much prior to version 2.0 are lost in the mists of time.

> *Plea:* Additions to this section are particularly welcome. If you or your friends (or enemies, to be evenhanded) have been unfairly omitted from this list, we would like to add your names!


So that they may not regard their many labors as thankless, we particularly thank those who shepherded [GDB] through major releases: Andrew Cagney (releases 6.3, 6.2, 6.1, 6.0, 5.3, 5.2, 5.1 and 5.0); Jim Blandy (release 4.18); Jason Molenda (release 4.17); Stan Shebs (release 4.14); Fred Fish (releases 4.16, 4.15, 4.13, 4.12, 4.11, 4.10, and 4.9); Stu Grossman and John Gilmore (releases 4.8, 4.7, 4.6, 4.5, and 4.4); John Gilmore (releases 4.3, 4.2, 4.1, 4.0, and 3.9); Jim Kingdon (releases 3.5, 3.4, and 3.3); and Randy Smith (releases 3.2, 3.1, and 3.0).

> 为了让他们不把他们的许多辛勤工作视为毫无回报，我们特别感谢那些带领GDB完成重大版本更新的人：Andrew Cagney（发布6.3、6.2、6.1、6.0、5.3、5.2、5.1和5.0）；Jim Blandy（发布4.18）；Jason Molenda（发布4.17）；Stan Shebs（发布4.14）；Fred Fish（发布4.16、4.15、4.13、4.12、4.11、4.10和4.9）；Stu Grossman和John Gilmore（发布4.8、4.7、4.6、4.5和4.4）；John Gilmore（发布4.3、4.2、4.1、4.0和3.9）；Jim Kingdon（发布3.5、3.4和3.3）；以及Randy Smith（发布3.2、3.1和3.0）。


Richard Stallman, assisted at various times by Peter TerMaat, Chris Hanson, and Richard Mlynarik, handled releases through 2.8.

> 理查德·斯托曼，在不同时期受到彼得·特马特、克里斯·汉森和理查德·米拉尼克的协助，负责发布 2.8 版本。


Michael Tiemann is the author of most of the [GNU] C++ demangler. Early work on C++ was by Peter TerMaat (who also did much general update work leading to release 3.0).

> 麦克尔·蒂曼是[GNU] C++ 解码器的大部分作者。早期C++的工作是由彼得·特马特（他还为发布3.0做了大量的更新工作）完成的。


[GDB] uses the BFD subroutine library to examine multiple object-file formats; BFD was a joint project of David V. Henkel-Wallace, Rich Pixley, Steve Chamberlain, and John Gilmore.

> [GDB]使用BFD子程序库来检查多种对象文件格式；BFD是David V. Henkel-Wallace、Rich Pixley、Steve Chamberlain和John Gilmore的联合项目。


David Johnson wrote the original COFF support; Pace Willison did the original support for encapsulated COFF.

> 大卫·约翰逊写了原始的COFF支持；佩斯·威利森完成了封装COFF的原始支持。

Brent Benson of Harris Computer Systems contributed DWARF 2 support.


Adam de Boor and Bradley Davis contributed the ISI Optimum V support. Per Bothner, Noboyuki Hikichi, and Alessandro Forin contributed MIPS support. Jean-Daniel Fekete contributed Sun 386i support. Chris Hanson improved the HP9000 support. Noboyuki Hikichi and Tomoyuki Hasei contributed Sony/News OS 3 support. David Johnson contributed Encore Umax support. Jyrki Kuoppala contributed Altos 3068 support. Jeff Law contributed HP PA and SOM support. Keith Packard contributed NS32K support. Doug Rabson contributed Acorn Risc Machine support. Bob Rusk contributed Harris Nighthawk CX-UX support. Chris Smith contributed Convex support (and Fortran debugging). Jonathan Stone contributed Pyramid support. Michael Tiemann contributed SPARC support. Tim Tucker contributed support for the Gould NP1 and Gould Powernode. Pace Willison contributed Intel 386 support. Jay Vosburgh contributed Symmetry support. Marko Mlinar contributed OpenRISC 1000 support.

> 亚当·德·布尔和布拉德利·戴维斯贡献了ISI Optimum V支持。佩尔·博斯纳，宗行行，和阿莱桑德罗·弗林贡献了MIPS支持。让-丹尼尔·费凯特贡献了Sun 386i支持。克里斯·汉森改进了HP9000支持。宗行行和长井智之贡献了索尼/新闻操作系统3支持。大卫·约翰逊贡献了Encore Umax支持。Jyrki Kuoppala贡献了Altos 3068支持。杰夫·劳贡献了HP PA和SOM支持。凯斯·帕卡德贡献了NS32K支持。道格·拉布森贡献了Acorn Risc Machine支持。鲍勃·鲁斯克贡献了Harris Nighthawk CX-UX支持。克里斯·史密斯贡献了Convex支持（和Fortran调试）。乔纳森·斯通贡献了Pyramid支持。迈克尔·蒂曼贡献了SPARC支持。蒂姆·塔克贡献了Gould NP1和Gould Powernode的支持。佩斯·威利森贡献了Intel 386支持。杰·沃斯堡贡献了Symmetry支持。马尔科·姆林尔贡献了OpenRISC 1000支持。

Andreas Schwab contributed M68K [GNU]/Linux support.


Rich Schaefer and Peter Schauer helped with support of SunOS shared libraries.

> 理查德·谢弗和彼得·肖尔帮助支持SunOS共享库。


Jay Fenlason and Roland McGrath ensured that [GDB] and GAS agree about several machine instruction sets.

> 杰伊·芬拉森和罗兰德·麦格拉思确保GDB和GAS在几种机器指令集上保持一致。


Patrick Duval, Ted Goldstein, Vikram Koka and Glenn Engel helped develop remote debugging. Intel Corporation, Wind River Systems, AMD, and ARM contributed remote debugging modules for the i960, VxWorks, A29K UDI, and RDI targets, respectively.

> 帕特里克·杜瓦尔、特德·戈尔茨坦、维克拉姆·科卡和格伦·恩格尔帮助开发远程调试。英特尔公司、Wind River Systems、AMD和ARM分别为i960、VxWorks、A29K UDI和RDI目标提供了远程调试模块。


Brian Fox is the author of the readline libraries providing command-line editing and command history.

> 布莱恩·福克斯是提供命令行编辑和命令历史记录的Readline库的作者。


Andrew Beers of SUNY Buffalo wrote the language-switching code, the Modula-2 support, and contributed the Languages chapter of this manual.

> 安德鲁·比尔斯（Andrew Beers）来自纽约州立大学布法罗分校（SUNY Buffalo），他编写了语言切换代码，提供了Modula-2支持，并为本手册撰写了语言章节。


Fred Fish wrote most of the support for Unix System Vr4. He also enhanced the command-completion support to cover C++ overloaded symbols.

> 弗雷德·费希尔为Unix System Vr4编写了大部分支持程序。他还增强了命令完成支持，以涵盖C++重载符号。


Hitachi America (now Renesas America), Ltd. sponsored the support for H8/300, H8/500, and Super-H processors.

> Hitachi America（现为Renesas America）有限公司赞助支持H8/300、H8/500和Super-H处理器。

NEC sponsored the support for the v850, Vr4xxx, and Vr5xxx processors.


Mitsubishi (now Renesas) sponsored the support for D10V, D30V, and M32R/D processors.

> 三菱（现在是Renesas）赞助了D10V、D30V和M32R/D处理器的支持。

Toshiba sponsored the support for the TX39 Mips processor.

Matsushita sponsored the support for the MN10200 and MN10300 processors.

Fujitsu sponsored the support for SPARClite and FR30 processors.


Kung Hsu, Jeff Law, and Rick Sladkey added support for hardware watchpoints.

> 孔许、杰夫·劳和里克·斯拉德基增加了硬件观察点的支持。

Michael Snyder added support for tracepoints.

Stu Grossman wrote gdbserver.


Jim Kingdon, Peter Schauer, Ian Taylor, and Stu Grossman made nearly innumerable bug fixes and cleanups throughout [GDB].

> 吉姆·金登、彼得·沙尔、伊恩·泰勒和斯图·格罗斯曼在GDB中几乎无数次地修复了bug和清理了代码。


The following people at the Hewlett-Packard Company contributed support for the PA-RISC 2.0 architecture, HP-UX 10.20, 10.30, and 11.0 (narrow mode), HP's implementation of kernel threads, HP's aC++ compiler, and the Text User Interface (nee Terminal User Interface): Ben Krepp, Richard Title, John Bishop, Susan Macchia, Kathy Mann, Satish Pai, India Paul, Steve Rehrauer, and Elena Zannoni. Kim Haase provided HP-specific information in this manual.

> 以下人员在惠普公司对PA-RISC 2.0架构、HP-UX 10.20、10.30和11.0（窄模式）、HP实现的内核线程、HP的aC++编译器和文本用户界面（前称终端用户界面）提供支持：Ben Krepp、Richard Title、John Bishop、Susan Macchia、Kathy Mann、Satish Pai、India Paul、Steve Rehrauer和Elena Zannoni。Kim Haase为本手册提供了HP特定的信息。


DJ Delorie ported [GDB] to MS-DOS, for the DJGPP project. Robert Hoehne made significant contributions to the DJGPP port.

> DJ Delorie移植了GDB到MS-DOS，为DJGPP项目提供支持。Robert Hoehne对DJGPP端口做出了重大贡献。


Cygnus Solutions has sponsored [GDB] fulltime include Mark Alexander, Jim Blandy, Per Bothner, Kevin Buettner, Edith Epstein, Chris Faylor, Fred Fish, Martin Hunt, Jim Ingham, John Gilmore, Stu Grossman, Kung Hsu, Jim Kingdon, John Metzler, Fernando Nasser, Geoffrey Noer, Dawn Perchik, Rich Pixley, Zdenek Radouch, Keith Seitz, Stan Shebs, David Taylor, and Elena Zannoni. In addition, Dave Brolley, Ian Carmichael, Steve Chamberlain, Nick Clifton, JT Conklin, Stan Cox, DJ Delorie, Ulrich Drepper, Frank Eigler, Doug Evans, Sean Fagan, David Henkel-Wallace, Richard Henderson, Jeff Holcomb, Jeff Law, Jim Lemke, Tom Lord, Bob Manson, Michael Meissner, Jason Merrill, Catherine Moore, Drew Moseley, Ken Raeburn, Gavin Romig-Koch, Rob Savoye, Jamie Smith, Mike Stump, Ian Taylor, Angela Thomas, Michael Tiemann, Tom Tromey, Ron Unrau, Jim Wilson, and David Zuhn have made contributions both large and small.

> Cygnus Solutions 已赞助全职的 GDB，包括 Mark Alexander、Jim Blandy、Per Bothner、Kevin Buettner、Edith Epstein、Chris Faylor、Fred Fish、Martin Hunt、Jim Ingham、John Gilmore、Stu Grossman、Kung Hsu、Jim Kingdon、John Metzler、Fernando Nasser、Geoffrey Noer、Dawn Perchik、Rich Pixley、Zdenek Radouch、Keith Seitz、Stan Shebs、David Taylor 和 Elena Zannoni。此外，Dave Brolley、Ian Carmichael、Steve Chamberlain、Nick Clifton、JT Conklin、Stan Cox、DJ Delorie、Ulrich Drepper、Frank Eigler、Doug Evans、Sean Fagan、David Henkel-Wallace、Richard Henderson、Jeff Holcomb、Jeff Law、Jim Lemke、Tom Lord、Bob Manson、Michael Meissner、Jason Merrill、Catherine Moore、Drew Moseley、Ken Raeburn、Gavin Romig-Koch、Rob Savoye、Jamie Smith、Mike Stump、Ian Taylor、Angela Thomas、Michael Tiemann、Tom Tromey、Ron Unrau、Jim Wilson 和 David Zuhn 都做出了大大小小的贡献。


Andrew Cagney, Fernando Nasser, and Elena Zannoni, while working for Cygnus Solutions, implemented the original [GDB/MI] interface.

> 安德鲁·卡吉尼、费尔南多·纳赛尔和埃琳娜·赞农尼在Cygnus Solutions工作期间，实施了原始的[GDB/MI]接口。


Jim Blandy added support for preprocessor macros, while working for Red Hat.

> 吉姆·布兰迪在为红帽工作时增加了预处理器宏的支持。


Andrew Cagney designed [GDB]'s architecture vector. Many people including Andrew Cagney, Stephane Carrez, Randolph Chung, Nick Duffek, Richard Henderson, Mark Kettenis, Grace Sainsbury, Kei Sakamoto, Yoshinori Sato, Michael Snyder, Andreas Schwab, Jason Thorpe, Corinna Vinschen, Ulrich Weigand, and Elena Zannoni, helped with the migration of old architectures to this new framework.

> 安德鲁·卡格尼设计了GDB的架构向量。许多人，包括安德鲁·卡格尼、斯特凡·卡雷兹、兰道夫·钟、尼克·达费克、理查德·亨德森、马克·凯特尼斯、格雷斯·塞恩斯伯里、佐藤慶紀、迈克尔·斯奈德、安德烈亚斯·施瓦布、杰森·索尔普、科琳娜·文申、乌尔里希·魏根德、埃莉娜·扎农尼，帮助将旧架构迁移到这个新框架上。


Andrew Cagney completely re-designed and re-implemented [GDB] unwinder, Jeff Johnston the libunwind unwinder, and Andrew Cagney the dummy, sentinel, tramp, and trad unwinders. The architecture-specific changes, each involving a complete rewrite of the architecture's frame code, were carried out by Jim Blandy, Joel Brobecker, Kevin Buettner, Andrew Cagney, Stephane Carrez, Randolph Chung, Orjan Friberg, Richard Henderson, Daniel Jacobowitz, Jeff Johnston, Mark Kettenis, Theodore A. Roth, Kei Sakamoto, Yoshinori Sato, Michael Snyder, Corinna Vinschen, and Ulrich Weigand.

> 安德鲁·卡格尼（Andrew Cagney）彻底重新设计和实现了GDB解开器，杰夫·约翰斯顿（Jeff Johnston）的libunwind解开器，以及安德鲁·卡格尼（Andrew Cagney）的虚拟、哨兵、跳跃和传统解开器。基于架构的更改，每个更改都涉及对架构的帧代码的完全重写，由吉姆·布兰迪（Jim Blandy）、乔尔·布罗贝克尔（Joel Brobecker）、凯文·布特纳（Kevin Buettner）、安德鲁·卡格尼（Andrew Cagney）、斯蒂芬·卡雷（Stephane Carrez）、兰多夫·春普（Randolph Chung）、奥尔扬·弗里伯格（Orjan Friberg）、理查德·亨德森（Richard Henderson）、丹尼尔·雅各布绪（Daniel Jacobowitz）、杰夫·约翰斯顿（Jeff Johnston）、马克·凯特尼斯（Mark Kettenis）、西奥多·A·罗斯（Theodore A. Roth）、桑本慧（Kei Sakamoto）、佐藤義則（Yoshinori Sato）、迈克尔·斯奈德（Michael Snyder）、科琳娜·温森（Corinna Vinschen）和乌尔里希·魏根（Ulrich Weigand）完成。


Christian Zankel, Ross Morley, Bob Wilson, and Maxim Grigoriev from Tensilica, Inc. contributed support for Xtensa processors. Others who have worked on the Xtensa port of [GDB] in the past include Steve Tjiang, John Newlin, and Scott Foehner.

> 克里斯蒂安·赞克尔、罗斯·莫利、鲍勃·威尔逊和Tensilica公司的马克西姆·格里戈里耶夫为Xtensa处理器提供支持。过去在Xtensa版本的[GDB]上工作过的其他人包括史蒂夫·蒋、约翰·纽林和斯科特·弗恩纳。


Michael Eager and staff of Xilinx, Inc., contributed support for the Xilinx MicroBlaze architecture.

> 麦克尔·伊格尔和Xilinx公司的员工为Xilinx MicroBlaze架构提供了支持。


Initial support for the FreeBSD/mips target and native configuration was developed by SRI International and the University of Cambridge Computer Laboratory under DARPA/AFRL contract FA8750-10-C-0237 (\"CTSRD\"), as part of the DARPA CRASH research programme.

> 初始支持的FreeBSD/mips目标和本地配置是由SRI国际和剑桥大学计算机实验室在DARPA/AFRL合同FA8750-10-C-0237（“CTSRD”）下开发的，作为DARPA CRASH研究计划的一部分。


Initial support for the FreeBSD/riscv target and native configuration was developed by SRI International and the University of Cambridge Computer Laboratory (Department of Computer Science and Technology) under DARPA contract HR0011-18-C-0016 (\"ECATS\"), as part of the DARPA SSITH research programme.

> 初始支持FreeBSD/riscv目标和本地配置由SRI国际和剑桥大学计算机实验室（计算机科学与技术系）在DARPA合同HR0011-18-C-0016（“ECATS”）下开发，作为DARPA SSITH研究计划的一部分。


The original port to the OpenRISC 1000 is believed to be due to Alessandro Forin and Per Bothner. More recent ports have been the work of Jeremy Bennett, Franck Jullien, Stefan Wallentowitz and Stafford Horne.

> 据信OpenRISC 1000的原始端口是由Alessandro Forin和Per Bothner完成的。最近的端口是由Jeremy Bennett，Franck Jullien，Stefan Wallentowitz和Stafford Horne完成的。


Weimin Pan, David Faust and Jose E. Marchesi contributed support for the Linux kernel BPF virtual architecture. This work was sponsored by Oracle.

> 魏敏潘、大卫·福斯特和何塞·E·马切西为Linux内核BPF虚拟架构提供了支持。这项工作由甲骨文公司赞助。

---

::: header
Previous: [Free Documentation](Free-Documentation.html#Free-Documentation)]
:::
