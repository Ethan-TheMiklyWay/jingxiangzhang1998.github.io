---
lng_pair: UN2_AM
title: Agricultural Modeling
author: Jingxiang Zhang
category: Competition
tags: [Mathematics, C/C++]
img: ":UN_2_AM/profile.gif"
date: 2019-06-15 00:00:00
---

### Preface
I participate in this agricultural modeling competition in the second year of my undergraduate study. At that time, I have no idea how to create animation to demonstrate the whole process. Therefore, I use SketchUp (3D design software) to build the model, and export the image. Then I create a series a image by Photoshop to simulate the transformation, and combine them together by C program language.

### Background Information
In most of the existing carbon dioxide supply systems in agricultural greenhouse, the carbon dioxide supply is uneven, because the air pressure in the different location of the tube is completely different. It is high in the begin of the tube, while it is low in the end of the tube. To solve this problem, we need to design a series of tubes with different size and combine them together. In a real example, ten greenhouse share only one carbon dioxide container, and we need to <!-- outline-start -->make the air pressure in a complex tube system as even as possible.<!-- outline-end -->

### Theoretical Calculation

According to the Static Regain Method, and Energy Equation, we get the following equation

![equation](:UN_2_AM/equation.png){:data-align="center"}

And the sketch of this system:

![sketch](:UN_2_AM/sketch.png){:data-align="center"}

***

### Computer Simulation

![simulation](:UN_2_AM/profile.gif){:data-align="center"}
