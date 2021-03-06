# R 语言教程笔记

> 参考教程 ：[R语言教程 ](https://www.math.pku.edu.cn/teachers/lidf/docs/Rbook/html/_Rbook/index.html)



## 数据类型与相应的运算

### 1.常量和变量

#### 常量

1. 数值  2.字符串

> 中文编码 :`GBK`格式  和`UTF-8`格式，一般用`UTF-8`保存

#### 变量

用来保存输入的值或者计算得到的值，可以保存以下类型：

| 标量 | 向量       | 矩阵   | 数据框     | 函数     |
| ---- | ---------- | ------ | ---------- | -------- |
| x    | c(1,2,3,4) | matrix | data.frame | function |

#### R数据类型

1. 数值型 

   ​	整数、浮点数、复数

2. 逻辑型 

   ​	True、FALSE

3. 文本型

### 2.数值型向量及其运算

#### 数值型向量

```R
marks <-c(10, 6, 4, 7, 8)
x <- c(1:3, 10:13)
x1 <- c(1, 2)
x2 <- c(3, 4)
x <- c(x1, x2)
x
```

> 亦可写 `12345:12349`来表示连续元素构成的向量
>
> `length(x)`求x的长度， `numeric(x)生成元素个数为x的向量



#### 向量运算

##### 标量和标量运算

`+ - * / ^` `%%` (求余)

##### 向量与标量运算

```R 
x <- c(1, 10)
x + 2
## [1]  3 12
x - 2
## [1] -1  8
x * 2
## [1]  2 20
x / 2
## [1] 0.5 5.0
x ^ 2
## [1]   1 100
2 / x
## [1] 2.0 0.2
2 ^ x
## [1]    2 1024
```

##### 等长向量运算

```R
x1<-c(1,10)
x2<-c(4,2)
x1+x2
x1-x2
x1*x2
x1/x2
```

##### 不等长向量的运算

```R
x1<-c(10,20)
x2<-c(1,3,5,7)
x1+x2
## [1] 11 23 15 27

```

#### 向量函数

##### 向量化的函数

```R
sqrt(c(1,4,6.25))
##[1] 1.0 2.0 2.5
```

查看数学函数：`help.start()`点击 “Search Engine and Keywords”， 找到“Mathematics”栏目

- 舍入：`celing`(向上取整) `floor`向下取整 ,`round`四舍五入

- 符合函数：`sign`
- 绝对值 `abs`
- 平方根 `sqrt`
- 对数和指数函数 `log`,`exp`,`log10`,`log2`
- 三角函数 `sin`,`cos`,`tan`

- 贝塔函数 `beta`, `lbeta`
- 伽马函数 `gamma`,`lgamma`,`digamma`,`trigamma`,

- 组合数 `choose`,`lchoose`
- 富利叶变换和卷积 `fft`, `mvfft`, `convolve`

- 正交多项式 `poly`

- 求根 `polyroot`, `uniroot`
- 最优化 `optimize`, `optim`
- Bessel函数 `besselI`, `besselK`, `besselJ`, `besselY`
- 样条插值 `spline`, `splinefun`
- 简单的微分 `deriv`

> `vectorize()`函数可以将非向量函数转化为向量版本

##### 排序函数

`sort(x)` 返回排序结果

`rev(x)` 把各元素排列次序反转后的结果。

`order(x)` 返回排序的下标

```R
x <- c(33, 55, 11)
sort(x)
## [1] 11 33 55
rev(sort(x))
## [1] 55 33 11
order(x)
## [1] 3 1 2
x[order(x)]
## [1] 11 33 55
```

##### 统计函数

`sum(x)`,`mean(x)`,`var(X)`,`sd`,`min(x)`,`max(x)`,`range(x)`

`prod`求所有元素的乘积

`cumsunm` 计算累加 

`cumprod`计算累乘积



生成规则序列的函数

`seq(5)`,``seq(11,15,by=2)`,`seq(from=2,to=5)`

`rep()`生成重复数值

##### 练习

```R
sqrt(seq(1,100))
seq(1,100)^(1/3)
```

```R 
x<-c(77,60,91,73,85,82,35,100,66,75)
x01<-sort(x)
order(x01)

seq(0,1,by=0.01)
```

### 3.逻辑型向量及其运算

##### 逻辑型向量与比较运算

==TRUE==  :    ==FALSE== :

````R
#例
sele<-(log10(15)<2);print(sele)
## [1] TRUE
````

向量比较型结构为逻辑型向量

```R
c(1, 3, 5) > 2
## [1] FALSE  TRUE  TRUE
(1:4) >= (4:1)
## [1] FALSE FALSE  TRUE  TRUE
```

> 向量与标量的运算是向量每个元素与标量都分别运算一次， 等长向量的运算时对应元素的运算， 不等长但长度为倍数关系的向量运算是把短的从头重复利用。

`is.na()`函数：判断向量每个元素是否NA

`is.fintie()`判断向量每个元素是否inf值

比较运算符：

```R
<   <=  >  >=  ==  !=  %in%
```

`%in%`比较特殊的比较， ` x %in% y`的运算把向量y看成集合， 运算结果是一个逻辑型向量， 第个元素的值为x的第元素是否属于y的逻辑型值。

```R
c(1,3) %in% c(2,3,4)
## [1] FALSE TURE 
c(NA,3) %in% c(2,3,4)
## 【1】 FALSE  TRUE
```

`match(x,y)`函数类似于`x %in% y`,但其返回结果不是找到与否， 而是对`x`的每个元素， 找到其在`y`中首次出现的下标，找不到时取缺失值。



##### 逻辑运算

|         且          | 或                  |     非      |
| :-----------------: | ------------------- | :---------: |
|         `&`         | \|                  |      !      |
| `age<=3 & sex='女'` | `age<=3 | sex='女'` | `!(age<=3)` |

##### 逻辑运算函数

`all`():测试向量的所有元素为真

`any`():测试向量至少一个元素为真

`which`()：返回真值对应的所有下标

```R
which(c(FALSE,TRUE,TRUE,FALSE,NA))
## [1] 2 3
which((11:15)>12)
## [1] 3 4 5
```



`identical(x,y)`比较两个R对象，x与y的内容是否完全相同,返回`TRUE` or `FALSE`



`duplicated()`：返回每个元素是否为重复值的结果

`unique()`返回去掉重复值的结果



#### 4. 字符型数据及其处理

##### paste() 函数

用来连接两个字符型向量,例如

```R
paste(c('ab','cd'),c('ef','gh'))

paste('x',1:3,sep='')相当于
c('x1','x2','x3')

```

`collapse=`参数可以把字符串向量的各个元素连接成单一的字符串

```R
paste(c('a','b','c').collapse="")
'abc'
```



取子串

`substr(x,start,stop)`从字符串x中取出从第start个到第stop个的子串

```R
substr('Jame',1,4)
```

##### 类型转换

`as.numeric()`：把内容数字的字符串转化为数值型

```R 
substr('JAN07', 4, 5)
## [1] "07"
substr('JAN07', 4, 5) + 2000
## Error in substr("JAN07", 4, 5) + 2000 : 
##   non-numeric argument to binary operator
as.numeric(substr('JAN07', 4, 5)) + 2000
## [1] 2007
as.numeric(substr(c('JAN07', 'MAR66'), 4, 5))
## [1]  7 66
```

`as.character`()函数把数值型转化为字符型

```R
as.character(1,2,3)

```



##### 正则表达式



#### 5. R向量下标和子集

##### 整数下标

```R 
x<-c(1,2,3,4)
x[2]
## [1] 4
x[2]<-99;x
## 1,99,3,4
x[c(1,3)]<-c(11,12)
## 11,2,12,4
x<-c(1,3,4)
x[-2]
## [1] 
```

负下表表示扣除相应的元素后的子集

```R
x<-c(1,2,3)
x[-2]
## 1  3

```

##### 空下标和零下标

`x[]`表示取x的全部元素作为子集

```R
x <- c(1,4,6.25)
x[] <- 999
x
## [1] 999 999 999
x <- c(1,4,6.25)
x <- 999
x
## [1] 999
```

##### 下标超界

如果使用大于的下标， 读取时返回缺失值，并不出错。 给超出的下标元素赋值， 则向量自动变长， 中间没有赋值的元素为缺失值。

```R
x<-c(1,2,3,4)
x[5]
## [1] NA
x[5]<-0
x
##[2]
1,2,3,4,0

```

##### 逻辑下标

```R
x<-c(1,4,6.25)
x[x>3]
## [1] 4.00 6.25

```

取出x的大于3的元素组成的子集

```R
f<-function(x){
    y<-numeric(length(x))
    y[x >=0]<-1
    y[x<0]<-0 
    y
}
```



##### 各种函数

`which()`、`which.min()`、`which.max()`函数

`which()`用来找到满足条件的下标

```R
x <- c(3, 4, 3, 5, 7, 5, 9)
which(x > 5)
## [1] 5 7
seq(along=x)[x > 5]
## [1] 5 7
```

##### 元素名

```R
ages <- c("李明"=30, "张聪"=25, "刘颖"=28)
```

或

```R
ages <- c(30, 25, 28)
names(ages) <- c("李明", "张聪", "刘颖")
```

或

```R
ages <- setNames(c(30, 25, 28), c("李明", "张聪", "刘颖"))
```



##### 用R向量下标作映射

```R
price_map <- c(68, 88, 168)

items<-c(3,2,1,1,2,2,3)
y<-price_map[items];print(y)
## [1] 168 88 68 88 88 168
```

```R
sex <- c("男", "男", "女", "女", "男", "女", "女", "女", "女", "男")

sex_color<-c('男'='blue','女'='red')
```

```R 
cols<-sex_color[sex];print(cols)
```

```R
unname(cols)
```



##### 集合运算

```R
unique(c(1,5,2,5))
## [1] TRUE 
c(5,6) %in% c(1,5,2)
## [1] TRUE FALSE
```



```R
match(5,c(1,5,2))
## [1] 2
match(5,c(1,5,2,5))
## [1] 2
match(c(2,5),c(1,5,2,5))
## [1] 3 2
match(c())
```



#### 6. R数据类型的性质

##### 存储模式与基本类型

`typeof()`函数返回一个变量或表达式的类型

```R
typeof(1:3)
## [1] 'iiinteger'
typeof(c(1,2,3))
## [1] 'double'
typeof(c(1,2.1,3))
## [1] 'double'
typeof(c(TRUE,NA,FALSE))
## [1] 'logical'
typeof('Abc')
## [1] "character"
typeof(factor(c('F', 'M', 'M', 'F')))
## [1] "integer"
```



```R
is.interger(c(1,-3))
## [1] FALSE
is.interger(c(1L,-3L))
## [1] TRUE
```



`is.finite()`判断是否有限值

此外还有`is.infinite`,`is.nan`等用法

 

##### 类型转化与类型升档

```R
as.numeric(c(FALSE,TRUE))
## [1] 0 1
as.character(sqrt（1:4))

```

```R
TRUE +10 
## [1] 11
paste('abc',1)
## [1] 'abc 1'

```

##### 属性

`attributes`函数

```R
x <- table(c(1,2,1,3,2,1)); print(x)
## 
## 1 2 3 
## 3 2 1
attributes(x)
## $dim
## [1] 3
## 
## $dimnames
## $dimnames[[1]]
## [1] "1" "2" "3"
## 
## 
## $class
## [1] "table"
```

`attr`函数

用`attr(x,'属性名')`的格式读取或定义x的属性

```R
x<-c(1,3,5)
attr(x,'theta')<-c(0,1)
print(x)
##[1] 1 3 5
## attr(,"theta")
## [1] 0 1
```



##### names 属性

```R
x<-1:5
y<-x^2
lmr<-lm(y ~x)
print(names(lmr))
```



`dim`属性



类属



`str()`函数



