---
lng_pair: UN3_SE
title: Animal Archive Management System Based on SSM
author: Jingxiang Zhang
category: Course Project
tags: [Java, Full Stack]
img: ":UN_3_SE/demonstration/background.gif"
date: 2020-07-20 00:00:00
---

### Introduction

This project was the Software Engineering course project, and there were 6 members in our project team. <!-- outline-start -->We use SVN as project management tool, and Myeclipse as our development tool. This project was developed by Java, SSM framework, and use MySQL as back-end database. <!-- outline-end --> Before programming, we did tons of project analysis to ensure rationality and correctness, such as business research, requirements analysis, etc. Although we have 6 members in the group, we fully take part in every step of our project, to make sure we can learn as much as we can in the Software Engineering course.

### Background Information

Animal models (e.g., mice, rats) and humans have the same property, and it is useful in research. There are thousands of animal models in one research facility, and it is a big problem to manage those animals. Therefore, it is necessary to develop a animal archive management system to record and manage the animals, such as the weight of animal, the time of doing experiment, and so on.

Before develop the system, we do a minute investigation, write a detailed development plan, and use Rational Rose as Unified Modeling Language (UML). The documents are as follow:

- Business Research Report
- Requirements Analysis Report
- Design Summary Report.
- Database Design Report
- Detail Design Report
- Encoding Specification.
- Software Manual

### Demonstration

Because the steps of developing it is complicated, I put the demonstration part before the design part. Next come the login page.

![login](:UN_3_SE/demonstration/login.png){:data-align="center"}

To make our login page distinctive and stand out of other group, I append a new front page with the Matrix feature.

![background](:UN_3_SE/demonstration/background.gif){:data-align="center"}

There are 6 main modules in our system, each of our group member developed one part of the system:
- File append
- File update
- File query
- File initiation
- File authority management
- File advertising

My work was to developed file update module. So, I will only demonstrate this part. User could edit or delete 5 types of file in the system, which are:
- Animal archive
- Animal experiment archive
- Animal health archive
- Animal breed archive
- Animal feed archive

The main interface of my file update module:

![main interface](:UN_3_SE/demonstration/main.png){:data-align="center"}

Take the animal archive for a example, the picture below demonstrate how the user edit the animal archive file:

![file edit](:UN_3_SE/demonstration/file_edit.png){:data-align="center"}

Delete animal archive file:

![file delete](:UN_3_SE/demonstration/file_del.png){:data-align="center"}

Each time when a user edit or delete a file, there will be a log record in the database, and super administer can view all the logs:

![log](:UN_3_SE/demonstration/log.png){:data-align="center"}

Delete a file is dangerour. So, a user could not delete a file directly, he can only submit an application to delete a file. The manager could view  all the delete file application, and decide whether approve the application to delete the file, or refuse the application to keep the file.

![check](:UN_3_SE/demonstration/check.png){:data-align="center"}

## SVN Configuration

SVN is a project management tool, like git. The different between SVN and git is that, SVN is a centralized tool, you will need a server to install SVN and all the user need to connect to this SVN server, while git is a distributed tool, all user have a complete project development history.

This part was done by me.

![SVN](:UN_3_SE/SVN.png){:data-align="center"}

