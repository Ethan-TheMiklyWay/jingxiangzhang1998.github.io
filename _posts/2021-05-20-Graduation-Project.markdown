---
lng_pair: UN4_GP
title: Distributed Agricultural Data Acquisition System Based on Raspberry Pi
author: Jingxiang Zhang
category: Course Project
tags: [Python, Single-Chip]
img: ":UN_4_GP/NodeMCU/Broadcast.png"
date: 2021-05-20 00:00:00
---

### Introduction

This is my undergraduate graduation project. There are 4 parts of my project, which are: <!-- outline-start --> Data acquisition and transmission in Nodemcu node and programmed by Lua. Data receiving and forwarding in Raspberry Pi. Client interface development. Design communication protocol.<!-- outline-end --> 

### Background Information

Precision agriculture can help manage agriculture data and increase the production. In order to increase crop yield and farmers' income, information technology has been widely used in agricultural production. This project designed a set of distributed information collection system based on NodeMCU and Raspberry Pi. Here is the top architecture of the system.

![structure](:UN_4_GP/structure.png){:data-align="center"}

- NodeMCU, as a single chip computer, it connected with the sensor DHT11 directly. I designed a program that can automatically detect and connect LAN WiFi, detect and connect MQTT server, read and transmit DHT11 sensor data through Lua scripting language 
- Raspberry PI is a server to set up mosquito, which is a MQTT communications server. It will automatically detect the NodeMCU device on the LAN, and store and show the data transmitted by NodeMCU. At the same time, It opens the TCP communication protocol, parse and execute the data from the client, and transmit the data in the same time. 
- As the most upstream platform, Client software will store and show the data. When accessing the Raspberry PI LAN, the client software will automatically connects to the Raspberry PI device, obtaining data, and control the NodeMCU device.

Here is the technical route of my works:

![technical route](:UN_4_GP/technique_route.png){:data-align="center"}

### NodeMCU Design

NodeMCU is an open source Internet of Things (IoT) platform based on the ESP8266 single-chip. It has WiFi module that can transfer data by wireless network. It support many network communication protocal. DHT11 is a temperature and moisture sensor, and can be linked to NodeMCU. So, I use DHT11 as data acquisition tool in this project.

Harsh environment will have a great impact on the signal transmission process. Traditional signal transmission protocol is expensive, so it is not suitable for agricultural scenes, which have large scale and poor signal environment. While message queue telemetry transmission (MQTT) protocol is more suitable, because MQTT protocol is a lightweight, simple, open and easy to implement. These characteristics make it applicable to a wide range of applications. In this project, MQTT will be used to transmit data between sensors (DHT11 link to NodeMCU) in farmland and raspberry PI.

In this part, I will design the the program running in NodeMCU. There are 4 essential functions, which are:

- WiFi status monitor: ensure WiFi is connected, and it will auto connected if WiFi disconnected.
- Acquire MQTT server ip address automatically.
- Sensor data acquisition, transmission and sensor identification
- Sensor parameter acquisition and control

#### WiFi Status Monitor

The WiFi connection module in Lua scripting language is non-blocking connection, that is, the following code will continue to execute after the WiFi connection function is called, and the execution will not wait for the WiFi connection to complete. This also makes the design of the program difficult, each operation needs to judge whether the WiFi connection is successful. Lua language development programs mostly use timer TMR to achieve robust programming. Timers are the only way to achieve multithreading in Lua. Timers can be used for non-blocking function operations and periodic function execution operations. Therefore, how to build the timer's switching operation is at the heart of NodeMCU's programming.

Here is my design:

![NodeMCU WiFi status](:UN_4_GP/NodeMCU/NodeMCU_structure.png){:data-align="center"}

#### Acquire MQTT Server IP Automatically

Mosquitto server sends UDP broadcast every a few second. Once the broadcast is received by NodeMCU, it can locate Mosquitto server location.

![broadcast](:UN_4_GP/NodeMCU/Broadcast.png){:data-align="center"}

#### Sensor Parameter Acquisition

In order to make the project more convenient to user, it is necessary to design a control method to adjust the parameter remotely. This project use MQTT protocol to transmit control command.

![NodeMCU control](:UN_4_GP/NodeMCU/NodeMCU_control.png){:data-align="center"}

#### Demonstration

Start data acquisition:

![demonstration](:UN_4_GP/NodeMCU/demonstration.png){:data-align="center"}

Set parameter, and WiFi reconnected after disconnected.

![set parameter and WiFi reconnected](:UN_4_GP/NodeMCU/NodeMCU_WiFi.png){:data-align="center"}

### Raspberry Pi Design

In this project, raspberry Pi side needs to install Mosquitto, Python, MySQL. Set raspberry PI auto start SSH function. Raspberry PI is a intermediate node. It connects NodeMCU on the down side, and connects client on the up side. Therefore, I need to conside 3 things: 

- Storage data in Raspberry Pi
- Receive data from NodeMCU
- Send data to client

#### Data Model in Rasperberry Pi

![Pi data model](:UN_4_GP/Pi/Pi_data_model.png){:data-align="center"}

#### Receive Data from NodeMCU

![Pi receive data](:UN_4_GP/Pi/Pi_parameter.png){:data-align="center"}

#### Send Data to Client

![send data](:UN_4_GP/Pi/pi_client.png){:data-align="center"}

#### Demonstration

Here is the NodeMCU user interface. This interface was programmed by Python, tkinter.

![user interface](:UN_4_GP/Pi/interface.png){:data-align="center"}

This is the load test. According to the test, 7 NodeMCU could work well in the same LAN.

![load test](:UN_4_GP/Pi/load.png){:data-align="center"}

### Client Design

In the client side, the main function is store and show data, send instruction to NodeMCU. Here is the data model:

![data model](:UN_4_GP/client/ER.png){:data-align="center"}

Client software architecture:

![client software architecture](:UN_4_GP/client/sequence.png){:data-align="center"}

#### Demonstration

User login interface:

![login](:UN_4_GP/client/login.png){:data-align="center"}

Main interface:

![main interface](:UN_4_GP/client/main.png){:data-align="center"}

![main interface 2](:UN_4_GP/client/main2.png){:data-align="center"}

To see more about the project, please click [here](https://github.com/Jingxiang-Zhang/Graduation-Project---Raspberry-Pi).
