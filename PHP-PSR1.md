## PSR-1:基础编程规范 ##
*7/20/2017 6:24:09 PM*

该部分规范包含了一些在分享PHP代码时为保证代码的高可读性而需要考虑的编程基础方面的规范。

本文档中的**“必须”**，**“绝不”**，**“应该”**，**“不应该”**，**“可以”**，**“可选”**等关键词应按文档[RFC2119](http://www.ietf.org/rfc/rfc2119.txt)中的描述理解。（PS：原文中有十个关键词，我按自己对RFC2119文档的理解改成了六个）

----

### 1. 概述	 ###

- 所有PHP源文件**必须**只能使用`<?php`和`<?=`标签。
- 所有PHP源文件**必须**只能使用UTF-8编码格式且不带字符顺序标记BOM。
- 每一个PHP源文件**应该**要么只作为声明（如类、函数、常量），要么只用来做其他具有副作用的操作（如输出、修改配置等），但**不应该**两者兼顾。
- 命名空间（namespaces）和类（class）**必须**遵守PSR-0和PSR-4的“自动加载”标准。
- 所有类名**必须**以“StudlyCaps”方式命名。（PS：驼峰式camelCase命名的变种，区别简而言之就是首字母大小写）
- 类常量**必须**由大写字母和下划线组成。
- 方法名**必须**以驼峰法（camelCase）命名。

### 2. PHP文件 ###
	
#### 2.1. PHP标签 ####
PHP代码**必须**包含在`<?php ?>`或者`<?= ?>`标签内；**绝不**能使用其他标签。
#### 2.2. 编码格式 ####
PHP代码**必须**只能使用UTF-8编码格式且不能带字节顺序标志BOM。
#### 2.3. 副作用 ####
一个PHP文件**应该**只声明新标志（如类、函数、常量等）且不引起副作用或者只执行具有副作用的逻辑操作，而不应该两者兼顾。<br />

在这里“副作用”是指并不直接关联到文件内的声明类、函数、变量等行为的逻辑操作。<br />

“副作用”包括但不限于输出信息、明确使用`required`和`include`、连接外部服务、修改配置信息、提出错误或异常、修改全局变量或静态变量、文件读写及其他。<br />

下面是一个同时带有声明和副作用的PHP文件例子，同时具有声明和副作用这点我们需要避免。<br />

	<?php
	// side effect: change ini settings
	ini_set('error_reporting', E_ALL);
	// side effect: loads a file
	include "file.php";
	// side effect: generates output
	echo "<html>\n";
	// declaration
	function foo()
	{
	    // function body
	}

下面是一个带声明而没有副作用的PHP文件列子，这是我们提倡的。

	<?php
	// declaration
	function foo()
	{
	    // function body
	}
	
	// conditional declaration is *not* a side effect
	if (! function_exists('bar')) {
	    function bar()
	    {
	        // function body
	    }
	}

### 3. 命名空间和类名 ###

命名空间和类必须按照“自动加载”标准命名：[PSR-0](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md "PSR-0"),[PSR-4](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md)
。

本人PHP小白，这是按自己理解翻译的，觉得我这篇不怎么好的推荐看看[http://www.cnblogs.com/52php/p/5852572.html](http://www.cnblogs.com/52php/p/5852572.html)这篇文章。

最后对程序员道路上的前辈致以敬意。