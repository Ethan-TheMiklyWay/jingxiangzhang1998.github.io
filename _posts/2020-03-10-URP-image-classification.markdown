---
lng_pair: UN3_URP
title: URP - Target Detection and Full Stack Development
author: Jingxiang Zhang
category: Course Project
tags: [C#, Python, Full Stack, AI]
img: ":UN_3_URP/realtime_detection.png"
date: 2020-03-10 00:00:00
---

### Introduction
<!-- outline-start -->This project is Undergraduate Research Project (URP), it took our team a year to finish this<!-- outline-end -->. Though our team has three members, we fully participate in every process when we did this, in order to learn more knowledge. Here, I will only talk about my works.

### Background Information

It is difficult to keep track with each cow in dairy farm, while it is crucial because we need to know the status of each cow. For example, if we know how much food it eat, we may analyse that which cow is more easily to get sick, and we can do some security measure to prevent it.

Therefore, we decided to solve this problem by 4 parts. First, collect and tag image data from dairy farm. Second, train the target detection neural network (use tensorflow) with this data, and provide the detection interface to user. Third, train the image classification neural network. So that we could take the frame of video, locate the cow in the image by target dection network, and identify the cow by classification (I will not demonstrate image classification part, because it is not my work). Finally, we set up a website for dairy farmer, and using the detection interface to detect the cows in the video.


### Data Collection and Preprocessing	

The data was collected in December 14th, 2019, in Shunyi, Beijing. We took three parts of cow's body, which are the cow's back, the cow's side and the cow's head. Among them, there are about 400 pictures and 10 videos for the cow's back, 700 pictures and 20 videos for the cow's side, and 150 images and 10 videos for cow's head. 

![image collection](:UN_3_URP/image_collection.png){:data-align="center"}

After data cleansing, I tag the data by LabelMe.

![image tag](:UN_3_URP/image_tags.png){:data-align="center"}

Then, I use four methods to augment the data set: translation, horizontal flip, change contrast and brightness, and expand and shrink. 

![image augmentation](:UN_3_URP/image_augmentation.png){:data-align="center"}

For the video data, I took the frame of the video to do the detection.

![video frame](:UN_3_URP/video_frame.png){:data-align="center"}

### Target Detection	

In this process, I used two methods to detect the cow. One is classical target dectection algorithm, the other is deep learning Faster RCNN. Finally, I choosed deep learning.

#### Classical Detection method

![classical method](:UN_3_URP/classical_method.png){:data-align="center"}

#### Faster RCNN

![Faster RCNN](:UN_3_URP/faster_rcnn.jpg){:data-align="center"}

### Set Up Website

We use C# aspx as our backend website language, MVC architecture. There are 5 mainly part of our website:

![website architecture](:UN_3_URP/web_architecture.png){:data-align="center"}

The front page of website:

![frontpage](:UN_3_URP/frontpage.png){:data-align="center"}

Upload and manage user's own cows pictures

![cow group management](:UN_3_URP/cow_group_management.png){:data-align="center"}

Train the network by the new cows pictures

![train](:UN_3_URP/training.png){:data-align="center"}

You can examine the training log at any time 

![train log](:UN_3_URP/training_process.png){:data-align="center"}

After training the cow pictures, you can watch the realtime video target detection and identity recognition.

![realtime detection](:UN_3_URP/realtime_detection.png){:data-align="center"}

To see more about the project, please click [here](https://github.com/Jingxiang-Zhang/C_sharp_full_stack_web_developement_with_VGG_img_classification).
