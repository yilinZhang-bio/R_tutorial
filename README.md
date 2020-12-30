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
```
a <- 1:3 ## 冒号（：）是seq()函数的缩写, 用于生成序列数
typeof(a)
##对atomic vector排序
a <- c(4, 2, 1, 3)
b <- sort(a)
b
## [1] 1 2 3 4
```

### 二维数据结构：Matrices和DataFrame
### 2D: Matrices and DataFrame

#### Matrix
简单的讲，给atomic vector加上维度信息，它就变成了array。如果维度信息是二维的，它就是matrix。也就是说，matrix只是array的一个特例，而array是从atomic vector扩展而来的。我们来试着构建一个matrix。
```
vec <- 1:12
mat <- matrix(vec, ncol=3, nrow=4) ##ncol == number of column, nrow == number of row
mat 
##      [,1] [,2] [,3]
## [1,]    1    5    9
## [2,]    2    6   10
## [3,]    3    7   11
## [4,]    4    8   12

## 访问第二列
mat[, 2]
## [1] 5 6 7 8

## 访问第三列，但保持结果为matrix的形式
mat[, 3, drop=FALSE]
##      [,1]
## [1,]    9
## [2,]   10
## [3,]   11
## [4,]   12

dim(mat) ##matrix维度
nrow(mat) ## 有几行
ncol(mat) ## 有几列
length(mat) ## 这是继承的vector的属性
```
#### DataFrame

Data frame是R中最常被用到的数据结构。Data frame就是由一系列长度相等的vectors构成。它继承了vector的所有方法，包括atomic vector和list的方法，比如访问某一列可以使用'$'符号。它是2维的，它一样也有和matrix相同的方法，比如colnames(), rownames(), rbind(), cbind(), dim(), ncol(), nrow()等。

### 输入与输出
### I/O

无论是输入还是输出，首先面临的问题是如何改变工作路径的问题。在R中使用setwd()函数来改变当前目录，使用getwd()来获取当前目录。
```
path <- getwd() ##获取当前工作目录
```
```
test.txt <- data.frame(ArrayDataFile=paste("GSM28676", 1:8, sep=""), 
                       FactorValue=rep(c("control", "mutation"), each=4))
test.txt

```
```
##   ArrayDataFile FactorValue
## 1     GSM286761     control
## 2     GSM286762     control
## 3     GSM286763     control
## 4     GSM286764     control
## 5     GSM286765    mutation
## 6     GSM286766    mutation
## 7     GSM286767    mutation
## 8     GSM286768    mutation
```

### 字符串处理
### Strings

#### 常规操作
#### Basics

```
#赋值
mychar <- c("ACTACCACTAACCACT","TCATCCATTCGTGGG","GTTGTTCCATAG")
#获取字串长度
nchar(mychar)

```

正则的使用已经看到了，但是让人看不明白就是字符. \ | ( ) [ { ^ $ * + - ? 这些符号都是什么意思呢？下面就来仔细讲讲perl中的正则符号。

```
.  # 除了换行以外的任意字符
^    # 一行字符串的起始，它并不代表第一个字符，只代表这里开始新的一行字符串。
$    # 一行字符串的结束，它并不代表最后一个字符（因为换行符并不会被包含进匹配当中），只代表一行字符串到这里结束。
*    # 零个或者多个之前的字符
+    # 一个或者多个之前的字符
?    # 零个或者一个之前的字符
# 示例部分
t.e    # t后面跟任意一个非换行字符然后跟字符e
    # 它可以匹配        the
    #                 tre
    #                 tle
    # 但是不匹配 te
    #           tale
^f    # 一行字符以f起始
^ftp    # 一行字符以ftp起始
e$    # 一行字符以e结尾
tle$    # 一行字符以tle结尾
und*    # un跟着零个或者多个d字符
    # 它会匹配 un
    #         und
    #         undd
    #         unddd (etc)
.*    # 任意一个无换行的字符串，
    #  . 匹配任何一个非换行字符
    #  * 将匹配一个或者多个之前的字符.
^$    # 一个空行.

 # 在正则中有方括号[]，代表可以匹配其中任何一个字符。而^在[]中就有了新的意义，代表“非”, -代表了“之间”
[qjk]        # q，j，k中任意一个字符
[^qjk]        # 非q，j，k的任意其它字符
[a-z]        # a至z中任意一个小写字符
[^a-z]        # 非任意一个a至z小写字符的其它字符（可以是大写字符）
[a-zA-Z]    # 任意一个英文字母
[a-z]+        # 一个或者多个小写英文字母

 # |代表或者 小括号(...)可以把或者的部分括起来。注意小括号可能还有别的用途，但是在R当中先不使用。

jelly|cream    # jelly或者cream
(eg|le)gs    # eggs或者legs
(da)+        # da或者dada或者dadada 或者更多个da的重复

 # 大括号括住1至2个数字，代表重复次数。
*    # 零个或者多个之前的字符
+    # 一个或者多个之前的字符
?    # 零个或者一个之前的字符
{n}    # n个之前的字符
{n,}    # 大于等于n个之前的字符
{n,m}    # n至m个之前的字符

 # 下面的是一些字符被转义符\转义会赋以了一些新的（有可能是约定俗成的）意义
\n        # 换行符
\t        # tab
\w        # 任意字母（包括下划线）或者数字
        # 等同于[a-zA-Z0-9_]
\W        # \w的反义.
        # 等同于[^a-zA-Z0-9_]
\d        # 任意一个数字，等同于[0-9]
\D        # \d的反义，等同于[^0-9]
\s        # 任意一个空格，比如,
        # space, tab, newline, 等
\S        # \s的反义，任意一个非空格
\b        # 单词的边界, 不能使用在[]内
\B        # \b的反义

 # 很明显，对于保留字符$, |, [, ), \, / 等等都需要转义字符\来转义表示：

\|        # 竖线
\[        # \[左方括号 \]右方括号
\)        # \(左小括号 \)右小括号
\*        # 星号
\^        # 开号
\/        # 反斜杠
\\        # 斜杠
```
### 两大口号

在R中，
所有一切静态的存在都是对象(object),
所有一切可以执行的都是函数(function)。
换言之，R是全面面向对象的编程环境。无论你是否意识到这一点，它都存在在那里。“无一不是对象”，“所发生的一切都是函数”，是本质上理解R的两大口号。

