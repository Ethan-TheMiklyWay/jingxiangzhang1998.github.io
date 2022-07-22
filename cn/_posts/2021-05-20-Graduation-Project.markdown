---
lng_pair: UN4_GP
title: 基于树莓派的分布式农情数据采集系统
author: 张靖祥
category: 课程项目
tags: [Python, 单片机]
img: ":UN_4_GP/NodeMCU/Broadcast.png"
date: 2021-05-20 00:00:00
---

### 项目介绍

这是我的本科毕业设计，我的项目有4个部分组成，分别是：<!-- outline-start -->Lua语言编写的NodeMCU数据采集和传输，树莓派的数据接收和转发，客户端界面的开发，设计通信协议。<!-- outline-end -->

### 背景知识

精准农业可以帮助管理农业数据，提高产量。为了提高作物产量和农民收入，信息技术已广泛应用于农业生产。本课题设计了一套基于NodeMCU和树莓派的分布式信息采集系统，下面是系统的顶层架构。

![顶层架构](:UN_4_GP/structure.png){:data-align="center"}

- NodeMCU作为单片机，直接与传感器DHT11相连。我用Lua脚本语言设计了一个可以自动检测并连接局域网WiFi程序，自动检测并连接MQTT服务器，读取并传输DHT11传感器数据
- 树莓派搭建Mosquitto服务器用作MQTT通信服务器，同时自动检测局域网内的NodeMCU设备，存储并显示NodeMCU传输的数据。同时开启TCP通信协议，解析并执行来自客户端的数据，同时进行数据的传输。
- 客户端软件作为最上游的平台，负责数据的存储和显示。当客户端软件访问树莓派局域网时，会自动连接树莓派设备，获取数据并控制NodeMCU设备。

这是我工作的技术路线

![技术路线](:UN_4_GP/technique_route.png){:data-align="center"}

### NodeMCU设计

NodeMCU是一款基于ESP8266单片机的开源物联网平台。它具有WiFi模块，可以通过无线网络传输数据，支持多种网络通信协议。DHT11为温湿度传感器，可与NodeMCU连接。因此，我在这个项目中使用DHT11作为数据采集工具。

恶劣的环境会对信号的传输过程产生很大的影响。传统的信号传输协议消耗大，不适合规模大、信号环境差的农业场景。而消息队列遥测传输（MQTT）协议则更适合，因为MQTT协议是一种轻量级、简单、开放且易于实现的协议。这些特点使其具有广泛的应用范围。在这个项目中，MQTT将用于农田传感器（DHT11链接到NodeMCU）与树莓PI之间的数据传输。

在这一部分中，我将设计运行在NodeMCU中的程序。有4个基本功能，分别是:

- WiFi状态监控：确保WiFi连接状态，断开的WiFi自动重连。
- 自动获取MQTT服务器ip地址。
- 传感器数据采集、传输和传感器识别
- 传感器参数采集与控制

#### WiFi状态监控

Lua脚本语言中的WiFi连接模块为非阻塞连接，即调用WiFi连接函数后，会继续执行下面的代码，不会等待WiFi连接完成。这也使得程序的设计变得困难，每次操作都需要判断WiFi连接是否成功。Lua语言开发程序大多使用定时器TMR来实现鲁棒性的设计，计时器是在Lua中实现多线程的唯一方法。定时器可以用于非阻塞函数操作和周期性函数执行操作。因此，如何构建定时器的切换操作是NodeMCU编程的核心。

这是我的设计：

![NodeMCU WiFi状态](:UN_4_GP/NodeMCU/NodeMCU_structure.png){:data-align="center"}

#### 自动获取MQTT服务器ip地址

Mosquitto所在的服务器每隔几秒钟发送UDP广播。一旦NodeMCU接收到广播，它就可以将定位到服务器位置。

![广播](:UN_4_GP/NodeMCU/Broadcast.png){:data-align="center"}

#### 传感器参数获取

为了使该工程更加方便用户，有必要设计一种远程调节参数的控制方法。本项目使用MQTT协议传输控制命令。

![NodeMCU控制](:UN_4_GP/NodeMCU/NodeMCU_control.png){:data-align="center"}

#### 效果展示

开始数据采集：

![效果展示](:UN_4_GP/NodeMCU/demonstration.png){:data-align="center"}

参数设置与WiFi断线重连：

![参数设置与WiFi断线重连](:UN_4_GP/NodeMCU/NodeMCU_WiFi.png){:data-align="center"}

### 树莓派的设计

在这个项目中，树莓派方需要安装Mosquitto服务器、Python、MySQL，同时设置树莓派自动启动SSH功能。树莓PI是一个中间节点，向下连接NodeMCU，向上连接客户端。因此，我需要完成三件事：

- 数据在树莓派的存储
- 从NodeMCU接收数据
- 向客户端发送数据

#### 树莓派的数据模型

![数据模型](:UN_4_GP/Pi/Pi_data_model.png){:data-align="center"}

#### 从NodeMCU接收数据

![接收数据](:UN_4_GP/Pi/Pi_parameter.png){:data-align="center"}

#### 发送数据到客户端

![发送数据](:UN_4_GP/Pi/pi_client.png){:data-align="center"}

#### 效果展示

这是NodeMCU的用户界面，该界面由Python tkinter编写。

![用户界面](:UN_4_GP/Pi/interface.png){:data-align="center"}

这是负载测试，经测试，7个NodeMCU可以在同一局域网内正常工作。

![负载测试](:UN_4_GP/Pi/load.png){:data-align="center"}

### 客户端设计

在客户端，主要功能是存储和显示数据，并向NodeMCU发送指令。数据模型如下:

![数据模型](:UN_4_GP/client/ER.png){:data-align="center"}

客户端软件架构：

![客户端软件架构](:UN_4_GP/client/sequence.png){:data-align="center"}

#### 效果展示

用户登录界面

![登录](:UN_4_GP/client/login.png){:data-align="center"}

主界面：

![主界面](:UN_4_GP/client/main.png){:data-align="center"}

![主界面2](:UN_4_GP/client/main2.png){:data-align="center"}

点击[此处](https://github.com/Jingxiang-Zhang/Graduation-Project---Raspberry-Pi)查看项目代码。
