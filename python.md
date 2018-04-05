# Python 语法规范

`Python` 是一种解释型、面向对象、动态数据类型的高级程序设计语言。

* `Python` 是一种解释型语言： 开发过程中没有了编译这个环节。

* Python 是交互式语言： 可以在一个Python提示符，直接互动执行的程序。

* Python 是面向对象语言:支持面向对象的风格或代码封装在对象的编程技术。

> 交互式编程
> 交互式编程不需要创建脚本文件，是通过 Python 解释器的交互模式进来编写代码。

> 脚本式编程
> 通过脚本参数调用解释器开始执行脚本，直到脚本执行完毕。当脚本执行完成后，解释器不再有效。

### 1 基本

#### 1.1 下划线

以下划线开头的标识符是有特殊意义的

以单下划线开头（_foo）的代表不能直接访问的类属性，需通过类提供的接口进行访问，不能用"from xxx import "而导入；
以双下划线开头的（__foo）代表类的私有成员；
以双下划线开头和结尾的（foo）代表python里特殊方法专用的标识，如init（）代表类的构造函数。

#### 1.2 缩进

python用缩进来写模块。缩进的空白数量是可变的，但是所有代码块语句必须包含相同的缩进空白数量

```python
// 正确方式
if True:
    print "1"
else:
    print "2"
// 错误方式
if True:
      print "1"
else:
    print "2"
// IndentationError: unexpected indent
```

#### 1.3 引号

Python 可以使用引号( ' )、双引号( " )、三引号( ''' 或 """ ) 来表示字符串，引号的开始与结束必须的相同类型。
三引号可以由多行组成，编写多行文本的快捷语法，常用语文档字符串，在文件的特定地点，被当做注释。

```python
word = 'word'
sentence = "这是一个句子。"
paragraph = """这是一个段落。
                 包含了多个语句"""
```

#### 1.4 注释

python中单行注释采用 # 开头。

```python
# -*- coding: UTF-8 -*-
# 文件名：test.py

# 第一个注释
print "Hello, Python!";  # 第二个注释
```

python 中多行注释使用三个单引号(''')或三个双引号(""")。

```python
'''
这是多行注释，使用单引号。
这是多行注释，使用单引号。
这是多行注释，使用单引号。
'''
"""
这是多行注释，使用双引号。
这是多行注释，使用双引号。
这是多行注释，使用双引号。
"""
```

### 2 进阶

#### 2.1 代码编排

* 缩进。4个空格的缩进（编辑器都可以完成此功能），不要使用Tap，更不能混合使用Tap和空格。

* 每行最大长度79，换行可以使用反斜杠，最好使用圆括号。换行点要在操作符的后边敲回车。

* 类和top-level函数定义之间空两行；类中的方法定义之间空一行；函数内逻辑无关段落之间空一行；其他地方尽量不要再空行。

### 2.2 文档编排

* 模块内容的顺序：模块说明和docstring—import—globals&constants—其他定义。其中import部分，又按标准、三方和自己编写顺序依次排放，之间空一行。

* 不要在一句import中多个库，比如import os, sys不推荐。

* 如果采用from XX import XX引用库，可以省略‘module.’，都是可能出现命名冲突，这时就要采用import XX。

### 2.3 空格的使用

> 总体原则，避免不必要的空格。

* 各种右括号前不要加空格。
* 逗号、冒号、分号前不要加空格。
* 函数的左括号前不要加空格。如`Func(1)`。
* 序列的左括号前不要加空格。如`list[2]`。
* 操作符左右各加一个空格，不要为了对齐增加空格。
* 函数默认参数使用的赋值符左右省略空格。
* 不要将多句语句写在同一行，尽管使用‘；’允许。
* `if` / `for` / `while` 语句中，即使执行语句只有一句，也必须另起一行。

### 2.4 注释

