---
lng_pair: UN3_SE
title: 基于SSM的动物档案管理系统
author: 张靖祥
category: 课程项目
tags: [Java, 全栈开发]
img: ":UN_3_SE/demonstration/background.gif"
date: 2020-07-20 00:00:00
---

### 项目介绍

这个项目是软件工程课程的项目，我们的项目组共有6名成员。<!-- outline-start -->我们使用SVN作为项目管理工具，Myeclipse作为开发工具。本项目采用Java、SSM框架开发，采用MySQL作为后端数据库。<!-- outline-end -->在编程之前，我们做了大量的项目分析，以确保项目的合理性和正确性，比如业务研究，需求分析等。虽然我们小组有6名成员，但我们参与完成了项目的每一个步骤，以确保我们能在软件工程课程中学到尽可能多的东西。

### 背景知识

模式动物（如小鼠、大鼠）和人类具有相似的特征，在研究时很重要。一个研究设施中有成千上万的模式动物，管理这些动物是一个大问题。因此，有必要开发一个动物档案管理系统来记录和管理动物，如记录动物的体重、做实验的时间等。

在开发系统之前，我们做了详细的调查，编写了详细的开发计划，并使用Rational Rose作为统一建模语言（UML），文档如下:
- 业务研究报告
- 需求分析报告
- 概要设计报告。
- 数据库设计报告
- 详细设计报告
- 编码规范。
- 软件手册

### 项目展示

由于开发的步骤比较复杂，所以我把演示部分放在了前面。下面展示的是登录页面。

![登录](:UN_3_SE/demonstration/login.png){:data-align="center"}

为了使我们的登录页面与众不同，并在其他组中脱颖而出，我添加了一个黑客帝国风格的背景。

![背景](:UN_3_SE/demonstration/background.gif){:data-align="center"}

我们的系统有6个主要模块，我们组的每个成员开发了系统的一部分:

- 档案添加
- 档案修改
- 档案查询
- 档案初始化
- 档案授权管理
- 档案推广

我的工作是开发档案修改模块，因此我只演示这一部分。用户在系统中可以编辑或删除5种类型的档案，分别是:

- 动物档案
- 动物实验档案
- 动物健康档案
- 动物繁殖档案
- 动物饲料档案

这是我的档案修改模块的主界面

![主界面](:UN_3_SE/demonstration/main.png){:data-align="center"}

以动物存档为例，下图展示了用户如何编辑动物存档文件：

![档案编辑](:UN_3_SE/demonstration/file_edit.png){:data-align="center"}

删除动物档案：

![档案删除](:UN_3_SE/demonstration/file_del.png){:data-align="center"}

每当用户编辑或删除一个文件时，数据库中都会有一条日志记录，超级管理员可以查看所有日志: 

![日志](:UN_3_SE/demonstration/log.png){:data-align="center"}

删除文件是危险的行为，因此，用户不能直接删除文件，只能提交删除文件的申请。管理员可以查看所有删除文件的申请，并决定是否批准该应用程序删除文件，或拒绝该应用程序保留文件。 

![审核](:UN_3_SE/demonstration/check.png){:data-align="center"}

## 配置SVN

SVN是一个项目管理工具，类似于git。SVN和git的不同之处在于，SVN是一个集中式的工具，需要一个服务器来安装SVN，所有的用户需要连接到这个SVN服务器，而git是一个分布式的工具，所有的用户都有一个完整的项目开发历史。 

该部分是由我来完成的：

![SVN](:UN_3_SE/SVN.png){:data-align="center"}

