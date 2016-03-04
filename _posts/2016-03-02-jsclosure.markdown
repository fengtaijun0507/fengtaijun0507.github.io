---
layout: post

title:  "JS 面试题（一）"

date:   2016-03-04

---

1.声明提升

> console.log(x);//function x() {}
> 
> function x() {}
> 
> var x = 1; 

 声明提升：所有声明变量或声明函数都会被提升到当前函数的顶部。其实上面的代码实际情况如下;
> var x;
> 
> function x(){}
> 
> console.log(x);
> 
> x=1;

2.函数表达式与函数声明

 函数声明与函数表达式不同的是：函数声明会整体提升到所在定义域的顶部，而函数表达式只有变量名提升到顶部

>  console.log(x);//undefinded
> 
>  var x=function(){}
>  
>  var x = 1;

因为：

>  var x;
>  
>  console.log(x);
>  
>  x=function(){}
>  
>  x = 1;

3.[小小沧海——面试题](http://mp.weixin.qq.com/s?plg_nld=1&plg_auth=1&plg_nld=1&plg_dev=1&plg_uin=1&plg_usr=1&plg_vkey=1&plg_nld=1&scene=0&plg_uin=1&mid=402287118&plg_auth=1&plg_dev=1&sn=061815e160e8394af0ac15c31aa0f809&plg_nld=1&idx=1&__biz=MzAxODE2MjM1MA%3D%3D&plg_usr=1&plg_vkey=1#wechat_redirect)

	function Foo() {
	    getName = function () { alert (1); };
	    return this;
	}
	Foo.getName = function () { alert (2);};
	Foo.prototype.getName = function () { alert (3);};
	var getName = function () { alert (4);};
	function getName() { alert (5);}
	 
	//请写出以下输出结果：
	Foo.getName();
	getName();
	Foo().getName();
	getName();
	new Foo.getName();
	new Foo().getName();
	new new Foo().getName();

4.[闭包](http://web.jobbole.com/84328/)

	function fun(n,o) {
	  console.log(o)
	  return {
	    fun:function(m){
	      return fun(m,n);
	    }
	  };
	}
	var a = fun(0);  a.fun(1);  a.fun(2);  a.fun(3);//undefined,?,?,?
	var b = fun(0).fun(1).fun(2).fun(3);//undefined,?,?,?
	var c = fun(0).fun(1);  c.fun(2);  c.fun(3);//undefined,?,?,?

重点是三个fun()函数之间的关系，这个很重要，要多看几遍



5.题目
		
	if (!("a" in window)) {
	var a = 1;
	 }
	console.log(a);//undefined  
  声明提升

6.函数声明提前，并且在变量声明之后： 
   
    function a(x) {
        return x * 2;
    }
    var a;
    alert(a);

alert的结果：

    function a(x) {
        return x * 2;
    }
7.arguments

	function b(x, y, a) {
	    arguments[2] = 10;
	    alert(a);
	}
	b(1, 2, 3);//10

8.找出数字数组中最大的元素（使用Math.max函数）

    var arrayName=[0,12,3]
	Math.max.apply(null,arrayName)

9.js map：

	var arr = Array(3);
	arr[0] = 2;
	arr.map(function(elem){return '1';});

10.关于闭包的一些问题：
1）定义：

  JS里的function能访问它们的：

  1. 参数

  2. 局部变量或函数

  3. 外部变量（环境变量？），包括

    3.1 全局变量，包括DOM

    3.2 外部函数的变量或函数。

  
 如果一个函数访问了它的外部变量，那么它就是一个闭包。


 注意：函数也是一种"量"，所以引用他也算一种闭包

2）特点：

   嵌套函数

   内部函数可以引用外部函数的**参数或者变量**

   垃圾回收机制

   **参数****和内部变量**不会被清除，

3）闭包的用途:
 
 * 在模块化编程中，通过提供接口访问私有成员这种方式，防止了全局变量被污染，保护函数内的变量安全

 *　在内存中维持变量：可以缓存数据

4）怎么释放闭包的变量内存
 
  手动设置变量为null

5)缺点：造成内存泄漏

11.一些代码块：

    window.onload = function(){
            var aLi = document.getElementsByTagName('li');
            for (var i=0;i<aLi.length;i++){
                    (function(i){
                            aLi[i].onclick = function(){
                                    alert(i);
                            };
                    })(i);
            }
            };
 