This is my [note](https://github.com/Jingxiang-Zhang/AnimalArchiveManagement_JAVA_SSM_SVN/blob/main/note/SVN%20Configuration.pdf) about SVN.

### Investigation and Documents

#### Business Research

In this very begining of our investigation, we did the business research first, to figure out how their company run. We did the following works:

- Company structure
- Works of each department
- Works of each position
- Transaction flow diagram
- Business form
- Expectation

I will only show some part of it, click [here](https://github.com/Jingxiang-Zhang/AnimalArchiveManagement_JAVA_SSM_SVN/blob/main/document/1.%20Business%20Research%20Report.pdf) to view the full version of the report.

Animal model company structure:

![company structure](:UN_3_SE/document/business_research/company_structure.png){:data-align="center"}

Transaction flow diagram:

![transaction flow diagram](:UN_3_SE/document/business_research/Level_1_Business_Flow_Chart.png){:data-align="center"}

#### Requirements Analysis 

After we understood how their company work, we try to analyse their requirement, and got the following conclusion list:

- Case analysis
- Data dictionary
- Use case description
- Domain class diagram
- Non-functional requirements

Similarly, I will only show some part of it, click [here](https://github.com/Jingxiang-Zhang/AnimalArchiveManagement_JAVA_SSM_SVN/blob/main/document/2.%20Requirements%20Analysis%20Report.pdf) to view the full version of the report.

Product functional structure diagram:

![functional structure](:UN_3_SE/document/requirement_analysis/function_structure.png){:data-align="center"}

Data dictionary:

![data dictionary](:UN_3_SE/document/requirement_analysis/data_dictionary.png){:data-align="center"}

Use case:

![use case](:UN_3_SE/document/requirement_analysis/use_case.png){:data-align="center"}

The transaction flow diagram:	

![transaction flow](:UN_3_SE/document/requirement_analysis/use_case.png){:data-align="center"}

#### Design Summary

After analyse the company requirement, we started to design our system part by part, we did the following works:

- Preliminary design
- Sequence diagram design
- Activity diagram design
- System status diagram design
- Class diagram design
- Business logic design
- Exception handling design
- Package diagram design
- Software architecture and component diagrams design
- Hardware configuration diagram design

Click [here](https://github.com/Jingxiang-Zhang/AnimalArchiveManagement_JAVA_SSM_SVN/blob/main/document/3.%20Design%20Summary%20%20Report.pdf) to view the full version of the report.

Preliminary design:

![preliminary design](:UN_3_SE/document/design/preliminary.png){:data-align="center"}

Sequence diagram design:

![sequence diagram](:UN_3_SE/document/design/sequence.png){:data-align="center"}

Activity diagram design:

![activity diagram](:UN_3_SE/document/design/avtive.png){:data-align="center"}

System status diagram design:

![status diagram](:UN_3_SE/document/design/phase.png){:data-align="center"}

Class diagram design:

![class diagram](:UN_3_SE/document/design/interface.png){:data-align="center"}

Package diagram design:

![package diagram](:UN_3_SE/document/design/package.png){:data-align="center"}

Software architecture and component diagrams design:

![component diagram](:UN_3_SE/document/design/component.png){:data-align="center"}

Hardware configuration diagram design:

![hardware diagram](:UN_3_SE/document/design/system.png){:data-align="center"}

#### Database Design

Before we start our software design, we need to design database as detailed as possible, in order to reduce the unnecessary data modification. In this project, we use MySQL as our database.

- Database naming conventions
- Database entity relationship design
- Database logic design
- Database physical design
- Database form design
- Database index design
- Database view design
- Database authorization design

Click [here](https://github.com/Jingxiang-Zhang/AnimalArchiveManagement_JAVA_SSM_SVN/blob/main/document/4.%20Database%20Design%20Report.pdf) to view the full version of the report.

Database entity relationship design

![database entity relationship design](:UN_3_SE/document/database/entity.png){:data-align="center"}

ER diagram

![ER diagram](:UN_3_SE/document/database/ER.png){:data-align="center"}

#### Detail Design

In this part, we worked on design the software of the project, and we did the following works:

- The application of Spring MVC
- The application of Spring Mybatis
- Website interface elements design
- Status realized method
- Data structure detail design
- System running detail design
- Algorithm design

Click [here](https://github.com/Jingxiang-Zhang/AnimalArchiveManagement_JAVA_SSM_SVN/blob/main/document/5.%20Detail%20Design%20Report.pdf) to view the full version of the report.

#### Encoding Specification

Finally, to unify our coding format, we write this encoding specification manual. Click [here](https://github.com/Jingxiang-Zhang/AnimalArchiveManagement_JAVA_SSM_SVN/blob/main/document/6.%20Encoding%20Specification.pdf) to view the the manual.

To see more about the project, please click [here](https://github.com/Jingxiang-Zhang/AnimalArchiveManagement_JAVA_SSM_SVN).