这是我的SVN配置[笔记](https://github.com/Jingxiang-Zhang/AnimalArchiveManagement_JAVA_SSM_SVN/blob/main/note/SVN%20Configuration.pdf)。

### 调研与文件

#### 业务调研

在我们撰写文档的开始，我们首先做了业务，弄清楚该公司是如何运作的。我们做了以下的调研:  

- 组织结构
- 部门工作内容  
- 岗位工作内容
- 业务流程图
- 业务表单  
- 特别期许

我只展示了一部分，查看详细文档请点击[这里](https://github.com/Jingxiang-Zhang/AnimalArchiveManagement_JAVA_SSM_SVN/blob/main/document/1.%20Business%20Research%20Report.pdf)。

模式动物公司组织结构：

![组织结构](:UN_3_SE/document/business_research/company_structure.png){:data-align="center"}

业务流程图：

![业务流程图](:UN_3_SE/document/business_research/Level_1_Business_Flow_Chart.png){:data-align="center"}

#### 需求分析

在了解了他们公司的运作情况后，我们尝试分析了他们的需求，得到了如下的结论清单:  

- 案例分析  
- 数据字典  
- 用例描述  
- 领域类图  
- 非功能性需求 

同样的，我只展示一部分，查看详细文档请点击[这里](https://github.com/Jingxiang-Zhang/AnimalArchiveManagement_JAVA_SSM_SVN/blob/main/document/2.%20Requirements%20Analysis%20Report.pdf)。

产品功能结构图：

![功能结构图](:UN_3_SE/document/requirement_analysis/function_structure.png){:data-align="center"}

数据字典：

![数据字典](:UN_3_SE/document/requirement_analysis/data_dictionary.png){:data-align="center"}

用例描述：

![用例描述](:UN_3_SE/document/requirement_analysis/use_case.png){:data-align="center"}

事务流程图：	

![事务流程图](:UN_3_SE/document/requirement_analysis/use_case.png){:data-align="center"}

#### 概要设计

在分析了公司的需求之后，我们开始了系统的设计各个部分，我们做了以下工作：

- 概要设计
- 时序图设计
- 活动图设计
- 系统状态图设计
- 类图设计
- 业务逻辑设计
- 异常处理设计
- 包图设计
- 软件架构和组件图设计
- 硬件配置图设计

点击[此处](https://github.com/Jingxiang-Zhang/AnimalArchiveManagement_JAVA_SSM_SVN/blob/main/document/3.%20Design%20Summary%20%20Report.pdf)查看完整版报告。

概要设计：

![概要设计](:UN_3_SE/document/design/preliminary.png){:data-align="center"}

时序图设计：

![时序图](:UN_3_SE/document/design/sequence.png){:data-align="center"}

活动图设计：

![活动图](:UN_3_SE/document/design/avtive.png){:data-align="center"}

系统状态图设计：

![系统状态图](:UN_3_SE/document/design/phase.png){:data-align="center"}

类图设计：

![类图](:UN_3_SE/document/design/interface.png){:data-align="center"}

包图设计：

![包图](:UN_3_SE/document/design/package.png){:data-align="center"}

软件架构和组件图设计：

![组件图](:UN_3_SE/document/design/component.png){:data-align="center"}

硬件配置图设计：

![硬件配置图](:UN_3_SE/document/design/system.png){:data-align="center"}

#### 数据库设计

在开始我们的软件设计之前，我们需要尽可能详细地设计数据库，以减少不必要的数据修改。在这个项目中，我们使用MySQL作为我们的数据库。  

- 数据库命名规范  
- 数据库实体关系设计  
- 数据库逻辑设计  
- 数据库物理设计  
- 数据库表单设计  
- 数据库索引设计  
- 数据库视图设计  
- 数据库授权设计 

点击[此处](https://github.com/Jingxiang-Zhang/AnimalArchiveManagement_JAVA_SSM_SVN/blob/main/document/4.%20Database%20Design%20Report.pdf)查看完整版报告。

数据库实体关系设计：

![数据库实体关系](:UN_3_SE/document/database/entity.png){:data-align="center"}

ER图

![ER图](:UN_3_SE/document/database/ER.png){:data-align="center"}

#### 详细设计

在这一部分，我们进行了项目软件的设计，主要做了以下工作：

- Spring MVC的应用  
- Spring Mybatis的应用  
- 网站界面元素设计  
- 状态实现方法  
- 数据结构详细设计  
- 系统运行详细设计  
- 算法设计 

点击[此处](https://github.com/Jingxiang-Zhang/AnimalArchiveManagement_JAVA_SSM_SVN/blob/main/document/5.%20Detail%20Design%20Report.pdf)查看完整版报告。

#### 编码规范

最后，为了统一编码格式，我们编写了本编码规范手册。点击[此处](https://github.com/Jingxiang-Zhang/AnimalArchiveManagement_JAVA_SSM_SVN/blob/main/document/6.%20Encoding%20Specification.pdf)查看完整版报告。

点击[此处](https://github.com/Jingxiang-Zhang/AnimalArchiveManagement_JAVA_SSM_SVN)查看项目源代码。
