---
layout: article
title: Sql注入&Nosql注入&XSS漏洞小结
category: 网络安全
tag: web
---
**总结之前做过的相关漏洞学习笔记**

## 纲要知识
--base64编码原理  
--Unicode编码以及UTF-8的编码原理  
--SQL注入  
&nbsp;&nbsp;&nbsp;&nbsp;-了解不同SQL数据库中的SQL语法  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;常用SQL注入语法表单：https://portswigger.net/web-security/sql-injection/cheat-sheet  
&nbsp;&nbsp;&nbsp;&nbsp;-利用SQL注入改变应用交互逻辑  
&nbsp;&nbsp;&nbsp;&nbsp;-union攻击  
&nbsp;&nbsp;&nbsp;&nbsp;-SQL盲注（基于布尔条件响应、基于布尔条件报错、基于详细报错信息、基于时间延迟、带外技术等）  
--了解json数据格式和Javascript基础语法  
--正则表达式的格式及使用  
&nbsp;&nbsp;&nbsp;&nbsp;语法详解：https://www.runoob.com/regexp/regexp-syntax.html  
--NoSQL注入：语法注入、操作符注入  
&nbsp;&nbsp;&nbsp;&nbsp;-熟悉noSQL操作符（MongoDB常用操作符：$where,$ne,$regex,$in）  
--浏览器同源策略和CORS策略  
--XSS攻击：反射型XSS，存储型XSS，DOM型XSS  
&nbsp;&nbsp;&nbsp;&nbsp;-熟悉html格式和常用html语法  
&nbsp;&nbsp;&nbsp;&nbsp;-使用开发者工具进行页面测试  
&nbsp;&nbsp;&nbsp;&nbsp;-测试XSS  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;对于DOM型XSS，掌握漏洞sink：document.write，innerHTML，hashchange等  

## 杂记知识点
--JSON和XML都是数据交换格式语言  
--Object.keys(obj)返回值是对象中每一项key的数组，Object.values(obj)返回值是一个包含对象自身的所有可枚举属性值的数组  
--触发alert()常用payload：https://www.cnblogs.com/xyz315/p/14850359.html  
--XSS漏洞事件函数：https://blog.csdn.net/qq_63844103/article/details/128009363  
--测试XSS漏洞详细指南（测试方法）：https://blog.csdn.net/Gherbirthday0916/article/details/138494063  
--漏洞挖掘实战历程：https://cloud.tencent.com/developer/article/2008742  
--XSS漏洞基础知识：  
&nbsp;&nbsp;&nbsp;&nbsp;在XSS漏洞中，sink 是指数据流的终点，即数据最终被处理或执行的地方。在 XSS 攻击中，sink 通常是浏览器中执行 JavaScript 代码的地方。攻击者通过将恶意代码注入到应用程序中，并确保这些代码在浏览器中执行，从而实现攻击目的。具体来说，sink 可以是以下几种情况：  
&nbsp;&nbsp;&nbsp;&nbsp;1.DOM 操作：如 innerHTML、document.write 等方法，这些方法会将数据直接插入到页面的 DOM 中并执行。  
&nbsp;&nbsp;&nbsp;&nbsp;2.事件处理器：如 onclick、onmouseover 等事件属性，这些属性会在特定事件发生时执行代码。  
&nbsp;&nbsp;&nbsp;&nbsp;3.JavaScript 执行环境：如 eval、setTimeout、setInterval 等函数，这些函数会动态执行传入的字符串作为代码。  
&nbsp;&nbsp;&nbsp;&nbsp;-在XSS漏洞中，source 是指数据流的起点，即用户输入或外部数据进入应用程序的地方。常见的 source 包括：  
&nbsp;&nbsp;&nbsp;&nbsp;1.用户输入：如表单输入、URL 参数、HTTP 请求头等。  
&nbsp;&nbsp;&nbsp;&nbsp;2.外部数据：如从数据库、文件系统或第三方 API 获取的数据。  
&nbsp;&nbsp;&nbsp;&nbsp;-在XSS漏洞中，anchor（锚点）通常用来指在DOM中可能成为恶意脚本注入的具体位置。虽然这个术语在XSS文献中并不如source和sink那么常见，但可以理解为一个特定的sink类型或是一个容易成为攻击目标的DOM节点位置。  
--识别网页使用的js框架：  
&nbsp;&nbsp;&nbsp;&nbsp;控制台命令  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;jQuery: !!window.jQuery  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AngularJS: !!window.angular  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;React: !!window.React  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Vue.js: !!window.Vue  
--在AngularJS中，$on是一个事件处理函数，而constructor是一个特殊的方法，用于创建和初始化类对象实例。当你看到$on.constructor时，它实际上是在调用构造函数，并传递参数来执行其字符串形式的代码。例如，$on.constructor('alert(1)')()会弹出一个警告框，显示数字1。  
&nbsp;&nbsp;&nbsp;&nbsp;链接：https://stackoverflow.com/questions/72637416/what-does-on-constructor-do-in-angularjs
