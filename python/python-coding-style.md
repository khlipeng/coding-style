# 安居客python代码格式规范

目前的规范基于[pep-0008](http://www.python.org/dev/peps/pep-0008/)

## 基本格式

### 缩进
使用4个空格进行缩进

### 行宽
每行代码尽量不超过80个字符

理由：

* 这在查看side-by-side的diff时很有帮助
* 方便在控制台下查看代码
* 太长可能是设计有缺陷

### 换行
Python支持括号内的换行。这时有两种情况。

1) 第二行缩进到括号的起始处

```python
foo = long_function_name(var_one, var_two,
                         var_three, var_four)
```

2) 第二行缩进4个空格，适用于起始括号就换行的情形

```python
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)
```

使用反斜杠`\`换行，二元运算符`+` `.`等应出现在行首，并与上一行的`.`或`=`对齐；或者缩进4个空格。长字符串也可以用此法换行

```python
foo = variable_with_long_name \
    + another_variable \
    + variable

session.query(MyTable) \
       .filter_by(id=1) \
       .one()

this_is_a_very_long(function_call, 'with many parameters') \
    .that_returns_an_object_with_an_attribute

print 'Hello, ' \
      '%s %s!' % \
      ('Harry', 'Potter')
```

多个元素的list或者tuple，在起始括号后换行，第二行缩进4个空格

```python
items = [
    'this is the first', 'set of items', 'with more items',
    'to come in this line', 'like this'
]
```

禁止复合语句，即一行中包含多个语句：

```python
# yes
do_first()
do_second()
do_third()

# no
do_first();do_second();do_third();
```

`if/for/while`一定要换行：

```python
# yes
if foo == 'blah':
    do_blah_thing()

# no
if foo == 'blah': do_blash_thing()
```

### 空行
* 模块级函数和类定义之间空两行；
* 类成员函数之间空一行；
* 不要使用太多的连续空行来区分代码的逻辑块

```python
class A:
    """This is a simple docstring."""

    def __init__(self):
        pass
    
    def hello(self):
        pass


def hello(name):
    print "Hello %s!" % name


def main():
    pass
```

* 可以使用多个空行分隔多组相关的函数
* 函数中可以使用空行分隔出逻辑相关的代码


## 表达式

### 空格
* 一元运算符不加空格
* 在二元运算符两边各空一格`[=,-,+=,==,>,in,is not, and]`:

```python
# yes
exp = -1.05
i = i + 1
submitted += 1
x = x * 2 - 1
hypot2 = x * x + y * y
c = (a + b) * (a - b)

# no
exp = - 1.05
i=i+1
submitted +=1
x = x*2 - 1
hypot2 = x*x + y*y
c = (a+b) * (a-b)
```

* 函数的参数列表中，`,`之后要有空格

```python
# yes
def complex(real, imag):
    pass

# no
def complex(real,imag):
    pass
```

* 函数的参数列表中，默认值等号两边不要添加空格

```python
# yes
def complex(real, imag=0.0):
    pass

# no 
def complex(real, imag = 0.0):
    pass
```

* 左括号之后，右括号之前不要加多余的空格

```python
# yes
spam(ham[1], {eggs: 2})
value = my_list[index]

# no
spam( ham[1], { eggs : 2 } )
value = my_list[ index ]
```

* 字典、列表对象的左括号之前不要多余的空格

```python
# yes
dict['key'] = list[index]

# no
dict ['key'] = list [index]
```

* 不要为对齐赋值语句而使用的额外空格

```python
# yes
x = 1
y = 2
long_variable = 3

# no
x             = 1
y             = 2
long_variable = 3
```

### 比较

* 使用变量在左，常量在右
* 不显示进行对`True`、`False`的比较
* 否定比较采用，`foo not in bar`的形式，而不是`not foo in bar`
* 使用`instance(a, C)`进行实例的类型检查，而不是`type(A) is C`

```python
# yes
if method == 'md5':
    pass
if not foo:
    pass
if foo not in bar:
    pass
if instance(a, C):
    pass
# no

if 'md5' == method:
    pass
if foo == False:
    pass
if not foo in bar:
    pass
if type(A) is C:
    pass
```

### 引号
简单说，自然语言使用双引号，机器标示使用单引号，因此 __代码里__ 多数应该使用 __单引号__

 * ***自然语言*** **使用双引号** `"..."`  
   例如错误信息；很多情况还是unicode，使用`u"你好世界"`
 * ***机器标识*** **使用单引号** `'...'` 
   例如dict里的key
 * ***正则表达式*** **使用原生的双引号** `r"..."`
 * ***文档字符*** **使用三个双引号** `"""......"""`


## import语句
* import语句应该分行书写

```python
# yes
import os
import sys

# no
import sys,os

# yes
from subprocess import Popen, PIPE
```
* import语句应该使用 __absolute__ import

```python
# yes
from foo.bar import Bar

# no
from ..bar import Bar
```

* import语句应该放在文件头部，置于模块说明及docstring之后，于全局变量之前；
* import语句应该按照顺序排列，每组之间用空行分隔

```python
import os
import sys

import msgpack
import zmq

import foo
```

* 导入其他模块的类定义时，可以使用相对导入

```python
from myclass import MyClass
```

* 如果发生命名冲突，则可使用命名空间

```python
import bar 
import foo.bar

bar.Bar()
foo.bar.Bar()
```


## 注释

### 块注释
`#`号后空一格，段落间用空行分开（同样需要`#`号）

```python
# 块注释
# 块注释
#
# 块注释
# 块注释
```

### 行注释
至少使用两个空格和语句分开，使用有意义的注释

```python
# yes
x = x + 1  # 边框加粗一个像素

# no
x = x + 1 # x加1 
```

### docstring
docstring的规范在 [PEP 257](http://www.python.org/dev/peps/pep-0257/) 中有详细描述，其中最其本的两点：

1. 所有的公共模块、函数、类、方法，都应该写docstring。私有方法不一定需要，但应该在def后提供一个块注释来说明。
2. docstring的结束"""应该独占一行，除非此docstring只有一行。

```python
"""Return a foobar
Optional plotz says to frobnicate the bizbaz first.
"""

"""Oneline docstring"""
```

## 命名规范
* 应避免使用小写字母`l(L)`，大写字母`O(o)`或`I(i)`单独作为一个变量的名称，以区分数字`1`和`0`
* 包和模块使用全小写命名，尽量不要使用下划线
* 类名使用`CamelCase`命名风格，内部类可用一个下划线开头；  
  约定的缩写保留原样，例如使用`HTTPWriter`而不是`HttpWriter`
* 函数使用下划线分隔的小写命名，`lowercase_with_underscores`
* 当参数名称和Python保留字冲突，可在最后添加一个下划线，尽量不是使用缩写或自造的词
* 常量使用以下划线分隔的大写命名，`UPPERCASE_WITH_UNDERSCORES`
* Precompiled regular expressions: `name_re`

```python
MAX_OVERFLOW = 100

Class FooBar:
    
    def foo_bar(self, print_):
        print(print_)
    
```

Function and method arguments:

* Class methods: `cls` as first parameter.
* Instance methods: `self` as first parameter.
* Lambdas for properties may have the first parameter replaced with `x`, as in
  `display_name = property(lambda x: x.real_name or x.username)`.


## 编码
* 文件使用UTF-8编码
* 文件头部加入`#-*-coding:utf-8-*-`标识
