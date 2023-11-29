---
layout: "post"
title: "SpringMVC"
date: "2020-08-17 22:02"
categories: framework,SpringMVC
tags: [Computer Language, framework, SpringMVC]
---

# SpringMVC初识
## 什么是MVC？

`MVC`是模型(Model)、视图(View)、控制器(Controller)的简写，是一种软件设计规范。将业务逻辑、数据、显示分离方法来组织代码。MVC主要作用是降低了视图与业务逻辑间的双向耦合。是一种**架构模式**

`Model`(模型): 数据模型。提供要展示的数据，因此包含数据和行为，可以认为是领域模型或JavaBean组件（包含数据和行为），不过现在一般都是分离开来： Value Object（数据DAO） 和服务层（行为Service），也就是模型提供了模型数据查询和模型数据的状态更新等功能，包括数据和业务。

`View`(视图)： 负责进行模型的展示，一般就是我们见到的用户界面，客户想看到的东西

`Controller`（控制器）： 接收用户请求、委托给模型进行处理（状态改变），处理完毕后把返回的模型数据返回给视图，由视图负责展示。控制器做了个调度员的工作

**最典型MVC: JSP + Servlet + JavaBean**

## SpringMVC

SpringMVC是Spring框架的一个模块

SpringMVC运行流程：




