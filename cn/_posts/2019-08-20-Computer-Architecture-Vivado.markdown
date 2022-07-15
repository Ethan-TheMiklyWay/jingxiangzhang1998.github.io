---
lng_pair: UN2_CA_V
title: 基于MIPS和VIvado的单周期CPU设计
author: 张靖祥
category: 课程项目
tags: [体系结构]
img: ":UN_2_CA_V/Databus.png"
date: 2019-08-20 00:00:00
---

### 项目介绍
<!-- outline-start -->本课题是基于MIPS指令集和Vivado的32位单周期CPU设计，使用Xilinx公司的xc7a100tfgg484开发板下载运行CPU。<!-- outline-end -->

在设计这个项目的时候，我的团队主要关注了控制器模块、指令获取模块、内存模块和顶层模块的设计。我们参考了教材中的一些重点知识点，包括数据库、解码器、IO接口和ALU的设计。经过模拟仿真后，我们将项目下载到开发板并运行CPU。 

当系统在开发板运行时，CPU将从RAM中读取并运行机器码。机器码由Minisys1Av2.2生成，因此，我编写了控制开关和LED的程序，并用Minisys1Av2.2将其转换成机器码，然后将这些代码导入到RAM中，由Vivado编译整个CPU。


### CPU设计

这是MIPS指令集的数据通路

![数据通路](:UN_2_CA_V/Databus.png){:data-align="center"}

根据数据通路与MIPS，我们可以在Vivado中设计Verilog程序，这是ALU的一些代码片段

![ALU](:UN_2_CA_V/ALU_segment.png){:data-align="center"}

点击[此处](https://github.com/Jingxiang-Zhang/Vivado_MIPS_CPU/blob/main/Vivado-MIPS%20CPU.pdf)获取更多关于CPU设计的细节.

### 汇编程序

这是一个源码乘法程序，它从开关中读取两个数字，并通过ALU计算乘法，最后用LED发送并显示结果

![positive code multiplication](:UN_2_CA_V/positive_code_multiplication.png){:data-align="center"}

![LED](:UN_2_CA_V/LED.png){:data-align="center"}

点击[此处](https://github.com/Jingxiang-Zhang/Vivado_MIPS_CPU)获取完整项目。
