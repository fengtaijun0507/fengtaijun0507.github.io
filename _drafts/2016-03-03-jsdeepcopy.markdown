---
layout: post

title:  "Angular.js学习笔记（一）"

date:   2016-02-28

---

### 一.angular:书写习惯：

1）ngAnimate：这样写基本是**模块**，模块可以在依赖注入的地方写，也可以一在ng-app=“ngAnimate”处引入

2）ng-repeat：这个一般是写在html中的，称为**指令**，一般内置的指令充当元素的属性，以这种形式来使用：ng-model，ng-controller，ng-if

A．此处注意：官方文档出左侧的指令直接写：ngModel，而在使用的时候却是加“-”，这个非常不理解。

B．自定义指令的使用方式：有直接是元素，有的是充当元素的自定义属性各有不同的功能，充当元素的对应相应的模板内容，而元素的额自定义属性一般对应相应的功能

也就是ACE的匹配模式相对应的方式，这个再写blog的时候再吧四种模式的列子都写


C．以$开头的的内置的，是type，provider，service中的一种：$http, $filter,
service这类一般以参数的形式，通过注入的方式下载控制器下面
自定义sevice: mymodule.factory创建，再通过控制器去注入

D．发现angular自定义：总是通过mymodule.filter，mymodule.directive等等方式来进行


### 二.angular概述

 * 优势1.MVC，2.模块系统，3.指令系统，4.依赖注入，5.双向数据绑定
  


 * 应用方向：

     1）双向数据绑定：CRUD是指在做计算处理时的增加(Create)、读取(Retrieve)（重新得到数据）、更新(Update)和删除(Delete)几个单词的首字母简写。

     2）路由系统：单页Web应用（single page web application，SPA），就是只有一张Web页面的应用。单页应用程序 (SPA) 是加载单个HTML 页面并在用户与应用程序交互时动态更新该页面的Web应用程序。

 
### 三.开发基于angularjs框架的文件结构：（bookstore）

     一个模型model，多个controller，多个view，加上公共的service

controller的使用注意点：

1）	contoller负责的是业务逻辑，业务逻辑一般是针对性比较强，可复用性弱。尽量不要复用controller

2）	操作Dom交给指令去操作，因为Dom的操作效率是比较低的




### 四.模块

1.	模块，是一个集合包扩自己的modal,view,controller，ditecvtive,service，filter等的一个集合

    模块化，相对于全局（对全局造成变量污染）：
   
    angular.module('moduleName',['依赖模块数组'])

    angular常见的module:'ngRoute', 'ngAnimate','ui.router'

2.


### 五.控制器


### 五.指令



### 六.服务


### 七.工具函数


### 八.其他

1.scope


2.双向数据绑定


3.一些注意事项






