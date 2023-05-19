---
lng_pair: MS_2_CG_1
title: 基于OpenGL的地形渲染
author: 张靖祥
category: 课程项目
tags: [图形学, C/C++]
img: ":MS_2_CG_1/demo.gif"
date: 2023-3-01 00:00:00
---

## 地形渲染项目

<!-- outline-start -->这是计算机图形学课程的第一个作业，在这个项目中，我将通过 OpenGL 渲染地形。 输入的高度图是一张灰度图，图像的每个像素代表地形的高度<!-- outline-end -->

例如，给定如下输入：

![heightmap](:MS_2_CG_1/Heightmap.jpg){:data-align="center"}

渲染结果为：

![render](:MS_2_CG_1/demo.gif){:data-align="center"}


项目配置环境

- Windows系统

- visual studio 2017或更高版本

第三方库：

- GLUT： 用于窗口创建
- GLEW：用于OpenGL核心库
- GLM：OpenGL数学运算库
- jpeg：图像输入输出

键盘与鼠标控制：

- 拖动鼠标：
  - 拖动鼠标左键：模型沿 x、y 轴旋转
  - 拖动鼠标中键：模型沿 z 轴旋转
- Control + 拖动鼠标：
  - Control + 拖动鼠标左键：模型沿 x、y 轴平移
  - Control + 拖动鼠标中键: 模型沿 z 轴平移
- Shift + 拖动鼠标：
  - Shift + 拖动鼠标左键：模型沿 x、y 轴缩放
  - Shift + 拖动鼠标中键: 模型沿 z 轴缩放
- 键盘按键：
  - 数字键 1：点云模式，模型被渲染为点云
  - 数字键 2：线条模式，模型被渲染为线条
  - 数字键 3：三角网格模式，模型被渲染为三角网格，该模式为默认选项
  - 数字键 4：平滑三角网格模式，模型更加平滑
  - 数字键 5：背景图像模式，模型将使用给定的背景图片

如何使用?

1. 点击 TerranRender.sln 打开项目
2. demonstration 文件夹展示了渲染结果
3. release 文件夹包含了项目编译后的版本。运行此文件，你需要提供 1 个额外参数，即高度图的路径。你也可以点击 render.bat 来运行演示用例
4. Bin文件夹包含了visual studio的输出。请注意项目运行需要用到 glew32.dll 与 freeglut.dll，所以你需要确保这两个文件在项目输出的目录中

点击[此次](https://github.com/Jingxiang-Zhang/TerranRender)获取项目源代码。
