---
lng_pair: Tools
title: 小工具
author: 张靖祥
category: 工具
tags: [C#]
img: ":MT/GeneContrast/contrast.png"
date: 2020-10-01 00:00:00
---

### 介绍

<!-- outline-start -->我在空闲时间做了这些工具，有些是一时兴起，有些是我朋友的邀请。目前有两种工具。<!-- outline-end -->

### 文件打包工具

这是一个打包工具，用于将一组文件打包成一个单独的文件，也可以在打包文件的同时设置密码。它像一个压缩文件，但是更简单。我在2020年8月19日设计URP时编写了这个工具，该工具是用c#编写的。

工具主界面:

![主界面](:MT/Pack/main.png){:data-align="center"}

你可以选择一系列的文件：

![文件选择](:MT/Pack/drop_data.png){:data-align="center"}

设置密码并打包：

![设置密码](:MT/Pack/pack.png){:data-align="center"}

你可以通过左下角的按钮解包这些文件。

点击[此处](https://github.com/Jingxiang-Zhang/package_tool_Csharp)获取该工具的源代码。

### 基因对比工具

在朋友的邀请下，我做了一个工具来对比不同基因之间的差异，这个工具是我用c#编写的。

![主界面](:MT/GeneContrast/main.png){:data-align="center"}

你需要选择一个.out文件，请参考data_example了解数据格式，也可以修改源代码以适应自己的数据格式，下面是功能演示：

![基因对比](:MT/GeneContrast/contrast.png){:data-align="center"}

点击[此处](https://github.com/Jingxiang-Zhang/gene_contrast_Csharp)获取该工具的源代码。