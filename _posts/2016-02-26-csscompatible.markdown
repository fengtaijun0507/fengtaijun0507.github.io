---
layout: post

title:  "CSS 浏览器兼容性总结（一）"

date:   2016-02-26

---
## 1.常见的兼容性问题

### 1).H5标签的兼容性问题

### 2).IE6下最小高度问题
  
	在IE6下元素的高度的小于19px的时候，会被当做19px来处理，
	   
	解决办法:overflow:hidden;

### 3).IE6下父元素的宽度会被子元素撑开，高度应该做好精确的计算
	   
### 4)在IE6，7下，li本身没浮动，但是li的内容有浮动，li下边就会产生一个间隙

	解决办法:
		1.给li加浮动和height
		2.给li加vertical-align

### 5).当IE6下最小高度问题，和 li的间隙问题共存的时候 给li加浮动和overflow：hidden，
    
	li{ list-style:none;height:12px;border:1px solid #000;overflow:hidden; float:left;width:300px;}
    注意：父级此时需要定宽，否则float改变原先布局
    ul{width:302px;}

### 6).margin兼容性

     1.margin双边距，块级元素浮动造成横向双边距   
	   display：inline
     2.margin传递
 <iframe width="100%" height="300" src="http://jsfiddle.net/fengtaijun/5edw7ugj/embedded/result,html,css/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

	子元素的margin会穿透父元素，造成margin传递

    解决方法： .box{background:blue; border：1px solid #ccc}
              或者.box{background:blue; overflow: hidden;}
              兼容IE：{zoom:1} 触发hasLayout
<iframe width="100%" height="300" src="http://jsfiddle.net/fengtaijun/5edw7ugj/4/embedded/result,html,css/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>
             

     3.上下margin叠加，
       解决方法尽量都设置同一方向的margin，

### 7).在IE6，7子元素有相对定位的，父元素overflow无效，给父级添加position：relative

### 8).position=fixed在IE6下是不兼容的,可以通过js是可以解决，获取scrollTop利用position:absolute来解决

### 9).IE6 png透明效果失效

	<!--[if IE 6]>
	<script src="DD_belatedPNG_0.0.8a.js"></script>
	<script>
	DD_belatedPNG.fix('.box');
	</script>
	<![endif]-->

### 10).[display:inline-block](http://ued.taobao.org/blog/2012/08/inline-block/)

    1.inline-block:兼容IE的写法
	 display:inline-block
	*display:inline
	*zoom:inline

    2.inline-block元素之间会有间隙

      父级设置：{font-size：0;
                letter-spacing:-3px//根据设置全局font-size，这样这个值就会是定值
                *letter-spacing:normal
                word-spacing:-1px//IE6,7 1px误差}
      子元素设置恢复：{font-size:12px;
                     letter-spacing:normal;
                     word-spacing:normal;
                     vertical-align:top;}
### 11)输入类型表单控件：

	在IE6，7，输入的表单控件在上下有1px的间距，元素加上float（这个方法加上float可能会改变布局，视具体情况定，如果不需要兼容IE6，7自然不用加float:left）
    input{width:100px;height:30px;border:1px solid #000;margin:0;padding:0; float:left;}

	在IE6，border：none没有效果，给input重置一下背景
    input{width:100px;height:30px;border:none;margin:0;padding:0; float:left; background:#fff;}
     
	在IE6，输入文字会挤走背景图片：背景设置给父级，自己的背景清掉 background：none
    
                    
### 12）p元素嵌套块元素
  
* 块元素嵌套规则： p,hn,td:bu能再包含块级标签
* p元素嵌套块元素
   
          <p><div>代码</div></p>

          chorome中的最终代码是：

          <p></p><div>结果</div><p></p>

          所以这个不应该这么做


## 2.浏览器兼容性产生的原因

   多种浏览器对于w3c的规范的理解不尽相同，造成解析不同
   
## 3.几种常见hack方式

### 1）IE条件语句

	<!—[if IE]>
	这是IE
	<![endif]-->
	<!—[if IE 9]>
	 这是IE9
	<![endif]-->
		
	<!—[if IE 6]>//不能有空格
	 这是IE6
	<![endif]-->

###  2）css hack的使用

	Bg:blue\9(IE9之前的IE10之前的浏览器解析)
	*Bg:yellow(*,+IE7之前
	_Bg：blue（ie6之前）

###  3）媒体查询
	   Chorome：@media screen and（-webkit-min-device-pixel-ratio:0）{
	   Body{background-color:blue}


## 4.解决方案

   0)首先要积累经验

   1）先必须确认兼容的浏览器的版本

  * 对于不支持的效果采取优雅降级，border-radius

  * 或者对于不同的浏览器的效果差异做兼容性处理

  * 有人建议将浏览器分为现代浏览器和非现代浏览器，开发相应的版本，从而保证体验


   2）开发规范，每做完一个功能，效果，及时在不同的浏览器下进行测试   
   
   3）移动端的开发，由于都是基于webit内核的浏览器，所以这些css的相关兼容性问题大都不需要考虑，但是....

   

## 5.参考文献

### [1].[W3CHelp_兼容性](http://www.w3help.org/zh-cn/causes/)

### [2].[miaov web基础课程]()