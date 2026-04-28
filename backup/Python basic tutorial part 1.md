##### 黑话：str为字符串。seq为序列，可以是列表也可以是元组。st为列表。index为索引，从0开始计。方法(method)是指object.function()形式。布尔值：True and False。

## 格式化
#### 1.%格式：
**一般形式为：**
```python
%[flag][width][.precision] type
```
flag:为预留值设置对齐方式，可省略

| 符号    | 说明            |
| ----- | ------------- |
| -     | 左对齐           |
| +     | 右对齐且正数显示加号(+) |
| space | 右对齐           |

width:字符串的输出宽度，可省略
precision：数值保留的小数位数，可省略
type:格式符，**不可省略**，常用如下：

| 符号  | 说明  |
| --- | --- |
| %d  | 整数  |
| %f  | 小数  |

#### 2.format格式：
```python
# 位置参数
print("{} {}".format("Hello", "World"))  # Hello World

# 索引参数
print("{0} {1}".format("Hello", "World"))  # Hello World
print("{1} {0}".format("Hello", "World"))  # World Hello

# 命名参数
print("{name} is {age} years old".format(name="Alice", age=25))
# Alice is 25 years old
```

## 数值类型转换

>[!tip] 
>int()
float()
complex()
str()
eval()
tuple()
list()
set()


## print()函数的参数
```python
print(<expr>[,<expr>,...][,seq=<string>][,end=<string>])
```

``<expr>``为表达式
seq： ==多个==输出数据的分隔符，可省略，单个空格' ' by default
end:末尾输出内容，可省略，默认为换行符'\n'


 ---
 


# 五大字符串处理函数（其实是方法）



## 1.常用字符串转换函数==(准确来说用法是方法)==

| 函数名          | 功能             |
| ------------ | -------------- |
| capitalize() | 字符串首字母大写，其余小写  |
| title()      | 每个单词首字母大写，其余小写 |
| lower()      | 改小写            |
| upper()      | 改大写            |

## 2.常用字符串判断函数==(准确来说用法是方法)==

| 函数名       | 功能            |
| --------- | ------------- |
| isalpha() | 判断是否由字母构成     |
| isdigit() | 判断是否由数字构成     |
| islower() | 判断是否由小写构成     |
| isalnum() | 判断是否由数字or字母构成 |
>[!danger] 
>返回的是True或者False

##  3.常用字符串统计函数==(准确来说用法是方法)==

count(substr,[start,[end]])
len(str)

##  4.常用字符串拆合函数==(准确来说用法是方法)==

join(seq)
split(seq,[num]),``<num>``为拆分次数,以seq为分隔符，**默认是空格**

```python
st=['LMH','handsome.']
'is'.join(st)
print(st)
```
结果为'LMH is handsome.'


```python
st=[Hello,Python,C++]
st.split(',')   #以逗号为分割符
print(st)
```
结果为'Hello Pyhon C++'


## 5.常用字符串对齐函数==(准确来说用法是方法)==
center(width [,fillchar])
ljust(width [,fillchar])
rjust(width [,fillchar])

均为返回长度为width的字符串，分别居中，左对齐，右对齐，长度不足的部分就填充fillchar
（默认空格）



## 常用其他函数

**==id(object)==**  返回object的唯一标识符（内存地址）   
在浅复制、深复制梦幻联动的时候非常好用！！！


 ---


# random随机数模块

randint(min,max),返回一个[min,max]范围内的随机整数
uniform(min,max),返回一个(min,max)范围内的随机浮点数
random(),返回一个在[0,1)内的随机浮点数
randrange([start,] stop [,step]),返回一个在[start,stop)范围内的step步长的随机整数


 ---

# 列表(list)

#### 简单性质：
1. 访问和修改直接对st[index]进行
2. 成员判断为 object in [],回馈为布尔值
3. 有关索引index为负数：**`list[-n]`**：表示列表的倒数第 n 个元素（即 `list[len(list) - n]`）
 

## 1.列表常用函数==(除了len,del为正常函数用法，其他为方法用法)==

| 函数名             | 说明                            |
| --------------- | ----------------------------- |
| append(x)       | 尾部加单个元素x                      |
| index(x)        | 检索x所在位置                       |
| count(x)        | 统计x出现次数，不含x将返回0               |
| del seq[index]  | 删除列表索引为index的元素               |
| extend(str1)    | 加新表str1                       |
| pop(index)      | 删除索引为index的元素并弹出该元素           |
| len(str)        | 列表长度（可以计算重复元素，但是集合(set)不行）    |
| insert(index,x) | 插入单个元素x在索引index位置             |
| remove(x)       | 删除元素x，仅删除从左往右数第一个该元素x         |
| sort()          | 默认升序，数值型数据从小到大，字符串型数据则按字典顺序排序 |
| reverse()       | 逆序                            |

## 2.切片(slice)
###### --列表的子集
```python
seq[start:end: step]
```
start是索引开始处，可以省略，默认为0
end是结束位置，可以省略，默认为列表长度(len(seq))

全省略则可称为全切片[:]

step是步长，正数表示从左往右截取，负数表示从右往左截取，可以省略但不能为0，默认为1

>[!attention] 切片范围是左闭右开，即[start,end)


## 3.列表的产生方法

- ==range实现数值递增==
```python
range(start,end,step)
```
范围仍是左闭右开，即[start,end)
>[!attention] 注意！range函数使用后并不会在内存中立刻产生大量数字，只是产生一个可迭代对象，具体数值迭代过程逐一产生，有利于节省内存
>

这里可以将range()函数产生的迭代对象作为==**列表创建函数list()**==的参数
比如：
```python
a=range(1,5)
st=list(a)      #a是可迭代对象
print(st)
```
结果是[1,2,3,4]

- ==多维列表==，本质就是加了一列，仍然可以用``seq[][]``表示
- ==列表生成式！！！==非常重要
new_list=[表达式 for 变量 in 可迭代对象<if 条件>]
```python
st1=list(range(5))
print（st1）
```
结果为[0,1,2,3,4]

```python
st2=[x**2 for x in st]
print(st2)
```
结果为[0,1,4,9,16]

```python
st3=[x for x in st2 if x not in st1]
print(st3)
```
结果为[9,16]

```python
print([x for x in range(20) if x%3==0])
```
结果为[0,3,6,9,12,15,18]






