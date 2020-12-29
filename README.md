# R_tutorial

## Abstract of data structure

变量中保存一系列数字
a <- c(1, 2, 3, 4) ## c是combine缩写，可以简单地理解为将数据分组在一起
ls()函数来显示当前搜索路径下所有的变量名，然后再决定应该使用很什么样的新变量名

在逗号后一定使用空格。比如a, b, c。而不应该是a,b,c。这样做有利于系统自动换行。

在函数传递参数时等号（=）左右不使用空格。比如someFunc(a=1, b=2)，而不应该是someFunc(a = 1, b = 2)。

在逻辑运算符左右使用空格，比如a == b。

在赋值运算符左右使用空格，比如a <- 2。
查看当前运行环境  sessionInfo()

数据结构是数据类型的封装方式。R的基本数据结构分为两类（如下表所示），一类是可以存放相同类型数据的(同质的)，一类是可以存放不同类型数据的(异质的)。什么是相同类型数据呢？我们知道，诸如C之类的计算机语言将数据类型化分为char, float (double), int, bool等类型，相应的，在R中，基本的数据类型被分为character, double, integer以及logical。double及integer类型又被统一称为numeric类型。如果数据都为character，或者double，或者integer，或者logical，就被称为同质的(Homogeneous)，否则被称为异质的(Heterogeneous)

维度|同质的|异质的
---|:--:|---:
1维|Atomic vector|List
2维|Matrix|Data frame
3维|Array|

```
##查看a和b的封装类
class(a)
```
