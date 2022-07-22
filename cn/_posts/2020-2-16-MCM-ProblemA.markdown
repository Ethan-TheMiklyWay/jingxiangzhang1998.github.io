---
lng_pair: UN3_MCM
title: 美国大学生数学建模竞赛
author: 张靖祥
category: 竞赛
tags: [Python, 数学]
img: ":UN_3_MCM/ocean.gif"
date: 2020-02-16 00:00:00
---

### 竞赛介绍

<!-- outline-start -->该比赛是2020年数学建模竞赛（MCM）的A题，受海洋温度增长的影响，鱼群将如何移动的问题。<!-- outline-end -->作为团队的一员，我的工作就是编写所有的相关程序，我使用Python作为编程语言。 

### 题目背景

由于全球变暖，海洋温度将持续增长，与此同时，生活在英国周围海洋中的鱼群会向北寻找最适宜的温度。因此，为了捕鱼，渔民将花费更多，而我们的任务就是理清整个过程。 

### 数据爬取与分析

首先，我在[oceanwatch](data from: https://oceanwatch.pifsc.noaa.gov/erddap/griddap)网上爬取了海洋温度数据。这些数据包括从1985年到2014年地球上所有海洋的温度测量结果。 

![数据](:UN_3_MCM/data.png){:data-align="center"}

然后我提取了北大西洋的海洋温度信息，并对其进行着色。 

![北大西洋海洋温度](:UN_3_MCM/data_show.png){:data-align="center"}

从这组图片中，我得出结论，海洋温度确实在升高。为了更好地理解它，我计算了北大西洋的平均温度，得到以下结果： 

![北大西洋海洋平均温度](:UN_3_MCM/average.png){:data-align="center"}

### 预测与总结

我在这部分的工作是对数据进行拟合，并预测未来的趋势。所以我大胆预测，未来的海洋温度会在较短的时间内持续增长，并且上下波动很小，算法的细节可以达到我的项目代码。 

![海洋温度预测](:UN_3_MCM/Ocean_temperature_prediction.png){:data-align="center"}

该动画展示了未来英国附近的海洋的温度变化趋势。

![海洋温度动画](:UN_3_MCM/ocean.gif){:data-align="center"}

最后，我画出了鱼类最适宜温度的等温线，可以用于我的同伴们计算渔民在未来的花费。 

![鱼群最适宜温度的等温线](:UN_3_MCM/future.png){:data-align="center"}

点击[此处](https://github.com/Jingxiang-Zhang/2020_MCM_Problem_A)查看详细信息。
