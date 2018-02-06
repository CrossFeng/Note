# Python

变量规范命名方式:

* 下划线 my_variable
* 驼峰式 myVariable

语义化版本的参数一般代表

* 主版本号: 不兼容的API修改
* 次版本号:做了向下兼容功能性的新增
* 修订号：做了向下问题修正

Python的运行原理

源代码先转化为中间字节码然后再被虚拟机运行
python会生成一个.pyc文件 .py->.pyc->PVM ->processor

python 是一个结合了解释性、编译性、互动性和面向对象的脚本语言

python会生成一个.pyc文件 .py->.pyc->PVM ->processor

交互式语言

jupyter notebook

## 二进制浮点数

符号位 0 + 1 -
指数部分 $2^n$ 
基数部分:具体数值，决定精度

## 神一样的错误

- [ ] SyntaxError: EOF while parsing 
- [ ] SyntaxError invalid syntax
- [ ] NameError: not defined
- [ ] ModuleNotFoundError
- [ ] AttributeError
- [ ] IndexError
- [ ] TypeError
- [ ] KeyError
- [ ] FileNotFoundError

## Pip

管理python工具包的工具组合

## Conda

type dir help

## 基本类型

Python 可以处理任意大小的整数 可以使用十六进制 
浮点型 小数
字符串 string
布尔型
空值

Python 中是没有常量的

0b1111 二进制

## 基本的输入和输出  和基本数据类型的转换

输入

isinstance

exec()执行传入带代码段

格式化输出 print("string %format1.."%(var1,..))
%u %o %x %X %d
print("myname {name_in} ,my age {age_in}" .format(name_in=name,age_in=age))

集合 set

函数

def  lambda 默认参数 多参数 传入字典 *args **args

## print

```python
#comment this is one line comment 
string1 = 'string1';
string2 = "string2";
string3 = """
this is a p block
"""
print(string1);
print(string2 + string3);
print(string1 ,end="");
print(string1 \
     string2 \
     string3);
```

## import

```python
import somemodule
from somemodule import somefunction
from somemodule import fun1,fun2,arg
```

type

`int float bool complex`

## Data Type

Number

String
`+str [0:-1] [0] [2:] *n`

List
[ ]

Tuple
()

Sets
{ "" } set()

Dictionary
{key:value}

## convert

to String

`str repr eval`

## del

`del var1[,var2[,var3[]]]`

## caculater

power **
abs absolute
ceil  up
exp  power of e
fabs absolute of float
floor 
log
log10
max(var1,var2)
min
round 
sqrt

# Random

| random.                        |
| ------------------------------ |
| randrange([start,]stop[,step]) |
| shuffle                        |
| choice(seq)                    |
| uniform(x,y)                   |
| random                         |



# python opencv

pip install opencv-python

pip install -U numpy

pip install numpy -I