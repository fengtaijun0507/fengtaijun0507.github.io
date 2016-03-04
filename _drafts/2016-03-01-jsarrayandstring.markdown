---
layout: post

title:  "js 数组与字符串学习笔记（一）"

date:   2016-02-28

---

## Js数组与字符串操作：

### 一.js数组
1.	string String(包装类)

2.	数组的length属性可读写，字符串不可以

3.	数组方法：
	
		1)添加与删除：push(),pop();shift(),unshift()
	
		2)splice(开始，长度，元素)，插入，删除，替换
		       
             先删除<长度>的元素 再添加规定元素

		     splice(开始,0,添加元素)：插入
             splice(开始,length,添加元素)：替换
	         splice(开始,length)：删除
             
             返回删除的元素的数组

		3)join(“_”),将数组变为字符串，返回字符串 
	
		        split()字符串方法，返回字符串数组
	
		4)数组slice(“开始“，”结束“)取子数组，不包括结束位置
		         与字符串相同
             substring(“开始“，”结束“),不包括结束位置
		5)sort(function(num1,num2){
		          Return-1;
		          Return-2;
		          Return 0;
		})
		fn为比较函数
		按照字符串，字典序排列，大写在前，小写在后,默认情况下，把比较函数都是转为字符串比较
		所以需要传入比较函数

		注意：typeof(数组)返回的是对象，typeof(字符串)有string，有object

                 6)reverse(),

                 7)concat()

                 8)toString()

                    Array.toString()
                    numvarible.toString(16)转换成相应进制

		数组去重：先排序，然后查看两个临近的两个数字的大小
		
		数组复制: concat([]),连接空数组


                    
### 二.字符串


   1，属性，length

   Js中英文不区分

   2.方法：

	1) 取某个字符： charAt(),charCodeAt()(10进制)，String.fromCharCodeAt()
		              String[]不兼容ie6

		          indexOf(); lastIndexOf(), 字符串第一次出现的位置，没有返回-1

		          search(//)[]/(),?，+是数量他是以正则表达式的方式来搜索
		          区别在正则表达式
		          字符串.macth(),正则
		          字符串.replace(源字符，新字符)
	2) 取子字符串 ：是slice(开始，结束位置)，slice(开始) （默认为结束）
		            substring()与上面此两个功能相同
		            slice(-1)与substring(-1)的区别：返回整个字符,slice(-1)返回倒数第1个,slice(-2)返回倒数2个,依次类推

		            substr()与substring()的区别：第一个包含结束位置
	3) 比较：

	字符串1.localeCompare(字符串2)，根据当地人的习惯比较
	字符串2>字符串1  返回1

	4) 分割split(""),返回数组

	5) toUpperCase() toLowerCase()

### 三.字符串

   1.字符串与数组之间转化:split('')字符串转为数组，join('')：数组转为字符串

    	var str1 = 'abcd';
    	var str2 = 'jjhhgg';
    	var str3 = str1.concat(str2); 
    	var str4 = str3.split('').reverse().join('');
    	console.log(str4);
      
       ：gghhjjdcba

   2.reverse():为数组独有，而且有排序的功能；

   3.slice()为共有，并且。slice()

   4.有用的代码片段：著作权归作者所有。

		var arr = [1,2,3,4]
		var res = [];
		for (var i = 0, len = arr.length; i < len; i++) {
		  var j = Math.floor(Math.random() * arr.length);
		  res[i] = arr[j];
		  arr.splice(j, 1);//这一步骤很关键
		}
		console.log(res);