> 总体原则，错误的注释不如没有注释。所以当一段代码发生变化时，第一件事就是要修改注释！
> 注释必须使用英文，最好是完整的句子，**首字母大写**，句后要有结束符，结束符后跟两个空格，开始下一句。如果是短语，可以省略结束符。

* 块注释，在一段代码前增加的注释。在 `#` 后加一空格。段落之间以只有 `#` 的行间隔。

* 行注释，在一句代码后加注释。比如：`x = x + 1 # Increment x`，但是这种方式尽量少使用。

* 避免无谓的注释。

#### 2.5 文档描述

* 为所有的共有模块、函数、类、方法写docstrings；非共有的没有必要，但是可以写注释（在def的下一行）。

* 如果docstring要换行，参考如下例子,详见PEP 257

```python
"""Return a foobang

Optional plotz says to frobnicate the bizbaz first.

"""
```

#### 2.6 命名规范

> 总体原则，新编代码必须按下面命名风格进行，现有库的编码尽量保持风格。

* 尽量单独使用小写字母‘l’，大写字母‘O’等容易混淆的字母。

* 模块命名尽量短小，使用全部小写的方式，可以使用下划线。

* 包命名尽量短小，使用全部小写的方式，不可以使用下划线。

* 类的命名使用CapWords的方式，模块内部使用的类采用_CapWords的方式。

* 异常命名使用CapWords+Error后缀的方式。

* 全局变量尽量只在模块内有效，类似C语言中的static。实现方法有两种，一是__all__机制;二是前缀一个下划线。

* 函数命名使用全部小写的方式，可以使用下划线。

* 常量命名使用全部大写的方式，可以使用下划线。

* 类的属性（方法和变量）命名使用全部小写的方式，可以使用下划线。

* 类的属性有3种作用域public、non-public和subclass API，可以理解成C++中的public、private、protected，non-public属性前，前缀一条下划线。

* 类的属性若与关键字名字冲突，后缀一下划线，尽量不要使用缩略等其他方式。

* 为避免与子类属性命名冲突，在类的一些属性前，前缀两条下划线。比如：类Foo中声明__a,访问时，只能通过Foo._Foo__a，避免歧义。如果子类也叫Foo，那就无能为力了。

* 类的方法第一个参数必须是self，而静态方法第一个参数必须是cls。

#### 2.7 其他

* 编码中考虑到其他python实现的效率等问题，比如运算符 `+` 在CPython（Python）中效率很高，都是Jython中却非常低，所以应该采用.join()的方式。

* 尽可能使用 `is` `is not` 取代 `==` ，比如 `if x is not None` 要优于 `if x`。

* 使用基于类的异常，每个模块或包都有自己的异常类，此异常类继承自Exception。

* 异常中不要使用裸露的except，except后跟具体的exceptions。

* 异常中try的代码尽可能少。比如：

```python
try:
    value = collection[key]
    except KeyError:
    return key_not_found(key)
else:
    return handle_value(value)
```
要优于

```python
try:
# Too broad!
    return handle_value(collection[key])
except KeyError:
# Will also catch KeyError raised by handle_value()
    return key_not_found(key)
```

* 使用 `startswith()` `endswith()` 代替切片进行序列前缀或后缀的检查。比如

`Yes: if foo.startswith(‘bar’):` 优于 `No: if foo[:3] == ‘bar’:`

* 使用isinstance()比较对象的类型。比如

`Yes: if isinstance(obj, int):` 优于 `No: if type(obj) is type(1):`

* 判断序列空或不空，有如下规则

```python
Yes: if not seq:
if seq:
```

优于

```python
No: if len(seq)
if not len(seq)
```

* 字符串不要以空格收尾。

* 二进制数据判断使用 if boolvalue的方式。


### 3 实现Node.js与Python脚本语言混编

实现原理非常简单，使用Node.js的 `child_process` 这个模块其实是帮助开发者在Node.js环境中建立一个子进程。然后在这个子进程中使用系统命令行运行python脚本，如 `python test_py.py arg0 
arg1` 实现对python脚本的调用。



