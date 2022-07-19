---
lng_pair: UN3_FC
title: PY0语言设计
author: 张靖祥
category: 课程项目
tags: [C, C++]
img: ":UN_3_FC/demonstration.gif"
date: 2020-06-10 00:00:00
---


### Introduction项目介绍

<!-- outline-start -->根据python的语法，我用c++设计了PY0语言，作为《编译基础》课程的期末项目。<!-- outline-end -->我一共用了几个星期的时间来设计和编程该项目。PY0是一种解释型语言，因此，该编译器的效率相对较低。但是通过阅读这个程序的源代码，我希望读者能够更好地了解编译过程。

### 语法设计

PY0的语法模仿了Python的语法。所以，如果你懂Python，理解起来并不困难。

```
#1. the start of the input
<file_input> := (NEWLINE | <stmt>)* ENDMARKER

#2. statement and simple statement
<stmt> := <simple_stmt> | <compound_stmt>
<simple_stmt> := <small_stmt> NEWLINE
<small_stmt> := (<del_stmt> | <expr_stmt> | <pass_stmt> | <flow_stmt> | <import_stmt>)

<expr_stmt> := <or_test> | (NAME ((<augassign> <or_test>) | ('=' <or_test>)))
<augassign> := ('+=' | '-=' | '*=' | '/=')

<del_stmt> := 'del' NAME
<pass_stmt> := 'pass'
<flow_stmt> := <break_stmt> | <continue_stmt> | <return_stmt>
<break_stmt> := 'break'
<continue_stmt> := 'continue'
<return_stmt> := 'return' or_test
<import_stmt> := 'import' ( STRING | NAME )


#3. compound statement
<compound_stmt> := <if_stmt> | <while_stmt> | <for_stmt> | <funcdef>
<if_stmt> := 'if' <or_test> ':' <suite> ('elif' <or_test> ':' <suite>)*['else' ':' <suite>]
<while_stmt> := 'while' <or_test> ':' <suite>
<for_stmt> := 'for' NAME 'in' <or_test> ':' <suite>

<suite> := NEWLINE INDENT <file_input> DEDENT
<funcdef> := 'def' NAME <parameters> ':' <suite>
<parameters> := '(' [typedargslist] ')'
<typedargslist> := NAME (',' NAME )*


<or_test> := <and_test> ('or' <and_test>)*
<and_test> := <not_test> ('and' <not_test>)*
<not_test>:= ['not'] <comparison>
<comparison> := <expr> [<comp_op> <expr>]

<comp_op> := '<' | '>' | '==' | '>=' | '<='
<expr> := <term> (('+'|'-') <term>)*
<term> := <factor> (('*' | '/') <factor>)*
<factor> ::= <atom> <trailer>*
<atom> := <atom_base>  | <array> | '(' or_test ')'
<atom_base> := NAME | NUMBER | STRING
<array> := '(' <or_test> (',' <or_test>)* ')'

<trailer> := '(' [<arglist>] ')' | '[' <subscript> ']'
<subscript> := <or_test>
<arglist> := <or_test> (',' <or_test>)*
```

### 程序架构

各模块的项目架构如下。为了避免循环引用，我拆分了一些模块。下面显示的所有模块都是头文件，不是类继承。下面我将详细说明各个模块的功能以及各个功能的设计。

![程序架构](:UN_3_FC/architecture.png){:data-align="center"}

这个项目总共有9个部分，接下来我将逐一介绍。

#### 符号表

最基本的模块之一。它不调用任何其他模块，几乎所有模块都调用此模块的内容，将抽象数字转换为枚举。这是我设计的第一个模块，从那以后它就没有改变过。

![符号表](:UN_3_FC/symbol.png){:data-align="center"}

#### 错误处理

它不调用任何其他模块，它用于提供错误处理。它需要由其他模块调用。由于时间有限，我只对关键错误做了非常简短的描述，错误报告的内容也比较简单。

!错误信息](:UN_3_FC/error_msg.gif){:data-align="center"}

#### 词法分析

此模块用于分词。相比设计之初，它添加了很多额外的功能，以满足更多的需求，以下是功能介绍：

- 根据文件名对输入文件进行分割
- 读取下一个词
- 读取上一个词
- 跳过代码段
- 获取代码长度
- 获取当前代码位置
- 跳转光标到指定位置

#### 程序运行时基础与语法分析基础

之所以将这两部分与它的主体部分分开，是为了避免循环引用。以下是这两部分的部分代码：

![基础结构](:UN_3_FC/structure_base.png){:data-align="center"}

#### 程序运行时管理

本部分主要完成了以下工作：

- 向变量表中添加变量
- 获取变量表中的变量对象
- 增加或减少代码段的级别
- 调用新函数时，保留原函数变量
- 退出函数时，将变量放入当前变量表中
- 删除变量
- 记录import列表
- 显示整个变量表

#### 内置函数初始化

该模块为函数初始化，并在main函数中调用。为了满足程序的层次化结构，我将功能分为两类：1. 内置函数，例如print和input函数。2. 用户自定义函数。此函数用于初始化所有内置函数，所有内置函数都使用函数指针，并将指向该函数的指针存储在符号表中以供调用。函数指针类型定义如下:

```
typedef phrase::return_value(*funpointer)(phrase::infunction_type * infunction); 
```

内置函数有以下几个：

![内置函数](:UN_3_FC/built_in_function.png){:data-align="center"}

#### 语义语法分析

分析所有代码，包括：

- **float, int, string** 类型的变量
- **break, continue** 在循环中的语法
- **del** 删除语法
- 向量操作
- **import** 语法
- **if, elif, else** 分支语句
- **while, for** 循环结构
- **def** 用户自定义函数与函数调用
- 内置函数调用


#### 主函数

显示界面及基本功能。PY0项目有两种方法可以使用，一种是使用命令行，拖动打开，在一个PY0文件中传递路径作为命令行参数；第二个选项是进入命令操作界面，而不传入命令行参数。

### 项目展示

![项目展示](:UN_3_FC/demonstration.gif){:data-align="center"}

点击[此处](https://github.com/Jingxiang-Zhang/PY0_program_language_design)获取项目源代码。