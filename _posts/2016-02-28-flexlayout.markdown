---
layout: post

title:  "CSS flex布局学习（一）"

date:   2016-03-04

---


设为Flex布局以后，子元素的float、clear和vertical-align属性将失效

1.flex布局的概念：

2.flex 容器：{flex项目：{ main size,cross size,沿着主轴依次分布}，主轴(水平轴)，交叉轴(纵轴)，原点在矩形左上角，矩形为其第一象限}，(各种属性的初始化值)

  flex的属性：{flex-direction，flex-wrap，flex-flow，justify-content，align-items，align-content}

  flex—direction:row|row-reverse|cloumn|colomn-reverse.定义主轴方向
  flex-wrap:nowrap|wrap|wrap-reverse.定义排列是否换行，wrap从左到右，向下排列，wrap-reverse，从左到右，向上排列
  flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。

  justify-content:flex-start,flex-end,center,space-between,space-around;调整对齐方式,具体对齐方式与主轴的方向有关。

  align-items:flex-start|flex-end|center|baseline | stretch;交叉轴的对齐方式

  align-content: flex-start | flex-end | center | space-between | space-around | stretch;多根轴线的对齐方式

3.flex项目的属性：

  order:<interger>  从小到大排列  默认为0？

  flex-grow:<number>  定义项目的放大比列

  flex-shrink        定义项目的放小比列　

  flex-basis:length   定义项目占据主轴的的宽度，通过他计算主轴还剩多少空间

  flex:flex-grow flex-shrink flex-basis

  align-self:auto
  

  注意：当width与flex-basis共存时，flex-basis>width

   flex-basis指定item的宽度，若项目的总宽度>容器的宽度，则按比例缩放，若是<容器的宽度，则需要指定
   flex-grow，才能按比例放大。

<iframe width="100%" height="300" src="http://jsfiddle.net/fengtaijun/3uhqsoeh/embedded/result,css,html/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

