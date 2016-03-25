---
layout: post

title:  "JS 浏览器缓存学习笔记（一）"

date:   2016-03-23

---

1.在产品开发的时候我们总是想办法避免缓存产生，而在产品发布之时又在想策略管理缓存提升网页的访问速度.
web缓存分为很多种，比如数据库缓存、代理服务器缓存、还有我们熟悉的CDN缓存，以及浏览器缓存。本次主要研究浏览器缓存，分为HTTP协议定义的缓存机制和非HTTP协议定义的缓存机制



2.HTTP协议定义的缓存机制

> Expires； Cache-control等

摘自[流云诸葛-浏览器缓存知识小结及应用](http://mp.weixin.qq.com/s?__biz=MjM5MTA1MjAxMQ==&mid=402202185&idx=3&sn=abbc03511d2c393d7a4867ff532224ab&scene=23&srcid=0323BHq5mBzOUSSxNC2zeJUO#rd)

概述：浏览器缓存基本认识

它分为强缓存（200  from cache）和协商缓存（status code：304 Not Modified）： 

Ⅰ. 强缓存：

1）浏览器在加载资源时，先根据这个资源的一些http header判断它是否命中强缓存，强缓存如果命中，浏览器直接从自己的缓存中读取资源，不会发请求到服务器。比如某个css文件，如果浏览器在加载它所在的网页时，这个css文件的缓存配置命中了强缓存，浏览器就直接从缓存中加载这个css，连请求都不会发送到网页所在服务器；

2）当强缓存没有命中的时候，浏览器一定会发送一个请求到服务器，通过服务器端依据资源的另外一些http header验证这个资源是否命中协商缓存，如果协商缓存命中，服务器会将这个请求返回，但是不会返回这个资源的数据，而是告诉客户端可以直接从缓存中加载这个资源，于是浏览器就又会从自己的缓存中去加载这个资源；

3）强缓存与协商缓存的共同点是：如果命中，都是从客户端缓存中加载资源，而不是从服务器加载资源数据；区别是：强缓存不发请求到服务器，协商缓存会发请求到服务器。

4）当协商缓存也没有命中的时候，浏览器直接从服务器加载资源数据。

http header
A:Expires（http1.0）

在第一次请求时，在response header加上Expires表示过期时间，是一个绝对时间，浏览器将相应资源和header一并的缓存，再次请求的时候，浏览器取出Expires与当前请求事件相比较，如果在Expires之前，命中缓存，如果没有命中则向服务器请求，并更新Expires

Expires的缺点是他是一个绝对时间确定是否过期，如果时间比较长，或者更改了客户端的系统时间都会造成失误



B:Cache-Control（http1.1）

与Expires不同m,Cache-Control:public, max-age=7200;7200s是一个相对时间，相对第一次请求的时间，那么第一次请求的时间是Date的时间


注意:这两个header可以只启用一个，也可以同时启用，当response header中，Expires和Cache-Control同时存在时，Cache-Control优先级高于Expires：


C：强缓存的设置


D：强缓存存在的问题
   开发时候时候不能及时更新，可通过gulp watch的方式或者其他工具及时更新，
   上线版本的文件替换后不及时更新，通过在资源添加随机数
   这两方式比较有效

Ⅱ. 协商缓存

协商缓存是利用的是**Last-Modified，If-Modified-Since**和**ETag、If-None-Match**这两对Header来管理的。



A. Last-Modified，If-Modified-Since

* 　浏览器第一次请求的时候在reponse header中添加Last-Modified来表示文件修改时间
 　
* 　浏览器第二次进行缓存的的时候在request header中添加If-Modified-Since，他的值就是前一次的Last-Modified，服务器根据If-Modified-Since和文件修改时间作比较来判断文件是否修改，如果没有修改，返回304 Not modified，浏览器从本地缓存加载资源，如果存在修改，服务器正常返回资源

* 　如果协商缓存没有命中，浏览器直接从服务器加载资源时，Last-Modified Header在重新加载的时候会被更新，下次请求时，If-Modified-Since会启用上次返回的Last-Modified值。

Ｂ．但是有时候也会服务器上资源其实有变化，但是最后修改时间却没有变化的情况。为解决这种情况，通过判断修改时间的变化改为判断Tag（一段字符串）是否发生变化，也就是ETag与If-None-Match的组合方式，过程与Last-Modified，If-Modified-Since相似。


C.协商缓存的方式的设置

大部分web服务器都默认开启协商缓存，而且是同时启用****Last-Modified，If-Modified-Since和 ETag、If-None-Match**，比如：appache，nginx

注意：

* 分布式系统里多台机器间文件的Last-Modified必须保持一致，以免负载均衡到不同机器导致比对失败；

* 分布式系统尽量关闭掉ETag(每台机器生成的ETag都会不一样）；

注意：
1）协商缓存需要配合强缓存使用，你看前面这个截图中，除了Last-Modified这个header，还有强缓存的相关header，因为如果不启用强缓存的话，协商缓存根本没有意义。因为协商缓存只是在强缓存中增加一次判断，如果命中他取出的内容也是通过强缓存方式缓存的文件
2）
* 当ctrl+f5强制刷新网页时，直接从服务器加载，跳过强缓存和协商缓存；

* 当f5刷新网页时，跳过强缓存，但是会检查协商缓存




总结：也就是说一般情况下，协商缓存的话交给web服务器设置，并且作为前端需要了解服务器如何设置这两种缓存的设置
第二种强缓存的话可以通过后端来设置，但是现在主要的情况是前后端分离，对于对于后端主要是提供数据，这就要涉及ajax缓存的知识了，ajax请求也是http请求，但是他的缓存和浏览器缓存是不相同的，通过jQuery来配置缓存。接下来先把web服务器设置****Last-Modified，If-Modified-Since和 ETag、If-None-Match**弄清楚，至于分布式的情况，现在是无法了解太多了，appache需要开启相应的模块才能开启cache-control和expires，这个回来再来设置吧，卧槽，设置太麻烦

**关于这个配置文件网上还是参差不齐，还是有机会向后端的人请教一下吧，然后主要nginx，appache的配置强缓存**
appache主要是添加相应的模块，譬如expires，将配置文件中的注释去掉

LoadModule expires_module modules/mod_expires.so

再添加下面的一句话，就可以配置好了，[参考1](http://yulp2010.blog.51cto.com/983828/479796),[参考2](http://www.lampweb.org/seo/4/14.html)

<IfModule expires_module>
    ExpiresActive On
    ExpiresByType text/html "access plus 15 days 2 hours"
    ExpiresDefault "access plus 1 month"
</IfModule>

模块mod_headers,似乎可以设置cache-control


3.非HTTP协议定义的缓存机制

> HTML Meta 标签
    
    这下面的三个标签看了京东的首页都没有发现，所以我觉得可以暂时不研究了

	<meta http-equiv="expires" content="0">
    <meta http-equiv="cache-control" content="no-cache">
    <meta http-equiv="pragma" content="no-cache">



