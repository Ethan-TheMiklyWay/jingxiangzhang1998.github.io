---
lng_pair: UN3_MCM
title: Mathematical Contest in Modeling
author: Jingxiang Zhang
category: Competition
tags: [Python]
img: ":UN_3_MCM/ocean.gif"
date: 2020-02-16 00:00:00
---

### Introduction

This competition is <!-- outline-start -->Mathematical Contest in Modeling (MCM) in 2020, problem A<!-- outline-end -->, predict how the fish will move toward by the influential of ocean temperature growth. As a part of a team, my job was to complete all of relative program of this problem. I use Python as a programming language.

### Background Information

Because of the global warming, the ocean temperature will keep growthing. In the same time, the fish living in the ocean around England will go north to find the optimum temperature. As a result, fisher will need to spend more on catching the fish. And our job was to figure out the whole process. 


### Data Crawling and Analysis

First, I crawled the global ocean temperature data from [oceanwatch](data from: https://oceanwatch.pifsc.noaa.gov/erddap/griddap). Those data include the temperature measure result of all the oceans in the earth, from 1985 to 2014.

![data](:UN_3_MCM/data.png){:data-align="center"}

Then, I extract the ocean temperature information in North Atlantic, and color it.

![ocean temperature in North Atlantic](:UN_3_MCM/data_show.png){:data-align="center"}

From this group of image, I conclude that the ocean temperature is indeed increase. To get a better understanding of it, I computed the average temperature in North Atlantic, and got this:

![average 	ocean temperature in the past in Atlantic](:UN_3_MCM/average.png){:data-align="center"}

### Prediction and Conclusion

My work here was to make a regression of the data, and predict the future trend. Therefore, I make a bold prediction, that the ocean temperature in the future will keep growing in a relative short period, with a little bit fluctuating up and down. The algorithm detail can be reached in my project code.

![ocean temperature prediction](:UN_3_MCM/Ocean_temperature_prediction.png){:data-align="center"}

And I make this animation to demonstrate how the temperature will become in the future.

![ocean temperature animation](:UN_3_MCM/ocean.gif){:data-align="center"}

Finally, I draw the isotherms of fish's favorite temperatures, which can be used for my teammate to calculate fisher's spending in the future.

![isotherm of fish's favorite temperature](:UN_3_MCM/future.png){:data-align="center"}

To see more about the competition, please click [here](https://github.com/Jingxiang-Zhang/2020_MCM_Problem_A).
