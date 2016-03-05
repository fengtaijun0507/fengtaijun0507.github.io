---
layout: post

title:  "Angular.js学习笔记（一）"

date:   2016-03-06

---

### 一.angular:书写习惯：

1）ngAnimate：这样写基本是**模块**，模块可以在依赖注入的地方写，也可以一在ng-app=“ngAnimate”处引入

2）ng-repeat：这个一般是写在html中的，称为**指令**，一般内置的指令充当元素的属性，以这种形式来使用：ng-model，ng-controller，ng-if

> A．此处注意：官方文档出左侧的指令直接写：ngModel，而在使用的时候却是加“-”，这个非常不理解。
> 
> B．自定义指令的使用方式：有直接是元素，有的是充当元素的自定义属性，并有各有不同的功能，
> 
>    充当元素的相应的模板内容，而元素的额自定义属性一般对应相应的功能,也就是ACE的匹配模式相对应的方式
> 
> 
> C．以$开头的的内置的，是type，provider，service中的一种：$http, $filter,service这类一般以参数的形式，通过注入的方式下载控制器下面
> 自定义sevice: mymodule.factory创建，再通过控制器去注入
> 
> D．发现angular自定义：总是通过mymodule.filter，mymodule.directive等mymodule.的方式来进行
> 
> 注意：这也就说都是挂载在module上，若不是在同一个module下的话，需要通过引入相应自定义模块，才能使用
> 

### 二.angular概述

 * 优势1.MVC，2.模块系统，3.指令系统，4.依赖注入，5.双向数据绑定
  


 * 应用方向：

     1）双向数据绑定：CRUD是指在做计算处理时的增加(Create)、读取(Retrieve)（重新得到数据）、更新(Update)和删除(Delete)几个单词的首字母简写。

     2）路由系统：单页Web应用（single page web application，SPA），就是只有一张Web页面的应用。单页应用程序 (SPA) 是加载单个HTML 页面并在用户与应用程序交互时动态更新该页面的Web应用程序。

 
### 三.开发基于angularjs框架的文件结构：（bookstore）

     一个主模型model，多个controller，多个view，加上公共的service
    
  ![文件结构](http://fengtaijun0507.github.io/testpages/angular/img/bookstore.png)

### 四.模块

1.	模块，是一个集合包扩自己的modal,view,controller，ditecvtive,service，filter等的一个集合

    模块化，相对于全局（对全局造成变量污染）：
   
    angular.module('moduleName',['依赖模块数组'])

    angular常见的module:'ngRoute', 'ngAnimate','ui.router'

2. 始终有一个主模块，这个主模块，通过ng-app加载，ng-app="mainModuleName"

3. 一个简单的列子
<iframe width="100%" height="300" src="http://jsfiddle.net/fengtaijun/nu85befx/embedded/result,html,js/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

### 五.控制器
controller通过

    var moduleName=angular.module('test1', [dependencies])
    moduleName.controller("name",["$scope",],funtion($scope){})

     
> "一个主模型model，多个controller，多个view，加上公共的service",跟这个框架还是很契合
> 
> controller的使用注意点：
> 
> 1）	contoller负责的是业务逻辑，业务逻辑一般是针对性比较强，可复用性弱。尽量不要复用controller
> 
> 2）	操作Dom交给指令去操作，因为Dom的操作效率是比较低的




### 五.指令

#### 1.自定义指令

<iframe width="100%" height="300" src="http://jsfiddle.net/fengtaijun/ad4esj5z/4/embedded/result,js,html" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

    var mymodule = angular.module("MyModule", []);
    mymodule.directive('hello', function() {
    return {
    restrict: 'AECM',
    template: '<div>Hi everyone!</div>',
    replace: true
    }
    })

#### 参数解释：首先需要注意的是他是需要返回一个对象

1）restrict

[A：attribute，E：Element,C:class,M:comment](https://jsfiddle.net/fengtaijun/ad4esj5z/6/)

A:增加功能的时候，自定义属性,该属性可能是包括模板内容，也可能包括各种行为

E:使用自定义模板。

M:使用必须配合replace: true,才能有效果

C:

2)template:模板，使用字符串
  
  可以使用templateUrl替代它(可以使用函数或者字符串写明模板文件的位置)
  templateUrl:funtion(attr,element){
      return ".html"
   }
 或者
  templateUrl:".html"
  
  其中函数参数element:为宿主标签(A)或者指令本身(E)

  详细见[例子](待会上传到gh-pages)

3)replace:true

 表示模板内容是否会替换原文的标签，如果设置为false，则模板内容为原内容的子元素

	亲测：对restrict：AECM都有效果，并且原本元素的属性内容会保留,

	只是M：必须配合此配置参数,才能有效果
	
	E按道理也必须与replace配合因为浏览器无法识别自定义标签

 
4)transclude：自定义指令内部标签的签套
            transclude: true,
            template: "<div>Hello everyone!<div ng-transclude></div></div>",

保护原html文件中，自定义标签的中嵌套的内部元素不被改变，见[例子](https://jsfiddle.net/fengtaijun/pqzfhj09/14/)

注意：transclude与ng-transclude需要配合使用，另外transclude内部的元素获取的scope，并非独立scope而是外层scope,见[例子](http://plnkr.co/edit/?p=preview)

5)指令的独立scope：scope:{}



6）指令与控制器之间的通信

 [例子](https://jsfiddle.net/fengtaijun/532b5zaa/)

	 注意：1）属性后面能加函数，能加表达式，那么函数是从scope上寻找的
	       2）link:function(scope, element, attr){
            }
           scope：父级或者宿主元素的scope/当指定了独立scope时候，为自己的scope 	
           element:


7)指令与指令之间的通信

 [例子](https://jsfiddle.net/fengtaijun/532b5zaa/)

   通信：通过require:"^directiveName",增加这个属性后link函数中的第四个参数才可以使用


   逻辑是靠下面两个函数是实现
   contoller:['$scope',function($scope){}]
   link:function(scope, element, attr,parentCtrl){
      }
    
8）**这个问题：在指令中定义controller,单独定义contoller有什么不同？**


### 六.服务

当多个controller相似时候，不要试图对多controlle重用，做的是将controller抽象为公共服务service

service的特性

1）service是都是单例的

2）secive由$injector实例化

3）service在整个应用的生命周期内存在，可以用来共享数据

4）在需要使用的的地方利用“依赖注入”的机制注入service

5）自定义service需要写在内置的Service后面

6）内置service以$开头，自定义应该避免

[示例](http://fengtaijun0507.github.io/testpages/angular/1service.html)

### 八.参考

#### 1.[官方文档](https://docs.angularjs.org/guide)

#### 2.[慕课网——angular课程](http://www.imooc.com/learn/156)

#### 3.[妙味angular课程]()










