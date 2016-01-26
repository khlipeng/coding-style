#PHP 基本代码规范(更正版)

> 该版本命名将使用驼峰命名法

如果与 [PHP The Right Way][PHP-FIG] 里的标准 [PSR-0][PSR-0] 、 [PSR-1][PSR-1] 、 [PSR-2][PSR-2] 、 [PSR-4][PSR-4] 有冲突的地方，我们将逐渐改进。

  [PHP-FIG]: http://www.phptherightway.com/
  [PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
  [PSR-1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
  [PSR-2]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
  [PSR-4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader-meta.md
  [RFC-2119]: http://www.ietf.org/rfc/rfc2119.txt
  
## 基本代码规范
 * 本篇规范制定了代码基本元素的相关标准，以确保共享的PHP代码间具有较高程度的技术互通性。

	关键词：
	
	>  必须(MUST) 、 一定不可/一定不能(MUST NOT) 、 需要(REQUIRED) 、 将会(SHALL) 、 不会(SHALL NOT) 、 应该(SHOULD) 、 不该(SHOULD NOT) 、 推荐(RECOMMENDED) 、 可以(MAY) 、 可选(OPTIONAL)
		
	详细描述可参见 [RFC 2119][RFC-2119] 。
	
## 概览

 * PHP代码文件必须以 <?php 标签开始；

 * PHP代码文件必须以 不带 BOM 的 UTF-8 编码；

 * PHP代码中应该只定义类、函数、常量等声明，或其他会产生 从属效应 的操作（如：生成文件输出以及修改.ini配置文件等），二者只能选其一；

 * 命名空间以及类必须符合 PSR 的自动加载规范：PSR-0 或 PSR-4 中的一个；

 * 类的命名必须遵循 StudlyCaps 大写开头的驼峰命名规范；

 * 类中的常量所有字母都必须大写，单词间用下划线分隔；

 * 方法名称必须符合 camelCase 式的小写开头驼峰命名规范。

## 文件

### PHP标签

 * PHP代码必须使用 <?php 长标签，一定不可使用其它自定义标签；

 * 在`*.php`的源代码文件里不使用`?>`关闭标签。

### 字符编码

 * PHP代码必须且只可使用不带BOM的UTF-8编码。

### 从属效应（副作用）

 * 一份PHP文件中应该要不就只定义新的声明，如类、函数或常量等不产生从属效应的操作，要不就只有会产生从属效应的逻辑操作，但不该同时具有两者。

 * “从属效应”(side effects)一词的意思是，仅仅通过包含文件，不直接声明类、函数和常量等，而执行的逻辑操作。

 * “从属效应”包含却不仅限于：生成输出、直接的 require 或 include、连接外部服务、修改 ini 配置、抛出错误或异常、修改全局或静态变量、读或写文件等。
	
	以下是一个反例，一份包含声明以及产生从属效应的代码：
	
	```php

	<?php
	// 从属效应：修改 ini 配置
	ini_set('error_reporting', E_ALL);

	// 从属效应：引入文件
	include "file.php";

	// 从属效应：生成输出
	echo "<html>\n";

	// 声明函数
	function foo()
	{
	    // 函数主体部分
	}

	```
	下面是一个范例，一份只包含声明不产生从属效应的代码：
	
	```php
	<?php
	// 声明函数
	function foo()
	{
	    // 函数主体部分
	}

	// 条件声明**不**属于从属效应
	if (! function_exists('bar')) {
	    function bar()
	    {
	        // 函数主体部分
	    }
	}
	```
	
## 命名空间和类

 * 命名空间以及类的命名必须遵循 [PSR-0][PSR-0]、[PSR-4][PSR-4].
	
 * 根据规范，每个类都独立为一个文件，且命名空间至少有一个层次：顶级的组织名称（vendor name）。

 * 类的命名必须 遵循 StudlyCaps 大写开头的驼峰命名规范。

 * PHP 5.3及以后版本的代码必须使用正式的命名空间。

	例如：
	
	```php
	<?php
	// PHP 5.3及以后版本的写法
	namespace Vendor\Model;

	class Foo
	{
	}
	```
 * 5.2.x及之前的版本应该使用伪命名空间的写法，约定俗成使用顶级的组织名称（vendor name）如 `Vendor_` 为类前缀。
	
	例如：
	
	```php
	<?php
	// 5.2.x及之前版本的写法
	class Vendor_Model_Foo
	{
	}
	```
	
## 类的常量、属性和方法

 * 此处的“类”指代所有的类、接口以及可复用代码块（traits）

### 常量

 * 类的常量中所有字母都必须大写，词间以下划线分隔。

	参照以下代码：
	
	```php
	<?php
	namespace Vendor\Model;

	class Foo
	{
	    const VERSION = '1.0';
	    const DATE_APPROVED = '2016-02-2';
	}
	```

### 属性

 * 类的属性命名可以遵循 大写开头的驼峰式 (`$StudlyCaps`)、小写开头的驼峰式 (`$camelCase`) 又或者是 下划线分隔式 (`$under_score`)，本规范不做强制要求，但无论遵循哪种命名方式，都应该在一定的范围内保持一致。这个范围可以是整个团队、整个包、整个类或整个方法。
	
### 方法

 * 方法名称必须符合 `camelCase()` 式的小写开头驼峰命名规范。
	
## 代码排版规则
	
### 花括号

 * 强制使用花括号，即使不需要使用

 * 起始花括号在一行的最后，结束花括号独立一行

	```php
	<?php
	// 正确
	if ($foo == $bar) {
	    echo 'equals';
	}

	// 错误
	if ($foo == $bar) echo 'equals';
	if ($foo == $bar)
	    echo 'equals';
	```
	
### 空格使用

 * 缩进使用 **4个字符的空格** ，不使用TAB制表符。建议使用anyedit插件，可以方便的将tab缩进转换为空格缩进。
 
 * 标识符之间使用一个空格区分。

 * 行尾去掉无用的空格。

	```php
	<?php
	// 正确
	$i = 0;
	if (($i < 2) || ($i > 5)) {
	}
	foo($a, $b, $c);
	$i = ($j < 5) ? $j : 5;

	// 错误
	$i=0;
	if(( $i<2 )||( $i>5 )) {
	}
	foo ( $a,$b,$c );
	$i=($j<5)?$j:5;
	```
		
### 引用

  * 缺省 **使用单引号**
  * ***需要转义或内嵌变量时*** **使用双引号**

	```php
	<?php
	// 正确
	echo 'Hello, World!';
	echo "Hello, {$name}";

	// 错误
	echo "Hello, World!";
	echo 'Hello, ' . $name;
	```

### SQL语句

 * SQL 关键字使用大写，数据库对象使用小写。

	```sql
	SELECT id, name FROM foobar WHERE updated < :updated ORDER BY display_order;
	```

### 换行

 * 一行不要太长到难以阅读。

### 注释

 * 提供给其他开发人员调用的代码，建议使用phpdoc格式的注释，特别是函数的返回类型。



