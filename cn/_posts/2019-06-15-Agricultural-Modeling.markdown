---
lng_pair: UN2_AM
title: 农建大赛
author: 张靖祥
category: 竞赛
tags: [数学, C语言]
img: ":UN_2_AM/profile.gif"
date: 2019-06-15 00:00:00
---

### 前言
我在大二的时候参加了这次农业建模比赛，当时我并不知道如何制作动画来演示这个过程。所以，我先用SketchUp（3D设计软件）建立模型并导出图像。然后我用Photoshop制作了一系列的图像来模拟变换过程，最后用C语言的程序将它们组合在一起。 

### 背景信息
在农业大棚现有的大部分二氧化碳供应系统中，二氧化碳供应是不均匀的，这是因为不同位置的管道内的空气压力完全不同。在管子开头的地方很高，而在管子的末端则很低。为解决这个问题，我们需要设计一系列不同尺寸的管子，并将它们组合在一起。在某个真实的实例中，十个温室共用了一个二氧化碳容器，而我们需要<!-- outline-start -->使复杂的管道系统中的空气压力尽可能的相同。<!-- outline-end -->

### 理论计算

根据静压复得法、能量方程，我们可以得到如下的方程

![equation](:UN_2_AM/equation.png){:data-align="center"}

通过草图模拟这个系统

![sketch](:UN_2_AM/sketch.png){:data-align="center"}

***

### 计算机模拟

![simulation](:UN_2_AM/profile.gif){:data-align="center"}
