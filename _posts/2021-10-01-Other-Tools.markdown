---
lng_pair: Tools
title: Miscellaneous Tools
author: Jingxiang Zhang
category: Tools
tags: [C#]
img: ":MT/GeneContrast/contrast.png"
date: 2021-10-01 00:00:00
---

### Introduction
<!-- outline-start -->I made these tools in my free time. Some were made at whim, some were made by my friend's invitation.<!-- outline-end --> Current there are two tools.

### File Package Tool

This is a package tool, used to pack a group of file into one single file, and you can set password while pack the file. It likes a compressed file, but much more simple. I programmed this tool in August 19, 2020, when I designed URP. This tool was programmed by C#.

The main window of this tool:

![main window](:MT/Pack/main.png){:data-align="center"}

You can select a series of files into this tool:

![file selection](:MT/Pack/drop_data.png){:data-align="center"}

Set a password and pack it up:

![set password](:MT/Pack/pack.png){:data-align="center"}

You can unpack the data by the bottom left button.

Click [here](https://github.com/Jingxiang-Zhang/package_tool_Csharp) to get the code of this tool.

### Gene Contrast Tool

By my friend's invitation, I made a tool to contrast the differential between different genes. I programmed this tool by C#.

![main window](:MT/GeneContrast/main.png){:data-align="center"}

You will need to select a .out file. Please read data_example.out to understand the data format, or you can change the source code to fit for your own data format. Here is the demonstration.

![gene contrast](:MT/GeneContrast/contrast.png){:data-align="center"}

Click [here](https://github.com/Jingxiang-Zhang/gene_contrast_Csharp) to get the code of this tool.