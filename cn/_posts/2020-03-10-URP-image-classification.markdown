---
lng_pair: UN3_URP
title: URP - 目标检测与全栈开发
author: 张靖祥
category: 课程项目
tags: [C#, Python, 全栈开发, AI]
img: ":UN_3_URP/realtime_detection.png"
date: 2020-03-10 00:00:00
---

### 项目介绍
<!-- outline-start -->该项目是本科研究项目（URP）<!-- outline-end -->，我们团队花了一年的时间完成这个项目。虽然我们的团队只有3个人，但为了学习更多的知识，我们完全参与了每一个过程。在这里，我只介绍我完成的部分。

### 项目背景

在奶牛场跟踪每一头奶牛是很困难的，但却很重要，因为我们需要知道每一头奶牛的状态。例如，如果我们知道奶牛吃多少食物，我们可以分析哪一头牛更容易生病，我们可以提前做出预警。

因此，我们决定用4个部分来解决这个问题。首先，对奶牛场图像数据进行采集和标记。其次，利用这些数据训练目标检测神经网络（使用tensorflow），并向用户提供检测接口。第三，训练图像分类神经网络。这样我们就可以取视频的帧，通过目标检测网络定位图像中的奶牛，并通过分类来识别奶牛（图像分类部分我就不演示了，因为这不是我的工作）。最后，我们搭建了一个网站，利用检测界面对视频中的奶牛进行检测。


### 数据采集与预处理

该数据于2019年12月14日在北京顺义采集。我们取了牛身体的三部分，分别是牛的背部、牛的侧面和牛的头部。其中牛背图约400张，视频10个，牛侧图700张，视频20个，牛头图150张，视频10个。

![图像采集](:UN_3_URP/image_collection.png){:data-align="center"}

在清理数据之后，我用LabelMe标记数据。

![图像标记](:UN_3_URP/image_tags.png){:data-align="center"}

然后，我使用四种方法来扩充数据集：平移、水平翻转、改变对比度和亮度、图片缩放。

![数据增强](:UN_3_URP/image_augmentation.png){:data-align="center"}

对于视频数据，我通过取出视频中的帧来进行识别。

![视频帧](:UN_3_URP/video_frame.png){:data-align="center"}

### 目标检测	

在这个过程中，我使用了两种方法来检测奶牛。一种是经典的目标检测算法，另一种是深度学习Faster RCNN。最终的方案中，我选择了深度学习。

#### 经典的目标检测算法

![经典算法](:UN_3_URP/classical_method.png){:data-align="center"}

#### Faster RCNN

![Faster RCNN](:UN_3_URP/faster_rcnn.jpg){:data-align="center"}

### 搭建网站

我们使用c# aspx作为后台网站语言，MVC架构。我们的网站主要有5个部分:

![网站架构](:UN_3_URP/web_architecture.png){:data-align="center"}

网站首页

![首页](:UN_3_URP/frontpage.png){:data-align="center"}

上传和管理用户自己的奶牛图片

![奶牛群组的管理](:UN_3_URP/cow_group_management.png){:data-align="center"}

通过新的奶牛图片训练网络

![训练](:UN_3_URP/training.png){:data-align="center"}

你可以随时查看训练日志

![训练日志](:UN_3_URP/training_process.png){:data-align="center"}

训练完成后，可以实时观看监控中的目标检测和身份识别。

![实时监测](:UN_3_URP/realtime_detection.png){:data-align="center"}

点击[此处](https://github.com/Jingxiang-Zhang/C_sharp_full_stack_web_developement_with_VGG_img_classification)获取更多项目信息。
